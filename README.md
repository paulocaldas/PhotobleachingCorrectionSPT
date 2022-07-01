## Photobleaching Correction for Single-Particle Measurements

**Approach**

Since TIRF microscopy only excites fluorophores close to glass coverslip, we can measure the time a fluorescently protein resides on the supported membrane, either due to direct interaction with the lipid bilayer, as in the case of FtsA, or because it is recruited by a membrane binding protein, as in the case of FtsZ. The termination of the fluorescent signal corresponds to the detachment of the protein from the membrane into the buffer solution. 
To obtain quantitative information about protein recruitment to the membrane, we combine single molecule imaging experiments with automated particle-tracking. For this aim we use TrackMate, a very powerful and user-friendly plugin for ImageJ/Fiji. The output is a table containing a distribution of lifetimes for all the tracked particles for a given time-lapse movie. Each experimental condition is recorded using multiple acquisition times and the output tables from TrackMate are used as input for our script.
The distribution of lifetimes of proteins on the membrane corresponds to a mono-exponential decay, which is described by:


y(t) = a*exp(-k_eff*t)   [Eq. 1]

where k_eff is the effective detachment rate of protein from the membrane. This effective rate is the sum of the actual detachment rate of the protein (k_off) and photobleaching rate (k_pb):

k_eff = k_off + k_pb [Eq. 2]

This photobleaching rate (k_pb) is proportional to the intensity and frequency we illuminate our sample, which is the ratio of the exposure time (t_ex) and acquisition time (t_ac) [1,2]:

k_pb = kb*t_ex/t_ac

Where kb is the photobleaching constant.  From eq.1 and eq.2, we can define keff as follow:

k_eff*t_ac = k_off*t_ac + kb*t_ex

Thus, we plot k_eff*t_ac as a function of t_ac to obtain k_off from the slope of a linear regression. 
The true lifetime is then given by 1/k_off. The y-intercept corresponds to k_b*t_ex, which allows to estimate the photobleaching constant k_b.

**Procedure**

A dialog window allows you to select multiple files with different acquisition times (t_ac). 
The script recognizes  t_ac from filename (msec, ms or sec) and extracts lifetimes from the column named TRACK_DURATION (in seconds).
See folder with example data.

**Parameters**

threshN: in frames; discard particles that stay bound for less than treshN frames <br>
bin_width: in frames;  size of each bin; 2 frames by default <br>
cut_off: in frames; discard particles that stay bound for longer than cut_off frames (stuck particles) <br>
t_exp: in seconds; the exposure time used in all experiments <br>

References:
[1] Gebhardt, J., Suter, D., Roy, R. et al. Single-molecule imaging of transcription factor binding to DNA in live mammalian cells. Nat Methods 10, 421–426 (2013). https://doi.org/10.1038/nmeth.2411
[2] N. Baranova, M. Loose, Chapter 21 - Single-molecule measurements to study polymerization dynamics of FtsZ-FtsA copolymers, Methods in Cell Biology, Academic Press,
Volume 137, 2017, Pages 355-370, https://doi.org/10.1016/bs.mcb.2016.03.036.
