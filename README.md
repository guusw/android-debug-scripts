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

## Scripts & usages

### `set_device_id <DEVICE_ID>`

Run the first time from a new working directory to set the device ID to debug on. Use the output from `adb devices`

### `launch_debug <PACKAGE_NAME> <ACTIVITY_NAME>`

Launches the package/activity in debug mode while waiting for the java debugger to attach

### `launch_jdb_continue`

Attached the java debugger and signals the previously launched process to continue

### `launch_ndebug <PACKAGE_NAME> <ACTIVITY_NAME>`

Launches the package/activity without debugging and streams logcat output to console and `logcat.log` file in the current working directory

### `launch_code_debug <PACKAGE_NAME> <ACTIVITY_NAME>`

Launches the package/activity in debug mode and attaches the vscode debugger from the `vscode-lldb` extension. Does not require manual use of `launch_jdb_continue`

### `logcat`

Receive process log output in stdout and the `logcat.log` file in the current working directory

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
