# Table of Contents
 
1. [Prerequisites and Stability Tests](#prerequisites-and-stability-tests)
   1. [Setup](#setup)
   2. [Overclocking Software](#overclocking-software)
   3. [Monitoring Software](#monitoring-software)
   4. [Benchmarks](#benchmarks)
      1. [Recommended](#recommended)
      2. [Avoid](#avoid)
2. [Overclocking Info](#overclocking-info)
   1. [What is Overclocking and Undervolting?](#what-is-overclocking-and-undervolting)
   2. [Benefits of Overclocking and Undervolting](#benefits-of-overclocking-and-undervolting)
   3. [Overclocking vs. Undervolting](#overclocking-vs-undervolting)
   4. [Definitions of HWiNFO Performance Limits](#definitions-of-hwinfo-performance-limits)
   5. [Misconceptions](#misconceptions)
4. [Overclocking](#overclocking)
   1. [Finding a Core Clock](#finding-a-core-clock)
   2. [Finding a Memory Clock](#finding-a-memory-clock)
5. [Undervolting](#undervolting)
   1. [Finding a Voltage](#finding-a-voltage)
   2. [Tuning Voltage](#tuning-voltage)
7. [Flashing a VBIOS](#flashing-a-vbios)
   1. [VBIOS Information](#vbios-information)
   2. [How to Flash a VBIOS](#how-to-flash-a-vbios)
   3. [VBIOS Troubleshooting](#vbios-troubleshooting)
8. [Miscellaneous](#miscellaneous)
   1. [Fixing a Boot Loop](#fixing-a-boot-loop)
   2. [NVCleanstall/DDU](#nvcleanstallddu)
9. [Tips and Tricks](#tips-and-tricks)
   
# Prerequisites and Stability Tests
  ## Setup
  1. Download [MSI Afterburner](https://www.msi.com/Landing/afterburner/graphics-cards) and set a fan curve. Settings -> Fan -> Enable User Defined Control. Set a fan curve as high as possible while still being audibly tolerable. Setting a high fan curve is always preferable for benchmarking, but the same overclock settings may not be stable on a lower fan speed.
  
     ![image](https://user-images.githubusercontent.com/69487009/155074841-203d5993-73db-49fe-bb48-8289d175a0ef.png)

  2. While still in settings, go to User Interface -> User interface skinning properties and select a skin, such as the MSI Cyborg Afterburner skin, as it will be easier to follow.
  3. Download [HWiNFO](https://www.hwinfo.com/download/) and run it in sensors only.
  
     ![image](https://user-images.githubusercontent.com/69487009/155072633-1e3f814e-3350-4043-8640-b36f842d52c6.png)
  
  4. Go to MSI Afterburner, max out power and temp limits, and prioritize the power limit. Note that laptops and some GPUs cannot go over 100%. Some GPUs can have a higher power limit by shunting or by [flashing a higher power limit VBIOS](#flashing-a-vbios).
  
     ![image](https://user-images.githubusercontent.com/69487009/155073843-d60e666a-f3b8-4422-91a8-e331f663270b.png)
  
  5. If using a Lovelace GPU, disable ECC in the Nvidia Control Panel for more performance (needs more testing).
     
     ![image](https://i.postimg.cc/Px8GdbbN/01-lovelace-ecc.png)
     
  ## Overclocking Software
   * [MSI Afterburner](https://www.msi.com/Landing/afterburner/graphics-cards): This software is the most widely used and robust. Other software may be lacking in certain features and are generally not recommended.
  ## Monitoring Software
   * [HWiNFO](https://www.hwinfo.com/download/): HWiNFO is the most frequently used monitor software as it presents the values of all the sensors available and is an excellent software to have when overclocking your CPU, RAM, and GPU.
   * [GPU-Z](https://www.techpowerup.com/download/techpowerup-gpu-z/): GPU-Z is a software that reports the model, VBIOS, and the hardware specifics of your GPU.
   * [OCCT](https://www.ocbase.com/download): OCCT stress tests while providing sensor values from HWiNFO. OCCT can be used instead of HWiNFO as well.
  ## Benchmarks
  ### Recommended
   * One of the best stress tests is just playing games. Unfortunately, there is no conclusive stress test for GPUs other than OCCT, and playing games is a great way to find instability. Instability is when you have application crashes, freezes, driver crashes, BSODs, major stutters, or shutdowns. 
   * [Superposition](https://benchmark.unigine.com/superposition): This benchmark will stress your GPU and VRAM well and is good at finding instability. One should use Superposition for reliable scores to see performance regressions. Make sure to set the preset so it maxes out the VRAM *without going over.* <img align="center" src="https://i.postimg.cc/RZXxdZVC/02-superposition-vram.png">
   
     ![image](https://user-images.githubusercontent.com/69487009/155036041-4eed7d4b-1103-4d88-876c-d5878cbaf70e.png)
   
   * [3DMark](https://store.steampowered.com/app/223850/3DMark/): This is widely used to stress your GPU well and is also good at finding instability. Note that it is not recommended for performance regressions as there is a lot of variance in scores, and Superposition is better for getting accurate scores. There is a demo version you can download for free. Run the Time Spy benchmark, as it is the most relevant test.
   
     ![image](https://user-images.githubusercontent.com/69487009/156465473-db75ddc7-13ed-45aa-bce9-6154aeb50d88.png)

   * [OCCT](https://www.ocbase.com/): This test is the best for finding errors and stressing your GPU; however, it requires careful fine-tuning and takes a while to find the “sweet spot” as it power throttles at stock settings. Also, make sure you do not turn off your monitor, as some graphics drivers crash because of this.
   
     * V10: Go to the 3D Standard tab under test. Turn on error detection and shader complexity to 8. Next, decrease the GPU usage limit (%) until you barely (5% of the time) power throttle. Then, click start and leave it running for an hour.
     
     ![image](https://i.postimg.cc/3rmM6BJc/03-occt-standard.png)
     
     * V11: Go to the 3D Adaptive tab under test and set the values to the screenshot below. You can tweak these values to your GPU, such as the minimum and maximum intensity. Then, click start and leave it running for an hour.
     
     ![image](https://i.postimg.cc/gjvfZYTW/04-occt-adaptive.png)

  ### Avoid
   * Furmark: Draws a lot of power and doesn’t effectively test due to elevated temperatures and power limiting.
   * Kombustor: Same issue as Furmark.
   * Heaven: This is an ancient testing program (13 years ago) that doesn’t stress your GPU much. However, it can be helpful because you can run it in the background and loop it for free. I would not recommend this program unless you want to run it in the background for extended periods. If you decide to use this, your settings should look like this:
   
     ![image](https://user-images.githubusercontent.com/69487009/155033902-2cc5dc72-f71a-48f2-b3b4-5fe1c069b65d.png)
  
# Overclocking Info
 ## What is Overclocking and Undervolting?
  * Overclocking is the process of increasing clock speeds and performance for generally higher heat and lower stability. For the GPU, that means increasing the speed at which the core and VRAM run, which are core and memory clock speeds, respectively. Undervolting limits the amount of voltage supplied to the GPU and will lower wattage, voltage, and temperatures.
 ## Benefits of Overclocking and Undervolting
  * Overclocking can provide those extra frames or decrease the processing time in workloads and provide you with a slightly better experience. Undervolting will reduce temperatures and voltages and provide a quiet and stable experience. Combining the two is possible and is commonly done.
 ## Overclocking vs. Undervolting
  * Overclocking typically increases temperatures to gain performance. Undervolting will decrease temperatures and voltage to give consistent performance. While with overclocking, you may achieve a higher clock speed than undervolting, that clock speed may not be sustained under stress. They both have their place, and you should choose the one that better fits your needs. For Ampere and Lovelace, undervolting is heavily recommended as they consume a lot of power and power throttle very often unless they are modded in some way or have a high power limit.
 ## Definitions of HWiNFO Performance Limits
  * Here is a list of all the abbreviations and definitions of performance limits in HWiNFO:
  
    | Performance Limit                         | Abbreviation | Definition                                                      |
    | :---------------------------------------- | :----------: | :-------------------------------------------------------------- |
    | Performance Limit - Power                 | Pwr          | GPU has hit the power limit defined by its VBIOS and throttled. | 
    | Performance Limit - Thermal               | Thrm         | GPU has hit the thermal limit and throttled.                    |
    | Performance Limit - Reliability Voltage   | vRel         | Too much voltage for current temps.                             |
    | Performance Limit - Max Operating Voltage | VOp          | GPU has hit the voltage limit defined by its VBIOS.             |
    | Performance Limit - Utilization           | Util         | GPU is not under full load.                                     |
 ## Misconceptions
  * Overclocking is dangerous: Modern Nvidia GPUs are locked in terms of how far you can push the voltage unless you have a modded VBIOS or have a physical modification to your card. Therefore, your card’s voltage is safe, and increasing clock speeds will not increase the voltage to unsafe values.
  * Overclocking too much is dangerous: There is no such thing as overclocking a modern GPU with a hard voltage lock and a normal VBIOS too much. An overclock is only "bad" when unstable, fixed by stability testing.
  * Undervolting will lower performance: Undervolting will improve performance when power limited and reduce temperatures otherwise (12.5 (Pascal) - 15 MHz (Turing, Ampere, and Lovelace) increase for every 5 °C cooler).
  * Core voltage increases voltage used: The core voltage slider will generally not do much, but it increases the aggressiveness of the V/F curve and makes your GPU use the higher voltage points within the threshold of safe voltages of the card but does not work on most modern cards.
   * Dragging the point at the correct voltage to your desired clock speed is a common way to undervolt. This is an [unoptimal way](https://www.youtube.com/watch?v=RH3FZXvBkiE) because the effective clock speed is lower than the clock speed displayed when using this method. Instead, use the slider in Afterburner to change clock speeds.
     <img align="center" src="https://i.postimg.cc/YS0KsBh6/05-effective-clock.png">
   
     <img align="center" src="https://i.postimg.cc/LsWKdQ1r/06-core-clock.png">
  * The best or maximum overclock for a specific card: There is no best or maximum overclock. Every physical chip is different and will overclock differently, so copying settings is not advisable as there may be more headroom to overclock, or it may be unstable.
  * Undervolting reduces effective clocks on Lovelace: This is a misconception caused by improper undervolting and will not happen if undervolted properly.

     
# Overclocking
  
  * **Before proceeding, ensure you have read the [Setup](#setup) portion of the guide.**
  * You can combine an overclock with an undervolt or choose one over the other. An overclock with an undervolt will lead to more performance, however.
  ## Finding a Core Clock
  1. Open Afterburner and put the core clock offset to +75 as a baseline. This baseline will generally be stable, and 75 MHz ensures it fits with the 12.5 MHz steps that Pascal uses and the 15 MHz steps that Turning, Ampere, and Lovelace use.
  
     ![image](https://user-images.githubusercontent.com/69487009/155863420-bc3c3d17-07b9-4992-b3d6-1550352a7bbd.png)

  2. Apply the settings <img align="center" src="https://user-images.githubusercontent.com/69487009/155014073-4aac5d7b-91d6-4b96-abd1-ab51287cb248.png"> and save <img align="center" src="https://user-images.githubusercontent.com/69487009/155004968-6f7ee82e-1575-4605-9932-644e5d702d45.png"> them to a profile. <img align="center" src="https://user-images.githubusercontent.com/69487009/155006086-5e300602-f099-4c6e-a3bf-29962b2905d2.png">
  
  3. Click this <img align="center" src="https://user-images.githubusercontent.com/69487009/155013987-f6c7f084-c4cb-4804-bc98-1786056959a7.png"> to have the overclock applied at startup.
  
  4. Test the overclock, see if it is stable in both benchmarks and games, and monitor the temperatures using HWiNFO and stay under 80 °C on the core and 95 °C for the hotspot. Instability includes application crashes, freezes, driver crashes, BSODs, major stutters, and shutdowns.
  
  5. If stable, increase core clock speeds in increments of +15 MHz (Turing, Ampere, and Lovelace) /12.5 MHz (Pascal) using the slider or typing in a value. If the benchmarks or games crash, decrease clock speeds by the same amount and retest until you have reached stability. Temperatures and power limits will always be limiting factors. There is no “limit” on how far you can overclock; however, you will know you have reached the limit once you experience errors or crashes in stress tests and games. Remember that an overclock can be stable in one game but not another.
  ## Finding a Memory Clock
  * After testing the core overclock sufficiently and confirming its stability, you can increase the memory clock.
  
     ![image](https://user-images.githubusercontent.com/69487009/155074055-b1c4fab6-7f5f-4cc5-9bb6-f10a564705b5.png)

  1. Start at a memory clock offset of 500 MHz and increase in 50-100 MHz increments. Memory clocks usually scale much higher than core clocks (even over 1000 MHz).
  
  2. To test the stability of the memory clock, you will need to look for performance regressions and artifacts. If you see any receding or a lower score or visual artifacts, decrease the memory clock by 50-100 MHz and retest. The recommended benchmark for finding performance regressions (GDDR6X) is [Unigine Superposition](https://benchmark.unigine.com/superposition), as the scores are consistent.
  
     ![image](https://user-images.githubusercontent.com/69487009/155003914-986b3fbb-6f76-4f8a-b4c5-0d5351b7d2f6.png)
     
     1. Here are some examples of artifacts:
  
        ![image](https://user-images.githubusercontent.com/69487009/156505132-831c5bbe-a475-4bc5-9065-e5230612cb8e.png)
     
        ![image](https://user-images.githubusercontent.com/69487009/156505872-97d4ee36-6799-4c36-a9b1-d5672827fcba.png)

  * Test the overclock, see if it is stable in both benchmarks and games, and monitor the temperatures using HWiNFO and stay under 80 °C on the core and 95 °C for the hotspot.
  * If stable, increase memory clock by 50-100 MHz; if unstable, decrease memory clock in 50-100 MHz increments and retest. Continue repeating this process until you have found your maximum stable overclock.
 # Undervolting
  * **Before proceeding, ensure you have read the [Setup](#setup) portion of the guide.**
  * Undervolting can be done by itself or combined with [overclocking](#overclocking). Increasing the core clock after an undervolt will reset the graph, so you must redo the undervolt each time you increase the core clock. *This does not apply to the memory clock.*
  ## Finding a Voltage
  1. Click CTRL F to open the curve editor and [this video guide](https://www.youtube.com/watch?v=LPpW9yXHvOU) and start at a baseline of 900 mV. Anything above this value will likely power throttle on many cards, and going above this value is situational, and the temperature difference will not be as noticeable. You can raise this in a later step.
     1. Your curve should look like this to start:
    
       ![image](https://user-images.githubusercontent.com/69487009/156475780-19ff599b-56da-4d43-ae22-3ac738e9bc05.png)

  2. Select all the points past the voltage you want (900 mV) by holding down shift and left click and highlighting.
  3. Drag all the points down by selecting a point and dragging it down. Ensure the highest point on the part you are dragging down is lower than the highest point to its left. (Optionally, with everything selected including the maximum preferred voltage (ex. 900mV), click on 900mV - hold shift - press ENTER twice)
 
     1. Your curve should now look like this:
       
       ![image](https://user-images.githubusercontent.com/69487009/155075101-33097614-e25c-4678-aa7f-342abfaaedff.png)
  
  4. Apply the settings <img align="center" src="https://user-images.githubusercontent.com/69487009/155014073-4aac5d7b-91d6-4b96-abd1-ab51287cb248.png"> and save <img align="center" src="https://user-images.githubusercontent.com/69487009/155004968-6f7ee82e-1575-4605-9932-644e5d702d45.png"> them to a profile. <img align="center" src="https://user-images.githubusercontent.com/69487009/155006086-5e300602-f099-4c6e-a3bf-29962b2905d2.png">
  
  5. Click this <img align="center" src="https://user-images.githubusercontent.com/69487009/155013987-f6c7f084-c4cb-4804-bc98-1786056959a7.png"> to have the overclock applied at startup.
  
     1. Your curve should look like this:
 
       ![image](https://user-images.githubusercontent.com/69487009/155066400-0bce9ab3-da3a-431e-98e5-3ba9b88271d4.png)
       
  ## Tuning Voltage
  1. Run various workloads and games and check HWiNFO for power throttling in sensors only under GPU Performance Limiters.
 
       ![image](https://user-images.githubusercontent.com/69487009/155013749-0e22d23b-4d01-4e3a-b253-374171d38ae2.png)
     
  2. If you are power throttling in-game, lower voltage by 25 mV and retest. Once you are satisfied with temperatures and are not power throttling, you have found the optimum voltage. 25 mV is an arbitrary baseline value and can be changed to larger or smaller increments.
  
     1. Lowering voltage by 25 mV means that you will be at 875 mV from 900 mV, and your curve should look like this:
 
        ![image](https://user-images.githubusercontent.com/69487009/155066793-85249e79-b72a-492c-96a3-48d5e5fe5c21.png)
        
  3. Continue to lower voltage until satisfied with temperatures and power throttling. Too low voltage may have performance regression because of the decreased core clock.

# Flashing a VBIOS
 This section is for people who have already tested their overclocks but still want additional headroom. Flashing a VBIOS can be very helpful as it can increase power limits and overclocking headroom. However, it can also be risky and will void the warranty.
 ## VBIOS Information
  * Ensure that the card of the new VBIOS you’re flashing from has the same power connectors as the card you’re flashing to (2x8 pin, 1x12 pin, etc.).
  * Check the number of HDMI and DP ports of the new VBIOS and the card you’re flashing and make sure they match. Note that this is not mandatory, but ports may not function if they differ.
  * When you flash a VBIOS, the V/F curve and fan curve will differ, so your current overclock may not be stable or lower than usual, and the fan speeds may differ.
  * If your power goes out while flashing, there is a chance of bricking your card, just like a motherboard BIOS flash.
 ## How to Flash a VBIOS
  * Download [GPU-Z](https://www.techpowerup.com/gpuz/) and go to Advanced -> NVIDIA BIOS -> Power Limit -> Maximum.
  
     ![image](https://user-images.githubusercontent.com/69487009/155074239-f430056b-6141-4d60-8ff5-03e7350875b7.png)

  * After you have followed the steps above, go [here](https://www.techpowerup.com/vgabios/) and locate a suitable VBIOS with a higher power limit for your card.
 
     ![image](https://user-images.githubusercontent.com/69487009/155030699-7616020e-ac97-4ae0-9b26-9bd0ff8a379c.png)
  * There may be some XOC VBIOSes with a 1000w power limit, but these are highly discouraged unless you know what you are doing and have sufficient cooling/power.
  * After finding a VBIOS, download it and [NVFlash](https://www.techpowerup.com/download/nvidia-nvflash/).
  * Create a new folder in your home directory with any name and put the ROM and the contents of the extracted NVFlash folder inside. The folder should look like this. 
   
     ![image](https://user-images.githubusercontent.com/69487009/155030951-b4ed2a12-f5e5-4e15-a655-73116b429701.png)
    
  * Shift right-click inside the folder and select Open in Windows Terminal/Powershell.
  * Once the window is open, type `./nvflash64.exe --save example.rom`
    * Two dashes before save
  * Then type `./nvflash64.exe -6 `(type the first letter of the ROM and hit tab to complete)
    * One dash before 6.
  * Type “y” when prompted (twice), and keep in mind that your screen will flash/go black for a moment.
 ## VBIOS Troubleshooting
  * If the VBIOS failed to flash and you confirmed all the prerequisites to flashing, type `./nvflash64.exe —protectoff` before flashing.
  * If that still fails, try [this](https://www.techpowerup.com/download/nvidia-nvflash-with-board-id-mismatch-disabled/) version of NVFlash.

# Miscellaneous
 ## Fixing a Boot Loop
  * Hold down shift and click restart.
  * At the Choose an option screen, go to Troubleshoot > Advanced options > Startup Settings > Restart. Finally, type `4` to boot into safe mode.
  
     ![image](https://user-images.githubusercontent.com/69487009/155035875-c7a04198-6f72-45a8-8c81-af7b1bac496e.png)
  * Go into MSI Afterburner and uncheck this to have your overclock not applied at startup. If you have this checked, uncheck it as well.
 
     ![image](https://user-images.githubusercontent.com/69487009/155035951-3d926aaf-ffb4-44db-9910-844f8b7ad50d.png)
  ## NVCleanstall/DDU
  This is used when you suspect your drivers are causing issues or want a less bloated driver.
   * Install the [latest drivers](https://www.nvidia.com/Download/index.aspx), [DDU](https://www.guru3d.com/files-details/display-driver-uninstaller-download.html), and [NVCleanstall](https://www.techpowerup.com/download/techpowerup-nvcleanstall/). 
   * Unplug your Ethernet/turn off Wi-Fi to ensure that Windows doesn’t install drivers on its own.
   * Hold down shift and click restart. Go to Troubleshoot > Advanced options > Startup Settings > Restart.
   * Finally, type 4 to boot into safe mode.
   * Run DDU, select GPU as the device, and click clean and restart.
   * Boot into your computer like normal and run NVCleanstall.
   * Select use driver files on disk and select the driver you installed earlier.
   * Make sure everything is unchecked unless you need PhysX or the HD audio via HDMI/USB-C Driver.
   
      ![image](https://user-images.githubusercontent.com/69487009/178170410-5f59263d-37f6-4234-84d5-f2a7889b14c2.png)
   * Click next and uncheck everything other than Disable Installer Telemetry & Advertising.
   * Lastly, click install, and your drivers will install.
 
# Tips and Tricks
 * The most crucial thing about overclocking is experimentation; try different things like increasing voltage to get higher clocks or lower voltage to get lower temps and more consistent clocks.
 * Temps are important. GPUs should stay as cool as possible for longevity, audibility, and performance:
   * For starters, taking off your side panel can improve thermals in limited airflow scenarios; if they do, a case with more airflow will help thermals considerably.
   * Repasting your GPU with a high-quality paste such as NT-H2, KPX, GELID GC-Extreme, or MX-4/6. It’ll last a long time and has an incredible impact on temperatures. Spreading the paste to ensure it covers the entire die is crucial.
     
       ![image](https://i.postimg.cc/SR0BRXVd/07-cinebench-chart.png)
   * Deshrouding and adding fans such as Phanteks T30s, Noctua NF-A12x25s, or ARCTIC P12s are also an excellent way to improve temps as stock fans tend to be less than great.
   * A more aggressive fan curve on your CPU, GPU, or case can help airflow and thermals. Go as high as audibly tolerable.
   * Removing dust filters can help with airflow due to the misalignment of holes.
   * Some GPU backplates act as insulators instead of heat dissipators, and replacing/removing them may be beneficial.
   * A PCI fan bracket mounted with fans blowing directly under the GPU may improve airflow.

     ![image](https://user-images.githubusercontent.com/69487009/155073843-d60e666a-f3b8-4422-91a8-e331f663270b.png)
  
  5. If using a Lovelace GPU, disable ECC in the Nvidia Control Panel for more performance (needs more testing).
     
     ![image](https://i.postimg.cc/Px8GdbbN/01-lovelace-ecc.png)
