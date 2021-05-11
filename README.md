# XPAVO
eXtended Probabilistic Augmented Visual Odometry

▶️ Possible Possible Shifts (Feature -> Possible Matches, motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 ➡️ Update probability `P(match)` (w\/ IMU Data) (w\/ sample for Bayes Theorem)<br>
⬇️ 🔄 🔄 ↔️ Probability (`P(match)`) above `50%`❓<br>
⬇️ 🔄 🔄 ↔️ Satisfies Matching Threshold (`T_m`), i.e. `P(match) > 1 - T_m`❓<br>
⬇️ 🔄 ⤵️ Conflicts, i.e. multiple options❓(else yield ⏬ the one given)<br>
⬇️ 🔄 ↪️ ↔️ Resolvable (`| max - max_2 | > T_cd`)❓ (else yield ⏬ `nothing`)<br>
⬇️ 🔄 ↪️ ➡️ Yield ⏬ `max`, and update ⏩ Matching Threshold (`T_m`) as `mean(max, mean(...others))`<br>
⬇️ 🔄 ➡️ Update probability `P(trackable)` (w\/ any conflict (first excluded)❓) (w\/ sample for Bayes Theorem)<br>
▶️ Possible Shifts (Feature -> Match, motion solved), with `P(trackable) = P(n_unresolvable_conflicts < 2)`<br>
⬇️ 🔄 🔀 Sort by `P(trackable)`<br>
⬇️ 🔃 Take while `P(trackable)` is within the Feature Buffer Threshold (`T_b`)❓<br>
⏩ 🔄 ↕️ Update Feature Buffer, use them to replace those that are dropped or fail `P(trackable) > 1 - T_b`❓<br>
⬇️ 🔄 ↔️ Satisfies Final Threshold (`T_f`), i.e. `P(trackable) > 1 - T_f`❓<br>
▶️ Usable Feature Shifts ( ↘️ OUT ↘️ )<br>
