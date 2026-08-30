# Benchmark entry — board 10 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_USB_Audio_Interface` |
| Board id | `usb_audio_interface` |
| Category | audio-mixed-signal |
| Difficulty | 3 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | audio analog noise, codec clocking, USB differential, ground return control |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

This is a mid-difficulty mixed-signal entry (category audio-mixed-signal, difficulty 3/5, brief detail 3/5): the brief states real intent about *what must be handled* — audio analog noise, codec clocking, USB differential, ground return control — while naming no parts, voltages, connectors, or dimensions. It tests whether an agent can co-locate a USB differential interface and whatever power conversion it chooses with a sensitive analog signal chain, and defend the partitioning rather than assert it — where the USB speed, the power topology, and whether the preferred four layers are adopted are themselves choices the brief leaves to the agent. The interesting failure mode here is not routing completion but unsubstantiated analog claims: the brief deliberately expresses constraints as goals ("low-jitter", "quiet", "away from") that only evidence-backed design choices can discharge.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
