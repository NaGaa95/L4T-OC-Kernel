# L4T-OC-Kernel (Mariko ONLY)

DISCLAIMER: USE AT YOUR OWN RISK!

This Kernel is very dangerous and can possibly damage your console. Therefore I do not recommend using it. If you decide to use it, USE AT YOUR OWN RISK. THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND.

Overclocking in general will shorten the lifespan of some hardware components. YOU ARE RESPONSIBLE for any problem or potential damage by using unsafe frequencies.

# Features 

* CPU Overclock up to 2600 MHz
  * EOS CPU UV 4
  * High-Frequency vMin reduced to 800mV
  * Limited to 2499 MHz on lower CPU Speedo
* CPU LUT Table increased to 63
  * Allow finer voltage steps
* GPU Overclock up to 1305 MHz
  * GPU Volt Offset -10
* Increased CPU/GPU vMin & SoC Voltage
  * May help achieve higher RAM Frequencies for Hynix NEE / Micron WTB users (3000+ MHz)
* Vdd2 Overvoltage up to 1212mV
* Multiple Refresh Rate Support
  * 50 Hz Added
* Fix for Nyxi Hyperion Series Joy-con
  * May also apply to other 3rd party Joycon with poor handshake implementation

## How to Install : 
1. Download latest [release](https://github.com/NaGaa95/L4T-OC-Kernel/releases).
2. Place `uImage` `nx-plat.dtimg` `modules.tar.gz` in `/switchroot/*ubuntu*/` on your SD Card
3. If not already done, set `dvfsb=1` / `gpu_dvfsc=1` in your L4T Boot config `(Bootloader/ini/*L4T*.ini)`
<br /> /!\ UV Kernel only is recommended for low speedo (-1600) and Switch Lite /!\

### Switch Lite :
* To unlock CPU / GPU Freqs you also need to replace the `boot.scr` file in `/switchroot/*ubuntu*/`
* /!\ Only use high frequencies with the charger plugged in otherwise, the Switch will instantly shut down due to excessive power draw /!\

### 1212mV vdd2 Overvoltage
* Use the modded Hekate-OC provided 

## Usefull Commands

Switch to 50Hz Refresh Rate 
- `xrandr --output DSI-0 --primary --mode 720x1280 --rotate left --panning 1280x720+0+0 --pos 0x0 --dpi 120 --fb 1280x720 --rate 50`

CPU Voltage & Real freq
- `watch -n1 "sudo cat /sys/kernel/debug/tegra_dfll_fcpu/rate && sudo cat /sys/kernel/debug/tegra_dfll_fcpu/output_mv"`

GPU Voltage
- `watch -n1 "sudo cat /sys/kernel/debug/57000000.gpu/voltage"`

RAM Vdd2 & Vddq Voltages
- `sudo cat /sys/kernel/debug/regulator/vdd-ddr/regulator/microvolts && sudo cat /sys/kernel/debug/regulator/vddio-ddr/regulator/microvolts"`

CPU Stability Test
- `sudo ionice -c 2 -n 0 nice -n -19 stress-ng --cpu 4 --cpu-method=matrixprod --metrics-brief -t 120s`

GPU Stress Test : 
- `./cuda95 120` 
Or any graphical stress test / bench

RAM Stress Testing : 
- `watch -n 5 mem-bench`
- `sudo memtester 64M | grep "Loop\|FAIL"`
<br /> Running both a the same time for optimal stability test
<br /> For 8GB Users use `128M` or `256M` allocation size


## Acknowledgement 
- CTCaer
- Meha
