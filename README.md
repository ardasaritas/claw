# 🐾 Claw

**Claw** is a one-command C development environment initializer for macOS.  
It sets up a complete, fully functional Visual Studio Code workspace for C or C++ projects with:

- 🛠 Build + Debug configuration   
- 🧠 VSCode IntelliSense (`c17` / `c++17` standards)  
- 🧪 Integrated build script with automatic extension handling  
- 💻 Support for both `.c` and `.cpp` files  

---

## 📦 What It Does

```bash
claw init my-project/
```

Creates the following inside `my-project/`:

```
.vscode/
├── tasks.json
├── launch.json
├── c_cpp_properties.json
├── settings.json
├── extensions.json
Makefile
main.cpp
```

You can open the folder in VSCode and immediately press **F5** to build and run your C code.

---

## ✅ Features

- ✅ Works with both `.c` and `.cpp` files  
- 🐚 Shell-based — no dependencies beyond macOS and VSCode  
- 📦 Copies a template `.vscode/` setup into any directory  
- 📋 Customizable architecture (`macos-clang-arm64` or Intel manually)  
- 🧹 Uses `clang` and `clang++` accordingly, cleans executables on command  
- ⚙️ Includes a Makefile for terminal builds  
- 🧪 Error output uses `$gcc` matcher for clean VSCode Problems tab integration  

---

## 💻 Requirements

Before using `claw`, make sure you have:

| Tool | How to Get It |
|:-|:-|
| **Xcode Command Line Tools** | Run: `xcode-select --install` |
| **Homebrew** | [Install Homebrew](https://brew.sh) |
| **Visual Studio Code** | [Download VSCode](https://code.visualstudio.com/) |
| **VSCode CLI (`code`)** | Cmd+Shift+P → “Install 'code' command in PATH” |

---

## 🍺 Installation via Homebrew

```bash
brew tap ardasaritas/clawtap
brew install claw
```

Then you can run:

```bash
claw init <folder>
```

---

## 🚀 Quick Start

```bash
claw init myproject
cd myproject
chmod +x .vscode/c_cpp_build.sh
code .
```

---

## 📁 Template Contents

| File | Purpose |
|:-|:-|
| `.vscode/tasks.json` | Compiles the active file using `clang` or `clang++` |
| `.vscode/launch.json` | Launches the compiled output with LLDB |
| `.vscode/c_cpp_properties.json` | Sets include paths, standards, and architecture |
| `.vscode/settings.json` | Enables squiggles and IntelliSense hints |
| `Makefile` | (Optional) terminal-based build |
| `main.c` | (Optional) Hello World for testing |

---

## ⌨️ VSCode Shortcuts

To initialize Run, Build, and Clean shortcuts: 
    Hit `Cmd + Shift + P` then type "Preferences: Open Keyboard Shortcuts (JSON)"
    Click `enter`, and paste the following: 
    
    `// Place your key bindings in this file to override the defaults
    [
        {
            "key": "cmd+shift+r",
            "command": "workbench.action.tasks.runTask",
            "args": "Build Current File"
        },
        
        {
            "key": "cmd+r",
            "command": "workbench.action.tasks.runTask",
            "args": "Run Current File"
        },

        {
            "key": "cmd+shift+c",
            "command": "workbench.action.tasks.runTask",
            "args": "Clean"
        }
    ]`
    
    You are done, customize it as you wish by changing the "key" field. 
    
| Shortcut | Action |
|:-|:-|
| `Cmd + Shift + R` | Build |
| `Cmd + R` | Run |
| `Cmd + Shift + C` | Clean |
| `fn + F5` | Debug |
| `Cmd + Shift + P` | Command palette |
| `Cmd + P` | Open file |

(You can learn many more) 
---

## 🐞 Debugging: I can't see my `printf()` output after `scanf()`

This is a common issue when debugging C programs using LLDB on macOS.

### 🧠 Symptom:
- You see the `scanf()` prompt and can enter input.  
- But `printf()` after `scanf()` never appears.  
- Or the terminal closes before showing final output.

### 🛠 Why it happens:
- When using `"externalConsole": true`, we're in a real Terminal.
- `stdout` may be **fully buffered** — `printf()` output doesn't show unless flushed.
- (You might want to google these terms for better understanding.)

### ✅ Solution:

At the beginning of `main()`:

```c
setvbuf(stdout, NULL, _IOLBF, 0); // force line-buffered output
```

Or manually flush:

```c
printf("You entered: %d\n", a);
fflush(stdout);
```

Or just use the easy trick of ending every printf string with a new line. It should mostly work. 

---

### ✅ If your program hangs after `scanf()`:
Make sure you're entering valid input and pressing Enter.  
For example, `scanf("%d", &a);`, it **waits until it gets a number**.

---

## 🎯 FAQ

### ❓ Why do we use `.cpp` files even for C?
Some departments default to `.cpp` for simplicity, even in pure C courses.  
Claw supports both `.c` and `.cpp`.

---

## ✨ Bonus Tips

- Use `make` if you prefer the terminal over F5
- You can theme VSCode: `Cmd + K`, then `Cmd + T` to choose.
  I've already added extensions 'C/C++ Themes' and 'Github Theme' for you. 
- Run `code .` from any folder to launch VSCode there

---

## 📜 License

MIT © Arda Sarıtaş  
Use freely, modify boldly, share kindly.

---

## 💬 Feedback

Questions or suggestions?  
Open an issue or reach out at: [github.com/ardasaritas](https://github.com/ardasaritas)
