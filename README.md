![Shape1](RackMultipart20230629-1-9ag2mm_html_53dda2028bb386b4.gif)

# AHRS-Yaw Calibration

#

# Problem Faced:

On observing the yaw value given as the output from the AHRS when connected to jetson, the yaw value observed as output was not stable and was constantly increasing.

# Solution

●After identifying the error, we tried to contact SBG-systems, through their official id and got a response from them to record a log file.

●Recording the log file:

●As we are using AHRS of SBG Systems Ellipse model, they have an exclusive software named **"SBG Centre",** which is available on their official site for all OS, Which can be used to configure the AHRS.

●We used this software to interface the AHRS directly to the laptop and connect it through the Software.

●We were able to observe the live response of AHRS to the manual Inputs given to it. When we observed the AHRS work completely fine and did not have any instability in measurement.

●Later we recorded a log file of the AHRS-Kept stationery in a still state for 2 minutes and that recorded file( **sbg format** ) was sent to their technical support team.

●Upon receiving their reply, our recorded file's output was observed to be

![](RackMultipart20230629-1-9ag2mm_html_f6b92ef1a38abe69.png)

●Where we can clearly observe the drifting of the yaw angle in the third image, hence we were able to conclude that the AHRS sensor's Solution mode was in " **Vertical-Gyro mode**", which makes an estimate of only roll and pitch angles [only roll and pitch values are taken for EKF estimation] and yaw is missed out to drift. So we had to change it to **"AHRS Mode"** and enable Magnetometers to **"rejection on automatic mode**")

![](RackMultipart20230629-1-9ag2mm_html_9de6b72062a89b4f.png)

●Vertical gyro mode:

Once roll and pitch angles are initialized, the EKF filter is running in a vertical gyro mode, where **only roll and pitch angles** are estimated. This mode uses a vertical reference and internal gyroscopes to estimate orientation. Therefore, the heading angle is freely drifting. Ship motion data is provided but may have degraded accuracy in dynamic environments.

●We have to change this to AHRS mode in order to make a proper estimation of yaw and to take that under consideration in EKF estimation. This requires a fresh calibration[rotate in yaw axis] of the yaw angle in the system[Place where it is going to be usedsituations].

●This can possibly be done through the SBG Center software, in the calibration menu, we calibrated in **2d-mode,**

And we're able to calibrate in the yaw axis, by slowly rotating the sensor slowly according to the analysis observed on the software,

●We calibrated twice and observed an effective precise output in the second calibration which was of **Three slow rotations** Later then flashed the calibration file into the AHRS internal memory, then our AHRS was working completely fine after that.

●Later, if the drifting persists, we have to make a 3d recalibration by placing the AHRS in its position in the system and involves effective rotations w.r.t all three axes.

**3d calibration gives the best performance,** but in situation where we cannot rotate the system in all 3 axes, we can perform 2d calibration.

●Need to Calibrate:

●Whenever there is a hard iron or soft iron distortion, A new calibration should be initiated. When a new metallic or magnetic component is added to the system, a new calibration should be initiated, in order to make the AHRS accommodate new magnetic fields, as orientation calculations depend on magnetic fields around it(Earth's Magnetic fields).

●In spite of a calibration rated as "GOOD", the AHRS pursues to show a deflection in the 2nd decimal of radian values, which might cause an offset o approximately 0.5-1 deg, which is completely natural.

●Resources:

[https://support.sbg-systems.com/sc/kb/v2/inertial-sensors-installation/magnetic-calibration](https://support.sbg-systems.com/sc/kb/v2/inertial-sensors-installation/magnetic-calibration)

[https://support.sbg-systems.com/sc/kb/latest/inertial-measurements-units/magnetometers](https://support.sbg-systems.com/sc/kb/latest/inertial-measurements-units/magnetometers)

[https://www.youtube.com/watch?v=U0cvJMbNIKI](https://www.youtube.com/watch?v=U0cvJMbNIKI)

[https://support.sbg-systems.com/sc/kb/latest/inertial-sensors-installation/magnetic-calibration](https://support.sbg-systems.com/sc/kb/latest/inertial-sensors-installation/magnetic-calibration)

![Shape2](RackMultipart20230629-1-9ag2mm_html_ae836f0cfc53e32d.gif) ![Shape3](RackMultipart20230629-1-9ag2mm_html_ac0d82252628cb98.gif)

![](RackMultipart20230629-1-9ag2mm_html_1f2e93545f6ebfc0.jpg)
