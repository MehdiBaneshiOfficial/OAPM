# 🔑 Open AG Patcher (English Guide)

Open-source patcher for Antigravity IDE and the standalone Antigravity app: removes regional restrictions without a VPN and without changing your Google account region. This is an open-source equivalent of the "Antigravity IDE in Russia without VPN and without changing Google account region" utility.

## 🎦 Video Install & Troubleshooting Guide
Links to the video guide (YouTube, Dzen, VK Video, Telegram) are in the original repository README.

## ⚠️ HTTP 500 Internal Server Error
If you get an HTTP 500 Internal Server Error in Antigravity IDE, there's nothing to be done — change your account (ideally to a region where Antigravity IDE officially works, or one with a paid subscription). Even the paid utility doesn't fix this.

## ⚠️ HTTP 429 Too Many Requests
If you encounter `HTTP 429 Too Many Requests`, it means your Google-side limits (quota) are exhausted. This is usually tied to a session being linked to an exhausted quota.

**Solution:**
1. Use the built-in patcher feature — **option 7: Fix HTTP 429 (Too Many Requests)**.
   - The script backs up the data folder and clears the old configuration (resetting tokens/quota), but **keeps your conversations**.
   - You'll need to sign in again afterward.
2. If the built-in fix doesn't help — try switching your Google account.
3. **Important:** using a VPN or other restriction-bypass methods may be detected by Google and cause the 429 error to reappear.

More details in [issue #10](https://github.com/AvenCores/open-antigravity-patcher/issues/10).

## ⚠️ HTTP 400 Bad Request
If you get `HTTP 400 Bad Request` with the message `User location is not supported for the API use`, Google has determined your location to be unsupported.

**Important:** using a VPN, proxy, or other restriction-bypass methods may be detected by Google and trigger this same error. Google actively fights bypass methods, and if your IP address or other session parameters look suspicious, access may be blocked.

**Solution:**
1. If you're on Antigravity IDE version **1.23.0 or higher**, apply the patch (**option 1: Apply patch**). The patcher automatically adds the necessary parameters to `settings.json` to work around this error (see the "Temporary runtime settings workaround" section below).
2. If the patch is already applied or your version is below 1.23, try switching Google accounts or using a different VPN.
3. You can try **[Xbox DNS](https://xbox-dns.ru/)** (special DNS servers for bypassing restrictions on a PC or router).

## 📚 Additional Error Information
For a deeper understanding of HTTP error types and diagnostics, this guide is recommended:
- [5xx Server Errors: The Complete Guide](https://komodor.com/learn/5xx-server-errors-the-complete-guide/)

## 🌟 Features
- Automatic detection of installed Antigravity IDE, the standalone Antigravity app, and Antigravity CLI (`agy`) in standard paths and the Windows registry.
- **Antigravity CLI patch** — removes the "Eligibility Check" screen in the Go binary (`agy`/`agy.exe`) at the machine-code level via a byte signature (with backup and rollback).
- Full unpacking, modification, and repacking of `app.asar` for Antigravity, preserving the structure of unpacked external files (`.unpacked`).
- Integrated local HTTP proxy server for dynamic patching of JS code loaded in the standalone Antigravity app.
- Linux support: searches `/usr/share/antigravity-ide`, detects version via `dpkg`, `rpm`, and `package.json`.
- macOS support: searches for the `.app` bundle in `/Applications` and `~/Applications`, ad-hoc re-signing after modifying `main.js` or `app.asar`.
- Creates a backup before making changes.
- Apply and roll back the patch via a simple menu.
- Supports `resources/app/out/main.js` and `resources/app/main.js` paths.
- Colored output and automatic privilege elevation attempt (UAC on Windows, `sudo` prompt on Linux).
- Checks minimum Antigravity IDE version (>= `2.0.1`) before applying the patch.
- Detects Antigravity IDE version via the Windows registry, a Linux package manager, or `package.json` on macOS.
- Detects an already-applied patch and offers to reapply it.
- Temporary runtime workaround for Antigravity IDE `1.23+`: pins a stable Cloud Code endpoint and disables problematic Cascade/model experiments via `settings.json`.

## 🚀 How to Use
1. Close Antigravity IDE or Antigravity.
2. Run the patcher as administrator (the script will request elevation itself if needed).
3. Choose an action from the menu:

| Menu item | Description |
|---|---|
| `1. Apply Antigravity IDE patch` | Apply the patch to `main.js` for Antigravity IDE |
| `2. Apply Antigravity patch` | Apply the patch to `app.asar` for standalone Antigravity |
| `3. Apply Antigravity CLI (agy) patch` | Apply the patch to the `agy`/`agy.exe` binary for Antigravity CLI |
| `4. Restore Antigravity IDE from backup` | Restore the original `main.js` for Antigravity IDE |
| `5. Restore Antigravity from backup` | Restore the original `app.asar` for standalone Antigravity |
| `6. Restore Antigravity CLI from backup` | Restore the original `agy`/`agy.exe` |
| `7. Fix HTTP 429` | Reset configuration to fix the 429 error (keeps conversations) |
| `8. Open GitHub repository` | Open the project page in a browser |
| `9. Select custom path` | Manually select the app folder or file path |
| `0. Exit` | Exit |

Run from source:
```bash
python main.py
```

Run with a path specified (for Antigravity IDE, standalone Antigravity, or Antigravity CLI):
```bash
# Windows
python main.py "C:\Users\<username>\AppData\Local\Programs\Antigravity IDE"
python main.py "C:\Users\<username>\AppData\Local\Programs\Antigravity\resources\app.asar"
python main.py "C:\Users\<username>\AppData\Local\agy\bin\agy.exe"

# Linux
python main.py /usr/share/antigravity-ide
python main.py /opt/Antigravity
python main.py /usr/local/bin/agy

# macOS
python3 main.py /Applications/Antigravity\ IDE.app
python3 main.py /Applications/Antigravity.app
python3 main.py /usr/local/bin/agy
```

If `main.js` or `app.asar` is located next to the script, you don't need to specify a path — it will be found automatically.

> **macOS:** if `Antigravity IDE.app` is in `/Applications`, writing requires `sudo` (the script will offer to restart with it). For installs in `~/Applications` or a user directory, `sudo` is not needed. After a successful patch, the `.app` is automatically re-signed with an ad-hoc signature (`codesign --force --deep --sign -`) — without this, Electron apps with Hardened Runtime won't launch on macOS.

### 🍎 Using on macOS
Since pre-built binaries for macOS are not available in official releases (only Windows and Linux are), you can either run the patcher directly from source or build the executable yourself.

**Option 1: Run from source (recommended)**
1. Create and activate a virtual environment, then install dependencies:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```
2. Fully close Antigravity or Antigravity IDE.
3. Run the patcher, specifying the path to the app:
   ```bash
   # For Antigravity IDE
   python3 main.py "/Applications/Antigravity IDE.app"
   
   # For the standalone version
   python3 main.py "/Applications/Antigravity.app"
   ```
   *Note: if the app is in `/Applications`, the script will automatically request elevated privileges (`sudo`) to write.*

**Option 2: Build the binary yourself**
If you need a ready-made executable, you can build it yourself following the instructions in the "🛠️ Build" section.

After a successful build, run the compiled file via Terminal:
```bash
cd dist
chmod +x Open_AG_Patcher_macOS
sudo ./Open_AG_Patcher_macOS
```
If macOS blocks the compiled file from running, remove the quarantine attribute:
```bash
xattr -dr com.apple.quarantine Open_AG_Patcher_macOS
```

**What to choose in the menu**
- `1. Apply Antigravity IDE patch` for `Antigravity IDE.app`
- `2. Apply Antigravity patch` for standalone `Antigravity.app`
- `3. Apply Antigravity CLI (agy) patch` for the `agy` binary (if installed)
- `4`, `5`, or `6` to restore from backup

For standalone `Antigravity.app`, the patcher usually finds it automatically at:
```text
/Applications/Antigravity.app
```
If auto-detection doesn't find the app, choose `9. Select custom path` and enter one of:
```text
/Applications/Antigravity.app
/Applications/Antigravity IDE.app
```

**Verify the signature**
After patching, the `.app` is automatically re-signed with an ad-hoc signature. Verify with:
```bash
codesign -dv /Applications/Antigravity.app 2>&1 | grep Signature
```
Expected output:
```text
Signature=adhoc
```

## ❓ What Exactly Changes

### Patch for Antigravity IDE
The patcher makes **4 edits** to `main.js` and applies a separate temporary runtime workaround in the user's `settings.json`. Changes to `main.js` are reversible via a backup (`main.js.bak`), and `settings.json` is backed up separately before being written.

**1. `if(isGoogleInternal)` → `if(true)`**
Replaces the `isGoogleInternal` flag check with an unconditional `true`, removing regional/internal restrictions. Applied to all occurrences in the file (pattern `if(this.<svc>.isGoogleInternal)`).

**2. `if(X(),this.Y.isGoogleInternal)` → `if(X(),true)` (auth service)**
The auth service checks different patterns depending on version:
- **v1.22–v1.22.x:** `if(this.w.resetIsTierGCPTos(),this.t.isGoogleInternal)` → `if(this.w.resetIsTierGCPTos(),true)`
- **v1.23+:** `if(this.t.send({...}),this.y.resetIsTierGCPTos(),this.w.isGoogleInternal)` → `if(this.t.send({...}),this.y.resetIsTierGCPTos(),true)`

The patcher automatically detects the Antigravity IDE version and applies the matching pattern.

**3. `ideName` → `"antigravity-insiders"`**
Replaces `ideName:"antigravity"` with `ideName:"antigravity-insiders"` for correct client identification.

**4. `ineligible` screen — bypass (v1.22+)**
Replaces the spread ternary `...s?{}:{errorType:"ineligible",reason:a,verificationUrl:i}` with `...s?{}:{}` — the ineligible error is no longer sent and the block screen is not shown.

**5. Temporary runtime settings workaround (v1.23+)**
Starting with Antigravity IDE `1.23+`, some users get this error after updating:
```json
{
  "error": {
    "code": 400,
    "message": "User location is not supported for the API use.",
    "status": "FAILED_PRECONDITION"
  }
}
```
Logs show requests to `daily-cloudcode-pa.googleapis.com` and new Cascade/model experiments. This is a temporary fix and should be removed or reviewed once Antigravity IDE stabilizes the new route/experiment or restores compatible behavior. The workaround adds the following to the user's `settings.json`:
```json
{
  "jetski.cloudCodeUrl": "https://cloudcode-pa.googleapis.com",
  "codeiumDev.forceDisableExperiments": "CASCADE_DEFAULT_MODEL_OVERRIDE,CASCADE_USE_EXPERIMENT_CHECKPOINTER,CASCADE_NEW_MODELS_NUX,CASCADE_NEW_WAVE_2_MODELS_NUX",
  "codeiumDev.languageServerEnv": {
    "BORG_DISABLE_EXPERIMENTS": "CASCADE_DEFAULT_MODEL_OVERRIDE,CASCADE_USE_EXPERIMENT_CHECKPOINTER,CASCADE_NEW_MODELS_NUX,CASCADE_NEW_WAVE_2_MODELS_NUX",
    "BORG_EXPERIMENTS": ""
  }
}
```
If `settings.json` already exists, a backup named `settings.json.bak-YYYYMMDD-HHMMSS` is created before modification. If `main.js` is already patched, `Apply patch` will still apply the runtime workaround without needing to re-modify `main.js`.

### Patch for Standalone Antigravity (ASAR)
For the standalone version, the patching process differs because the UI logic is loaded dynamically over the network:
1. The original archive is copied to a backup (`app.asar.bak` or `app1.asar.bak`) for later rollback, and the archive itself is unpacked into a temporary folder.
2. A network-request interceptor is registered in `dist/main.js`.
3. When Antigravity starts, all requests to frontend scripts (`/main.js`) are redirected to a local HTTP proxy server created inside the app itself.
4. The proxy server downloads the original frontend script, replaces `isGoogleInternal` checks with `true` on the fly, redirects auth-error states to a successful sign-in (`signedIn`), caches the result, and serves it to the app.
5. The modified files are repacked back into `app.asar`, with correct integrity hash computation (SHA256 blocks) and preservation of the unpacked external file structure (`.unpacked`).

> **Note:**
> - The "onboardUser injection" patch has been disabled since v1.22+, since in newer Antigravity IDE versions `onboardUser` is already called natively, and the injection duplicates the call, breaking the auth flow.
> - Since patcher v1.0.8, a **version-based auth pattern selection** is used: the old pattern is applied for Antigravity IDE versions below 1.23, and the new pattern (with an extra `send()` call) for v1.23+.

### Patch for Antigravity CLI (agy)
Antigravity CLI is a separate Go binary (`agy.exe` on Windows, `agy` on Linux/macOS) that also shows a cosmetic "Eligibility Check" screen blocking further use. Since this is a compiled binary (not JS), patching is done **at the machine-code level** via a unique byte signature.

1. In the `handleAuthResult` function, the eligibility gate is built on the server-side field `AuthResult.hasValidAuth` (byte at offset `+8`):
   ```asm
   test rax,rax      ; 48 85 c0
   je   ...          ; 0f 84 xx xx xx xx
   cmp  byte[rax+8],0; 80 78 08 00     <-- eligibility check
   jne  ...          ; 0f 85 xx xx xx xx
   ```
2. The patcher finds this sequence by signature (with wildcards for displacement bytes) and rewrites `cmp byte[rax+8],0` as `test rax,rax ; nop` (`48 85 c0 90`). This makes `ZF=0`, so the conditional jump `jne` always takes the "eligible" branch — the Eligibility screen is no longer shown.
3. Before writing, a backup named `agy.exe.agybak` (or `agy.agybak` on POSIX) is created. If an existing backup is stale (the app auto-updated), it's automatically refreshed — stale copies aren't kept.
4. On macOS, the binary is re-signed ad-hoc after modification (same as with `.app`).

**Patch safety:**
- If the byte signature isn't found in the binary (unknown/unsupported version), the patcher **refuses to patch** and changes nothing — it prints "signature not found (unsupported version?)".
- If the signature appears more than once, the patcher also refuses ("not unique — refusing to guess") rather than guessing which site to edit.
- Rollback is done via `6. Restore Antigravity CLI from backup`, restoring from `.agybak`.

> **Platform note:** the signature has been verified on Windows (`agy.exe` Go binary). Discovery searches for the binary cross-platform (`PATH`, scoop on Windows, `/usr/local/bin`, `/opt/antigravity/bin`, `~/.local/bin` on POSIX). On Linux/macOS, the `agy` binary may be compiled differently and the signature may not match — in that case the patch will honestly report this without modifying the file.

## 🔍 File Search Logic
The patcher searches for `main.js` in this order:
1. Command-line argument (path to a directory or directly to `main.js`).
2. Current directory (`./main.js`).
3. Automatic search in standard paths:
   - **Windows:** `%LOCALAPPDATA%\Programs\Antigravity IDE`
   - **Linux:** `/usr/share/antigravity-ide`, `/opt/Antigravity IDE`, `/opt/Antigravity IDE/resources/app/out`
   - **macOS:** `/Applications/Antigravity IDE.app/Contents/Resources/app`, `~/Applications/Antigravity IDE.app/Contents/Resources/app`
4. Windows registry (key `{AA73B3E3-C6C8-45C8-B1DC-4AE56C751432}_is1` in `HKCU` and `HKLM`: `SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall\`).

Inside the found directory, these paths are checked:
- `resources/app/out/main.js`
- `resources/app/main.js`
- `out/main.js` (macOS)
- `main.js` (if the path is given directly)

On macOS, the script also accepts a path to the `.app` bundle directly — `Contents/Resources/app/out/main.js` is resolved automatically.

### Antigravity CLI (`agy`) Discovery
The `agy` binary (`agy.exe` on Windows) is searched for in a location-agnostic way — via `PATH` and standard directories, with no hardcoded paths/versions:
1. Command-line argument or menu option `9. Select custom path → 3` (path to the `agy`/`agy.exe` file or folder).
2. `PATH` (`shutil.which("agy")`).
3. Standard directories:
   - **Windows:** `%LOCALAPPDATA%`, `%PROGRAMFILES%`, `%PROGRAMFILES(X86)%`, `%ProgramData%`, `%APPDATA%` (+ `Programs` subfolder), scoop (`%USERPROFILE%\scoop\apps`, `%SCOOP%\apps`). Patterns: `agy/bin/agy.exe`, `agy/*/bin/agy.exe` (scoop version-dirs), `agy*/agy.exe`.
   - **Linux/macOS:** `/usr/local/bin`, `/usr/bin`, `/opt/antigravity/bin`, `/opt/antigravity`, `~/.local/bin`, `~/bin`.

If multiple copies are found (e.g., scoop with several versions), the most recent by mtime is selected.

## 🔎 Antigravity IDE Version Detection

| Platform | Version detection method |
|---|---|
| **Windows** | Registry: `DisplayVersion` from key `{AA73B3E3-...}_is1` |
| **Linux (deb)** | `dpkg-query -W antigravity-ide` |
| **Linux (rpm)** | `rpm -q --queryformat %{VERSION} antigravity-ide` |
| **Linux (portable/snap/flatpak)** | `package.json` next to `main.js` |
| **macOS** | `package.json` in `Antigravity IDE.app/Contents/Resources/app/` |

If the version can't be detected, the patcher offers to continue without checking. If the version is below `1.22.2`, it warns and again offers a choice.

## 🔒 Already-Patched Check
Before patching, the script checks whether the file has already been patched, based on two signs:
- absence of `if(this.X.isGoogleInternal)` (the pattern has been replaced with `if(true)`)
- presence of the string `"antigravity-insiders"`

If both signs are found, a warning is shown asking for confirmation to reapply.

## 🛡️ Privilege Elevation
- **Windows:** automatic UAC prompt via `ShellExecuteW` with the `runas` parameter. Correctly handles paths with spaces.
- **Linux:** if the script isn't running as root, it offers to restart via `sudo` (`os.execvp`). If declined, it continues with a warning about possible write errors. The runtime workaround writes to the original user's `settings.json` (`SUDO_USER`/`SUDO_UID`), not to `/root/.config/...`.
- **macOS:** uses the same posix branch — `sudo` is offered if not run as root. For `~/Applications/Antigravity IDE.app` you can answer "n" to the sudo prompt (the directory is already writable), but for `/Applications/Antigravity IDE.app` you should agree. When run via `sudo`, the user's `settings.json` is also read from the original user's home, not `root`'s.

## 🍎 macOS Specifics

**Re-signing the `.app` after patching**
Any change to a file inside a signed `.app` bundle breaks the code signature. Electron apps with Hardened Runtime enabled (Antigravity IDE is one of them) will **not launch** on macOS after this — even before Gatekeeper shows the user a dialog.

For the `.app` to keep working, the script automatically runs the following after `do_patch` and `do_restore`:
```bash
codesign --force --deep --sign - /path/to/Antigravity\ IDE.app
xattr -dr com.apple.quarantine /path/to/Antigravity\ IDE.app
```
`--sign -` means an ad-hoc signature (no Developer ID). This is enough for running the app locally. Notarization isn't required.

Requires `codesign` to be installed, which comes with **Xcode Command Line Tools**:
```bash
xcode-select --install
```

**"Operation not permitted" error while patching**
If you hit this error: `[!] Backup error: [Errno 1] Operation not permitted: '/Applications/Antigravity IDE.app/Contents/Resources/app/out/main.js.bak'`:
1. Grant Full Disk Access to your terminal: **System Settings → Privacy & Security → Full Disk Access**.
2. Remove the app's quarantine attribute:
   ```bash
   sudo xattr -rd com.apple.quarantine /path/to/Antigravity\ IDE.app
   ```

**If the app won't launch after patching**
1. Make sure `codesign` is available: `which codesign`.
2. Check that the `.app` was re-signed: `codesign -dv /Applications/Antigravity\ IDE.app 2>&1 | grep Authority` — it should show `Signature=adhoc`.
3. If macOS still blocks it: go to **System Settings → Privacy & Security** — at the bottom there will be an "Open Anyway" button.

## ⚙️ Requirements
- **Python** 3.x
- **Dependencies:** `packaging` (for version comparison)
- **OS:**
  - **Windows** — full support for auto-detection via the registry and UAC.
  - **Linux** — auto-detection in `/usr/share/antigravity-ide`, version detection via `dpkg`/`rpm`/`package.json`, sudo elevation.
  - **macOS** — auto-detection in `/Applications/Antigravity IDE.app` and `~/Applications/Antigravity IDE.app`, version detection via `package.json`, ad-hoc re-signing via `codesign` (Xcode Command Line Tools).
- **Minimum Antigravity version:** `2.0.1`
- **Supported versions:** `2.0.1` and above (with version-based auth pattern selection for `1.23+`)

## 🛠️ Build
To build executables, using a virtual environment is recommended. (Full pyinstaller commands for Windows, Linux, and macOS are in the original project files, unchanged.)

## Project Structure
- `main.py` — main entry point for the patcher (handles permission checks and CLI launch).
- `patcher/` — main patcher source code with a modular architecture:
  - `constants.py` — global constants, regular expressions, versions, and injection templates.
  - `cli.py` — console user interface, menu, and input handling.
  - `utils/` — system helper utilities (console colors, admin rights, POSIX permissions, file hashing).
  - `ide/` — logic for finding and patching Antigravity IDE directly (`main.js` files).
  - `asar/` — logic for unpacking/repacking ASAR archives and patching the Antigravity app.
  - `agy/` — logic for finding and byte-signature patching the Antigravity CLI binary (`agy`/`agy.exe`).
- `requirements.txt` — build and runtime dependencies.
- `build.txt` — example build commands for different OSes.
- `icon.ico` — icon for the `exe`/`app`.

## 📜 License
This project is distributed under the GPL-3.0 license. The full license text is in the `LICENSE` file.

---
*This is a quick translation of the original Russian README for the "Open AG Patcher" open-source project. Note that this tool bypasses Google's regional/eligibility restrictions, which may conflict with these services' terms of use; use at your own risk.*