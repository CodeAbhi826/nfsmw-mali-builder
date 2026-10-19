# NFSMW Mali engine builder (orchestration only)

Public build runner for the **native (Mali/Vulkan)** NFSMW engine APK.

This repo contains **no game data and no app source**. It:

1. checks out the source from `CodeAbhi826/nfsmwrecomp-mali` at the requested ref;
2. fetches the PAL (Spanish) reference `default.xex` from a **private** repository
   using a read-only deploy key (Actions secret `NFSMW_XEX_DEPLOY_KEY`);
3. fetches the ReXGlue third-party sources;
4. builds the host `rexglue` code generator;
5. runs `tools/codegen.sh app` (game → C++);
6. enables Gradle's `externalNativeBuild`;
7. builds `assembleRelease` with NDK 28.2.13676358 and uploads the APK artifact.

The private harness (XEX + enable script) lives in
`CodeAbhi826/nfsmw-engine-builder` and must never be made public.

## Run

**Actions → engine-apk → Run workflow** (defaults: `ref=dev`, CMake `3.31.6`).

## Device run

```
--log_verbose=true --log_level=trace --nfsmw_nativo_simular_vulkan11=true
```

`nfsmw_nativo_cuatro_conjuntos=true` also enables the four-descriptor-set path
that Mali-G71 needs (the source check accepts either cvar).
