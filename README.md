# 🐾 Claw

**Claw** is a one-command C development environment initializer for macOS.  
It sets up a complete, fully functional Visual Studio Code workspace for C or C++ projects with:

- Build + Debug configuration   
- VSCode IntelliSense (`c17` / `c++17` standards)  
- Integrated build script with automatic extension handling  
- Support for both `.c` and `.cpp` files  

---

## Usage


https://github.com/user-attachments/assets/25c16a4e-377d-4c0e-8bfb-0c7de1557a89


## What It Does

```bash
claw init <folder>
```

Creates the following inside `<folder>`:

```
.vscode/
├── c_cpp_build.sh
├── c_cpp_properties.json
├── launch.json
├── settings.json
└── tasks.json
Makefile
main.cpp
```

You can open the folder in VSCode and immediately start building, running, debugging your C code. 

---

## Features

- Works with both `.c` and `.cpp` files  
- Shell-based — no dependencies beyond macOS and VSCode  
- Copies a template `.vscode/` setup into any directory  
- Customizable architecture (`macos-clang-arm64` or Intel manually)  
- Uses `clang` and `clang++` accordingly, cleans executables on command  
- Includes a Makefile for terminal builds  
- Error output uses `$gcc` matcher for clean VSCode Problems tab integration  

---

## Requirements

Before using `claw`, make sure you have:

| Tool | How to Get It |
|:-|:-|
| **Xcode Command Line Tools** | Run: `xcode-select --install` |
| **Homebrew** | [Install Homebrew](https://brew.sh) |
| **Visual Studio Code** | [Download VSCode](https://code.visualstudio.com/) |
| **VSCode CLI (`code`)** | Cmd+Shift+P → “Install 'code' command in PATH” |

---

## Installation via Homebrew 🍺

```bash
brew tap ardasaritas/claw
brew install claw
```

---

## Quick Start

```bash
claw init <folder>
```
then 
```bash
cd <folder>
chmod +x .vscode/c_cpp_build.sh
code .
```
These commands will also show up as Next Steps when you initialize the folder with claw. 
Just copy and paste, then click enter. 
(Change `<folder>` with the name you'd like for your root folder. For instance, claw init CTIS151)

---

## Template Contents

| File | Purpose |
|:-|:-|
| `.vscode/tasks.json` | Initializes tasks for building, running, debugging, and cleaning |
| `.vscode/launch.json` | Launches the compiled output with LLDB for debugging|
| `.vscode/c_cpp_properties.json` | Sets include paths, standards, and architecture |
| `.vscode/settings.json` | Enables squiggles and IntelliSense hints |
| `Makefile` | Terminal-based build |
| `main.cpp` | Hello World for testing |

---

## VSCode Shortcuts

To initialize Run, Build, and Clean shortcuts: 
    Hit `Cmd + Shift + P` then type "Preferences: Open Keyboard Shortcuts (JSON)"
    Click `enter`, and paste the following: 
    
    // Place your key bindings in this file to override the defaults
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
    ]

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

## Debugging: I can't see my `printf()` output after `scanf()`

This is a common issue when debugging C programs using LLDB on macOS.

### Symptom:
- You see the `scanf()` prompt and can enter input.  
- But `printf()` after `scanf()` never appears.  
- Or the terminal closes before showing final output.

### Why it happens:
- When using `"externalConsole": true`, we're in a real Terminal.
- `stdout` may be **fully buffered** — `printf()` output doesn't show unless flushed.
- (You might want to google these terms for better understanding.)

### Solution:

Manually flush after every printf() statement:

```c
printf("You entered: %d\n", a);
fflush(stdout);
```

Or just use the easy trick of ending every printf string with a new line. It should mostly work. 

---

### If your program hangs after `scanf()`:
Make sure you're entering valid input and pressing Enter.  
For example, `scanf("%d", &a);`, it **waits until it gets a number**.

---

## FAQ

### Why do we use `.cpp` files even for C?
Some departments default to `.cpp` for simplicity, even in pure C courses.  
Claw supports both `.c` and `.cpp`.

---

## Bonus Tips

- Use `make` if you prefer the terminal over F5
- You can theme VSCode: `Cmd + K`, then `Cmd + T` to choose.
  I've already added extensions 'C/C++ Themes' and 'Github Theme' for you. 
- Run `code .` from any folder to launch VSCode there

---

---

## Updating Claw

To upgrade Claw to the latest version:

```bash
brew update
brew upgrade claw
```

You can verify the installed version:

```bash
brew list --versions claw
```

If you haven’t tapped the repo yet:

```bash
brew tap ardasaritas/claw
```

---

## Uninstalling Claw

To remove Claw completely from your system:

```bash
brew uninstall claw
brew untap ardasaritas/claw
```

## License

MIT © Arda Sarıtaş  
Use freely, modify boldly, share kindly.

---

## Feedback

Questions or suggestions?  
Open an issue or reach out at: [github.com/ardasaritas](https://github.com/ardasaritas)
