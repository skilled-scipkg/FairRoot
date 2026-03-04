# fairroot source map: Getting Started

Generated from source roots:
- `examples`
- `fairroot`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "ActivateHttpServer|Run\(|SetSink|Macro finished" examples/advanced/MbsTutorial`
- `rg -n "fairGetDevice|addCustomOptions" examples/MQ/Lmd`
- `rg -n "FairRunOnline::|FairLmdSource::|FairMbsSource::" fairroot/online`

## Suggested source entry points
### First-run online macro path
- `examples/advanced/MbsTutorial/unpack_mbs.C` | source/sink/task wiring and runtime DB save path.
- `examples/advanced/MbsTutorial/FairMBSUnpack.cxx` | unpacker behavior.
- `examples/advanced/MbsTutorial/FairMBSTask.cxx` | first analysis task behavior.

### MQ LMD starter chain
- `examples/MQ/Lmd/startMQExLmd.sh.in` | generated launcher template.
- `examples/MQ/Lmd/runLmdSampler.cxx` | sampler CLI options and device factory.
- `examples/MQ/Lmd/runMBSMQUnpacker.cxx` | unpacker device setup.
- `examples/MQ/Lmd/runMBSSink.cxx` | sink behavior and output writing.
- `examples/MQ/Lmd/FairMBSUnpacker.cxx` | unpack logic used by the MQ chain.

### Framework-level first-run behavior
- `fairroot/online/steer/FairRunOnline.cxx`
- `fairroot/online/source/FairLmdSource.cxx`
- `fairroot/online/source/FairMbsSource.cxx`
- `fairroot/online/source/FairUnpack.cxx`
- `fairroot/basemq/devices/FairMQLmdSampler.h`
- `fairroot/mbsapi/fLmd.c`

### Regression anchors
- `tests/examples/simulation/Tutorial1/test_FairTutorialDet1Geo.cxx`
- `tests/examples/MQ/pixelDetector/test_PixelGeo.cxx`

## Quick behavior checks
- `root -l examples/advanced/MbsTutorial/unpack_mbs.C`
- `./startMQExLmd.sh` (from generated build `bin` directory)
- `ctest --test-dir <build> -R 'ExSimulation1|ExPixel' --output-on-failure`
