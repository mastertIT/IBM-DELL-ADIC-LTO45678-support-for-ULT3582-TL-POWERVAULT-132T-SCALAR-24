# IBM-ULT3582-TL---DELL-POWERVAULT-132T---ADIC-SCALAR-24-LTO4-LTO5-LTO6-FW
Modified Firmware for IBM ULT3582-TL - DELL POWERVAULT 132T - ADIC SCALAR 24 to accept LTO4 LTO5 LTO6 tape drives from IBM. ensure the dip switches are set identically to the original drive as well as the Blue J8 LDI connector being reconnected to the drive.
FC ID Jumper (Black loop) needs to be plugged into J39 for drives above LTO4, this is taken from original LTO1 or LTO2 drive.


## Install the library firmware

1. Extract the ZIP and open PowerShell in the directory.
2. Stop backup jobs, unload the drives and allow the library to become idle.
3. Connect the **library controller RS-232 port** to the Windows host. This is
   separate from the RMU serial port beside Ethernet.
4. Close any terminal program using that COM port. The commands below use
   **COM1**; replace `-C1` with your port number, such as `-C3` for COM3.
5. Run the command for your library below. The downloader uses 19200 baud.
   Wait for **`main passed`** and the automatic restart. Keep power applied
   until programming and restart finish.

### IBM 3582-L23 — 314B.GY001

```powershell
.\tools\dls24.exe -C1 -F .\firmware\library\ibm\3582-LTO-314B-LTO456-R1.lif
```

### Dell PowerVault 132T LTO — 314D.GY001

```powershell
.\dls24.exe -C1 -F .\firmware\library\dell\PV132T-LTO-314D-LTO456-R1-EXPERIMENTAL.lif
```

### ADIC / Quantum Scalar 24 LTO — 314A.GY001

```powershell
.\tools\dls24.exe -C1 -F .\firmware\library\adic\SC24-LTO-314A-LTO456-R1-EXPERIMENTAL.lif
```

## Update the IBM RMU

**The included RMU firmware is for the IBM 3582 only. Do not install it on a
Dell or ADIC RMU.** The RMU update is separate from the library update.

### Through the RMU website

1. Log in to the IBM RMU and close open virtual-console windows.
2. Open **Firmware → RMU Firmware** and upload:

   ```text
   firmware/rmu/ibm/IBM-RMU-210C-ConsoleFix4c-EXPERIMENTAL.lif
   ```

3. Wait for programming and the RMU restart to finish.
4. Reload the website with cached content bypassed. Open the diagnostic console
   and confirm **ConsoleFix4c: Ready**. The base RMU revision remains
   **210C.00002**.

### Through the RMU RS-232 port

Use the **RMU serial port beside Ethernet**, a straight-through serial cable,
and **38400 baud, 8N1, no flow control**. Interrupt boot when prompted.

For the boot monitor offering `X`, `V`, `Z` and `@`:

1. Select **X** and send the following IMG using **XMODEM, 128-byte packets**:

   ```text
   firmware/rmu/ibm/IBM-RMU-210C-ConsoleFix4c-EXPERIMENTAL.img
   ```

2. Select **V** to verify the received image. Continue only if verification succeeds.
3. Select **Z** to program flash and wait for completion.
4. Select **@** to restart the RMU.

Use the **LIF for the website** and the **IMG for RMU serial loading**.
Do not send either RMU file through `dls24.exe`.

## Tested drives and firmware

Testing was performed in the **IBM 3582-L23** with IBM **full-height Fibre Channel** drives.

| Drive model | Part numbers (PN) | Drive firmware | Test result |
|---|---|---|---|
| IBM ULT3580-TD4 — LTO4 | 95P4516 / 95P5192 | C7QH | Initialization, host load/unload, backup and restore successful |
| IBM ULT3580-TD5 — LTO5 | 46X1362 / 46X2550 | H976 | Initialization, host load/unload, backup and restore successful |
| IBM ULT3580-TD6 — LTO6 | 35P1970 / 39U3420 | H4T0 | Initialization, host load/unload, backup and restore successful |
| IBM ULT3580-TD6 — LTO6 | 35P1970 / 39U3420 | KAJ8 | Initialization, host load/unload, backup and restore successful |
