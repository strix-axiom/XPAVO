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
⏩ In the Feature Buffer, 🔄 ⏩ remove those that fail the threshold (`T_s`) and `P(trackable) >= T_x` test❓(else ⬇️)<br>
▶️ Feature Buffer<br>
⬇️ 🔄 Satisfies Final `P(usable)` threshold (`T_u`), where `P(usable) = P(trackable) * P(stationary)`❓<br>
▶️ Resulting Chosen Features ( ↘️ OUT ↘️ )<br>

main system (~stat) :

\[\[ IN \]\]<br>
V<br>
\{ Extract All Features \}<br>
V<br>
\{ Random Injection \}<br>
V<br>
\[ Feature Buffer \] <--|--> \{ Additional Validation \} -> \{ Average \} -> \[\[ OUT \]\]<br>
V<br>
\{ Assess Motion \} ---^<br>
^<br>
|----- \(\( IMU \)\)<br>

ALSO keep track of a random sample of features IN sample_buffer<br>
ALSO keep track of (IN sample_buffer) which ones are actually general ( i.e. P(specific) )<br>

Bayesian, update the probability of this feature accurately representing reality

with Accuracy:<br>
--> O( general | specific ) = O(general) \* bayes_factor<br>
where bayes_factor = P( specific | general ) / P( specific | \!general )<br>

prior FROM buffer<br>
P( specific | general ) FROM sample_buffer<br>
P( specific | \!general ) FROM sample_buffer<br>

Use this to yield both P(trackable) as well as the more obvious P(stationary). 

Trackable means avoiding conflicts, where there are multiple possible matches for a given feature that the IMU test deems OK. 

\[ All Even Slightly Likely Matches \] -> \[ Threshold 1 (Very Low) \] -> \{ Update (w\/ IMU) \} ->  \[ Threshold 2 (Med., Normal Value) \] --|

\{ Update Conflict Threshold \} <- \[ Conflict Threshold (High) \] <- \{\{ Significant Delta? (max v 2nd) \}\} <- \{\{ Conflict? (else exit) \}\} <-|<br>
\{ ^^^ @ mean(max, mean(others)) \}<br>
