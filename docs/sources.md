# Sources — Stereo USB Audio Interface

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Audio codec datasheet and application notes | The brief delegates the anti-alias/reconstruction network to the codec vendor, so the vendor document is the authority for filter values, supply and decoupling requirements, clock input jitter tolerance, and layout/grounding guidance — for whichever converter architecture the selected codec uses. |
| USB-capable MCU or USB audio bridge datasheet | Establishes USB speed and PHY requirements, serial audio interface capability, clocking options (including any on-chip PLL), and whether the stereo in/out rate load is actually supported. |
| USB specification for the targeted revision and speed | Sets the differential pair impedance, routing and matching limits, connector pinout, and VBUS current rules that apply to whichever revision and speed the design targets — none of which a component datasheet supplies. |
| USB Audio Class specification and host driver documentation | Needed to substantiate any claim of class compliance or driverless operation for the chosen device architecture. |
| Clock source documentation with phase-noise or jitter data | The 'low-jitter' requirement can only be discharged by comparing a specified source — discrete oscillator, crystal plus driver, or an on-chip PLL characterised in its host device's datasheet — against the codec's stated jitter tolerance. |
| Regulator and LDO datasheets with output noise density and PSRR versus frequency | 'Quiet analog supplies' becomes a measurable claim only against noise and rejection curves, especially at any switching frequency present on the board. |
| ESD protection device datasheet | Clamping performance and junction capacitance are both needed: one to support the protection claim, the other to show the USB pair still meets its signal integrity budget. |
| PCB fabricator capability and controlled-impedance stackup tables | A USB impedance target is credible only against a real vendor stackup at the layer count actually chosen, together with its minimum trace/space and via rules. |
| Assembly-house process documentation and land-pattern standards | Footprints, courtyards, and any panelization or single/double-sided assembly decision must trace to the process actually used. |
| Connector mechanical drawings and mating specifications | USB and audio connector selection carries footprint, retention, panel-alignment and shield-connection facts that the mechanical and grounding decisions depend on. |
| ESD immunity test standards | Required if the design states an ESD withstand level rather than merely including protection; the level must trace to a defined test condition. |
| Audio measurement method references | Any SNR, THD+N, dynamic range, or crosstalk figure the design claims needs a stated measurement bandwidth, weighting, and load to be meaningful. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
