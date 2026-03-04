# fairroot source map: Doxygen

Generated from source roots:
- `cmake`
- `doxygen`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Fast source navigation
- `rg -n "BUILD_DOXYGEN|Doxygen_FOUND|add_subdirectory\(doxygen\)" CMakeLists.txt`
- `rg -n "DoxygenDoc|CONFIGURE_FILE|doc_makeall" doxygen/CMakeLists.txt doxygen/*.in`
- `rg -n "Doxygen" cmake/private/FairRootSummary.cmake`

## Suggested source entry points
### Top-level build gating
- `CMakeLists.txt` | symbols: `Option(BUILD_DOXYGEN)`, `find_package2(PRIVATE Doxygen ...)`.
- `cmake/private/FairRootSummary.cmake` | summary strings that confirm enabled/disabled state.

### Documentation target construction
- `doxygen/CMakeLists.txt` | symbols: `CONFIGURE_FILE(...)`, `ADD_CUSTOM_TARGET(DoxygenDoc ...)`.
- `doxygen/doxyfile.in` | Doxygen configuration values used at configure time.
- `doxygen/doc_makeall.sh.in` | shell wrapper executed by the custom target.
- `doxygen/fairDoxy.conf` | project-specific Doxygen configuration fragments.

### Helper macros used in config stage
- `cmake/modules/FairMacros.cmake` | common macros that can affect configure-time behavior.

## Quick behavior checks
- `cmake -S . -B <build> -DBUILD_DOXYGEN=ON`
- `cmake --build <build> --target DoxygenDoc`
- `test -f <build>/doxygen/doc/html/index.html`
