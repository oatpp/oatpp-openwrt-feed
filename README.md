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

### Note on Oat++-LibreSSL
We do not bundle a working LibreSSL recipe/makefile for OpenWRT. You have to create you own to fit your needs.
OpenWRT only ships OpenSSL-1.1 which is not compatible with LibreSSL.

## Configurations

Oat++-OpenWRT behaves differently on OpenWRT then it's non-embedded version.
Libraries are build as shared objects instead of static libraries, the test-lib is not installed and libraries are symlinked to `/usr/lib`.

### Main-Module

#### OATPP_BUILD_TYPE
Build Oat++ libraries and moduels as static or shared libraries. (Default: Shared)

#### OATPP_VERSIONIZE
By default, Oat++ is installed to `/usr/lib/oatpp.so`
To match the desktop-behaviour Oat++ can be installed to `/usr/lib/oatpp-<version>/oatpp.so` with this switch 

#### OATPP_INSTALL_TEST_LIB
Install the Oat++ testing library. (default: no)

#### OATPP_INSTALL_TEST_BIN
Install the Oat++ testing binary. (default: no, depends on `OATPP_INSTALL_TEST_LIB`)

### LibreSSL

#### OATPP_LIBRESSL_INSTALL_TEST_BIN
Install the Oat++-LibreSSL testing binary. (default: no, depends on `OATPP_INSTALL_TEST_LIB`)

### Swagger

#### OATPP_SWAGGER_INSTALL_UI
Install the Swagger-UI resources to `/usr/share/oatpp-$(PKG_VERSION)/bin/oatpp-swagger/res`
(default: y, why would you install swagger if not?)

#### OATPP_SWAGGER_INSTALL_TEST_BIN
Install the Oat++-Swagger testing binary. (default: no, depends on `OATPP_INSTALL_TEST_LIB`)

### Websocket

#### OATPP_SWAGGER_INSTALL_TEST_BIN
Install the Oat++-Websocket testing binary. (default: no, depends on `OATPP_INSTALL_TEST_LIB`)

## License

See [LICENSE](LICENSE) file.
