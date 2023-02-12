---
layout: page
title: Samsung Galaxy Note 10.1 Mainline Progress
---

<br/>

Last update: 2022-04-10

# Driver Upstreaming

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
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>GPU</td>
            <td>Mali</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Audio Codec</td>
            <td>WM1811</td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/c1d8e876dce0224baaf40f9711aba6da42502dbc" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/c1d8e876dce0224baaf40f9711aba6da42502dbc" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Wifi</td>
            <td>BCM4334</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Bluetooth</td>
            <td>BCM4334</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
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
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>RTC</td>
            <td>MAX77686</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Fuel Gauge</td>
            <td>MAX17042</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Charger</td>
            <td>SMB347</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.18) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=38dfe352b5a56df9cdf3e40ec5a09bb539757352" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <th colspan="5">Display</th>
        </tr>
        <tr>
            <td>LCD</td>
            <td>Sec LTL101AL01</td>
            <td class="mainline-ok">Upstream (6.1) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=a6aa679a70e9d8fa4ad3f519c060db9bb186e21c" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-ok">Upstream (6.0) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=6c52573bf4c3a0f6e7142264fb36b31ae2c3707a" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Backlight</td>
            <td>PWM Backlight</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (6.0) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=6c52573bf4c3a0f6e7142264fb36b31ae2c3707a" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Touchscreen</td>
            <td>Atmel MXT1664S</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <th colspan="5">Sensors</th>
        </tr>
        <tr>
            <td>Compass</td>
            <td>AKM AK8975C</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Accelerometer</td>
            <td>STM LSM330DLC</td>
            <td class="mainline-ok">Upstream <a href="https://github.com/Viciouss/linux/commit/04563b7696180ba9bda539de268ae2a33aa3f398" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/88b781e03a41db0f1e22593daa837160c0a90519" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Gyroscope</td>
            <td>STM LSM330DLC</td>
            <td class="mainline-ok">Upstream <a href="https://github.com/Viciouss/linux/commit/a96d1377acbe91e24309a9f7fff88464c3f9c5a2" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/88b781e03a41db0f1e22593daa837160c0a90519" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>Light</td>
            <td>Liteon-Semi AL3201</td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/7384d21c05f55e7711218a6564736bfcbe74cf3f" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/d70078cc802a8e6ff01aa230fb575542baff31a2" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <th colspan="5">Connector</th>
        </tr>
        <tr>
            <td>USB peripheral mode</td>
            <td>DWC2</td>
            <td class="mainline-ok">Upstream</td>
            <td class="mainline-ok">Upstream (5.11) <a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f48b5050c301f7235ef61d8cbbbf0410a5e0245f" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>USB host mode</td>
            <td>DWC2</td>
            <td class="mainline-ok">Upstream <a href="https://github.com/Viciouss/linux/commit/b36ec53ee5a170e9238fc9726781290e340e2623" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Downstream <a href="https://github.com/Viciouss/linux/commit/af3b234993d2a7e0c3c74e07786e7e8af0d72164" target="_new"><sup>[*]</sup></a></td>
        </tr>
        <tr>
            <td>30 Pin Extcon (USB switch)</td>
            <td>-</td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/commit/24584076dc6ba3441ae67250709541b14842856a" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/commit/78f2d95c56b8caa3d9b40c96c330ab0b80ba36cc" target="_new"><sup>[*]</sup></a></td>
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
            <td>Pen Input</td>
            <td>Wacom G5SP</td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/commit/14b435adeb5f2679faa13880f6feb0b005b124bd" target="_new"><sup>[*]</sup></a></td>
            <td class="mainline-wip">Experimental <a href="https://github.com/Viciouss/linux/commit/4ba0c9cf0b6fe6b7c2172bdaaf0290db4c075d00" target="_new"><sup>[*]</sup></a></td>
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

<br/>
# Other Patches/Improvements

<table>
    <thead>
        <tr>
            <th>What</th>
            <th>Patch</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>BGR Support for Exynos4/5</td>
            <td class="mainline-ok">Upstream (5.18)<a href="https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=2d684f4e155c1e80ff63bd503930171c460eac5b" target="_new"><sup>[*]</sup></a></td>
        </tr>
    </tbody>
</table>

