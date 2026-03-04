# fairroot source map: Inputs and Modeling

Generated from source roots:
- `examples`
- `fairroot`
- `tests`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "SetMaterials|SetGeometryFileName|GEOMPATH|CONFIG_DIR" examples`
- `rg -n "setFirstInput|setSecondInput|setOutput|saveOutput" fairroot/parbase`
- `rg -n "FairGeo|FieldFactory|Serializer" fairroot`

## Suggested source entry points
### Geometry and transport configuration inputs
- `examples/common/gconfig/g3Config.C`
- `examples/common/gconfig/g4Config.C`
- `examples/common/gconfig/FairVMCConfig.cxx`
- `examples/common/geometry/media.geo`
- `examples/common/geometry/pixel.geo`

### Parameter container production/consumption in tutorials
- `examples/simulation/Tutorial2/macros/run_tutorial2.C`
- `examples/simulation/Tutorial2/macros/create_digis.C`
- `examples/simulation/Tutorial2/src/FairTutorialDet2Digitizer.cxx`
- `examples/simulation/Tutorial2/src/FairTutorialDet2DigiPar.cxx`
- `examples/MQ/pixelDetector/macros/run_digi.C`
- `examples/MQ/pixelDetector/src/PixelDigiPar.cxx`
- `examples/simulation/Tutorial4/parameters/example.par`
- `examples/simulation/Tutorial4/src/param/FairTutorialDet4MisalignPar.cxx`
- `examples/simulation/Tutorial4/src/reco/FairTutorialDet4HitProducerIdealMisalign.cxx`

### Framework internals for geometry and runtime DB
- `fairroot/geobase/FairGeoLoader.cxx`
- `fairroot/geobase/FairGeoInterface.cxx`
- `fairroot/geobase/FairGeoBuilder.cxx`
- `fairroot/base/field/FairFieldFactory.cxx`
- `fairroot/base/field/FairField.cxx`
- `fairroot/parbase/FairRuntimeDb.cxx`
- `fairroot/parbase/FairParAsciiFileIo.cxx`
- `fairroot/parbase/FairParRootFileIo.cxx`

### Serialization policy hooks
- `fairroot/basemq/policies/Serialization/RootSerializer.h`
- `fairroot/basemq/policies/Serialization/BoostSerializer.h`

### Regression anchors
- `tests/geobase/tests_FairGeoSet.cxx`
- `tests/examples/simulation/Tutorial2/test_FairTutorialDet2Geo.cxx`
- `tests/examples/MQ/pixelDetector/test_PixelGeo.cxx`

## Quick behavior checks
- `root -l -q 'examples/simulation/Tutorial2/macros/run_tutorial2.C(10, "TGeant4", true)'`
- `root -l -q examples/simulation/Tutorial2/macros/create_digis.C`
- `ctest --test-dir <build> -R 'GeoBase|ExSimulation2|ExPixel' --output-on-failure`
