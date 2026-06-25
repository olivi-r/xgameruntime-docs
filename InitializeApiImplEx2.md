# InitializeApiImplEx2

```c
HRESULT WINAPI InitializeApiImplEx2(
    ULONG gdkVer,
    ULONG gsVer,
    char mode,
    struct {
        UINT32 unknown; // always 1
        BOOL isInline; // only 1 when XGameRuntimeOptions::gameConfigSource == XGameRuntimeGameConfigSource::Inline
        const char *gameConfig; // identical pointer to XGameRuntimeOptions::gameConfig
    } *options
);
```

InitializeApiImplEx2 is called by both of the following functions:
- [XGameRuntimeInitialize](https://learn.microsoft.com/gaming/gdk/docs/reference/system/xgameruntimeinit/functions/xgameruntimeinitialize)
- [XGameRuntimeInitializeWithOptions](https://learn.microsoft.com/gaming/gdk/docs/reference/system/xgameruntimeinit/functions/xgameruntimeinitializewithoptions)

`mode` appears to be a bitfield likely related to both the runtime version and `options` value.

`mode` flag values seen:
- `0x01` - Set when a method is queried when the runtime has not been initialized. It is also set when calling [XGameRuntimeInitializeWithOptions](https://learn.microsoft.com/gaming/gdk/docs/reference/system/xgameruntimeinit/functions/xgameruntimeinitializewithoptions) with `gameConfigSource` set as [XGameRuntimeConfigSource::Default](https://learn.microsoft.com/xbox/gdk/docs/reference/system/xgameruntimeinit/enumerations/xgameruntimegameconfigsource).
- `0x02` - Unknown, always set.
- `0x08` - Set when `xgameruntime.dll` is in the same directory as the executable, as is required for GDK titles on the Steam Deck.
