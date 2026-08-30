# Stereo USB Audio Interface

Stereo USB audio interface with stereo line in and line out, built from a USB-capable MCU or USB audio bridge plus an audio codec supporting at least 24-bit/48 kHz operation.

This repository holds the design problem for a **stereo USB audio interface** with stereo line input and stereo line output. The brief fixes the functional shape — a USB-capable MCU *or* a USB audio bridge, an audio codec supporting at least 24-bit/48 kHz, anti-alias/reconstruction components as recommended by the codec vendor, a low-jitter audio clock strategy, ESD at USB, quiet analog supplies, and switching power kept away from the codec and the analog connectors — and states a preference for four layers. Everything else is left to the design agent: the specific bridge/MCU and codec parts, connector types, USB speed and audio-class model, sample rates above the stated floor, power source and rail structure (including whether any switching converter exists on the board at all), clock topology, grounding and return-path scheme, whether the four-layer preference is followed and the stackup and impedance targets that follow from it, and the board outline. Nothing in this scaffold selects a part, a voltage, a dimension, or a protection device; those decisions belong to the design work and must be justified against cited evidence when made.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 13 requirements and deliberately leaves
17 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Function | Stereo USB audio interface with stereo line input and stereo line output | brief |
| Host interface / controller | USB, implemented with either a USB-capable MCU or a USB audio bridge (the brief permits either) | brief |
| Audio converter | An audio codec supporting at least 24-bit/48 kHz operation (a floor, not a ceiling); no converter architecture is named | brief |
| Analog filtering | Anti-alias / reconstruction components as recommended by the codec vendor | brief |
| Clocking | A low-jitter audio clock strategy is to be included; the source, topology and master/slave direction are not specified | brief |
| Protection | ESD is to be included at USB; no device, topology or immunity level stated | brief |
| Analog supplies | Quiet analog supplies are to be included; no rail voltages, noise figures or regulator types stated | brief |
| Power/analog partitioning | Switching power kept away from the codec and the analog connectors (a constraint on switching power wherever it is used; the brief does not say a switching converter must exist) | brief |
| Layer count | Four layers are preferred — a stated preference, not a fixed count | brief |
| Likely layer count | 4 | metadata |
| Category / difficulty / brief detail | audio-mixed-signal; difficulty 3/5; detail 3/5 | metadata |
| Primary stressors | audio analog noise; codec clocking; USB differential; ground return control | metadata |
| Connectors (USB and audio) | Not fixed by the brief — design agent's choice | open |
| Power source (bus-powered vs. external) and rail set | Not fixed by the brief — design agent's choice | open |
| Board outline, dimensions, mounting and enclosure fit | Not fixed by the brief — design agent's choice | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 10 of 32 |
| Category | audio-mixed-signal |
| Difficulty | 3 / 5 |
| Brief detail | 3 / 5 |
| Likely layer count | 4 |
| Primary stressors | audio analog noise, codec clocking, USB differential, ground return control |

This is a mid-difficulty mixed-signal entry (category audio-mixed-signal, difficulty 3/5, brief detail 3/5): the brief states real intent about *what must be handled* — audio analog noise, codec clocking, USB differential, ground return control — while naming no parts, voltages, connectors, or dimensions. It tests whether an agent can co-locate a USB differential interface and whatever power conversion it chooses with a sensitive analog signal chain, and defend the partitioning rather than assert it — where the USB speed, the power topology, and whether the preferred four layers are adopted are themselves choices the brief leaves to the agent. The interesting failure mode here is not routing completion but unsubstantiated analog claims: the brief deliberately expresses constraints as goals ("low-jitter", "quiet", "away from") that only evidence-backed design choices can discharge.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `.claude/skills/` | the claim-audit and accountability-review skills [CLAUDE.md](CLAUDE.md) requires before a push |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_USB_Audio_Interface.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `d41fafe3049a87824dedd21687552fbab3b88aea546bd234e467615580c6bec7`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
