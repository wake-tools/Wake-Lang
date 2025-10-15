# 🌀 Wake Lang

> The live scripting language of the **Wake JIT Engine** — designed for instant execution, modularity, and creativity.

---

### ⚙️ Overview
Wake Lang is a lightweight, C-based scripting language built to run **instantly** inside the [Wake JIT Engine](https://github.com/wake-tools/Wake).  
It allows live execution, rapid prototyping, and direct interaction with native libraries — no compilation delay, no overhead.

Wake language is **branchless, deterministic, and linear** — a language designed to be *followed, not guessed*.

There are no hidden branches, no random states, and no ambiguous logic.  
Every line executes in the exact order it’s written — **clear, predictable, and easy to trace**.

---

| Principle | Description |
|:-----------|:-------------|
| **Branchless** | No `if`, `else`, or branching logic. Wake Lang focuses on describing **flows**, not decisions. |
| **Deterministic** | Every execution produces the same result — no race conditions, no state drift, no randomness. |
| **Linear** | Commands flow top-to-bottom in a perfectly ordered sequence — you can literally read it like a book. |
| **Traceable** | The execution path is obvious at all times. There’s no hidden logic — what you see *is exactly what happens*. |

---

### 💡 Why it matters

This design makes Wake Lang:

- 🧩 **Exceptionally easy to read** — anyone can open a `.jc` file and instantly understand what it does.  
- 🚀 **Fast to learn** — no complex syntax, no nested logic, no mental gymnastics.  
- ⚙️ **Efficient to maintain** — every instruction is self-contained and predictable.  
- 🕒 **Time-saving** — less debugging, fewer side effects, faster iteration.  
- 🧠 **Mentally lightweight** — scripts are linear and composable; no context-switching required.

> ⚡ *By removing branching and ambiguity, Wake Lang achieves what most languages can’t:*  
> *a perfectly predictable, visual, and human-readable flow of execution.*


---

### 🚀 Highlights
- **Real-time execution** — scripts compile and run instantly.  
- **C99 syntax** — familiar, minimal, and powerful.  
- **Modular runtime** — directly integrated with Wake Tools and Wake Packages (.wpkg).  
- **Cross-platform** — Windows, Linux, and macOS.  

---

### 🧩 Ecosystem
- 🔹 [Wake JIT Engine](https://github.com/wake-tools/Wake) — the runtime powering Wake Lang  
- 🔹 [Wake Tools](https://github.com/wake-tools/Wake-Tools) — standard packages and utilities  
- 🔹 [Wake Lang Wiki](https://github.com/wake-tools/Wake-Lang/wiki) — full reference and examples  

---

### 🔹 Core Syntax (currently implemented)

| Symbol | Purpose | Description |
|:-------:|:---------|:-------------|
| `>` | Sequence | Runs commands in order (waits for completion). |
| `\|` | Parallel | Runs commands simultaneously. |
| `{}` | Variables | Dynamic placeholders using JSON-like nodes. |

---

### 💡 Typical language from
```c
build | build > run
```

### 💡 Minimal example
```c
/*|------------------------------------------------------------>>
  | run: wake > hello.jc
  |------------------------------------------------------------>>
    <:jit:w32|w64>
        {wk.module.sys.r}wake-tools/tcc-v0.1w/tcc
            -xc -shared {this.file}
            -o {jit.file}
        >
        #Jit.reload
    <:/jit:>
  |------------------------------------------------------------>>
*/
#include <stdio.h>

int main(void) {
    printf("Hello, Wake!\n");
    return 0;
}
```

> Run it instantly inside the Wake environment, no build step required.

---
### 🔹 Execution Metadata

Execution metadata defines **how a Wake Lang script is built and executed**.  
These tags can appear at the beginning of a file — or even *inside C code blocks* — allowing **dynamic recompilation**, *runtime code injection*, or *conditional JIT execution*.

| Tag | Purpose | Description |
|:----:|:---------|:-------------|
| `<:jit:>` | JIT Block | Defines how the file is compiled and executed in Wake. |
| `<:/jit:>` | JIT End Block | Defines how the file is compiled and executed in Wake. |
| `w32 \| w64` | Target | Indicates 32-bit or 64-bit platform targets. |
> 🧩 *Execution metadata can live both **around** and **within** code — enabling nested instructions, live recompilation, and self-modifying scripts.*
---

### 🔹 Execution Directives

These special tags control **how and when** a Wake Lang script is reloaded or re-executed by the runtime.  
They are used inside the `<:jit:>` block to provide *live reactivity* and *dependency awareness*.

| Tag | Purpose | Description |
|:----:|:---------|:-------------|
| `#Jit.reload` | Reload Directive | Reloads and executes the compiled code instantly, and automatically when the file is modified. |
| `#Jit.depends` | Dependency Directive | Registers one or more files as dependencies; triggers reload when any of them is modified. |

> 🧩 *Execution directives bring Wake Lang to life — enabling live editing, auto-reload, and hot dependency tracking.*

---

### 🔹 Built-in Variables List

Wake Lang exposes several **core environment variables** that provide context about the runtime, build system, and file paths.  
They make scripts **portable and self-adaptive**, automatically resolving to the correct directories depending on the platform and mode.

| Variable | Description | Example Output |
|:----------|:-------------|:----------------|
| `{wk.include}` | Absolute path to the include directory for Wake headers and packages. | `wake/runtime/include/` |
| `{wk.libs}` | Absolute path to the Wake runtime libraries. | `wake/runtime/libs/` |
| `{wk.module}` | Absolute path to the Wake system modules. | `wake/runtime/module/` |
| `{wk.module.sys.r}` | Absolute path to the Wake system modules in **release mode**. | `wake/runtime/module/w64-r/` |
| `{wk.module.sys.d}` | Absolute path to the Wake system modules in **debug mode**. | `wake/runtime/module/w64-d/` |
| `{build.sys}` | Current build system name derived from the Wake executable type. | `win64` |
| `{build.sys.r}` | Build system identifier for **release mode**. | `win64-r` |
| `{build.sys.d}` | Build system identifier for **debug mode**. | `win64-d` |
| `{this.file}` | Reference to the current `.jc` file being executed. | `samples/hello.jc` |
| `{jit.file}` | Reference to the JIT-compiled binary generated by Wake. | `samples/hello.dll` |

> 🧩 *These variables are automatically provided by the Wake runtime and resolved before command execution. They ensure scripts remain consistent across environments, architectures, and build modes.*

---

### 📦  Package Resolution System 

Wake Lang relies on a **strict, deterministic, and secure package system** —  
ensuring that every dependency is *perfectly resolved*, *cryptographically verified*, and *immutable* once installed.

Whenever a path like `{wk.module.sys.r}wake-tools/tcc-v0.1w/tcc` is referenced, Wake will:

1. 🧩 **Detect the package name** (`wake-tools/tcc-v0.1w`)  
2. 🔍 **Check if it exists** locally under `{wk.module.sys.r}`  
3. 🌐 **Fetch it automatically** if missing (via Wake’s signed `.wpkg` format)  
4. 🔏 **Verify its Ed25519 signature** and ensure integrity before mounting  
5. ⚙️ **Load and execute** the referenced tool or library instantly — no setup, no rebuild

---

| Icon | Component | Description | Example |
|:----:|:-----------|:-------------|:---------|
| 📦 | `.wpkg` | Wake Package — compressed and signed module archive. | `tcc-v0.1w.wpkg` |
| 🧱 | `{wk.module.sys.r}` | System package root (release mode). | `wake/runtime/module/w64-r/` |
| 🌍 | `wake-tools/<package>` | Remote namespace or repository source. | `wake-tools/tcc-v0.1w` |
| ⚙️ | `.sm` | Optional submodule containing runtime metadata or preload. | `.sm/clear-sapp.sm` |

> 🔒 *All Wake packages are cryptographically signed and resolved deterministically.  
They cannot be overridden or tampered with — ensuring a stable, reproducible, and secure runtime.*

> 🧩 *Wake automatically fetches missing packages, verifies signatures, and loads them live — enabling scripts to run anywhere without setup.*

---
