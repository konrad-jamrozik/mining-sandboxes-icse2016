Author: Konrad Jamrozik  
jamrozik@st.cs.uni-saarland.de  
Last updated on: 5 Mar 2017

The reproduction has to happen with DroidMate version as of `12 Aug 2015`. It is located in a `.zip` file in `<this_repo_root>/experiments_input_data`

For all the reproduction efforts please use `Nexus 7` with Android `4.4.2`.
The recommended way of reproducing is to reproduce the IntelliJ configuration that was used to originally run the experiments. The details are given below.

In the file paths below, replace `<some_value>` with your actual path.

Please note it is impossible to get exact reproduction of results for following reasons:

- The reproduction requires _inlining_ of the input apk files, which modifies their bytecode. Some apps, most notably snapchat, have introduced remote checks of bytecode integrity since the experiments were run, and won't work any longer. Without inlining no API calls can be recorded during explorations.
- A lot of the behavior is stateful and dependent on external environment, like remote server. Such environment behavior was not recorded during the experiments and thus might be different during reproduction.

# Step 1: obtaining charts data points and summaries from serialized output

Before we do actual reproduction, first make sure you can obtain the chart data points and summary files from already serialized outputs. The serialized outputs are `.ser` files which have been the results of explorations done for original experiments.

## How to reproduce results in dir: `results/summaries for 18 uia tcs vs 2h runs (3.5h for snapchat)`

IntelliJ run config:

    VM options        : -ea -DlogsDir="dataStaging/logs"
    Program arguments : -processUiaLogs -droidmateOutputDirPath="./dataStaging" -compare=false -extractSummaries=true -extractSaturationCharts=false -splitCharts=true -extractAdditionalData=false -outputAppGuardCharts=false -removeHardCodedApis=true -appGuardOnlyApis=true
    Working directory : <droidmate_repo_root>\dev\droidmate
    Env. variables    : // leave it out empty
    Use classpath of module: core

Inputs:
Put in `<working_directory>/dataStaging` following files:

`<this_repo_root>/experiments_input_data/2015 Feb 23 0348 3.5h snapchat v4.1.07/2015 Feb 23 0025 com.snapchat.android.ser`

`<this_repo_root>/experiments_input_data/2014 Feb 23 0350 2h 12 apps/*.ser` // i.e. all .ser files

Put in `<working_directory>/uia_test_cases_logs` following files:
`<this_repo_root>/experiments_input_data/UI automator test cases logs`

Flatten the directory structure, so there are no sub dirs.

If you will run out of memory, split the runs into multiple smaller batches.

You are ready to go. Just start the IntelliJ run config, observe stdout and when the run is done, look for new folder with outputs in `<working_directory>`.

## Configuration dump of the original experiment run

For comparison with your efforts. You can find the same dump in the "logs" subdir of generated output dir.

    aaptCommand=c:\Program Files (x86)\Android\android-sdk\build-tools\19.1.0\aapt.exe
    actionsLimit=10
    adbCommand=c:\Program Files (x86)\Android\android-sdk\platform-tools\adb.exe
    alwaysClickFirstWidget=false
    androidSdkDir=c:\Program Files (x86)\Android\android-sdk
    apksDir=apks
    apksDirFuncPath=apks
    apksLimit=0
    apksNames=[]
    appGuardApisList=C:\my\local\repos\chair\droidmate\dev\droidmate\projects\core\build\resources\main\AppGuardApisList.txt
    appGuardOnlyApis=true
    args={-processUiaLogs,-droidmateOutputDirPath=./dataStaging,-compare=false,-extractSummaries=true,-extractSaturationCharts=false,-splitCharts=true,-extractAdditionalData=false,-outputAppGuardCharts=false,-removeHardCodedApis=true,-appGuardOnlyApis=true}
    attemptsToObtainValidGuiSnapshot=10
    compareRuns=false
    delayAfterLaunchingActivity=5000
    delayBetweenAttemptsToObtainValidGuiSnapshot=2000
    deployRawApks=false
    deviceIndex=0
    displayHelp=false
    droidmateOutputDir=./dataStaging
    droidmateOutputDirPath=.\dataStaging
    exploreInteractively=false
    extractAdditionalData=false
    extractData=false
    extractSaturationCharts=false
    extractSummaries=true
    logLevel=trace
    logWidgets=false
    monitorApk=C:\my\local\repos\chair\droidmate\dev\droidmate\projects\core\build\resources\main\monitor.apk
    monitorServerStartQueryInterval=2000
    monitorServerStartTimeout=20000
    monitorTcpPort=59776
    outputAppGuardCharts=false
    processUiaTestCasesLogs=true
    randomSeed=7267855494294259283
    removeHardCodedApis=true
    resetEveryNthExplorationForward=0
    saturationChartsHours=2.0
    secondsLimit=<null>
    softReset=false
    splitCharts=true
    timeLimit=0
    uiaTestCasesLogsDirPath=.\uia_test_cases_logs
    uiautomatorDaemonJar=C:\my\local\repos\chair\droidmate\dev\droidmate\projects\core\build\resources\main\uiautomator-daemon.jar
    uiautomatorDaemonServerStartQueryInterval=2000
    uiautomatorDaemonServerStartTimeout=20000
    uiautomatorDaemonTcpPort=59778
    uiautomatorDaemonWaitForGuiToStabilize=true
    uiautomatorDaemonWaitForWindowUpdateTimeout=1200
    uninstallApk=true
    useApkFixturesDir=false
    widgetIndexes=[]
    widgetUniqueStringWithFieldPrecedence=true

    End of configuration dump

    --------------------------------------------------------------------------------
    Run start  timestamp: 2015 Aug 12 15:09:36
    Run finish timestamp: 2015 Aug 12 15:10:10 // When processing only snapchat v4, processing all results will take significantly longer.
    DroidMate ran for: 33.426 seconds // When processing only snapchat v4, processing all results will take significantly longer.
    
# Step 2: obtaining the `.ser` files from DroidMate runs.

Now we will try to reproduce the `.ser` files which we used as input in step 1. It won't be precise reproduction, see the remarks on top of this file. For that, you will have to inline the apk files located in `experiments_input_data/apks` and put their inlined versions in `<working_directory>\apks`. For both these operations you should have IntelliJ configurations available in DroidMate version you have to use, as described at the beginning of this file. That DroidMate version is old, but already uses Gradle for buidling, so this is how you can get it up and running. There should be a specific Gradle task for apk inlining in one of the projects. If not, inlining can be done from IntelliJ run as in the current DroidMate version.
	
Questions? Problems? Need to reproduce something else? Write to me.
