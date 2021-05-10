# XPAVO
eXtended Probabilistic Augmented Visual Odometry

Visual odometry, progressively improving estimates of (<br>
--> probability that a given feature is generally usable for VO<br>
), where the overall VO system is augmented by an IMU to validate feature usability.<br>

▶️ Possible Features and their Possible Shifts (motion solved)<br>
⬇️ 🔄 🔄 Update probabilities (w\/ IMU Data) (w\/ sample)<br>
⬇️ 🔄 🔄 Satisfies Normal Threshold (`T_xn`)? (else ⏬)<br>
⬇️ 🔄 Conflicts, i.e. multiple within Conflict Threshold (`T_xc`)? (else ▶️ `max` ⏬)<br>
⬇️ 🔄 Significant difference (`| max - max_2 |`) (`T_xcd`)? (else ⏬)<br>
⬇️ 🔄 Choose `max` and update Conflict Threshold (`T_xc`) as `mean(max, mean(others))`!<br>
▶️ Possible Features with shifts resolved<br>
... TODO ...

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
