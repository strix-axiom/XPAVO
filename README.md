# XPAVO
eXtended Probabilistic Augmented Visual Odometry

▶️ Possible Possible Shifts (Feature -> Possible Matches, motion solved) ( ↙️ IN ↙️ )<br>
⬇️ 🔄 🔄 ➡️ Update probability `P(match)` (w\/ IMU Data) (w\/ sample for Bayes Theorem)<br>
⬇️ 🔄 🔄 ↔️ Probability (`P(match)`) above `50%`❓
⬇️ 🔄 🔄 ↔️ Satisfies Matching Threshold (`T_m`)❓<br>
⬇️ 🔄 ⤵️ Conflicts, i.e. multiple options❓(else yield ⏬ the one given )<br>
⬇️ 🔄 ↪️ ↔️ Resolvable (`| max - max_2 | > T_xcd`)❓ (else yield ⏬ `nothing`)<br>
⬇️ 🔄 ↪️ ➡️ Yield ⏬ `max`, and update ⏩ Matching Threshold (`T_x`) as `mean(max, mean(others))`<br>
⬇️ 🔄 ➡️ Update probability `P(trackable)` (w\/ any conflict (first excluded)❓) (w\/ sample for Bayes Theorem)<br>
▶️ Possible Shifts (Feature -> Match, motion solved), with `P(trackable)`<br>
⬇️ 🔄 🔀 Sort by `P(trackable)`<br>
⬇️ 🔃 Take while `P(trackable)` is within the Feature Buffer Threshold (`T_b`)❓<br>
⏩ Feature Buffer<br>

-- begin old --

⬇️ 🔄 Satisfies `P(trackable)` threshold for Feature Buffer (`T_xb`)❓<br>
⬇️ 🔄 🔀 Sort these by `P()`<br>
⏩ In the Feature Buffer, 🔄 ⏩ remove those that fail the threshold (`T_ui`) and `P(trackable) >= T_x`❓(else ⬇️)<br>
▶️ Feature Buffer<br>
⬇️ 🔄 Satisfies Final `P(usable)` threshold (`T_u`), where `P(usable) = P(trackable) * P(stationary)`❓<br>
▶️ Resulting Chosen Features ( ↘️ OUT ↘️ )<br>

-- end old --
