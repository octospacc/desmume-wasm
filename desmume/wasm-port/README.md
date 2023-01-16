# wasm-port

Latest HTML/JS/CSS source code is hosted on <https://ds.44670.org>.

`nds.js` and `nds.wasm` files are built from this repo, with Emscripten.

## Building from source

Ensure that the CMake and Emscripten SDKs are installed on your system, and that the `emmake`, `cmake` and `make` (or equivalent for your system) commands are available.

In the current directory (`desmume-wasm/desmume/wasm-port/`), run:

1. `emmake cmake .` (append `-DCMAKE_BUILD_TYPE=Release -DCMAKE_CONFIGURATION_TYPES=Release` for a release build, meaning smaller files)
2. `emmake make` (append `-j$(nproc --all)` to build with multiple threads)

You should get 2 runtime files: `nds` and `nds.wasm`.

### Get the webapp working

To get a working website, you need to download the external assets. You can use the `WebAssets.txt` list file, for example with wget: `for i in $(cat ./WebAssets.txt); do wget "https://ds.44670.org/$i"; done;`. Preferably run this in a clean folder without all the build files.

Now, you can move the `nds` and `nds.wasm` files built previously to `build/nds.js` and `build/nds.wasm` in the folder containing the downloaded web assets.

To run the app, serve the files from at least an HTTP web server for basic functionality, and HTTPS (due to service workers requirements) if you want the app to also work as an installable PWA.
