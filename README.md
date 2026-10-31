# darling-JavaScriptCore

## Upstream URL

https://github.com/apple-oss-distributions/JavaScriptCore/tree/JavaScriptCore-7611.3.10.1.3

## Updating Source

When updating the source code, make sure to refer to the [`Updating Sources`](https://docs.darlinghq.org/contributing/updating-sources/index.html#updating-sources) section from the Darling Docs website. Additional details (if any) can be found in [`darling/notes/UPDATE_SOURCE.md`](darling/notes/UPDATE_SOURCE.md).

## Interpreter build variants

The checked-in offlineasm headers contain configuration-specific structure
offsets and are guarded by `OFFLINE_ASM_ASSERT_ENABLED`. The interpreter must
select `debug/LLIntAssembly.h` when `ASSERT_ENABLED` is true and
`release/LLIntAssembly.h` otherwise, matching the other JavaScriptCore objects.
Do not force assertions on only for the interpreter or remove the generated
configuration guards: either would risk using incompatible structure offsets.
CMake supplies the architecture directory (`X86_64` or the i386 `C_LOOP`);
the translation unit selects the assertion variant, including when build flags
override the usual CMake configuration defaults.

Regenerate these headers only through `darling/scripts/generate-offlineasm.sh`
after the derived sources, as described in the source-update notes. Opcode
implementations belong in the LLInt assembly sources, not generated headers.