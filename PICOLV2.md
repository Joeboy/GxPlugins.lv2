# PicoLV2 build

The Pico build compiles the DSP-only LV2 binaries for the Cortex-M33 hard-float
ABI. It leaves the desktop build unchanged and uses the existing MOD metadata,
which does not reference the desktop X11 user interfaces. The build uses the
shared `Joeboy/zita-resampler` checkout at `../zita-resampler` instead of the
identical copies vendored by individual plugins.

Build and validate every plugin:

```sh
make -f Makefile.picolv2 check
```

Stage LV2 bundles under `build/picolv2-bundle`:

```sh
make -f Makefile.picolv2 install
```

Set `LV2DIR` to stage elsewhere, or set `PLUGINS` to build a subset:

```sh
make -f Makefile.picolv2 install \
    PLUGINS="GxSaturator.lv2 GxGuvnor.lv2" \
    LV2DIR=/path/to/pico-lv2-bundles
```

Set `ZITA_RESAMPLER_ROOT` if the resampler checkout is not a sibling of this
repository.

The only unresolved symbols permitted by `check` are the PicoLV2 allocation
and logging hooks supplied by the firmware host.
