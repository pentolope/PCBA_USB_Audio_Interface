# Requirements — Stereo USB Audio Interface

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `d41fafe3049a87824dedd21687552fbab3b88aea546bd234e467615580c6bec7`.

## Fixed by the brief

### REQ-01 — The board is a stereo USB audio interface.

Brief text:

> Design a stereo USB audio interface with stereo line input and stereo line output.

### REQ-02 — It provides stereo line input and stereo line output.

Brief text:

> Design a stereo USB audio interface with stereo line input and stereo line output.

### REQ-03 — The USB side is implemented with either a USB-capable MCU or a USB audio bridge; the brief permits either and mandates neither.

Brief text:

> USB-capable MCU or USB audio bridge plus an audio codec

### REQ-04 — An audio codec is used alongside the USB-capable MCU or bridge.

Brief text:

> Use a USB-capable MCU or USB audio bridge plus an audio codec supporting at least 24-bit/48 kHz operation.

### REQ-05 — The codec must support at least 24-bit / 48 kHz operation. This is a floor; the brief names no converter architecture and no upper limit.

Brief text:

> an audio codec supporting at least 24-bit/48 kHz operation

### REQ-06 — Anti-alias / reconstruction components must be included, and they must be the ones the codec vendor recommends — so this requirement is discharged against the selected codec's own documentation, not against a generic filter.

Brief text:

> Include anti-alias/reconstruction components recommended by the codec vendor

### REQ-07 — A low-jitter audio clock strategy must be included. The brief requires a strategy, not any named clock source, topology, or master/slave direction.

Brief text:

> Include anti-alias/reconstruction components recommended by the codec vendor, a low-jitter audio clock strategy

### REQ-08 — ESD must be handled at USB.

Brief text:

> Include anti-alias/reconstruction components recommended by the codec vendor, a low-jitter audio clock strategy, ESD at USB

### REQ-09 — The analog supplies must be quiet.

Brief text:

> Include anti-alias/reconstruction components recommended by the codec vendor, a low-jitter audio clock strategy, ESD at USB, and quiet analog supplies.

### REQ-10 — Switching power must be kept away from the codec and from the analog connectors — a placement and partitioning constraint, not only a schematic one. It constrains switching power wherever it is used; it does not itself require that a switching converter be present.

Brief text:

> Keep switching power away from the codec and analog connectors.

### REQ-11 — Four layers are preferred — the brief states a preference, not a mandated count.

Brief text:

> Keep switching power away from the codec and analog connectors. Four layers are preferred.

### REQ-12 — Stated requirements are authoritative; where the brief is open, the design agent makes and documents reasonable engineering decisions instead of inventing hidden user requirements.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-13 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic must not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Whether the USB side is a USB-capable MCU (with firmware) or a dedicated USB audio bridge, and which specific device.

The brief explicitly offers both options with 'or' and names no part; the trade (firmware burden, class compliance, clock control, BOM) is left entirely to the design agent.

*Decision:* **not yet made.**

### OPEN-02 — Which audio codec is selected, its converter architecture, and its package, digital audio interface format and control interface.

The brief constrains the codec only by 'at least 24-bit/48 kHz' and names no vendor, part, architecture, package, or interface.

*Decision:* **not yet made.**

### OPEN-03 — Sample rates and bit depths actually supported above the stated floor, and whether multiple rates or rate families are supported.

'at least 24-bit/48 kHz' sets a minimum; the brief says nothing about a maximum or about additional rates.

*Decision:* **not yet made.**

### OPEN-04 — USB speed, USB specification revision targeted, audio class model (class-compliant vs. driver-based), and descriptor/endpoint structure.

The brief names USB and ESD at USB but is silent on speed, revision, class compliance, and host driver strategy; stereo 24-bit/48 kHz in and out does not by itself force a speed grade.

*Decision:* **not yet made.**

### OPEN-05 — USB connector type, orientation, and mounting style.

The brief never names a connector; it only requires a USB interface with ESD handling.

*Decision:* **not yet made.**

### OPEN-06 — Audio connector type and count for the stereo line input and stereo line output, and whether input and output share a connector family.

The brief specifies stereo line in and stereo line out as functions only, and refers to 'analog connectors' with no type, pinout, or panel arrangement stated.

*Decision:* **not yet made.**

### OPEN-07 — Clock topology: crystal vs. packaged oscillator vs. recovered/PLL/rate-converted clocking, which device is audio clock master, and the phase-noise target that makes the strategy 'low-jitter'.

The brief requires a low-jitter audio clock strategy but prescribes no source, no master/slave direction, and no jitter figure.

*Decision:* **not yet made.**

### OPEN-08 — Power source: bus-powered from USB, externally powered, or both; any USB current budget that follows; and whether VBUS presence is sensed at all.

The brief is silent on where power comes from and on unplug behaviour; it only constrains where switching power may be placed if it exists.

*Decision:* **not yet made.**

### OPEN-09 — Rail count, rail voltages, and regulator topology per domain (linear vs. switching) for digital, analog, and any bias rails, plus whether a switching converter exists on the board at all.

'quiet analog supplies' states a goal with no voltages, no noise or PSRR figures, and no regulator type; the switching-power constraint bites only if a switcher is used, so an all-linear tree is not excluded.

*Decision:* **not yet made.**

### OPEN-10 — ESD protection scheme at USB: device type, placement, capacitance budget against the differential pair, and whether protection extends to the audio connectors.

The brief names ESD at USB as a stressor to handle, not a component or an immunity level, and says nothing about the audio ports.

*Decision:* **not yet made.**

### OPEN-11 — Grounding and return-path strategy: unified vs. partitioned analog/digital ground, where and how domains join, and how USB and any switching returns are steered away from analog returns.

'ground return control' is a listed stressor and the switching-power constraint implies partitioning, but the brief prescribes no grounding scheme.

*Decision:* **not yet made.**

### OPEN-12 — Whether the preferred four-layer count is adopted, and the stackup that follows: layer ordering and assignment, dielectric and copper weights, and the differential impedance target and tolerance for the USB pair.

The brief says four layers are preferred — a preference, not a mandate — and the metadata calls 4 the likely layer count; no impedance, material, or layer assignment is given, so both the count and the stackup are the design agent's to choose and justify.

*Decision:* **not yet made.**

### OPEN-13 — Board outline, dimensions, mounting hole pattern, connector edge placement, and any enclosure or panel fit.

The brief states no mechanical constraint of any kind.

*Decision:* **not yet made.**

### OPEN-14 — Analog signal conditioning around the codec: nominal line level, input attenuation or gain, buffering, single-ended vs. differential handling, AC coupling and DC bias.

The brief requires vendor-recommended anti-alias/reconstruction components but says nothing about levels, gain structure, or buffering.

*Decision:* **not yet made.**

### OPEN-15 — Whether any feature beyond stereo line in/out exists — headphone drive, level or mute controls, indicators, monitoring/loopback, firmware update path, or test points.

The brief describes only stereo line input and stereo line output; it neither requires nor forbids anything further.

*Decision:* **not yet made.**

### OPEN-16 — Manufacturing choices: fabricator and assembly process class, minimum trace/space and via geometry, single- vs. double-sided assembly, and panelization.

The brief states a layer preference only and names no vendor, process class, or assembly constraint.

*Decision:* **not yet made.**

### OPEN-17 — Which audio performance figures (SNR, THD+N, crosstalk, channel separation) the design commits to, and how they are to be verified.

The brief sets a resolution and sample-rate floor but states no performance targets or measurement conditions.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- Turning a stressor into a solution: the brief says 'ESD at USB', not 'a TVS array'. Naming a protection device is a design decision that must be justified against clamping and capacitance data, not read out of the brief.
- Asserting 'low-jitter' without numbers — no phase-noise figure for the chosen source and no codec jitter-tolerance spec — leaves the single clocking requirement undischarged while appearing satisfied.
- Claiming audio performance (SNR, THD+N, dynamic range, crosstalk) that was never measured and is not bounded by a cited datasheet figure under stated conditions.
- Declaring a controlled differential impedance for the USB pair without a fabricator stackup that actually produces it at the layer count chosen — four layers being a stated preference the design still has to adopt deliberately rather than inherit.
- Satisfying 'keep switching power away' by assertion rather than by a floorplan and a traced return path; separation is a measurable placement claim, not a sentence.
- Reflexively splitting the ground plane as an audio ritual, without analysing where USB and any switcher return currents actually flow — return control is a named stressor here, not a default.
- Copying a generic anti-alias/reconstruction network instead of the one the selected codec's vendor recommends for the selected configuration, which is what the brief actually requires.
- Inventing unstated specifics — a USB speed grade, a codec converter architecture, connector types, sample rate ceilings, rail voltages, the presence of a switching converter, board dimensions, or a bus-powered/self-powered decision — and presenting them as requirements rather than as documented design choices.
