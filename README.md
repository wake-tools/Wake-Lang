# 🌀 Wake Lang

> The live scripting language of the **Wake JIT Engine** — designed for instant execution, modularity, and creativity.

---

### 📘 Documentation
See the full documentation in the [**Wake Lang Wiki**](https://github.com/wake-tools/Wake-Lang/wiki).

---

### ⚙️ Overview
Wake Lang is a lightweight, C-based scripting language built to run **instantly** inside the [Wake JIT Engine](https://github.com/wake-tools/Wake).  
It allows live execution, rapid prototyping, and direct interaction with native libraries — no compilation delay, no overhead.

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
| `|` | Parallel | Runs commands simultaneously. |
| `{}` | Variables | Dynamic placeholders using JSON-like nodes. |


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

Run it instantly inside the Wake environment, no build step required.
