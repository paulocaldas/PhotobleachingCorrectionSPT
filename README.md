## Photobleaching Correction for Single-Particle Measurements

**Approach**

Since TIRF microscopy only excites fluorophores close to glass coverslip, we can use it in combination with supported lipid bilayers to quantify protein-membrane interactions, either due to direct interaction with the lipid bilayer, as in the case of FtsA, or because it is recruited by a membrane-binding protein, as in the case of FtsZ. The termination of the fluorescent signal corresponds to the detachment of the fluorescently labeled protein from the membrane into the buffer solution. However, due to photobleaching the recorded times can significantly deviate from the actually residence times of the protein. 

To obtain quantitative information about protein recruitment to the membrane, we combine single molecule imaging experiments with automated particle-tracking. To correct for the contribution photobleaching we record time lapse movies at different acquisation rates as described previously [1,2]. 

Single-molecule tracking is performed using TrackMate [3], a very powerful and user-friendly plugin for ImageJ/Fiji. The output is a table containing a distribution of lifetimes for all the tracked particles for a given time-lapse movie. Each experimental condition is recorded using multiple acquisition times and the output tables from TrackMate are used as input for our script.

The distribution of lifetimes of proteins on the membrane corresponds to a mono-exponential decay, which is described by:

<p align="center"> y(t) = a.exp(-k<sub>eff</sub>.t)   [Eq. 1] </p>

where k<sub>eff</sub> is the effective detachment rate of protein from the membrane. This effective rate is the sum of the actual detachment rate of the protein (k<sub>off</sub>) and photobleaching rate (k<sub>pb</sub>):

<p align="center">k<sub>eff</sub> = k<sub>off</sub> + k<sub>pb</sub> [Eq. 2] </p>

This photobleaching rate (k<sub>pb</sub>) is proportional to the intensity and frequency we illuminate our sample, which is the ratio of the exposure time (t<sub>ex</sub>) and acquisition time (t<sub>ac</sub>) [1,2]:

<p align="center">k<sub>pb</sub> = k<sub>b</sub>.t<sub>ex</sub>/t<sub>ac</sub> </p>

Where k<sub>b</sub> is the photobleaching constant.  From eq.1 and eq.2, we can define k<sub>eff</sub> as follow:

<p align="center">k<sub>eff</sub>.t_ac = k<sub>off</sub>.t<sub>ac</sub> + k<sub>b</sub>.t<sub>ex</sub> </p>

If we now plot k<sub>eff</sub>.t<sub>ac</sub> as a function of  t<sub>ac</sub> , we can obtain k<sub>off</sub> from the slope of a linear regression. The true lifetime is then given by  1/k<sub>off</sub>. The y-intercept corresponds to k<sub>b</sub>.t<sub>ex</sub>, which allows to obtain the photobleaching constant k<sub>b</sub>.

**Procedure**

A dialog window allows you to select multiple files with different acquisition times (t<sub>ac</sub>). 
The script recognizes  t<sub>ac</sub> from filename (msec, ms or sec) and extracts lifetimes from the column named TRACK_DURATION (in seconds).
See folder with example data.

**Parameters**

threshN: in frames; discard particles that stay bound for less than treshN frames <br>
bin_width: in frames;  size of each bin; 2 frames by default <br>
cut_off: in frames; discard particles that stay bound for longer than cut_off frames <br>
t_exp: in seconds; the exposure time used in all experiments <br>

**References**<br>
[1] Gebhardt, J., Suter, D., Roy, R. et al. Single-molecule imaging of transcription factor binding to DNA in live mammalian cells. Nat Methods 10, 421–426 (2013). https://doi.org/10.1038/nmeth.2411 <br>
[2] N. Baranova, M. Loose, Chapter 21 - Single-molecule measurements to study polymerization dynamics of FtsZ-FtsA copolymers, Methods in Cell Biology, Academic Press, Volume 137, 2017, Pages 355-370, https://doi.org/10.1016/bs.mcb.2016.03.036. <br>
[3] Tinevez, J.-Y. et al. TrackMate: An open and extensible platform for single-particle tracking. Methods (San Diego, Calif.) 115, 80–90 (2017).
