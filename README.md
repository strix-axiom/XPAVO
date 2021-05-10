# XPAVO
eXtended Probabilistic Augmented Visual Odometry

Visual odometry, progressively improving estimates of (<br>
--> probability that a given feature is generally usable for VO<br>
), where the overall VO system is augmented by an IMU to validate feature usability.<br>

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

\[ All Even Slightly Likely Matches \] -> \[ Threshold 1 (Very Low) \] -> \{ Update (w\/ IMU) \} ->  \[ Threshold 2 (Medium) \] -|

\{ Update Conflict Threshold \} <- \[ Conflict Threshold (High) \] <- \{\{ Significant Delta? (max v 2nd) \}\} <- \{\{ Conflict? \}\} <-|<br>
\{ @ mean(max, mean(others)) \}<br>
