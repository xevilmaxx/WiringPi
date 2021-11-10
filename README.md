# WiringPi 2.50 (already patched for generic debian)

WiringPi for Linux

Compatible with: **Unosquare.Raspberry.IO 0.17.2**


#### Actions to do in order to compile WiringPi

##### Disable Kernel strict security

1. Open with nano or through GUI file:
   **/boot/firmware/cmdline.txt**

2. Add following string at the end:
   **iomem=relaxed**

3. Final result should look like that:

4. ```
   console=tty0 console=ttyS1,115200 root=/dev/mmcblk0p2 rw fsck.repair=yes net.ifnames=0 cma=64M rootwait iomem=relaxed
   ```

5. Reboot to take effect (this steps are valid also for PiGPIO)

##### Compiling WiringPi

https://github.com/WiringPi/WiringPi/tree/final_official_2.50
https://github.com/sakaki-/genpi64-overlay/tree/master/dev-embedded/wiringpi/files

1. Clone 2.50 repo

2. ```bash
   #depth 1 in order to avoid downloading commits history
   git clone --depth 1 --branch final_official_2.50 https://github.com/WiringPi/WiringPi.git
   ```

3. Download also 2.44-pseudo-cpuinfo.patch from second link (name is not important)

4. Paste downloaded .patch file into cloned directory

5. ```bash
   patch -u < 2.44-pseudo-cpuinfo.patch
   ```

6. ```bash
   ./build
   ```

7. Test all works (you should see a table if all ok):

8. ```bash
   gpio readall
   ```

9. **Already patched GPIO version will be packed in Parko/Distrib/Utilities_Software/RaspberryPi**

10. ```bash
    #if wiringpi tells you have nothing in /etc/wiringpi/cpuinfo
    sudo mkdir /etc/wiringpi
    sudo cp /proc/cpuinfo /etc/wiringpi/cpuinfo
    ```

11. **Making compiled WiringPi usable by C# actual unosquare.wiringPi**

12. ```
    sudo ln -s /usr/local/lib/libwiringPi.so.2.50 /usr/lib/liblibwiringPi.so.2.50
    ```

    
