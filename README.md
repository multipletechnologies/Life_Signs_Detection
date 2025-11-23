# Life Signs Detection
A treatise on the creation of realistic life-signs detection mechanisms and systems. Based on current and evolving technologies that can be deployed for practical application in the medical and civil relief situation including but not limited to nature disaster.

## 1) Ways to detect electromagnetic fields from a distance (summary)

Passive magnetic sensing (magnetometers). Measure the static or time-varying magnetic flux density (B-field). Useful from centimeters to many meters depending on source strength — includes fluxgate, search-coil (induction) coils, optically-pumped atomic magnetometers (OPMs), SQUIDs, NV-diamond sensors. ( GMW Associates +2 PMC +2 )

Passive electric-field probes / E-field antennas. Measure the electric component (E-field) at RF and low frequencies; commonly used for EMC/EMI troubleshooting. Near-field probes (small antennas/coils) are used for short range. ( Antmicro )

Induction (transmit/receive) / electromagnetic induction (EMI) methods (active). You transmit a primary magnetic field and measure secondary (induced) fields from conductors/objects (metal detection, subsurface imaging). This is how many metal detectors and EMI geophysical systems work. Active methods increase signal-to-noise ratio vs. passive detection. ( GP Radar +1 )

Radar / RF backscatter (active). For radiating RF sources or reflective objects, transmit wideband pulses or CW and measure backscatter (range, doppler, polarimetric signatures). Standard for remote RF detection. ( ScienceDirect )

Array/beamforming techniques. Use multiple spatially separated sensors (magnetometers or antennas) to form direction estimates (bearing, TDOA, beamforming). Widely used for RF and for low-frequency arrays for geophysics. (Optica+1)

2) Most sensitive sensors available to the common market (practical list + typical sensitivities)

a. SQUID (superconducting quantum interference device)

Sensitivity: best lab/commercial SQUID systems ~sub-femtotesla per √Hz to a few fT/√Hz (some multiloop SQUIDs quoted ≈0.8 fT/√Hz).

Practical notes: highest sensitivity for DC/low-frequency magnetic fields but requires cryogenics or closed-cycle cryocoolers (operational complexity and cost). Commercial vendors exist but these are specialist instruments. Magnicon+1

b. Optically-Pumped Atomic Magnetometers (OPMs) — e.g., QuSpin and similar

Sensitivity: modern OPMs (zero-field / SERF and some scalar OPMs) reach low-fT to tens of fT/√Hz in relevant bands; some commercial devices quote single-digit fT–tens of fT range or pT depending on band and model. They approach SQUID performance without cryogenics. PMC+2 QUSPIN+2

c. NV-diamond magnetometers (nitrogen-vacancy centers)

Sensitivity: research systems have pushed toward pT and, in some lab demos and integrated designs, toward sub-pT or fT scale in restricted geometries; commercially available NV devices are generally higher noise than the best OPM/SQUIDs but are improving rapidly and provide compact, room-temperature sensors and excellent spatial resolution (microns to mm scale). Integrated Optics+1

d. Fluxgate magnetometers (classical solid-state)

Sensitivity: typical low-noise commercial fluxgates reach ~pT/√Hz to tens of pT/√Hz at 1 Hz depending on model; robust, broadband DC–low-frequency sensors, good for field mapping and many industrial tasks. Lower cost than OPMs/SQUIDs. GMW Associates+1

e. Induction (search) coils and loop antennas

Sensitivity: for AC fields (kHz and up) small coils and loop antennas combined with low-noise amplifiers are very sensitive and simple. Their sensitivity improves with coil area and number of turns but they are inherently insensitive to DC. Excellent for detecting time-varying fields and RF. Antmicro

Practical “common market” picks:

If you want a ready commercial sensor to prototype mapping & localization: fluxgate (Bartington, Billingsley) or commercial OPMs (QuSpin) are the sweet spot. SQUIDs give best sensitivity but have major logistical overhead. GMW Associates+1

3) Can a wide-band modulated signal be used to couple with an ambient field for detection? (Yes — active probing strategies)

Short answer: Yes. Active probing is a standard and powerful approach. Two distinct modes:

A. Transmit a controlled wide-band excitation and measure the response

Mechanism: transmit a wideband (or multi-frequency) magnetic/RF waveform; conductive and magnetic objects in the environment generate secondary fields (eddy currents, scattering) that modulate amplitude/phase across frequency. This is the basis of electromagnetic induction tomography (MIT), EMI geophysics, and wideband radar. Multi-frequency/wideband probing improves depth resolution and material discrimination. Wikipedia+2 MDPI+2

B. Inject a known modulation into your sensors (coherent detection / synchronous demodulation)

Mechanism: By modulating the transmitted field and using coherent (phase-sensitive) receivers you can extract tiny induced signals out of noise using matched filtering and lock-in techniques. This can boost detectability well below passive noise floors for the same receivers. Papers and systems in magnetic induction imaging and OPM-based active detection describe this. 
UCL Discovery+1

Practical caveats & constraints:

Bandwidth × depth tradeoff. Low frequencies penetrate farther but give coarser spatial resolution; higher frequencies give better spatial resolution but are attenuated more quickly. MIT and EMI use multi-frequency sweeps to balance this. MDPI

Regulatory limits. Transmitting EM energy (even magnetic fields) can be regulated (RF spectrum rules, conducted emissions, safety limits). For field trials check frequency/power limits for your jurisdiction.

Ambient noise and coupling. Active probing can mask or perturb the ambient field you might also want to measure passively; choose modulation patterns and synchronous processing to separate your probe from background. Lock-in, spread-spectrum, and coded waveforms help. 
GP Radar

4) Can the signal be used to triangulate the source of that lesser (weak) field? How to do localization

Yes — with caveats. Localization methods depend on frequency band and whether the field is radiating (far field) or near-field (inductive).

Localization approaches

Array/TDOA / Beamforming (RF / radiating sources). For radiating sources at RF, use an array of synchronized antennas and classical TDOA (time difference of arrival) or beamforming to get bearing and range (range needs absolute TDOA with known clocks or additional methods). Works best when source radiates and is in far-field. 
Optica

Amplitude/gradient inversion and vector field fitting (low-frequency magnetic near field). For low-frequency / magnetic dipole sources (near-field), the B-field of a magnetic dipole decays roughly as 
1/𝑟3 1/r3 (near field) and as 1/𝑟

1/r in the radiative far field — this rapid decay makes localization harder at larger ranges. Arrays of vector magnetometers (measuring all three components) and inversion algorithms (fit a dipole / multipole model) can localize sources if the SNR is sufficient and sensors cover a volume/plane around the source. Gradiometers (difference pairs) increase sensitivity to nearby sources and reject distant background. APS Links+1

Active probing + imaging (MIT / EMI tomography). Active multi-frequency excitation with multiple Tx/Rx positions lets you reconstruct conductivity/metallic anomalies via tomographic inversion. This gives spatial maps rather than a single “bearing” and is used for subsurface or cargo scanning. Resolution depends on frequency, array geometry and SNR. MDPI+1

Practical requirements to localize weak sources

Multiple sensors spaced over a baseline comparable to or larger than the expected source–sensor distance.

Synchronized sampling (for TDOA / phase interferometry). GPS clocks or a wired time base for small arrays.

Good SNR (use averaging, active probing, matched filtering, gradiometry).

Appropriate physical model (dipole vs more complex source) and inversion algorithm with regularization.

5) Engineering tradeoffs & prototyping recommendations (practical)

If you need maximum sensitivity and can manage complexity: SQUID or zero-field OPM arrays. SQUID → best fT performance but cryo overhead; OPM → near-SQUID sensitivity at room temperature in many bands. Magnicon+1

If you need a rugged, simple prototype quickly: fluxgate magnetometers (Bartington, Billingsley) or search coils for AC. Good for mapping, inexpensive, no cryo. GMW Associates+1

If you want to actively probe and localize hidden conductors/objects: design a multi-frequency EMI transmitter + arrayed receivers and use tomographic inversion (MIT/EMI literature is a good starting point). Use coded wideband waveforms and coherent demod to pull signals out of noise. Wikipedia+1

To localize an unknown weak radiating source: use antenna arrays and TDOA/beamforming if in RF; for low-frequency magnetic sources use vector magnetometer arrays plus inversion/gradiometry. Optica+1

# Human Life Sign Detection Focus

1) Physics and the main feasibility point — how large is the heart’s magnetic field and how it falls with distance

Key facts from literature and vendors:

Typical cardiac magnetic-field magnitude at the chest wall is on the order of tens to a few hundred picoTesla (pT). Many MCG sources quote ~50–100 pT at the anterior chest wall. ScienceDirect+1

Magnetic fields of a dipole-like source in the near field fall off like 
1/𝑟3
1/r3
. (Radiative far-field ≈1/r, but biomagnetic signals at heart rates are low frequency/near-field so 
1/𝑟3
1/r3 applies until you get very far out.) Nature

We’ll use those to make a few concrete SNR calculations for “can you detect a single person’s heart at X distance with Y sensor?” — this will show what’s realistic.

Assumptions for calculations (explicit):

Reference near-surface field 
𝐵𝑟𝑒𝑓=50 pT=50×10−12 TBref=50 pT=50×10−12 T at 𝑟𝑟𝑒𝑓=2 cm=0.02 mrref=2 cm=0.02 m. (This is conservative but representative.) ScienceDirect

Near-field scaling: 
𝐵(𝑟)=𝐵𝑟𝑒𝑓×(𝑟𝑟𝑒𝑓/𝑟)3B(r)=Bref	×(rref	/r)3.

Heartbeat useful bandwidth for the QRS/MCG features: assume BW ≈ 10 Hz (this is the signal bandwidth you’d want to capture for basic life-sign detection/heart rate and QRS shape).

Sensor noise is characterized as a noise spectral density 
𝑁𝐷ND in T/HzT/Hz
	​

. RMS noise in bandwidth BW is 
𝑁=𝑁𝐷×BWN=ND
	​

×BW	.

We compare sensors: SQUID ~1 fT/√Hz (best commercial), OPM (QuSpin QZFM gen3 quoted typically ~7–15 fT/√Hz in the 3–100 Hz band), fluxgate low-noise ~1 pT/√Hz (typical fluxgate is worse). QuSpin spec example: QZFM Gen-3 typical ~7–10 fT/√Hz (dual axis variants). QUSPIN+2 QUSPIN+2

Now do the arithmetic — step by step.

Signal at 1.0 m

scale factor 
(0.02/1.0)3=0.023=8.0×10−6(0.02/1.0)3=0.023=8.0×10−6.

𝐵(1.0 m)=50×10−12 T×8.0×10−6=4.0×10−16 T=0.4 fT.B(1.0 m)=50×10−12 T×8.0×10−6=4.0×10−16 T=0.4 fT.Sensor noise (RMS) in BW=10 Hz

SQUID: 
𝑁=1 fT/Hz×10=1×3.162=3.16 fT.N=1 fT/Hz	×10	=1×3.162=3.16 fT.

Good OPM (QuSpin typical 10 fT/√Hz used as round number): 
𝑁=10×3.162=31.6 fT.N=10×3.162=31.6 fT.
Fluxgate (1 pT/√Hz = 1000 fT/√Hz): 𝑁=1000×3.162=3162 fT.
N=1000×3.162=3162 fT.

Instantaneous SNR (single-beat, no averaging) = 
𝐵signal/𝑁Bsignal/N

SQUID: SNR ≈ 0.4 fT/3.16 fT≈0.130.4 fT/3.16 fT≈0.13 (i.e. −18 dB).
QuSpin OPM (10 fT/√Hz): SNR ≈ 0.4/31.6≈0.013
0.4/31.6≈0.013 (−38.7 dB).

Fluxgate: SNR ≈ 
0.4/3162≈1.3×10−40.4/3162≈1.3×10−4 (hopeless).

What integration/ensemble averaging would be required to reach SNR = 1?
Ensemble (or low-pass) averaging over time reduces noise RMS by 𝑇⋅BW

T⋅BW	
 if you’re averaging independent samples. For a periodic heartbeat you can do epoch averaging using the R-wave trigger: the reduction in noise improves roughly as 𝑁beats

Nbeats	​where 𝑁beats≈𝑇×HR/60Nbeats	≈T×HR/60.

Required averaging time 
𝑇
T to reach SNR = 1 can be found from

𝑇=(𝑁𝐷BW/𝐵signal)2BW=(𝑁𝐷𝐵signal)21BW.T=BW(ND BW/B signal)
2
	​

=(Bsignal	ND		)2BW1	.

Plug numbers:

SQUID: 𝑇≈(3.16/0.4)2/10≈(7.9)2/10≈62.4/10≈6.24 s.
T≈(3.16/0.4)
2/10≈(7.9)
2/10≈62.4/10≈6.24 s. → ~6 s of averaging (a few beats) to reach unity SNR at 1 m. 
AIP Publishing

OPM (~10 fT/√Hz): 
𝑇≈(31.6/0.4)2/10≈(79)2/10≈6241/10≈624 sT≈(31.6/0.4)2/10≈(79)2/10≈6241/10≈624 s → ~10.4 minutes of averaging (many hundreds of beats) to reach unity SNR at 1 m. 

QUSPIN

Interpretation:

With a high-performance SQUID, detection/MCG at ~1 m with short averaging is plausible (SQUIDs + shielded rooms or gradiometry typically used).

With current commercial OPMs (QuSpin gen3 ~7–15 fT/√Hz), unshielded detection at ~1 m is extremely challenging for single-beat detection but ensemble/epoch averaging or clever signal processing can extract the waveform with minutes of averaging in favorable conditions (and experimental work does show wearable/unshielded OPM-MCG demonstrations). PMC+1

Fluxgate sensors are not competitive for single-person MCG at meter ranges (they’re for pT-level and above DC/low-frequency mapping, navigation, geophysics).

So the oft-quoted “detect heart at 3 ft” claim depends critically on sensor type (SQUID vs OPM vs fluxgate), the amount of averaging, and the surrounding noise environment (urban EM noise and the earth’s field are large).

2) Commercially available options and constraints for a mobile system

Practical choices:

A. Portable SQUIDs

Offer the best sensitivity (sub-fT/√Hz). Historically used in shielded MCG labs. There are HTS SQUIDs and some mobile systems, but cryogenics or closed-cycle coolers complicate mobile deployment and add size/power/cost. Good for maximal raw sensitivity but poor for compact mobile units. AIP Publishing

B. Optically-Pumped Magnetometers (OPMs) — leading practical choice for mobile

Commercial OPMs (e.g., QuSpin QZFM Gen-3) offer ~7–15 fT/√Hz in the 3–100 Hz band and are room temperature and compact. Recent papers show wearable/unshielded OPM-MCG and even free-moving subject MCG in unshielded environments with careful compensation and signal processing. This is the best compromise for a mobile life-sign detector today. QUSPIN+1

C. Fluxgate magnetometers

Durable and cheap, but typical noise floors are pT/√Hz and up — not competitive if you want meter-range cardiac detection. Good for mapping larger fields or for gradiometric cancellation when combined with OPMs. Bartington

Recommendation (commercial): For a mobile system that can plausibly detect and localize heartbeat fields at useful ranges in realistic environments, use an array of multiple triaxial OPMs (QuSpin QZFM Gen-3 or equivalent) with active field compensation and adaptive signal processing. SQUIDs are better in sensitivity but are impractical for compact mobile systems due to cryogenics.

3) Active wide-band probing — your “induce a larger field and watch the modulation” idea

Short answer: yes in principle, but with strong practical limits.

Two distinct active strategies:

(A) Magnetic induction imaging / active probing (low frequency):

You transmit a controlled magnetic field (single-frequency, multi-frequency or pulsed) and measure the secondary fields produced by conductive structures (eddy currents) or magnetic response. This is effective for metallic/conductive targets (metal detectors, EMI geophysics). Humans are poor conductors for induction imaging at low frequencies and the cardiac/brain currents are small, so induced secondary fields due to passive conductivity of tissue are weak. EMI tomography does not naturally amplify the tiny internal bioelectric fields.

(B) Coherent modulation and synchronous detection (lock-in style):

If you transmit a known, coded magnetic field and use phase-sensitive receivers, you can detect tiny perturbations in that transmitted field caused by the presence and dynamics of nearby current sources (or moving conductive targets). Spread-spectrum/coded waveforms and matched filters can increase detectability by giving processing gain. This doesn’t magically amplify the heart’s intrinsic field — rather you create a large, controlled field and try to measure how the local small field perturbs amplitude/phase. The perturbation is tiny for biological tissue and will be dominated by motion and background.

Practical limits and notes

Tissue is mostly non-magnetic (µ≈µ0) and only weakly conductive; the interaction of a transmitted magnetic field with the internal cardiac currents is small. You can detect perturbations if you have a very large transmitted field or very sensitive gradiometry, but regulatory SAR and safety limits, and system portability, restrict how large you can make the transmit field.

Active probing works best when the target has contrast (metal, different conductivity) — humans are low-contrast in magnetic permeability and low in induced eddy current contrast at low frequencies. Thus active probing is great for detecting metal or pipes, less so for amplifying biomagnetic signals from heart/brain.

Bottom line for your idea (“create a large field and detect fluctuations caused by the small bio-field”): technically feasible to sense perturbations, but not an easy way to substantially extend detection range for cardiac/brain biomagnetism compared to simply improving passive sensor sensitivity (SQUID/OPM) and using array/processing techniques. Active probing may help in special cases (e.g., motion detection, breathing via chest conductivity changes), but it won't change the underlying small dipole amplitude of the heart by orders of magnitude.

4) Localization (triangulation) of a weak biomagnetic source

Approach depends on near- vs far-field and on whether you can actively average:

A. Near-field vector inversion (best for cardiac fields)

Use a small array of vector magnetometers (triaxial OPMs) at several known positions around the target area. Measure the three components of B at multiple points and fit a dipole (or multipole) model to estimate position and orientation. Because heart fields are approximately dipolar, a dipole fit works well if you get measurements on multiple sides or a distributed plane around the subject. Gradiometer configurations (difference sensors) dramatically improve SNR by rejecting spatially uniform noise. PMC+1

B. TDOA/phase interferometry (for radiating RF sources)

Not relevant for low-frequency biomagnetism (these are near-field, not radiating at the frequencies of interest). If you were searching for an RF transmitter, you’d use array TDOA and beamforming.

C. Practical localization accuracy

Accuracy scales with SNR and array geometry. With good SNR and sensors spaced by tens of centimeters, sub-10 cm localization is feasible for a dipole heart signal in controlled environments (papers on OPM-based mapping show mm–cm scale localization when sensors are near the chest). As range increases, required baseline and SNR grow rapidly (because the 
1/𝑟31/r3 decay magnifies errors). PMC

Important practical items:

Sensor synchronization (sample clocks) must be tight for phase-based methods; epoch-averaging requires stable relative timing (or an ECG trigger).

Active field compensation (coils producing cancel fields) or adaptive filtering against environmental noise will be necessary for field operation. There are commercial “field compensation” rigs used with OPM systems to operate unshielded. PMC

5) Concrete prototype plan (mobile life-sign detection & localization)

Goal: mobile unit that can detect heart rate and localize a person (single subject) at the maximum realistic distance, prioritizing a commercially feasible path.

Option A — maximal sensitivity (research/more complex):

Sensors: 3–7 × triaxial OPM sensors (QuSpin QZFM Gen-3). Use triax configuration so each sensor gives 3 components. QUSPIN

Array geometry: a small planar array (rigid frame) with ~20–50 cm aperture, or a 360° ring if you want bearing only. For longer range, increase aperture (meter scale) and sensor count.

DAQ & timing: low-noise ADC with 24-bit dynamic range and synchronous sampling across channels (or local clocks disciplined with PPS/GPS for distributed arrays). National Instruments or specialized digitizers.

Field compensation: lightweight active coils integrated into the frame to null the ambient DC field and to reduce dynamic range required of OPMs (field control + feedback). See unshielded OPM MCG literature. PMC

Signal processing: beat-synchronous averaging (epoch average using detected R-wave if you can get contact ECG; otherwise use blind periodicity search), matched filtering, ICA/PCA for noise removal, adaptive gradiometry.

Expected performance: near-chest detection (tens of cm) robust; detection/localization at ~0.5–1 m possible with SQUID-level sensitivity; with OPMs you get good detection within ~0.2–0.5 m in ordinary unshielded environments for single-beat detection, and multi-second averaging extends that range towards ~1 m in quiet environments. PMC+1

Option B — simpler, lower cost (proof-of-concept):

Sensors: 3–8 × high-quality fluxgate (Bartington MAG-13 or Mag-01H) as a coarse system to test localization algorithms at pT–nT levels and to develop field-nulling and motion compensation. These won’t see heart magnetics at meter range but are useful for engineering and gradiometer tests. Bartington+1

Active probing add-on (experimental):

Small coil capable of generating a controlled magnetic field (audio-band or LF sweep), used with synchronous demodulation on the magnetometers to attempt to detect perturbations caused by chest conductivity and motion (breathing). This could give additional detection channels for presence/motion but will not directly “amplify” the heart dipole signal substantially.

Short parts list (starting point):

4 × QuSpin QZFM Gen-3 OPM sensors (or equivalent) — for 3D vector you can use 3 sensors or triax variants. QUSPIN

1 × modular DAQ with synchronized channels (24-bit, sample ≥1 kS/s) (NI or alternatives).

1 × small active compensation coil set (custom frame coils + current driver).

Cables, battery/power, lightweight rigid frame (aluminum or carbon).

Optional: lightweight ECG chest patch for trigger and ground truth.

6) Risks, caveats & regulatory/safety notes

Environmental noise is the killer. Urban EM noise, vehicles, power lines, and magnetic materials create large interference. Active gradiometry and adaptive filtering are essential. Many research papers emphasize operation in magnetically quiet sites or using compensation coils. PMC

SQUIDs win on raw sensitivity but cryogenics are impractical for small mobile systems.

Active transmit fields are subject to safety/regulatory limits. Also they can mask the small biomagnetic signals and make signal extraction harder unless carefully coded and synchronized.

Privacy / ethics. Biomagnetic sensing of people raises privacy issues; consider policy/ethics and consent if used in the field.

# Technical Definitions

1 — What actually happens when two EMFs “come in contact”

Linearity / superposition: In free space and in most biological tissues Maxwell’s equations are linear (for the field strengths and frequencies we care about), so the resulting field is the vector sum of the fields you would have had separately. You do not get a new field that annihilates or morphs the sources magically — you get superposition (vector addition). Nonlinear interactions require a nonlinear medium (ferromagnetics at saturation, plasmas, nonlinear dielectrics, or devices that convert fields), which human tissue is not for our regime. In other words: the transmit B-field + heart B-field = B_total (vector sum). Wikipedia

Why “new” features appear: even though fields add linearly, the measured field (magnitude, phase, spatial pattern) at a receiver will change in ways that let you infer the presence of the small source. For example, the small dipolar field produced by a heart will slightly rotate the vector sum and change the local gradient and phase of a transmitted, coherent field. Those small changes are measurable if your receiver can see tiny changes in amplitude/phase against the large background and if you can reject environmental noise.

2 — What kinds of perturbations are physically plausible to measure

There are two distinct detection mechanisms to exploit:

A) Direct detection of the biofield added to the transmit field

You transmit a coherent low-frequency B-field. At a receiver (or gradiometer), the total field will be the transmit field plus the heart’s field. The heart’s contribution is still tiny (pT–fT scale), so you need a sensor with noise floor below that differential you want to measure (or you must average/lock-in). This is basically the same detectability equation as passive detection — injecting a big carrier does not magically amplify the dipole; it simply makes the environment dominated by a known field so phase/amplitude perturbations can be extracted coherently. If you measure phase/AM of your transmitted carrier very precisely (lock-in), you can pull a tiny perturbation out of the noise by matched filtering / long integration. Quspin

B) Induced secondary responses (eddy currents / conductivity contrast)

When you excite with a time-varying B-field, tissues and structures with conductivity will support eddy currents which in turn produce secondary fields. Methods that map these secondary fields are called Magnetic Induction Tomography (MIT) / EMI tomography. These methods work well when the target has electrical contrast (metal, strong conductors). Humans are weakly conductive (and mostly non-magnetic), so the eddy currents induced by a broadcast LF magnetic field are small; MIT tends to be low-contrast for small cardiac currents unless you are doing contact/near-field measurements or using special modalities (and inversion is ill-posed). In short: MIT amplifies presence of conductivity contrasts — not the tiny dipolar cardiac magnetic moment — so it’s useful for breathing/chest motion/bulk conductivity changes, but not a magic amplifier for heart magnetics. PubMed+1

3 — How “transmit above ambient” helps (and its limits)

Benefits:

Coherence & processing gain: Transmit a coded waveform (sinusoid, chirp, spread spectrum). Use synchronous demodulation / correlation / matched filters to get processing gain proportional to the time–bandwidth product — this can reveal perturbations orders of magnitude below raw noise. Think lock-in amplification, but you design the transmitted code to maximize discrimination of perturbations.

Known carrier vector: By controlling amplitude, phase and polarization of the transmit field you can design receivers to be maximally sensitive to small orthogonal perturbations (vector demod). That makes the small heart field easier to detect against a large, well-known background.

Hard limits:

Fractional perturbation scaling: the perturbation caused by a heart dipole is tiny relative to a large transmit field. If B_tx ≫ B_heart, the fractional change is ≈B_heart/B_tx; extracting that requires excellent linearity and dynamic range in the receivers and excellent common-mode rejection to cancel B_tx. You must design gradiometers / differential receivers that subtract the large, known component and reveal the tiny residual.

Power and coil currents required: producing large uniform low-frequency magnetic fields at meter scale requires heavy currents or close coupling (coil currents easily in tens to hundreds of amps for 100 μT uniform fields across a meter). That has obvious power, weight and thermal implications (I’ll quantify below).

Safety & regulation: public / occupational exposure limits exist for low-frequency magnetic fields (ICNIRP / FCC guidelines). Even in disaster relief, you must be aware of exposure limits and local regulations; emergency exemptions may be possible but you need to plan for this. ICNIRP+1

4 — Numbers: how big a transmit field can you practically make, and what fractional perturbation do you get?

Useful formula (on-axis field of a single loop radius 
𝑅
R at center):

𝐵(0)=𝜇0𝐼2𝑅B(0)=2Rμ0	I
	​
(For a pair of Helmholtz coils or multi-turn loops the constants change but scaling with 
𝐼/𝑅 I/R stays.)

Example quick calculations:

Suppose 
𝑅=1 mR=1 m. To produce 𝐵=100 𝜇TB=100 μT at the center we need

𝐼≈2𝑅𝐵𝜇0≈2⋅1⋅1×10−44𝜋×10−7≈1.6×102 A.I≈μ0	2RB	≈4π×10−72⋅1⋅1×10−4	≈1.6×102
 
 A.

That’s ≈160 A in a single turn loop — large, heavy cabling and very significant power/driver requirements. Smaller loop (R=0.2 m) reduces current to ≈32 A but then your field is localized (works only at short standoffs). (Derivation: Biot–Savart / on-axis loop formula; standard coil design.)

What fractional perturbation does a heart-caused dipole produce?

Heart field at ~1 m: earlier estimates put a freely radiating/dipole cardiac field ≈0.1–1 fT (this is consistent with literature estimates after 1/r^3 scaling from chest wall values). Compare to a 100 μT transmit field; fractional perturbation ≈ 
10−15 T/10−4 T=10−1110−15T/10−4T=10−11
 — eleven orders of magnitude smaller. You cannot measure that fractional change directly as a fractional amplitude change — instead you exploit that the heart’s field is not exactly colinear with your transmit field and has time structure (beat), so you look for those orthogonal/time-domain signatures with coherent detection and gradiometry rather than measuring an absolute amplitude change.

Bottom line from the numbers: realistically you cannot “overwhelm” the environment with a transmit field and expect the heart dipole to cause large amplitude changes in the carrier. Instead you should transmit coherently and detect tiny orthogonal/phase/time-locked perturbations with very sensitive vector receivers and strong differential (gradiometric) rejection. The transmit approach helps a lot if you can (a) make the transmit field strong enough at the location of interest without exceeding safety limits, (b) keep the transmit field stable and known, and (c) use sensor geometry and signal processing to null the large common term and amplify the small residual. ICNIRP gives reference levels you must consult for safety and operational planning. 
ICNIRP+1

5 — How a vehicle platform changes the design space (advantages & new possibilities)

Advantages:

Power & cooling: vehicle power (and the ability to carry batteries, heavy amplifiers, or even cryo systems) lets you build more powerful transmitter coils and high-performance receivers (even closed-cycle cryocoolers for SQUIDs if you accept weight/complexity).

Large fixed aperture and mobility: vehicle motion provides a synthetic aperture — you can move the sensor/transmitter around a scene and combine measurements to synthesize a large effective array for localization and imaging (improves angular resolution and SNR).

Compute & storage: onboard GPUs/FPGA permit real-time matched filtering, beamforming, and model-based inversion (e.g., EKF tracking of dipoles).

Mounting and mechanical stability: heavier coil frames and stable coil geometries are easier to integrate on vehicles.

Constraints:

Electromagnetic clutter: vehicles themselves are large metallic structures with eddy currents and magnetic signatures — you will need to characterize and subtract vehicle self-noise, and likely use boom-mounted coils/sensors to get away from vehicle fields.

Power & thermal management: large coil currents and high-power transmit amplifiers require heavy wiring, cooling and safety procedures.

Regulatory & safety: field strengths that are allowed for stationary use may be different for mobile use and in disaster zones; you’ll need appropriate approvals if fields exceed reference levels. 
ICNIRP

6 — Best practical architecture I recommend (vehicle or mobile)

A hybrid architecture that mixes coherent active probing with very sensitive, vector passive receivers and synthetic aperture localization gives the best shot:

Transmitter subsystem (active, coded):

Multi-turn, multi-coil (Helmholtz/pancake) transmit coils arranged to produce a controlled polarization and known phase. Use multi-frequency or chirped waveforms (audio to low-kHz depending on desired penetration vs resolution). Use coded waveforms (e.g., m-sequence, chirp) for matched-filter gain.

Drive with a high-current amplifier and pulse scheduling to stay within time-averaged exposure limits; use pulsed/low-duty transmit to get instantaneous high amplitude with lower average SAR if allowed.

Receiver subsystem (vector, gradiometric):

Array of vector OPMs (or SQUIDs if you can justify cryo) arranged as gradiometers to remove the large common transmit vector and environmental noise. OPMs are the practical sweet spot (room-temp, fT sensitivity). Use multiple baselines to allow dipole fitting. 
Quspin+1

Synchronous sampling tied to transmitter phase (lock-in / synchronous demod). Use both amplitude and phase outputs as detection channels.

Signal processing:

Matched filtering to the transmit code for processing gain.

Differential subtraction to remove the known transmit field vector (common mode). The residual contains orthogonal components and small phase shifts from the biofield.

Epoch averaging locked to heartbeat frequency / waveform (or blind detection via spectral-periodicity detection).

Synthetic aperture processing as the vehicle moves: combine coherent measurements to improve localization and reject static clutter.

Localization & tracking:

Fit a dipole (or small dipole ensemble) model to measured vector residuals across the array and over motion. Use EKF or particle filter to track a time-varying dipole amplitude/orientation and position. The vehicle motion produces diverse look angles and increases observability.

Safety & control:

Embed ICNIRP/FCC exposure checks into firmware; limit duty cycles and peak fields to safe windows. Precompute worst-case local exposures. ICNIRP+1

7 — Practical coil / power calculation (one worked example)

(illustrates why big transmit fields are expensive)

Helmholtz-like pair approximation: two identical circular coils radius 
𝑅
R, separated by 
𝑅
R, each N turns, carrying current I:

Center field (approx):

𝐵≈(45)3/2𝜇0𝑁𝐼𝑅B≈(54​)3/2Rμ0	NI	Take N=10 turns, R=0.5 m. To get B=100 μT:𝐼≈𝐵𝑅(45)3/2𝜇0𝑁≈1×10−4⋅0.50.7155⋅4𝜋×10−7⋅10≈5.6 AI≈(54	)3/2μ0	
NBR	≈0.7155⋅4π×10−7⋅101×10−4⋅0.5	≈5.6 A

That’s far more tractable than the single-turn large loop (because of N turns and smaller radius). But remember:

The uniform region is small (roughly inside the coil radius).

The coil inductance times driving frequency means you need power electronics to handle reactive currents at your modulation frequency.

Thermal dissipation and mechanical stresses must be handled.

This example shows design choices (coil radius R, turn count N, separation) let you trade current for turns and geometry; with vehicle power and a heavy coil you can generate sizable fields locally, but creating a large uniform field at tens of meters is still impractical. (Engineering references: coil design / Biot–Savart; MIT/EMI literature for inversion.) 
MDPI

8 — Regulatory / safety quick facts (must read before field trials)

ICNIRP provides recommended exposure reference levels for magnetic flux density and internal induced current density up to 100 kHz; those limits are frequency dependent. For many power-frequency ranges the public limit is on the order of 200–400 μT (reference levels vary with frequency) while occupational limits are higher; check the specific tables for the frequency bands you plan to use. Use these as design constraints for transmit amplitude/frequency/duty cycle. ICNIRP+1

FCC / national regulators: RF transmitters (above 100 kHz/AM) are regulated for field strength and power density; even for low Hz–kHz magnetic field transmitters, there are standards for human exposure and interference with medical devices. If you plan disaster-zone use, coordinate with local authorities for waiver/approval. FCC+1

9 — Recommended experimental plan (immediate steps you can do in the lab / field)

Short, prioritized sequence — do these now (you asked for no waiting; here are immediate experiments):

Bench phantom + single coil transmit test

Build a small coil (R≈0.2–0.5 m, N≈10 turns) and a drive amplifier capable of pulsed/current drive up to ~10 A for short pulses.

Place a magnetic dipole phantom (current loop or small dipole source that emulates heart magnitude) at known positions from 0.1–1.0 m. Measure how the induced field at a sensor changes with and without the transmit coil on (coherent demod). This tells you fractional perturbation scaling and dynamic range needs.

Receiver sensitivity & common-mode test

Use a QuSpin OPM or equivalent (commercial) and measure ability to detect a small known dipole while a transmit coil produces a large carrier; tune gradiometer subtraction and lock-in demod to see achievable residual noise floor (this is the real system test). QuSpin specs are documented and are a practical choice for mobile arrays. Quspin+1

Synthetic aperture trial (mobile)

Mount the transmit coil and 2–4 vector sensors on a mobile trolley and record while moving around the phantom; process data offline to test synthetic aperture dipole localization (coherent combination of different look angles). This will reveal how much motion helps localization and SNR.

Scaling & exposure calculation

For each transmit waveform and coil geometry, compute ICNIRP exposure at worst-case points and adjust duty cycle to stay within limits (or plan for waivers in controlled disaster scenarios). 
ICNIRP

10 — Short list of equipment suggestions (starting point)

Transmit coils & amplifier: custom wound Helmholtz / pancake coils (copper tube or heavy gauge wire), high-current linear amplifier or class-D power amp with controlled waveforms (design to handle low-frequency reactive loads).

Receivers: QuSpin QZFM Gen-3 OPMs (dual/triax variants) or high-end fluxgates for coarse testing. QuSpin typical sensitivity 7–15 fT/√Hz in single/dual axis and is a practical, off-the-shelf option. Quspin+1

DAQ & timing: Synchronous digitizer (24-bit ADC) with GPS/PPS timebase for distributed arrays. NI or equivalent.

Compute: FPGA/real-time board for matched filtering, GPU for inversion/beamforming.

Safety monitoring: field probes and exposure-calc software tied to transmit control.

11 — Final engineering takeaways (short)

Your active-probe idea is valid — transmit a large, known, coded field and look for small orthogonal/phase/time-locked perturbations. That approach leverages coherence and matched filtering and can outperform blind passive sensing in noisy environments.

But don’t expect a transmissive “amplification” of the heart field. The human heart will not significantly change the magnitude of a large broadcast field; it produces a tiny dipole that must be extracted as a residual via gradiometry and coherent processing. MIT-style induced eddy currents help for conductive contrast and motion (breathing), not for amplifying dipolar cardiac magnetism. PubMed+1

Vehicle mounting helps (power, synthetic aperture, cooling), but vehicle self-noise and coil/driver complexity are nontrivial engineering challenges.

Safety/regulatory limits and coil power requirements are real constraints: designing a transmit system that is both powerful enough to create a useful local carrier and safe/legal is a primary engineering task. Consult ICNIRP / FCC guidance for your planned frequency/content. ICNIRP+1
