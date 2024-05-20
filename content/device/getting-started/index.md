---
title: 🆒 Getting start
summary: ZIGGO device get start document 
date: 2024-05-01
authors:
  - admin
tags:
  - ZIGGO-Device
  - Basic
image:
  caption: "TBD"
weight: 18
---

## Table of Content

- [Table of Content](#table-of-content)
- [Folder Structure](#folder-structure)
- [Introduction to git branches](#introduction-to-git-branches)
- [Building and Starting the TSNPerf](#building-and-starting-the-tsnperf)


## Folder Structure

```bash
.
├── docs                     //documents for ZIGGO
├── figs                     //figures for docs
├── hardware                //hareware code, for PL part(pkt_gen, time sync in FPGA)
├── readme.md                  //readme for whole project
├── software                //software code, for ps part(pkt_gen, time sync)
└── testbed-build           //code for building testbed
```

## Introduction to git branches

| Branch Name     | Basic Function | Packet Resize | Online Analyze | Offline Analyze |
|:---------------:|:--------------:|:-------------:|:--------------:|:---------------:|
| main            | √              |               | √              |                 |
| packet_resize   | √              | √             | √              |                 |
| offline_analyze | √              |               |                | √               |

The branches of TSNPerf submitted this time can be divided into three categories. But the main branch is inconvenient to use in two ways. In order to solve the above two limitations, we have also submitted two patch branches.

* The `main` branch contains basic time synchronization and pkt_gen functions, as well as online analysis functions. However, its limitation is that it can only send Ethernet of MTU (1500B) size, and due to the limited performance of the zynq development board, online analysis may cause packet loss.
* `packet_resize` branch can send Ethernet frames of any size (64B-1500B).
* `offline_analyse` branch can forward the data packets to the PC for offline analysis to avoid packet loss. 

> Note1: When switch to 'packet_resize' branch, you also need to modify the `software/config/flow.json` 
> 
> ```
> {
>         "job_id": 0, 
>         "flow_id": 0,
>         "src": 1,
>         "dst": 2,
>         "period": 2048,
>         "MD": 1024,
>         "packet_size": 750 // add this attribute 
>  },
> ```

> Note2: When switch to 'offline_anaylze' branch, you need to link device to anthor PC (linux) by wire in ETH1.

## Building and Starting the TSNPerf

[Set up the FPGA board and initialize PS system](/device/hardware-build/)

[Compile software code, run the time synchronization & pkt _gen_app](/device/software-build/)
