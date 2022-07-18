# Android debug scripts

## Requirements

- `jdb` in PATH (from the JDK)
- `adb` in PATH (from android debug tools)

for launching vscode lldb session:

- `code` in PATH
- `vscode-lldb` extension

## Initial setup

For the first time when installing an app

- Copy `lldb-server` from the android NDK to the /data/local/tmp folder using `adb push <PATH> /data/local/tmp`
- Install the app
- Copy `lldb-server` to the apps data folder using `adb run-as <PACKAGE_NAME> cp /data/local/tmp/lldb-server ./`


## Usage

after installing, run:

```bash
./launch_debug <PACKAGE_NAME> <ACTIVITY_NAME>
```
The application and lldb-server will launch while waiting for the java debugger to attach

Run the following to continue execution:

```bash
./launch_jdb_continue
```

> NOTE: It has to be run from the same folder as you ran the launch_debug command


## VSCode usage

You can run:

```bash
./launch_code_debug <PACKAGE_NAME> <ACTIVITY_NAME>
```

to directly launch a vscode debug session, assuming you have the vscode-lldb extension installed

## Troubleshooting

- Make sure the app has `android:debuggable="true"` on the application tag in `AndroidManifest.xml`
- Make sure the app has the `android.permission.INTERNET` permission in `AndroidManifest.xml`s