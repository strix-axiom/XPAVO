# XPAVO
eXtended Probabilistic Augmented Visual Odometry

▶️ Possible Shifts (Feature -> Possible Matches, motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 ➡️ Update probability (w\/ IMU Data) (w\/ sample for Bayesian `P(match)`)<br>
⬇️ 🔄 🔄 ↔️ Satisfies Matching Threshold (`T_x`)❓<br>
⬇️ 🔄 ⤵️ Conflicts, i.e. multiple options❓(else ⏬ @ )
⬇️ 🔄 ↔️ Significant Difference (`| max - max_2 | > T_xcd`)❓ (else )
⬇️ 🔄 : 

▶️ Possible Features and their Possible Shifts (motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 Update probabilities (w\/ IMU Data) (w\/ sample for Bayesian `P(trackable)`)<br>
⬇️ 🔄 🔄 Satisfies Matching Threshold (`T_x`)❓ (else ⏬)<br>
⬇️ 🔄 Conflicts, i.e. multiple within Matching Threshold (`T_x`)❓ (else ⏬)<br>
⬇️ 🔄 Significant difference (`| max - max_2 |`) (`T_xcd`)❓ (else ⏬)<br>
⬇️ 🔄 Choose `max` and update ⏩ Matching Threshold (`T_x`) as `mean(max, mean(others))`!<br>
▶️ Possible Features with shifts resolved<br>
⬇️ 🔄 Update probabilities (w\/ IMU Data) (w\/ sample for Bayesian `P(stationary)`)<br>
⬇️ 🔄 Satisfies `P(stationary)` threshold for Feature Buffer (`T_sb`)❓<br>
⬇️ 🔄 🔀 Sort these by `P(stationary)`<br>
⏩ In the Feature Buffer, 🔄 ⏩ remove those that fail the threshold (`T_s`) and `P(trackable) >= T_x`❓(else ⬇️)<br>
▶️ Feature Buffer<br>
⬇️ 🔄 Satisfies Final `P(usable)` threshold (`T_u`), where `P(usable) = P(trackable) * P(stationary)`❓<br>
▶️ Resulting Chosen Features ( ↘️ OUT ↘️ )<br>
