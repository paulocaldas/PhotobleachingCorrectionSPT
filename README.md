## Photobleaching Correction for Single-Particle Measurements

**Approach**

In our single-particle imaging experiments, fluorophores appeared on the surface of the membrane, where they could be observed for several seconds without moving before they disappeared. Since TIRF microscopy only excites fluorophores close to the membrane, the termination of the fluorescent signal corresponds to a detachment of the fluorophore from the membrane into the buffer solution. We assume that this time corresponds to the time during which FtsZ monomers are incorporated in the FtsZ filament network. To obtain quantitative information about the lifetime of FtsZ monomers, we used the automated particle-tracking software TrackMate, a very powerful and user-friendly plugin for ImageJ/Fiji. The output is a table containing a distribution of lifetimes for all the tracked particles for a given time-lapse movie. Each experimental condition is recorded using multiple acquisition times and the output tables from TrackMate are used as input for our script.
Each distribution of lifetimes (i.e experiment) is fitted to a mono-exponential decay given by: <br>
y(t) = a.exp(-k_eff.t)

where k_eff is the effective rate of a monomer bound to a filament. <br>
This effective rate depends on the intrinsic detachment rate (k_off) from the membrane and on the photobleaching rate (k_pb): <br>

k_eff= k_off + k_pb		[eq.1] <br>

This photobleaching rate (k_pb) is proportional to the intensity and frequency we blast our sample, <br> 
which depends on the exposure time (t_ex) and acquisition time (t_ac):

k_pb = k_b.t_ex/t_ac 	[eq. 2] <br>

Where k_b is the photobleaching constant. <br>

From eq.1 and eq.2, we can re-define k_eff as follow: <br>

k_eff.t_ac = k_off.t_ac + k_b.t_ex

Thus, we plot k_eff.t_ac as a function of t_ac to obtain k_off from the slope of a linear regression. <br>
The true lifetime is then given by 1/k_off. The y-intercept corresponds to k_b.t_ex, which allows to estimate the photobleaching constant k_b.

**Procedure**

A dialog window allows you to select multiple files with different acquisition times ( tac). <br>
The script recognizes  tac from filename (msec, ms or sec) and extracts lifetimes from the column named TRACK_DURATION (in seconds). <br>
See folder with example data.

**Parameters**

threshN: in frames; discard particles that stay bound for less than treshN frames
bin_width: in frames;  size of each bin; 2 frames by default
cut_off: in frames; discard particles that stay bound for longer than cut_off frames (stuck particles)
t_exp: in seconds; the exposure time used in all experiments
