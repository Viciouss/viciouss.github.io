---
layout: page
title: Samsung Galaxy Note 10.1 Mainline Progress
---

<br/>

<table>
    <thead>
        <tr>
            <th>Device/Part</th>
            <th>Name</th>
            <th>Kernel Driver </th>
            <th>P4Note DT</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th colspan="5">System on Chip</th>
        </tr>
        <tr>
            <td>SoC Base</td>
            <td>Exynos4412</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>GPU</td>
            <td>Mali</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Audio Codec</td>
            <td>WM1811</td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/18fea83b230f99c26659ea23603e77a3499fb2db" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/18fea83b230f99c26659ea23603e77a3499fb2db" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Wifi</td>
            <td>BCM4334</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Bluetooth</td>
            <td>BCM4334</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>GPS</td>
            <td>BCM47511</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Charging</th>
        </tr>
        <tr>
            <td>PMIC</td>
            <td>MAX77686</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>RTC</td>
            <td>MAX77686</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Fuel Gauge</td>
            <td>MAX17042</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Charger</td>
            <td>SMB347</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/ebe50f80950407c937f1ae21c891b9a8f1ac9a5e" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Charger Manager</td>
            <td>-</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Display</th>
        </tr>
        <tr>
            <td>LCD</td>
            <td>Sec LTL101AL01-002</td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/57ad2e7b4fd50532ad80bf4626d030f15adb0a7e" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/c512479a608599e6f5c91f77d4a842300ac9a4b3" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Backlight</td>
            <td>PWM + GPIO enabled</td>
            <td>-</td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/commit/c512479a608599e6f5c91f77d4a842300ac9a4b3" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Touchscreen</td>
            <td>Atmel MXT1664S</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <th colspan="5">Sensors</th>
        </tr>
        <tr>
            <td>Compass</td>
            <td>AKM AK8975C</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Accelerometer</td>
            <td>STM LSM330DLC</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>Gyroscope</td>
            <td>STM LSM330DLC</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>Light</td>
            <td>Liteon-Semi AL3201</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Connector</th>
        </tr>
        <tr>
            <td>USB peripheral mode</td>
            <td>DWC2</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Accepted <a href="https://git.kernel.org/pub/scm/linux/kernel/git/krzk/linux.git/commit/?h=for-next&id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>USB host mode</td>
            <td>DWC2</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>30 Pin Extcon (USB switch)</td>
            <td>-</td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/blob/v5.6.5-p4note/drivers/extcon/extcon-p4note.c" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>Keyboard Dock</td>
            <td>-</td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/blob/v5.6.5-p4note-extcon/drivers/input/keyboard/samsung-ekd-k14.c" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>MHL (HDMI)</td>
            <td>SII9244</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Other</th>
        </tr>
        <tr>
            <td>Vibrator</td>
            <td>ISA1200</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Camera</th>
        </tr>
        <tr>
            <td>Rear Facing</td>
            <td>ISX012</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>Front Facing</td>
            <td>S5K6A3</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <td>Flash LED</td>
            <td>?</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
        <tr>
            <th colspan="5">Connectivity</th>
        </tr>
        <tr>
            <td>Modem</td>
            <td>XMM6262/MDM9X15?</td>
            <td class="mainline-open">Open</td>
            <td class="mainline-open">Open</td>
        </tr>
    </tbody>
    
</table>