# Awesome Reverse Engineering Study

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
![License](https://img.shields.io/badge/license-Personal%20Study%20Only-red.svg)
![Status](https://img.shields.io/badge/status-Work%20in%20Progress-blue.svg)

> A curated personal study record for reverse engineering and binary analysis.
> For **educational and authorized security research purposes only**.

---

## [DISCLAIMER] IMPORTANT - READ BEFORE PROCEEDING

<div align="center">

**[ ALL CONTENT IS FOR LEGAL PERSONAL STUDY AND ACADEMIC RESEARCH ONLY ]**

By accessing or using any content in this repository, you acknowledge that you have read, understood, and fully agree to all of the disclaimer terms below.

</div>

### 1. Legal Compliance Statement

- This repository is a **personal study notebook** for reverse engineering technology. All content is created and shared solely for **legal technical learning, academic research, and security testing within duly authorized scope**.
- Nothing in this repository constitutes, induces, or encourages any unauthorized software cracking, piracy, reverse engineering for commercial infringement, cyber-attack, or any other act that violates applicable laws or regulations.
- All tools, techniques, and methodologies referenced herein **must only be used** with **explicit written authorization from the rightful owner** or within **your own legally-owned test environment**.

### 2. Responsibility Disclaimer

- **ALL LEGAL LIABILITY AND CONSEQUENCES** arising from any act performed after referring to, studying from, or reproducing any content from this repository shall be borne **exclusively by the person committing such act**. The repository author assumes **no responsibility whatsoever**.
- The author shall not be liable for any direct, indirect, incidental, consequential, punitive, or any other damages, or for any criminal / administrative liability incurred by any person as a result of using the content of this repository.
- If your use of any content from this repository violates the laws or regulations of any jurisdiction, **you shall assume full liability on your own**.

### 3. Content Disclaimer

- All notes, analyses, and examples in this repository represent **personal learning records only** and are provided **AS-IS**, without warranty of any kind — express or implied — as to accuracy, completeness, currency, or fitness for any particular purpose.
- **No content in this repository constitutes technical advice or operational guidance of any kind.** Any decision or action you take based on the content herein is taken at your **sole risk**.
- All third-party tool names, software trademarks, and product names referenced are the property of their respective owners and are used solely for educational identification purposes.

### 4. Compliance with Applicable Law

- You are required to strictly comply with all applicable laws and regulations in your jurisdiction, including (but not limited to) copyright law, computer software protection regulations, cybersecurity law, and criminal law provisions related to computer offenses and intellectual property protection.
- **If the laws of your jurisdiction prohibit or restrict the study of reverse engineering subject matter, you must immediately close and cease all use of this repository.**

---

## Contents

- [Repository Introduction](#repository-introduction)
- [Reverse Engineering Toolkit](#reverse-engineering-toolkit)
- [Curated RE Projects on GitHub](#curated-re-projects-on-github)
  - [RE Frameworks & Suites](#re-frameworks--suites)
  - [Disassemblers & Decompilers](#disassemblers--decompilers)
  - [Dynamic Instrumentation & Debuggers](#dynamic-instrumentation--debuggers)
  - [Binary Analysis Libraries](#binary-analysis-libraries)
  - [Symbolic Execution & SMT Solvers](#symbolic-execution--smt-solvers)
  - [Packers / Unpackers / Protections](#packers--unpackers--protections)
  - [CTF & Exploitation Tooling](#ctf--exploitation-tooling)
  - [Obfuscation & Deobfuscation](#obfuscation--deobfuscation)
  - [Awesome Lists & Learning Repositories](#awesome-lists--learning-repositories)
- [Study Notes](#study-notes)
  - [1. Disassembly Fundamentals](#1-disassembly-fundamentals)
  - [2. Decompilation Techniques](#2-decompilation-techniques)
  - [3. ELF File Format Analysis](#3-elf-file-format-analysis)
  - [4. Machine Code & Instruction Encoding](#4-machine-code--instruction-encoding)
  - [5. Memory Analysis & Dynamic Debugging](#5-memory-analysis--dynamic-debugging)
- [Practice / Lab Records](#practice--lab-records)
- [Learning Roadmap (TODO)](#learning-roadmap-todo)
- [Final Statement](#final-statement)

---

## Repository Introduction

This repository serves as my **personal knowledge base and learning journal** for the study of **Reverse Engineering** and **Binary Analysis**. Topics to be covered include:

- Static and dynamic binary analysis (**authorized scope only**)
- Disassembly and decompilation fundamentals
- Executable file format research (ELF / PE / Mach-O)
- Machine code and CPU instruction set internals
- Process memory layout and dynamic debugging techniques

> **[ COMPLIANCE NOTICE ]** — All study topics listed above shall be practiced within a **legally authorized or self-owned test environment** exclusively.

---
## Reverse Engineering Toolkit

| Tool | Primary Purpose | Notes / Common Commands |
| :--: | :--------------: | :---------------------: |
| **Ghidra** | NSA's open-source RE suite — decompilation, disassembly, symbol analysis, scripting | Use `Script Manager` for Python/Java scripts; press `Ctrl+E` to rename; `Window → Decompile` for pseudocode. |
| **IDA Pro** | Industry-standard commercial disassembler/decompiler with rich plugin ecosystem | Use `F5` for Hex-Rays decompiler; `Shift+F12` for strings; IDAPython scripting. |
| **objdump** | GNU binutil — inspect ELF sections, disassemble `.text` segments | `objdump -d -M intel ./binary` ; `objdump -t ./binary` for symbol table. |
| **readelf** | Parse ELF headers, section headers, symbol tables, and dynamic linking info | `readelf -h -S -l ./binary` ; `readelf -s ./binary` ; `readelf -r ./binary` for relocations. |
| **GDB** | GNU debugger — runtime debugging, breakpoints, memory/register inspection | `gdb -q ./binary` ; `b *0x400123` ; `run` ; `info registers` ; `x/10gx $rsp` ; `set $rip=...` |
| **radare2 (r2)** | Scriptable CLI-first reverse engineering framework | `r2 -A ./binary` ; `aaa` ; `afl` list functions ; `pdf @ main` ; `izz` strings. |
| **Binary Ninja** | Modern commercial RE platform with clean UI and intuitive IL | Use `Medium Level IL` view; supports Python/C++ API; `Plugin Manager`. |
| **x64dbg** | Open-source 32/64-bit user-mode debugger for Windows | `F2` set breakpoint ; `F9` run ; `Ctrl+G` go to address ; `Alt+C` CPU window. |
| **nm** | List symbol table (function names, global variables, etc.) | `nm -C ./binary` demangle C++ symbols. |
| **strings** | Extract printable strings from a binary — quick keyword discovery | `strings -n 6 ./binary \| grep -i "password"` |
| **file** | Identify file type, architecture, endianness, and linkage | `file ./binary` ; `file --mime-type` for MIME. |
| **xxd / hexdump** | Hex viewers — inspect raw byte content directly | `xxd -g 1 ./binary \| head -100` ; `hexdump -C ./binary \| less`. |
| **Angr** | Python-based symbolic execution & binary analysis framework | `import angr; p = angr.Project('./binary'); state = p.factory.entry_state(); simgr = p.factory.simgr(state); simgr.explore(find=0x401234)` |
| **pwntools** | Python CTF library — wraps I/O, ROP gadgets, ELF parsing, etc. | `from pwn import *; e = ELF('./binary'); rop = ROP(e); p = process('./binary')` |
| **patchelf** | Modify ELF interpreter, RPATH, SONAME, and other attributes | `patchelf --set-interpreter /path/to/ld-linux.so.2 ./binary` ; `patchelf --print-rpath ./binary`. |

---

## Curated RE Projects on GitHub

A hand-picked list of open-source reverse engineering and decompilation projects hosted on GitHub. Click any link to jump directly to the repository.

### RE Frameworks & Suites

- [Ghidra](https://github.com/NationalSecurityAgency/ghidra) — NSA's official software reverse engineering (SRE) suite; feature-rich decompiler, multi-arch disassembly, scripting in Python/Java, and collaborative RE features.
- [rizin](https://github.com/rizinorg/rizin) — Modern, community-driven fork of radare2; a complete RE framework with clean CLI, RizinDB, scripting, and disassembly/decompilation frontends.
- [Cutter](https://github.com/rizinorg/cutter) — Qt-based cross-platform GUI frontend for Rizin, designed for a smoother Ghidra/IDA-like graphical experience.
- [radare2](https://github.com/radareorg/radare2) — The original CLI-first, scriptable reverse engineering framework; supports dozens of architectures and file formats.
- [Binary Ninja API](https://github.com/Vector35/binaryninja-api) — Public Python/C++ API and official plugins for the Binary Ninja RE platform.

### Disassemblers & Decompilers

- [RetDec](https://github.com/avast/retdec) — Avast's open-source machine-code-to-C decompiler supporting x86/x64/ARM/PowerPC/MIPS and more, with a REST API and IDA plugin.
- [Snowman](https://github.com/yegord/snowman) — Native-code-to-C/C++ decompiler targeting x86, x86-64, and ARM; ships as a standalone tool and an IDA plugin.
- [Reko](https://github.com/uxmal/reko) — .NET-based decompiler for a wide range of architectures (x86/x64/ARM64/MIPS/PowerPC/Z80/6502/…) with a GUI.
- [Boomerang Decompiler](https://github.com/BoomerangDecompiler/boomerang) — A general, retargetable native binary to C decompiler (x86, PPC, SPARC, ST20).
- [dnSpyEx](https://github.com/dnSpyEx/dnSpy) — Actively-maintained fork of dnSpy; .NET editor, debugger, and decompiler for CLR assemblies.
- [ILSpy](https://github.com/icsharpcode/ILSpy) — Long-standing open-source .NET decompiler, with plugins, cross-platform builds, and VS/VSCode integration.
- [CFR / Procyon ecosystem: java-decompiler.github.io](https://github.com/java-decompiler) — Collection of modern Java bytecode decompilers (CFR, Procyon, Fernflower/Krakatau references).
- [JADX](https://github.com/skylot/jadx) — DEX to Java source decompiler for Android; GUI + CLI; produces readable Java from `.dex` / `.apk`.
- [Bytecode Viewer](https://github.com/Konloch/bytecode-viewer) — Reverse engineering suite for Java/Android Bytecode; integrates multiple decompilers (CFR, Procyon, Fernflower, Krakatau).
- [pycdc](https://github.com/zrax/pycdc) — C++ bytecode decompiler for CPython `.pyc` files across Python 2.x / 3.x versions.
- [uncompyle6 / decompile3 — see pycdc and alternatives](https://github.com/rocky/python-decompile3) — Pure-Python `.pyc` decompilation and disassembly toolkit (for historical reference).
- [wasm-decompile / Wabt](https://github.com/WebAssembly/wabt) — The WebAssembly Binary Toolkit: disassemble, assemble, validate, and decompile Wasm binaries.
- [Wasmtime](https://github.com/bytecodealliance/wasmtime) — Bytecode Alliance's standalone Wasm runtime; also useful for instrumenting and tracing compiled Wasm.

### Dynamic Instrumentation & Debuggers

- [Frida](https://github.com/frida/frida) — World-class dynamic instrumentation toolkit; inject JavaScript or QuickJS into Android/iOS/macOS/Linux/Windows native processes; massive plugin/script ecosystem.
- [Frida CodeShare — examples](https://github.com/frida/frida-codeshare-examples) — Official community Frida script snippets ready to clone and adapt.
- [x64dbg](https://github.com/x64dbg/x64dbg) — Open-source Windows user-mode debugger for x32 and x64 targets with a Qt GUI and plugin system.
- [x64dbg Plugins](https://github.com/x64dbg/x64dbg-plugins) — Curated collection of third-party x64dbg plugins.
- [DynamoRIO](https://github.com/DynamoRIO/dynamorio) — Process-level dynamic binary instrumentation framework (x86/x64/ARM) with powerful instrumentation APIs.
- [Intel Pin — GitHub mirror / examples](https://github.com/intel/pin) — Intel Pin dynamic binary instrumentation (DBI) framework source examples and SDK wrappers.
- [QBDI](https://github.com/QBDI/QBDI) — QuarkslaB Dynamic binary Instrumentation; cross-platform DBI framework supporting x86/x64/ARM/ARM64.
### Binary Analysis Libraries

- [Capstone](https://github.com/capstone-engine/capstone) — Lightweight multi-arch disassembly engine used by Angr, radare2, pwntools, and many others.
- [Unicorn Engine](https://github.com/unicorn-engine/unicorn) — Lightweight multi-architecture CPU emulator; powers RE emulation in Angr, Qiling, etc.
- [Keystone Engine](https://github.com/keystone-engine/keystone) — Lightweight multi-arch assembler engine; complementary to Capstone/Unicorn.
- [LIEF](https://github.com/lief-project/LIEF) — Cross-platform library to parse, modify, and abstract ELF, PE, and Mach-O formats (Python & C++ bindings).
- [pyelftools](https://github.com/eliben/pyelftools) — Pure-Python library for parsing and analyzing ELF files and DWARF debugging information.
- [pefile](https://github.com/erocarrera/pefile) — Most-widely used pure-Python PE (Portable Executable) parser.
- [macholibre](https://github.com/aaronst/macholibre) — Mach-O binary parser & extractor for macOS/iOS binaries.
- [Triton](https://github.com/JonathanSalwan/Triton) — Dynamic binary analysis (DBA) framework with dynamic taint analysis, symbolic execution, and x86/x64/ARM/AArch64 AST representation.
- [Qiling](https://github.com/qilingframework/qiling) — Cross-platform, multi-arch binary emulation framework built on top of Unicorn; "the true successor to QEMU user-mode for RE."

### Symbolic Execution & SMT Solvers

- [Z3 Theorem Prover](https://github.com/Z3Prover/z3) — Microsoft Research's high-performance SMT solver; the de-facto standard for constraints in RE, program verification, and symbolic execution.
- [angr](https://github.com/angr/angr) — Python-based binary analysis platform with powerful symbolic/concrete execution, CFG recovery, value-set analysis, and out-of-the-box exploit helpers.
- [Manticore](https://github.com/trailofbits/manticore) — Trail of Bits' symbolic execution tool for EVM, native binaries (x86/x64/ARMv7), and WASM; great for program property checking.
- [Yices 2](https://github.com/SRI-CSL/yices2) — SRI's fast SMT solver with a small, embeddable C API; widely used for verification tasks.
- [STP](https://github.com/stp/stp) — Simple Theorem Prover; constraint solver originally built for bit-vector and array reasoning, used by early KLEE builds.
- [claripy](https://github.com/angr/claripy) — angr's abstract constraint solving backend; wraps Z3, Z3-str, and custom solvers behind a unified Python API.

### Packers / Unpackers / Protections

- [UPX — Ultimate Packer for eXecutables](https://github.com/upx/upx) — The most popular open-source portable executable compressor (PE / ELF / Mach-O / …).
- [Detect It Easy (DIE)](https://github.com/horsicq/Detect-It-Easy) — Modern, cross-platform packer/compiler/protector detector with huge signature databases and a Qt GUI.
- [PEiD — open-source reimplementation](https://github.com/Exocortex/PEiD) — Community-driven PE identifier clone; detects packers, cryptors, and compilers for Windows PE files.
- [XPEViewer](https://github.com/horsicq/XPEViewer) — Cross-platform PE file viewer and structural analyzer built by the DIE author.
- [ScyllaHide](https://github.com/x64dbg/ScyllaHide) — Advanced anti-anti-debug plugin for x64dbg, OllyDbg, and IDA; hides debugger artifacts from user-mode anti-debug checks.
- [TitanHide](https://github.com/mrexodia/TitanHide) — Kernel-mode driver that hides common debugger artifacts from ring-3 anti-debug techniques (x64dbg plugin friendly).

### CTF & Exploitation Tooling

- [pwntools](https://github.com/Gallopsled/pwntools) — Swiss-army CTF Python library for exploit development: tube I/O, ELF/DynELF parsing, ROP/Shellcraft, fmt-strings, and more.
- [ROPgadget](https://github.com/JonathanSalwan/ROPgadget) — Search gadgets in binaries (x86, x64, ARM, ARM64, MIPS, PowerPC, SPARC) for ROP chain construction.
- [Ropper](https://github.com/sashs/Ropper) — Another ROP gadget finder with a nice search DSL and support for common architectures.
- [one_gadget](https://github.com/david942j/one_gadget) — Find the best `execve("/bin/sh", {environ?}, NULL)` single gadget inside glibc for one-shot ROP.
- [pwninit](https://github.com/io12/pwninit) — Automate pwn CTF challenge setup: patch glibc/ld, generate solve.py template, fetch libc source via libc-database.
- [libc-database](https://github.com/niklasb/libc-database) — Build a searchable database of libc.so.6 builds; leak an address → identify exact libc → compute one_gadget / offsets.
- [LibcSearcher](https://github.com/lieanu/LibcSearcher) — Python wrapper around libc-database-style lookup for CTF libc identification.
- [GDB plugins: gef](https://github.com/hugsy/gef) — Enhanced features GDB plugin with heap inspection, ASLR info, Vmmap, start/entry breakpoints, and a friendly TUI.
- [GDB plugins: pwndbg](https://github.com/pwndbg/pwndbg) — Heavily-used GDB plugin focused on exploit development and RE; integrates with pwntools.
- [GDB plugins: peda](https://github.com/longld/peda) — The classic Python Exploit Development Assistance for GDB; older but still referenced in many write-ups.
- [radare2 r2pipe + r2ghidra-dec plugin](https://github.com/radareorg/r2ghidra-dec) — Deep Ghidra decompiler integration inside radare2 / rizin sessions.

### Obfuscation & Deobfuscation

- [Obfuscator-LLVM (OLLVM)](https://github.com/obfuscator-llvm/obfuscator) — The canonical LLVM-based code obfuscation project (control-flow flattening, bogus control flow, instruction substitution) — used as a baseline for many protection studies.
- [Hikari](https://github.com/61bcdefg/Hikari) — LLVM-based obfuscator forked from OLLVM; adds additional passes, stronger Flattening, IndirectBranches, and FunctionCallObfuscation.
- [AntiTibia](https://github.com/airbus-cert/AntiTibia) — Lightweight scripts for common deobfuscation tasks, useful for students exploring first stages of anti-reversing.
- [de4dot](https://github.com/de4dot/de4dot) — .NET deobfuscator and unpacker; supports many commercial .NET protectors.
- [unluac](https://github.com/HansWessels/unluac) — Lua 5.1 bytecode decompiler written in Java; frequently used for reversing Lua-based mobile games.
- [Simplify — Android Dex deobfuscator](https://github.com/CalebFenton/simplify) — Generic Android/Dalvik deobfuscator; executes code on a virtual machine to resolve reflection and string encryption.

### Awesome Lists & Learning Repositories

- [awesome-reversing](https://github.com/d3nom3/awesome-reversing) — The definitive community-curated list of RE resources: books, courses, tools, write-ups, CTF practice, competitions.
- [onethawt/reverseengineering](https://github.com/onethawt/reverseengineering) — Another great AWESOME.md for reverse engineering, with sections per topic and platform.
- [awesome-binary-exploitation](https://github.com/wtsxDev/List-of-awesome-binary-exploitation) — Curated list of binary-exploitation resources, heap exploitation papers, mitigations, and CTF write-up hubs.
- [CTF Resources — CTFtime / ctfs](https://github.com/ctfs) — Huge archive of CTF challenge sources and official write-ups; great source for practice RE/Pwn problems.
- [CTF All The Things](https://github.com/apsdehal/awesome-ctf) — All-in-one CTF methodology & tooling list covering RE, Pwn, Web, Crypto, Forensics, and OSINT.
- [Practical Binary Analysis — official repo](https://github.com/williballenthin/practical-binary-analysis) — Companion code & challenge binaries for the famous PBA book by Dennis Andriesse.
- [Reversing: Secrets of Reverse Engineering — related resources](https://github.com/onethawt/idaplugins-list) — Great complementary list of IDA Pro plugins and RE reading material.
- [CTF-cheatsheets — RE & Pwn cheatsheets](https://github.com/CompassSecurity/CheatSheets) — Quick-glance cheat sheets for CTF RE, Shellcoding, Heap, and Linux PrivEsc.

> **[ COMPLIANCE NOTICE ]** — All of the above open-source projects are referenced solely for learning and authorized research. You must comply with each project's own LICENSE and terms of use, and only use them on systems or binaries you are explicitly authorized to analyze.

---

## Study Notes

### 1. Disassembly Fundamentals

- **x86 / x86_64 Instruction Set**
  - Register classification:
    - General-purpose: `RAX, RBX, RCX, RDX, RSI, RDI, RBP, RSP, R8-R15` (x64) / `EAX, EBX, ECX, EDX, ESI, EDI, EBP, ESP` (x86).
    - Segment registers: `CS, DS, ES, FS, GS, SS`.
    - Flags register: `EFLAGS/RFLAGS` with key bits: `CF` (carry), `PF` (parity), `AF` (adjust), `ZF` (zero), `SF` (sign), `TF` (trap), `IF` (interrupt), `DF` (direction), `OF` (overflow).
    - Instruction pointer: `RIP/EIP`.
  - Common instructions:
    - Data movement: `mov`, `lea`, `push`, `pop`, `xchg`.
    - Arithmetic: `add`, `sub`, `inc`, `dec`, `mul`, `div`, `imul`, `idiv`, `neg`.
    - Logic: `and`, `or`, `xor`, `not`, `shl`, `shr`, `sar`, `rol`, `ror`.
    - Control flow: `jmp`, `call`, `ret`, `jcc` (conditional jumps like `je`, `jne`, `jg`, `jl`), `loop`.
    - Comparison: `cmp`, `test`.
  - Calling conventions:
    - **cdecl**: arguments pushed right-to-left, caller cleans stack, return value in `EAX/RAX`.
    - **stdcall**: arguments pushed right-to-left, callee cleans stack (used by Win32 APIs), return in `EAX`.
    - **fastcall**: first two args in `ECX, EDX` (x86) / `RCX, RDX, R8, R9` (x64), rest on stack, callee cleans.
    - **System V AMD64 ABI** (Linux x64): args in `RDI, RSI, RDX, RCX, R8, R9`, extra args on stack, return in `RAX`, caller-saved: `RAX, RCX, RDX, RSI, RDI, R8-R11`; callee-saved: `RBX, RBP, R12-R15`.

- **ARM Instruction Set**
  - Register model: `R0-R12` general purpose, `R13` stack pointer (SP), `R14` link register (LR), `R15` program counter (PC), `CPSR` status register.
  - Thumb / Thumb-2: 16-bit and mixed 32-bit instruction sets, used for code density; conditional execution via `IT` blocks.
  - ARM64 (AArch64): registers `X0-X30`, `SP` (X31 zero or SP depending on context), `PC` not directly accessible; calling convention: args in `X0-X7`, indirect result in `X8`, frame pointer `X29`, link register `X30`.

- **Disassembly snippets & analysis notes:**
  ```asm
  ; Example: function prologue/epilogue (x86_64)
  push   rbp            ; save old base pointer
  mov    rbp, rsp       ; set new base pointer
  sub    rsp, 0x20      ; allocate 32 bytes for locals
  ...
  leave                 ; mov rsp, rbp ; pop rbp
  ret
  ```
  分析：`push rbp` 保存调用者的栈帧基址，`mov rbp, rsp` 建立当前帧，`sub rsp, N` 分配局部变量空间，`leave` 等价于 `mov rsp, rbp; pop rbp` 恢复调用者栈帧。
### 2. Decompilation Techniques

- Reading & annotating Ghidra / IDA decompiler output:
  - Identify control flow patterns: `if-else`, `switch` (jump tables), loops (`while`, `for`, `do-while`).
  - Recognize structure recovery: arrays become pointer arithmetic, structs become offset accesses.
  - Spot virtual function tables: object pointer contains vtable at offset 0, indirect calls via `(*vtable[index])(...)`.
  - Handle inlined functions: decompiler may inline small functions, use cross-references and symbol names.
- Decompiled pseudocode vs. original source comparison:
  ```c
  /* Example Ghidra output with annotations */
  int main(int argc, char **argv) {
      if (argc < 2) {
          puts("Usage: ./prog <input>");
          return 1;
      }
      // check_password(argv[1]);
      int result = check_password(argv[1]);
      if (result == 0) {
          puts("Access granted");
      } else {
          puts("Access denied");
      }
      return 0;
  }
  ```
  说明：通过命名函数、修改变量类型（如 `char **`），可使反编译结果更可读。

### 3. ELF File Format Analysis

- **ELF Structure**
  - ELF Header (`Elf64_Ehdr`): `e_ident` magic `\x7fELF`, class (ELFCLASS32/64), data encoding (little/big endian), version, OS ABI; `e_type` (ET_REL=1, ET_EXEC=2, ET_DYN=3, ET_CORE=4); `e_machine` (EM_X86_64=62, EM_ARM=40, EM_AARCH64=183); `e_entry` entry virtual address; `e_phoff`, `e_shoff` offsets.
  - Program Headers (segments): used by loader; types: `PT_LOAD` (loadable segment), `PT_DYNAMIC` (dynamic linking info), `PT_INTERP` (interpreter path), `PT_NOTE`, `PT_GNU_STACK`, `PT_GNU_RELRO`.
  - Section Headers: used by linker; common sections: `.text` (code), `.data` (initialized data), `.bss` (uninitialized data), `.rodata` (read-only data), `.got`, `.plt`, `.dynsym`, `.dynstr`, `.strtab`, `.shstrtab`, `.rela.plt`, `.rela.dyn`.
- **Dynamic Linking Mechanism**
  - GOT (Global Offset Table): stores resolved addresses of global symbols; each entry initially points back to PLT resolver stub.
  - PLT (Procedure Linkage Table): stubs for external functions; first call jumps to resolver, subsequent calls jump directly to GOT entry.
  - Lazy binding: first call -> PLT -> GOT (points to PLT+offset) -> `_dl_runtime_resolve` -> updates GOT -> returns to function.
  - Symbol resolution: dynamic linker matches symbol names in `.dynsym` against loaded libraries.
- **Analysis log:**
  ```
  $ readelf -h ./binary
  ELF Header:
    Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
    Class:                             ELF64
    Data:                              2's complement, little endian
    Type:                              DYN (Shared object file)
    Machine:                           Advanced Micro Devices X86-64
    Entry point address:               0x1060
  $ objdump -d -M intel ./binary | grep "<main>:" -A 20
  ```

### 4. Machine Code & Instruction Encoding

- x86 instruction encoding format: optional prefixes (legacy, REX) → opcode (1–3 bytes) → ModR/M byte → SIB byte → displacement → immediate.
- REX prefix (0x40–0x4F): `W` bit (64-bit operand size), `R`, `X`, `B` bits extend ModR/M fields.
- ModR/M byte: `mod` (addressing mode), `reg/opcode` (register or opcode extension), `rm` (register or memory operand).
- SIB byte: scale, index, base for complex addressing.
- Instruction length calculation: count prefix bytes, opcode, then ModR/M (+SIB), then displacement/immediate sizes based on mod and opcode.
- Shellcode writing & encoding tricks: avoid null bytes, use `xor reg,reg` to zero, use `push`/`pop` to move small constants, use relative addressing to avoid absolute addresses.

```
; Example: x86_64 mov rbp, rsp encoding
; 48 89 e5
; 48 = REX.W prefix (64-bit operand)
; 89 = opcode for mov r/m64, r64
; e5 = ModR/M: mod=11 (register), reg=4 (rsp), rm=5 (rbp)
```

### 5. Memory Analysis & Dynamic Debugging

- **Process Memory Layout**
  - Userland virtual address space: typically stack at high addresses (grows down), heap at lower addresses (grows up), shared libraries / mmap region between, executable's `.text`, `.data`, `.bss` at fixed base (subject to ASLR).
  - Stack frame structure: `[higher addresses]` arguments, return address, saved `RBP`, local variables `[lower addresses]`; `RSP` points to top, `RBP` to frame base.
  - Mitigation internals:
    - **ASLR**: randomizes base addresses of stack, heap, libraries, and PIE executables.
    - **NX/DEP**: marks stack/heap non-executable, prevents shellcode execution.
    - **Stack Canary**: random value placed before saved `RBP`/return address; checked on function return.
    - **PIE**: position-independent executable, enables ASLR for main binary.
    - **RELRO**: Partial (GOT writable after relocation) / Full (GOT read-only after relocation), mitigates GOT overwrite.
- **Dynamic Debugging Techniques**
  - Breakpoint types: software (`INT 3` instruction), hardware (debug registers `DR0-DR3`), memory watchpoints (via debug registers).
  - Conditional breakpoints: `break *0x401234 if $rax == 0`
  - Log breakpoints: use GDB commands `commands` to print and continue.
  - Runtime memory patching: `set {int}0x601000 = 0x1234`, `set $rip = 0x400600`.
- **Heap Exploitation Fundamentals**
  - glibc `malloc`/`free` internals: chunks, bins (fastbins, tcache, unsorted bin, small bins, large bins), metadata.
  - Common vulns: Use-After-Free (UAF), Double Free, Heap Overflow.
  - Example: tcache poisoning to overwrite `__free_hook` or `__malloc_hook`.

```
; GDB session log example
(gdb) b main
(gdb) run
(gdb) info proc mappings
(gdb) x/20gx $rsp
(gdb) p/x $rax
(gdb) continue
```
---

## Practice / Lab Records

> **[ COMPLIANCE NOTICE ]** — All lab entries below shall be limited to **open-source software, public CTF challenges, self-built Crackmes, your own legally-owned test binaries, or targets for which you hold explicit written authorization**. Recording experiments against **unauthorized commercial software** is strictly prohibited.

| ID | Target / Challenge Source | Observation & Procedure | Knowledge Acquired | Pitfalls & Solutions |
| :-: | :-----------------------: | :---------------------: | :----------------: | :------------------: |
| 001 | pwnable.kr "bof" | Used IDA to disassemble; found `gets` overflow in `func`; overwrote return address with address of `system("/bin/sh")` | Stack buffer overflow, return address overwrite, finding libc offsets | Remote libc version mismatch; solved by using provided libc.so.6 and matching offsets |
| 002 | | | | |
| 003 | | | | |
| 004 | | | | |
| 005 | | | | |
| 006 | | | | |
| 007 | | | | |
| 008 | | | | |
| 009 | | | | |
| 010 | | | | |

---

## Learning Roadmap (TODO)

- [ ] Master x86_64 common instruction set and compile a personal cheat-sheet
- [ ] Deep-dive System V AMD64 ABI calling convention and stack frame layout
- [ ] Finish *"Reverse Engineering Core Principles"* book with chapter exercises
- [ ] Learn Ghidra scripting (Python / Java) for automated analysis tasks
- [ ] Complete IDA Pro workflow from basic usage to advanced plugin development
- [ ] Fully understand ELF format and build a handwritten ELF parser
- [ ] Study Windows PE file format structure and analysis methods
- [ ] Investigate GOT/PLT internals; construct `ret2plt` / `ret2dlresolve` exploits
- [ ] Master common CTF RE categories: crypto signature recognition, anti-disassembly (junk-code), VM-based obfuscation
- [ ] Learn Angr symbolic execution basics for automated constraint-solving
- [ ] Master glibc `malloc` internals across versions (tcache / fastbin / unsorted bin exploitation)
- [ ] Study ARM / ARM64 assembly and reversing methodology
- [ ] Research obfuscation techniques (CFF, opaque predicates, virtualization) and de-obfuscation approaches
- [ ] Practice a complete RE workflow end-to-end with radare2
- [ ] Learn Frida dynamic instrumentation; perform Android native-layer hooking hands-on
- [ ] Research introductory kernel-mode RE (Linux Kernel Module analysis)
- [ ] Understand compiler optimization levels (O0–O3) and recognize code patterns at each level
- [ ] Catalog signatures for common crypto algorithms (AES, RSA, TEA, XXTEA, RC4, MD5, SHA)
- [ ] Learn and practice binary patching and repackaging techniques
- [ ] Solve **at least 20 CTF Reverse Engineering challenges** and log them in the lab records table

---

## Final Statement

**Before using any content from this repository, please re-confirm each of the following:**

1. **[1]** All reverse engineering, debugging, and experimentation you perform is conducted within a **legally authorized or self-owned test environment**;
2. **[2]** You have read, understand, and comply with **all applicable laws and regulations** in your jurisdiction regarding reverse engineering, intellectual property, and computer security;
3. **[3]** You are fully aware that unlawful use may result in **civil, administrative, or even criminal liability**, and you accept such consequences **solely on your own behalf**;
4. **[4]** The author of this repository has never authorized, encouraged, or supported — in any form — the use of this repository's content for unlawful purposes. All improper acts are exclusively the responsibility of the actor.

**If you do not agree to any of the above terms, you must immediately cease accessing, referencing, or using any content from this repository.**

---

*Personal study notebook — continuously updated. Feedback within a lawful and compliant scope is welcomed.*
