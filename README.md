# dome-feed

OpenWrt package feed for [dome](https://github.com/ring0networks/dome) dependencies.

## Packages

| Package | Description |
|---------|------------|
| `lua-curl-5.5` | Lua 5.5 bindings to libcurl ([Lua-cURLv3](https://github.com/Lua-cURL/Lua-cURLv3)) |
| `lua-nftables-5.5` | Lua 5.5 bindings to libnftables ([luanftables](https://github.com/ring0networks/luanftables)) |
| `lua-socket-5.5` | Lua 5.5 socket library ([LuaSocket](https://github.com/lunarmodules/luasocket)) |

## Usage

Add both the [Lunatik](https://github.com/luainkernel/openwrt_feed) and dome feeds to your OpenWrt build:

```bash
# feeds.conf.default
src-git luainkernel https://github.com/luainkernel/openwrt_feed.git;lunatik-5
src-git dome https://github.com/ring0networks/dome-feed.git;firmament
```

The packages need OpenWrt 24.10 or later: their mirror hashes are of the `.tar.zst` archives that 24.10's download tooling produces, and `lua-nftables` needs libnftables 1.1, where OpenWrt 23.05 ships 1.0.8.

Then update and install:

```bash
./scripts/feeds update luainkernel dome
./scripts/feeds install -a -p luainkernel
./scripts/feeds install -a -p dome
```

Enable packages in `make menuconfig`:

```
Languages → Lua → lua-curl-5.5
Languages → Lua → lua-nftables-5.5
Languages → Lua → lua-socket-5.5
```

## Build

```bash
make package/feeds/dome/lua-curl-5.5/compile V=s
make package/feeds/dome/lua-nftables-5.5/compile V=s
make package/feeds/dome/lua-socket-5.5/compile V=s
```

## Dependencies

The dome system requires packages from two feeds:

```
dome-feed                  luainkernel feed
├── lang/                  ├── kernel/
│   ├── lua-curl-5.5       │   └── lunatik
│   ├── lua-nftables-5.5   └── lang/
│   └── lua-socket-5.5         └── lua5.5
```

The `luainkernel` feed provides Lua 5.5 and the Lunatik kernel framework. This feed provides additional userspace dependencies.

