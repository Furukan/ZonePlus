# ZonePlus

A Wally package of [1ForeverHD/ZonePlus](https://github.com/1ForeverHD/ZonePlus), ForeverHD's module for zones that
detect the players, parts and items within their parts, with Luau types.

```toml
[dependencies]
ZonePlus = "furukan/zoneplus@3.2.0"
```

```luau
local Zone = require(ReplicatedStorage.Packages.ZonePlus)

local zone = Zone.new(workspace.SafeZone)
zone.localPlayerEntered:Connect(function()
	print("Entered the safe zone")
end)
```

The full API is in the [upstream documentation](https://1foreverhd.github.io/ZonePlus/).

## Changes from upstream

The package is based on upstream commit `3bb4bdb` (`main`, ZonePlus v3.2.0 with the newer overlap filter names), and
its version follows the upstream version it is based on.

- **Wally package:** upstream's Rojo project is a whole DataModel; the package project is rooted at the Zone module, so
  it installs and works from any location in the DataModel. The files use the `.luau` extension and are formatted with
  StyLua.
- **Types:** `Zone.new` and `Zone.fromRegion` return an exported `Zone` type with the public properties, events and
  methods; the signals are typed with what they fire with (`playerEntered: Signal<Player>`). `Accuracy`, `Detection`,
  `Container` and `Item` are exported too.
- **Deprecated APIs:** `RaycastFilterType.Whitelist` is replaced with `Include`, and zone parts are checked to be in the
  `Default` collision group through `CollisionGroup` instead of `CollisionGroupId`.
- **Enum asserts:** the asserts that guard against repeated or reserved enum names always passed, as their conditions
  were wrapped in `typeof()`; they now check them.

The full history, with a tag for every published version, is in this repository.

## Development

Tools are pinned with Rokit (`rokit install`). luau-lsp builds the sourcemap from `default.project.json`. Publish with:

```sh
wally publish
```

## License

ZonePlus is licensed under the [MIT License](LICENSE) (Copyright (c) 2021 Ben Horton), and so is this package. The
license text ships inside the package, and the module's header names the author, the license and this repository.
