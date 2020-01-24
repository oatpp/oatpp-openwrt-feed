# Oat++ OpenWRT feed

## Description

This is the Oat++ OpenWRT-feed containing build-scripts, options and patches for applications, modules and libraries provided by Oat++.

Oat++ is the modern Web Framework for C++. It's fully loaded and contains all necessary components for
effective production level development. It's also light and has small memory footprint.

- [Website](https://oatpp.io/)
- [Docs](https://oatpp.io/docs/start/)
- [Api Reference](https://oatpp.io/api/latest/)
- [Supported Platforms](https://oatpp.io/supported-platforms/)
- Latest Benchmarks: [5 Million WebSockets](https://oatpp.io/benchmark/websocket/5-million/)

**Join the community**
- Join discussion on **Gitter**. [oat++ framework/Lobby](https://gitter.im/oatpp-framework/Lobby)
- Follow us on **Twitter** for latest news. [@oatpp_io](https://twitter.com/oatpp_io)
- Join community on **Reddit**. [r/oatpp](https://www.reddit.com/r/oatpp/)

## Usage

This repository is intended to be layered on-top of an OpenWrt buildroot. If you do not have an OpenWrt buildroot installed, see the documentation at: [OpenWrt Buildroot – Installation](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem) on the OpenWrt support site.

To install this feed and all its package definitions, run the following in your OpenWRT root-folder:
```
echo "src-git oatpp https://github.com/oatpp/oatpp-openwrt-feed.git" >> ./feeds.conf
./scripts/feeds update oatpp
./scripts/feeds install -a -p oatpp
```

Oat++ libraries and options are located in `Libraries/Oat++`.

## License

See [LICENSE](LICENSE) file.
