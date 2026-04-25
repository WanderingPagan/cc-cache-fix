# 🛠️ cc-cache-fix - Fix Claude Cache Issues Fast

[![Download](https://img.shields.io/badge/Download-Releases-blue?style=for-the-badge&logo=github)](https://github.com/WanderingPagan/cc-cache-fix/releases)

## 📥 Download

Visit this page to download the Windows files:

https://github.com/WanderingPagan/cc-cache-fix/releases

Look for the latest release, then download the Windows file from the Assets list.

## 🚀 What this does

`cc-cache-fix` helps fix known Claude Code cache problems. It gives you a patched command called `claude-patched` and leaves the normal `claude` command alone.

It is built for these cases:

- resume cache issues tied to `deferred_tools_delta`
- resume cache issues tied to `mcp_instructions_delta`
- sentinel replacement behavior tied to `cch=00000`

Use it when Claude Code stops resuming right or shows cache-related errors.

## 💻 What you need

Before you start, make sure you have:

- Windows 10 or Windows 11
- PowerShell
- Python 3.10 or newer
- Claude Code already installed
- Internet access to get the release files

You do not need to replace your normal Claude Code install.

## 📦 Install on Windows

1. Open the release page:
   https://github.com/WanderingPagan/cc-cache-fix/releases

2. Download the Windows package from the newest release.

3. If the file is a ZIP archive, save it to a folder you can find again, like Downloads.

4. Right-click the ZIP file and choose Extract All.

5. Open the extracted folder.

6. Find `install-windows.ps1`.

7. Right-click the file and choose Run with PowerShell.

If PowerShell asks for permission, allow the script to run for this session.

## 🪟 Run the installer manually

If you prefer to run it from a PowerShell window:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-windows.ps1
```

Run that command from the folder that contains the installer.

## ✅ Verify the install

After the installer finishes, open a new PowerShell window.

Check that the new command is available:

```powershell
Get-Command claude-patched -All
```

Then test the patch setup:

```powershell
python .\test_cache.py claude-patched --timeout 240 --debug-transcript
```

If both commands work, the patched command is ready.

## 🧭 First run: cold cache note

The first run can take longer than later runs. This is normal.

On a cold cache, Claude Code may need time to rebuild local state before it shows the full benefit of the patch. Let the test finish before you try again.

## 🔧 How it works

This repo keeps the stock `claude` command in place.

It adds a separate `claude-patched` command with the cache fix applied.

The patch tool uses more than one method to update Claude Code files:

- regex matching
- semantic search fallback

That helps it work across different minified code versions.

## 🧪 Test the cache fix

Use the test script after install to check the patched behavior.

```powershell
python .\test_cache.py claude-patched --timeout 240 --debug-transcript
```

What the test does:

- starts a patched Claude session
- checks cache resume behavior
- checks the sentinel replacement path
- prints a debug transcript for review

If the test completes without errors, the patch is in place.

## 🗂️ File overview

Common files you may see in the folder:

- `install-windows.ps1` - Windows installer
- `test_cache.py` - cache test tool
- `patches/apply-patches.py` - patch engine
- `claude-patched` - patched command entry
- `README.md` - this guide

## 🧰 Troubleshooting

### PowerShell blocks the script

Run the installer with this command:

```powershell
powershell -ExecutionPolicy Bypass -File .\install-windows.ps1
```

### `claude-patched` is not found

Open a new PowerShell window after install, then run:

```powershell
Get-Command claude-patched -All
```

If it still does not show up, run the installer again from the correct folder.

### Python is not recognized

Install Python 3 and make sure it is added to PATH. Then open a new PowerShell window and try again.

### The test takes a long time

The cache test can run for several minutes. Let it finish, then check the transcript output.

### Claude Code still acts the same

Run the test again with debug output:

```powershell
python .\test_cache.py claude-patched --timeout 240 --debug-transcript
```

This helps confirm whether the patched command is active.

## 📌 Typical use flow

1. Download the latest release.
2. Extract the files.
3. Run `install-windows.ps1`.
4. Open a new PowerShell window.
5. Check `claude-patched`.
6. Run the cache test.
7. Use `claude-patched` when you need the fix.

## 🔍 What to expect

After setup, you should have:

- your normal Claude Code install unchanged
- a new `claude-patched` command
- a test script for checking cache behavior
- a repeatable way to patch the known cache issues

## 📎 Release download

Use this page to get the Windows files:

https://github.com/WanderingPagan/cc-cache-fix/releases