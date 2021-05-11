# XPAVO
eXtended Probabilistic Augmented Visual Odometry

Visual odometry, progressively improving estimates of (<br>
--> probability that a given feature is generally usable for VO<br>
), where the overall VO system is augmented by an IMU to validate feature usability.<br>

▶️ Possible Features and their Possible Shifts (motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 Update probabilities (w\/ IMU Data) (w\/ sample for `P(trackable)`)<br>
⬇️ 🔄 🔄 Satisfies Matching Threshold (`T_x`)❓ (else ⏬)<br>
⬇️ 🔄 Conflicts, i.e. multiple within Matching Threshold (`T_x`)❓ (else ⏬)<br>
⬇️ 🔄 Significant difference (`| max - max_2 |`) (`T_xcd`)❓ (else ⏬)<br>
⬇️ 🔄 Choose `max` and update ⏩ Matching Threshold (`T_x`) as `mean(max, mean(others))`!<br>
▶️ Possible Features with shifts resolved<br>
⬇️ 🔄 Update probabilities (w\/ IMU Data) (w\/ sample for `P(stationary)`)<br>
⬇️ 🔄 Satisfies `P(stationary)` threshold for Feature Buffer (`T_sb`)❓<br>
⬇️ 🔄 🔀 Sort these by `P(stationary)`<br>
⏩ In the Feature Buffer, 🔄 ⏩ remove those that fail the threshold (`T_s`) and `P(trackable) >= T_x`❓(else ⬇️)<br>
▶️ Feature Buffer<br>
⬇️ 🔄 Satisfies Final `P(usable)` threshold (`T_u`), where `P(usable) = P(trackable) * P(stationary)`❓<br>
▶️ Resulting Chosen Features ( ↘️ OUT ↘️ )<br>
