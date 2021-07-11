# Introduction

DMon is hardware-assisted binary analysis framework, with the ability to perform re-hosting on powerful hardware, and to trace instruction/data with relatively low latency.

The project is still under active development and aims at offering a powerful and user-friendly API to make binary re-hosting easier and faster.

In a nutshell, Dmon runs ARM32 binaries using a re-hosted approach. In fact, instead of executing the code on a software emulator, DMon is able to execute the code natively on a powerfull processor. This hardware plateform is based on a specific SoC that combines a FPGA fabric and a powerful processor on a single DIE. This FPGA fabric emulates custom hardware IPs which are part of the DMon development effort. These IPs offer some powerful mechanisms to control and observe the execution the re-hosted program. With such feature, DMon aims at offering the same capability than a classi emulator like QEmu but with higher performance when based on a hardware-in-the-loop scheme. In fast, the emulation of firmware programs without the underlying hardware and especially peripherals is often painfull and requires significant manual efforts. Therefore, DMon does not try to replace the hardware but instead offers a very efficient way of interacting with it while offering higher introspection capability than the native device would offers.

## Get Started

Installation guide can be found [here](installation/installation/).

To get more details about how DMon works, please check here.



