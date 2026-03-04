# fairroot source map: Simulation Workflows

Generated from source roots:
- `examples`
- `fairroot`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "Run\(|SetSink|SetMaterials|SetGenerator|Macro finished" examples/simulation examples/MQ`
- `rg -n "FairRunSim::|FairRunAna::|FairRootFileSink::|FairRuntimeDb::" fairroot`
- `rg -n "fairroot_add_catch2_test_suite" tests/examples`

## Suggested source entry points
### Canonical macro orchestration
- `examples/simulation/Tutorial1/macros/run_tutorial1.C`
- `examples/simulation/Tutorial1/macros/eventDisplay.C`
- `examples/simulation/Tutorial2/macros/run_tutorial2.C`
- `examples/simulation/Tutorial2/macros/create_digis.C`
- `examples/simulation/Tutorial4/macros/run_tutorial4.C`
- `examples/simulation/Tutorial4/macros/run_reco.C`
- `examples/MQ/pixelDetector/macros/run_sim.C`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `examples/MQ/pixelDetector/macros/run_reco.C`

### MQ split workflow internals
- `examples/MQ/pixelSimSplit/run/runMQGen.cxx`
- `examples/MQ/pixelSimSplit/run/runMQTrans.cxx`
- `examples/MQ/pixelSimSplit/run/runMQChunkMerger.cxx`
- `examples/MQ/pixelSimSplit/src/devices/FairMQPrimaryGeneratorDevice.cxx`
- `examples/MQ/pixelSimSplit/src/devices/FairMQTransportDevice.cxx`

### Framework runtime behavior
- `fairroot/base/steer/FairRun.cxx`
- `fairroot/base/steer/FairRunSim.cxx`
- `fairroot/base/steer/FairRunAna.cxx`
- `fairroot/base/sink/FairRootFileSink.cxx`
- `fairroot/parbase/FairRuntimeDb.cxx`
- `fairroot/generators/FairBoxGenerator.cxx`
- `fairroot/fairmq/FairRunFairMQDevice.h`
- `fairroot/eventdisplay/FairEventManager.cxx`

### Regression anchors
- `tests/examples/simulation/Tutorial1/test_FairTutorialDet1Geo.cxx`
- `tests/examples/simulation/Tutorial2/test_FairTutorialDet2Geo.cxx`
- `tests/examples/simulation/Tutorial4/test_FairTutorialDet4Geo.cxx`
- `tests/examples/MQ/pixelDetector/test_PixelGeo.cxx`

## Quick behavior checks
- `root -l -q 'examples/simulation/Tutorial1/macros/run_tutorial1.C(10, "TGeant3")'`
- `root -l -q 'examples/simulation/Tutorial2/macros/run_tutorial2.C(10, "TGeant4", true)'`
- `ctest --test-dir <build> -R 'ExSimulation|ExPixel' --output-on-failure`
