# XPAVO
eXtended Probabilistic Augmented Visual Odometry

▶️ Possible Possible Shifts (Feature -> Possible Matches, motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 ➡️ Update probability `P(match)` (w\/ IMU Data) (w\/ sample for Bayes Theorem)<br>
⬇️ 🔄 🔄 ➡️ Update probability `P(stationary)` (w\/ `P(match)` data) (w\/ sample for Bayes Theorem)<br>
⬇️ 🔄 🔄 ↔️ Satisfies Matching Threshold (`T_x`)❓<br>
⬇️ 🔄 ⤵️ Conflicts, i.e. multiple options❓(else yield ⏬ the one given )<br>
⬇️ 🔄 ↪️ ↔️ Resolvable (`| max - max_2 | > T_xcd`)❓ (else yield ⏬ `nothing`)<br>
⬇️ 🔄 ↪️ ➡️ Yield ⏬ `max`, and update ⏩ Matching Threshold (`T_x`) as `mean(max, mean(others))`<br>
⬇️ 🔄 ➡️ Update probability `P(trackable)` (w\/ any conflict (first excluded)❓) (w\/ sample for Bayes Theorem)<br>
▶️ Possible Shifts (Feature -> Match, motion solved)<br>


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
