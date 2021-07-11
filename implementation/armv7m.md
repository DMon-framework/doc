# ARMv7m



Since the re-hosted code is designed to run on a different hardware environment, re-hosting requires some instrumentation to keep the execution consistent. For this purpose, DMon uses different mechanisms:

* When the re-hosted code accesses peripherals that are not present on DMon, the I/O forwarding mechanism seamlessly forwards the memory access to an attached device. This device is the one for which the fimware is designed to run natively. It contains the peripherals the firmware interact with during execution. Without this interactions the firmware execution would be inconsistent. The I/O forwarding interacts with the attached device through the JTAG interface that is common on embedded systems.
* The hardware peripherals on the attached device may also interact with the re-hosted firmware using interrupt signals. This interrupts are caught on the attached device using a custom software stub. This stub interact with DMon using a custom protocol for wich 2 GPIOs and a JTAG access are necessary. Most of the logic here is implemented in hardware to keep the interrupt forwarding fast. Once forwarded, the interrupt is executed on DMon natively. To keep the original behavior, DMon adds prologue and epilogue logic around interrupt handlers so that original behavior can be modeled correctly.
* The CPU used by DMon is a cortex-A9 which supports ARM32 ISA. However, some components may differ or need to be changed for analysis purpose. For instance, the co-processors may be different or the security analysist might need to execute helper functions when some specific instructions are fetched by the CPU. To make it possible, DMon has a hardware patch mechanism that replaces targetted instruction with invalid one. This forces the CPU to trig an exception that is caught by DMon software. Then, DMon software calls the expected helper function based on an ID stored in the invalid instruction. To make it fast, last invalid instruction is cached in DMon hardware IP \(so no DRAM access\).
* The memory layout of the re-hosted binary might be incompatible with DMon memory layout. To avoid any annoing code relocation, we use the MMU on the DMon plateform to virtualize the code/data location.

  In addition to this control mechanism, DMon offers a powerfull data-flow monitoring mechanism implemented purely in hardware. This mechanism trace data fetched by the DMon CPU over a USB 3.0 channel.

