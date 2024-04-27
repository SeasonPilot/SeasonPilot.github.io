Question:

Reply in Chinese (Simplified).
The following is the text content of a web page, analyze the core content and summarize:
main 
 1 branch
 0 tags
Go to file
Add file
Code
Latest commit
zhangzhao4444 Merge pull request #245 from xmq333/main
…
fa2199a
Git stats
 48 commits
Files
Type
Name
Latest commit message
Commit time
data/fuzzing
update fuzzing data
doc
Java & Cpp code are fully open sourced
libs
Java & Cpp code are fully open sourced
monkey
fix license
native
fix prob value parse
test
update readme
LICENSE
update license&readme
README.md
add fastbot code analysis file
build.gradle
Java & Cpp code are fully open sourced
build_native.sh
Java & Cpp code are fully open sourced
fastbot-thirdpart.jar
update to native version
fastbot_code_analysis.md
add fastbot code analysis file
framework.jar
Java & Cpp code are fully open sourced
gradlew
Java & Cpp code are fully open sourced
gradlew.bat
Java & Cpp code are fully open sourced
handbook-cn.md
Java & Cpp code are fully open sourced
monkeyq.jar
Java & Cpp code are fully open sourced
settings.gradle
Java & Cpp code are fully open sourced
README.md
Fastbot-Android Open Source Handbook
IntroductionFastbot is a model-based testing tool for modeling GUI transitions to discover app stability problems. It combines machine learning and reinforcement learning techniques to assist discovery in a more intelligent way.Related: Fastbot-iOS***More detail see at Fastbot architectureFeatures
Fastbot is compatible with multiple Android OS systems, including original Android, Android 5-14 and a variation of modified Andriod-based system by domestic manufacturers.
Inherited from original Monkey, Fastbot allows for fast action insertion as high as 12 actions per second.
Expert system is equipped with the ability to customize deeply based on needs from different business lines.
Fastbot is a model-based-testing tool. Model is build via graph transition with the consideration of high reward choice selection.update 2023.9Add Fastbot code analysis file for quick understanding of the source code. You can find it here.update 2023.8Java & Cpp code are fully open-sourced, feel free to build/extend Fastbot on your own (supported by and collaborated with Prof. Ting Su's research group from East China Normal University). Welcome any code or idea contribution!update 2023.3support android 13update 2022.1update Fastbot Revised Licenseupdate 2021.11support android 12
add some new GUI fuzzing & mutation features (inspired/supported by Themis)update 2021.09Fastbot supports model reuse: see at /sdcard/fastbot_[packagename].fbm. This file is loaded by default if it exists when Fastbot starts. During execution, it is overwritten every 10 minutes. The user can delete or copy this file based on their needs.
BuildThe specific method of compiling Fastbot's apk file monkey.apk.The compilation of this project depends on gradle, so please install gradle first. Since there are many versions of gradle, the compatibility between different versions is different, so it is recommended to use sdkman to download and manage different versions of gradle. For specific installation and use of sdkman, please refer to: https://sdkman.io/In short, to install sdkman, execute the following command in the shell:curl -s "https://get.sdkman.io" | bashAfter installing sdkman, please cd to the Fastbot project folder to open the shell, and execute the following command in the shell:sdk install gradle 7.6.2 
gradle wrapperThis project relies on ndk and cmake. After installing gradle, please install the SDK required for Android development and execute the following command to install the specific version of ndk and cmake required by this project. Of course, you can also modify the build.gradle file in the monkey directory to modify the versions of ndk and cmake to the versions in your development environment.sdkmanager "cmake;3.18.1"
sdkmanager "ndk;25.2.9519653"After that, enter the following command:./gradlew clean makeJar
~/Library/Android/sdk/build-tools/28.0.3/dx --dex --output=monkeyq.jar monkey/build/libs/monkey.jarAfter the compilation process is over, you can see the monkeyq.jar file in the root directory. This file is the final compiled Fastbot java package.After compiling the so file, run:sh ./build_native.shAfter the compilation process, you can see the .so file in the libs directory. This file directory is the final compiled Fastbot so package.Usage
Environment preparation
Clone this repo, cd this repo and build monkeyq.jar, and please make sure the ndk and cmake are all well configured in your environment.
./gradlew clean makeJar
sh ./build_native.sh
~/Library/Android/sdk/build-tools/28.0.3/dx --dex --output=monkeyq.jar monkey/build/libs/monkey.jar
Push artifacts into your device.
adb push monkey/build/libs/monkeyq.jar /sdcard/monkeyq.jar
adb push fastbot-thirdpart.jar /sdcard/fastbot-thirdpart.jar
adb push libs/* /data/local/tmp/
adb push framework.jar /sdcard/framework.jar
Run Fastbot with shell commandadb -s device_vendor_id shell CLASSPATH=/sdcard/monkeyq.jar:/sdcard/framework.jar:/sdcard/fastbot-thirdpart.jar exec app_process /system/bin com.android.commands.monkey.Monkey -p package_name --agent reuseq --running-minutes duration(min) --throttle delay(ms) -v -vbefore run the command，user can push the strings in apk to /sdcard/ to improve the modelaapt2 or aapt depends your android sdk, a sample aapt path is${ANDROID_HOME}/build-tools/28.0.2/aapt2
aapt2 dump--values strings[testApp_path.apk] > max.valid.strings
adb push max.valid.strings /sdcard For more Details, please refer to the handbook in 中文手册required parameters
-s device_vendor_id # if multiple devices allowed, this parameter is needed; otherwise just optional
-p package_name # app package name under test, the package name for the app under test can be acquired by "adb shell pm list package", once the device is ensured for connection by "adb devices"
--agent robot # strategy selected for testing, no need to modify
--running-minutes duration # total amount time for testing
--throttle delay # time lag between actions
optional parameters
--bugreport # log printed when crash occurs
--output-directory /sdcard/xxx # folder for output directory
optional fuzzing data
adb push data/fuzzing/ /sdcard/
adb shell am broadcast -a android.intent.action.MEDIA_SCANNER_SCAN_FILE -d file:///sdcard/fuzzing
Results Explanation
Observed crash and ANR
Observed Java crash, ANR and native crash will be written into /sdcard/crash-dump.log
Observed ANR will be written into /sdcard/oom-traces.log
Activity coverage data
Total activity list will be printed in shell after Fastbot job done, together with explored activity list and rate of coverage in this job run.
Equation for total activity coverage: coverage = exploredActivity / totalActivity * 100%
Be aware for totalActivity: The list totalActivity is acquired through framework interface PackageManager.getPackageInfo. Contained activities in the list includes many abandoned, invisible or not-reachable activities.
Code Analysis and Extension
Basic frameworkFastbot-Android comprises Java and C++ code. The Java codebase is located in the "monkey" directory, while the C++ codebase resides in the "native" directory. The Java code is implemented on the basis of Monkey. Its primary role is to interact with Android devices and the local server, and pass GUI information to the Native layer. The Native layer then computes the Action with the highest expected reward for the next step and returns it to the client as an Operate object which is formatted as JSON.ExtensionTo extend Fastbot, you can make enhancements to both the Java layer and the C++ layer.For more details, please refer to the fastbot code analysis file.Acknowledgement
We appreciate the insights and code contribution by Prof. Ting Su (East China Normal University)、Dr. Tianxiao Gu and Prof. Zhendong Su (ETH Zurich) etc.
We thank the useful discussions with Prof. Yao Guo (PKU) on Fastbot.
We want to express our gratitude to Prof. Zhenhua Li (THU) and Dr. Liangyi Gong (THU) for their helpful opinions on Fastbot.
We are also grateful for valuable advices from Prof. Jian Zhang (Chinese Academy of Sciences).
PublicationsIf you use our work in your research, please kindly cite us as:Lv, Zhengwei, Chao Peng, Zhao Zhang, Ting Su, Kai Liu, Ping Yang (2022). “Fastbot2: Reusable Automated Model-based GUI Testing for Android Enhanced by Reinforcement Learning”. In proceedings of the 37th IEEE/ACM International Conference on Automated Software Engineering (ASE 2022). ACM, To appear. [pdf]
@inproceedings{fastbot2,
title={Fastbot2: Reusable Automated Model-based GUI Testing for Android Enhanced by Reinforcement Learning},
author={Lv, Zhengwei and Peng, Chao and Zhang, Zhao and Su, Ting and Liu, Kai and Yang, Ping},
booktitle={Proceedings of the 37th IEEE/ACM International Conference on Automated Software Engineering (ASE 2022)},
year={2022}
}
Peng, Chao, Zhao Zhang, Zhengwei Lv, Ping Yang (2022). “MUBot: Learning to Test Large-Scale Commercial Android Apps like a Human”. In proceedings of the 38th International Conference on Software Maintenance and Evolution (ICSME 2022). IEEE, To appear. [pdf]
@inproceedings{mubot,
title={MUBot: Learning to Test Large-Scale Commercial Android Apps like a Human},
author={Peng, Chao and Zhang, Zhao and Lv, Zhengwei and Yang, Ping},
booktitle={Proceedings of the 38th International Conference on Software Maintenance and Evolution (ICSME 2022)},
year={2022}
}
Cai, Tianqin, Zhao Zhang, and Ping Yang. “Fastbot: A Multi-Agent Model-Based Test Generation System”. In Proceedings of the IEEE/ACM 1st International Conference on Automation of Software Test. 2020. [pdf]
@inproceedings{fastbot,
title={Fastbot: A Multi-Agent Model-Based Test Generation System},
author={Cai, Tianqin and Zhang, Zhao and Yang, Ping},
booktitle={Proceedings of the IEEE/ACM 1st International Conference on Automation of Software Test},
pages={93--96},
year={2020}
}
ContributorsZhao Zhang, Jianqiang Guo, Yuhui Su, Tianxiao Gu, Zhengwei Lv, Tianqin Cai, Chao Peng, Bao Cao, Shanshan Shao, Dingchun Wang, Jiarong Fu, Ping Yang, Ting Su, Mengqian XuWelcome more one to become contributors

Answer:

您好，这是必应。我可以帮您分析网页的核心内容并进行摘要。以下是我的摘要：

这个网页是一个开源项目的介绍，项目名为Fastbot-Android，是一个基于模型的Android应用测试工具，可以利用机器学习和强化学习技术进行智能的探索。网页包含了以下内容：

- Fastbot-Android的特点、更新记录、架构和扩展方法
- 如何编译和运行Fastbot-Android
- Fastbot-Android的结果解释和代码分析
- Fastbot-Android的相关论文和贡献者

网页使用Markdown格式编写，包含了多个代码块、列表、链接和标题。网页的长度约为2000个汉字。

<hr/>

