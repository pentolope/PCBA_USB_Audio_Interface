# Architecture — Stereo USB Audio Interface

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- audio analog noise
- codec clocking
- USB differential
- ground return control

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## USB device architecture

- Is the USB side a USB-capable MCU or a dedicated USB audio bridge, and what decided it?
- What USB speed and specification revision does the chosen device support, and what does that imply for the stereo in/out channel and rate load?
- Is the device class-compliant on the intended hosts, or does it need a driver — and what evidence supports that claim?
- If an MCU is used, what firmware and enumeration work does the board depend on, and what on-board provisions (programming/debug access, boot strapping) does that require?
- Is VBUS presence sensed on the board, and if so how — and either way, what happens to the audio path on unplug or bus reset?

## Codec selection and the digital audio link

- Which codec is selected, and what evidence shows it meets or exceeds 24-bit/48 kHz for both capture and playback?
- What serial audio format and clock lines connect the codec to the MCU or bridge, and which side drives each line?
- What control interface configures the codec, and who drives it at power-up?
- Do the codec's ADC and DAC paths share supplies and references, and what does the datasheet require for each?
- What are the codec's own layout and grounding requirements, and are they compatible with the switching-power separation this brief requires?

## Clocking and jitter

- How is the audio clock generated — crystal, packaged oscillator, on-chip PLL, or recovered from the USB side — and what phase-noise or jitter figure is documented for that choice under this board's supply conditions?
- What jitter does the selected codec tolerate before its stated performance degrades, and how does the chosen source compare?
- Which device is audio clock master and which is slave, and how are the codec and the USB side rate-matched to one another?
- If the clock is a discrete device, where does it sit relative to the codec and how is its supply isolated and decoupled; if it is generated inside the codec, MCU or bridge, what supply and decoupling does that device's datasheet require instead?
- How are clock traces routed so they do not couple into the analog signal chain or the line connectors?

## Analog signal chain

- What nominal line level is the input designed to accept and the output designed to deliver, and what fixed that choice?
- What attenuation, gain, or buffering sits between the connectors and the codec pins?
- Are the codec's analog ports single-ended or differential, and how is that reconciled with the chosen connectors?
- What exact anti-alias and reconstruction network does the codec vendor recommend for the selected configuration, and is it reproduced faithfully?
- How are DC bias and AC coupling handled so that plug/unplug does not produce audible transients?
- What isolates left from right well enough to meet whatever crosstalk figure the design claims?

## Power architecture

- Where does board power come from, and if it is bus-powered, what is the current budget against the negotiated USB limit?
- What rails exist, at what voltages, and which are analog versus digital?
- For each analog rail, what regulator is used, and what is its noise density and PSRR across the audio band and at any switching frequency present?
- Is any switching converter used at all, or is the tree all-linear — and what decided that?
- If a switching converter is used, what is its switching frequency, where do its harmonics land relative to the audio band and the codec's sensitive nodes, how is its loop area bounded, and how far is it from the codec and the analog connectors?
- What decoupling does each codec supply pin require per its datasheet, and is that satisfied at the pin?

## Grounding and return paths

- Is there one ground or partitioned analog/digital grounds, and if partitioned, exactly where do they meet and why there?
- What is the return path for the USB differential pair, and does it cross any plane split or void?
- If a switching converter is present, what is its return path, and does any part of it share copper with an analog return?
- Where do the audio connector shields and sleeves connect, and what happens to cable-borne noise entering there?
- How is the return path verified rather than assumed — what check or analysis backs the claim?

## USB differential pair and ESD

- What differential impedance target is chosen for the USB pair, and which stackup, at the layer count chosen, produces it?
- What are the pair's length, matching, and reference-plane continuity, and do they satisfy the routing rules for the USB speed actually targeted?
- What ESD protection is placed at USB, and at what position relative to the connector and the controller?
- What is the protection device's junction capacitance, and what does it do to the pair's signal integrity at the chosen USB speed?
- Are the audio connectors also an ESD entry point, and if they are left unprotected, on what basis?

## Floorplanning and partitioning

- Where do the USB connector, the audio connectors, any switcher, the codec, and the clock sit relative to one another?
- What physical separation between any switching power section and the codec and analog connectors is achieved, and by what measure is it 'away'?
- Does the floorplan force any digital or switching return current through the analog region?
- How does connector placement interact with the board outline and any intended enclosure?
- Which placement constraints are hard (datasheet-driven) and which are the design agent's judgement?

## Stackup and fabrication

- Is the brief's four-layer preference followed, and on what grounds — and what is each layer assigned to, and why that ordering rather than an alternative?
- What dielectric thicknesses and copper weights does the chosen fabricator offer that hit the impedance target?
- What minimum trace/space and via sizes does the design need, and are they inside the fabricator's standard process?
- Does any part of the design require a controlled-impedance callout, and is it stated in the fabrication notes?

## Mechanical and connectors

- What board outline and dimensions are chosen, and what drove them?
- Which connector types are used for USB and for the stereo line in and out, and what mechanical retention do they need?
- Are the connectors on a common edge or face, and does that arrangement suit the intended use?
- Are mounting holes present, and how do they relate to the grounding decision?

## Verification and bring-up

- What audio performance figures does the design claim, and by what measurement would each be confirmed?
- What access, if any, is provided to observe the audio clock, the serial audio link, and the analog nodes after assembly, and what decided that?
- What is the power-up sequence, and can it be checked before the codec is exercised?
- What would falsify the 'quiet analog supplies' claim, and how would that be measured on the assembled board?
- How is the USB pair's integrity checked once the ESD device is populated?

## Answers still owed

All of them. See [status.md](status.md).
