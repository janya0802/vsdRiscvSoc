# Task 1 – Repository Setup & Sync  
*Week 2 — `vsdRiscvScl180` Internship*  

---

## 🎯 Aim  
Establish a clean local workspace that tracks **my fork** of `vsdRiscvScl180`, stays synchronised with the mentor’s upstream `main`, and provides a dedicated `week2_<id>` branch for all Week 2 deliverables.

---

## 🧰 Tools & Accounts  

| Requirement | Details | Verification |
|-------------|---------|--------------|
| Git | `git --version` → `git version 2.42.1` | ✓ |
| GitHub account | `janya0802` | ✓ |
| **Fork** of mentor repo | `https://github.com/janya0802/vsdRiscvScl180` | ✓ (created 11 Jun) |
| Personal-Access Token | 40-char PAT with **repo** scope (label `cadence-server`) | ✓ |
| Workstation directory | `~/projects` | ✓ |

---

## 🚀 STEP 1 - Create workspace & clone my fork 

$ mkdir -p ~/projects
$ cd ~/projects
$ git clone https://github.com/janya0802/vsdRiscvScl180.git
Cloning into 'vsdRiscvScl180'...
remote: Enumerating objects: 2283, done.
remote: Total 2283 (delta 0), reused 0 (delta 0), pack-reused 2283
Receiving objects: 100% (2283/2283), 2.31 MiB | 6.80 MiB/s, done.
Resolving deltas: 100% (1354/1354), done.
$ cd vsdRiscvScl180
$ git status

On branch main
nothing to commit, working tree clean

## 🚀 STEP 2 -  Add  repository as upstream
![image](https://github.com/user-attachments/assets/bee6d030-e67b-4fa9-ac31-5e9ccbf6e86c)

## 🚀 STEP 3 - Synchronise main with upstream
$ git push origin main

To https://github.com/janya0802/vsdRiscvScl180.git

## 🚀 STEP 4 - Sanity checks
![WhatsApp Image 2025-06-11 at 22 13 08_8828606d](https://github.com/user-attachments/assets/2a8dc245-a52f-48f9-ad87-3115635240d3)


file:///home/snu/final/janya/ques1.png




