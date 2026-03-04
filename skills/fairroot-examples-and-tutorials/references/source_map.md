# fairroot source map: Examples and Tutorials

Generated from source roots:
- `examples`
- `fairroot`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "Macro finished|FairRunSim|FairRunAna|SetSink|Run\(" examples`
- `rg -n "fairGetDevice|addCustomOptions|InitTask|Run\(" examples/MQ examples/advanced/Tutorial3/MQ`
- `rg -n "fairroot_add_catch2_test_suite" tests/examples`

## Suggested source entry points
### Tutorial3 macro chain (single-process and time-based)
- `examples/advanced/Tutorial3/macro/run_sim.C`
- `examples/advanced/Tutorial3/macro/run_digi.C`
- `examples/advanced/Tutorial3/macro/run_reco.C`
- `examples/advanced/Tutorial3/macro/run_digi_timebased.C`
- `examples/advanced/Tutorial3/macro/run_reco_timebased.C`

### Tutorial3 MQ chain
- `examples/advanced/Tutorial3/MQ/start.sh.in` | command template for format switch (`binary|boost|flatbuffers|protobuf|tmessage`).
- `examples/advanced/Tutorial3/MQ/sampler.cxx` | `addCustomOptions`, `fairGetDevice`.
- `examples/advanced/Tutorial3/MQ/processor.cxx` | task/device wiring.
- `examples/advanced/Tutorial3/MQ/sink.cxx` | sink output behavior.

### Pixel detector MQ example
- `examples/MQ/pixelDetector/macros/run_sim.C`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `examples/MQ/pixelDetector/macros/run_reco.C`
- `examples/MQ/pixelDetector/run/runMQSim.cxx`
- `examples/MQ/pixelDetector/run/runPixelTaskProcessor.cxx`
- `examples/MQ/pixelDetector/run/runPixelFileSink.cxx`
- `examples/MQ/pixelDetector/src/devices/FairMQSimDevice.cxx`
- `examples/MQ/pixelDetector/src/devices/PixelFindHitsTask.cxx`

### Serialization and LMD quick pipelines
- `examples/MQ/serialization/startSerializationEx.sh.in`
- `examples/MQ/serialization/sampler.cxx`
- `examples/MQ/serialization/processor.cxx`
- `examples/MQ/serialization/sink.cxx`
- `examples/MQ/serialization/data_generator/dataGenerator.cxx`
- `examples/MQ/Lmd/startMQExLmd.sh.in`
- `examples/MQ/Lmd/runLmdSampler.cxx`
- `examples/MQ/Lmd/runMBSMQUnpacker.cxx`
- `examples/MQ/Lmd/runMBSSink.cxx`

### Framework hooks and regression anchors
- `fairroot/fairmq/FairRunFairMQDevice.h`
- `fairroot/base/steer/FairRunSim.cxx`
- `fairroot/base/steer/FairRunAna.cxx`
- `tests/examples/advanced/Tutorial3/test_FairTestDetectorGeo.cxx`
- `tests/examples/MQ/pixelDetector/test_PixelGeo.cxx`
- `tests/examples/advanced/propagator/test_FairTutPropGeo.cxx`

## Quick behavior checks
- `root -l -q examples/advanced/Tutorial3/macro/run_sim.C`
- `root -l -q examples/advanced/Tutorial3/macro/run_digi.C`
- `root -l -q examples/advanced/Tutorial3/macro/run_reco.C`
- `ctest --test-dir <build> -R 'ExTestDetector|ExPixel|ExPropagator' --output-on-failure`
