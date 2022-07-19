# Android debug scripts

## Requirements

- `jdb` in PATH (from the JDK)
- `adb` in PATH (from android debug tools)

for launching vscode lldb session:

- `code` in PATH
- `vscode-lldb` extension

## Initial setup

- Copy `lldb-server` from the android NDK to the /data/local/tmp folder using `adb push <PATH> /data/local/tmp`

- Call `set_device_id <ID>` once with the output from `adb devices`.

> This stores the ID in current working dir .android_debug folder. So run the other scripts from this same folder

## Usage

after installing, run:

```bash
launch_debug <PACKAGE_NAME> <ACTIVITY_NAME>
```
The application and lldb-server will launch while waiting for the java debugger to attach

Run the following to continue execution:

```bash
launch_jdb_continue
```

> NOTE: It has to be run from the same folder as you ran the launch_debug command

Additionally run:

```bash
logcat
```

To receive process log output in stdout and the `logcat.log` file in the current working directory


## VSCode usage

You can run:

```bash
launch_code_debug <PACKAGE_NAME> <ACTIVITY_NAME>
```

to directly launch a vscode debug session, assuming you have the vscode-lldb extension installed

Additionally this automatically runs:

```bash
logcat
```

which streams the current process log messages to stdout and to `logcat.log` in the current working directory

## Troubleshooting

- Make sure the app has `android:debuggable="true"` on the application tag in `AndroidManifest.xml`
- Make sure the app has the `android.permission.INTERNET` permission in `AndroidManifest.xml`
