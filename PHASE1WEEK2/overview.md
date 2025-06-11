# Week 2 Overview – *vsdRiscvScl180* Internship  
**Branch:** `week2_<your-id>`   **Dates:** 09 → 15 Jun 2025 (IST)

---

## 🎯 Overall Aim
> **Master the read-only exploration and first compile of the complete Caravel-based SoC RTL.**  
> By the end of the week you should be able to:
> 1. Navigate every major block confidently.  
> 2. Generate a hierarchical design map.  
> 3. Prove, by simulation, that the untouched RTL is self-consistent on *your* machine.

---

## 🧰 Toolchain & Environment

| Layer | Tool / Version | Purpose | Quick Check |
|-------|----------------|---------|-------------|
| **Source Control** | `git >= 2.25` | clone, branch, push PR | `git --version` |
| **Remote Hosting** | GitHub + Personal Access Token (PAT) | password-less HTTPS pushes | Settings ▸ Developer settings ▸ PAT |
| **RTL Analysis/Sim** | <br>• *Primary:* **Synopsys VCS Q-2024.12**<br>• *Fallback:* **Yosys 0.40 + Verilator 5.2** | compile + hierarchy dump | `vcs -full64 -h` or `yosys -Q` |
| **Editor / Viewer** | VS Code, Vim, or any IDE with SystemVerilog plug-in | fast code search/peek | `code --version` / `vim --version` |
| **Screenshot** | Flameshot / Snipping Tool | capture proof of clean sim run | flameshot –v |

> *If you don’t have VCS, the Yosys + Verilator route is fully acceptable—just note it in your logs.*

---

## 📈 Objectives & Tasks

| # | Task | Output File(s) | Why It Matters |
|---|------|----------------|----------------|
| 1 | **Synchronise Fork & Branch** | `task1_update_working_copy.md` | clean history; no merge noise later |
| 2 | **Top-Level Orientation** – identify 4 child blocks, boundary signals, first sync point | `task2_top_level_notes.md` | builds mental map |
| 3 | **Automated Hierarchy Dump** via VCS or Yosys | `hierarchy.txt` | searchable design tree |
| 4 | **Deep-Dive Checklist** – answer 6 pinpoint questions (padframe, SPI, WB, IRQ, GPIO, clk) | `task4_deep_dive.md` | demonstrates grep/navigation skills |
| 5 | **First Full-Chip Compile & Smoke-Test** | `compile.log`, `run.log`, `sim_finish.png` | proves build reproducibility |
| 6 | **Package & Push** everything under `week2/` | directory commit | one-stop deliverable for mentors |

---




