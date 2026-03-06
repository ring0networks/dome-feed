# dome-feed

OpenWrt package feed for [dome](https://github.com/ring0networks/dome) dependencies.

## Packages

| Package | Description |
|---------|------------|
| `lua-curl-5.4` | Lua 5.4 bindings to libcurl ([Lua-cURLv3](https://github.com/Lua-cURL/Lua-cURLv3)) |
| `lua-socket-5.4` | Lua 5.4 socket library ([LuaSocket](https://github.com/lunarmodules/luasocket)) |

## Usage

Add both the [Lunatik](https://github.com/luainkernel/openwrt_feed) and dome feeds to your OpenWrt build:

```bash
# feeds.conf.default
src-git luainkernel https://github.com/luainkernel/openwrt_feed.git;openwrt-24.10
src-git dome https://github.com/ring0networks/dome-feed.git;master
```

Then update and install:

```bash
./scripts/feeds update luainkernel dome
./scripts/feeds install -a -p luainkernel
./scripts/feeds install -a -p dome
```

Enable packages in `make menuconfig`:

```
Languages → Lua → lua-curl-5.4
Languages → Lua → lua-socket-5.4
```

## Build

```bash
make package/feeds/dome/lua-curl-5.4/compile V=s
make package/feeds/dome/lua-socket-5.4/compile V=s
```

## Dependencies

The dome system requires packages from two feeds:

```
dome-feed                      luainkernel feed
├── lang/                      ├── kernel/
│   ├── lua-curl-5.4            │   └── lunatik
│   │   (libcurl + lua5.4)     └── lang/
│   └── lua-socket-5.4               └── lua5.4
│       (lua5.4)
```

The `luainkernel` feed provides Lua 5.4 and the Lunatik kernel framework. This feed provides additional userspace dependencies.

