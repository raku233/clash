# clash

OpenClash 使用的 subconverter 模板是 `clash.ini`。大站点名单写成单条 `GEOSITE` / `GEOIP`，subconverter 不会再把它们展开成十几万条 `DOMAIN-SUFFIX`。旧模板在 `clash.ini.bak`。

启用前在 OpenClash 中：

1. 更新 GeoSite Dat 与 GeoIP Dat（使用 MetaCubeX 的 `geosite.dat` / `geoip.dat`，Smart / Meta 核心）。`GEOIP,netflix` 依赖 GeoIP Dat；只含国家代码的 mmdb 没有 `netflix` 类别。
2. 让订阅转换重新拉取本模板并更新订阅，不要沿用路由器上已经生成的那份 6MB 配置。
3. 先跑 OpenClash 自带的配置检查，通过后再启用。检查若报未知 `netflix` 类别，打开 GeoIP Dat（geodata）并更新数据库后重试。

## Shadowrocket

Shadowrocket 请使用 `shadowrocket.ini`，不要使用 `clash.ini`：Shadowrocket 不支持 `GEOSITE`，此模板改用远程域名规则集。

为保持配置小巧，已移除两份 MetaCubeX 大名单：`cn`（约 11 万条）和 `geolocation-!cn`（约 2.7 万条），保留局域网与各专项域名规则。未列入名单的域名经 DNS 解析后，CN IP 走「国内 / 直连」，其余走「国外」（FINAL）。取舍是分流依赖解析 IP，个别应用若分流不准，后续可添加单独规则修正。

通过局域网 subconverter 使用 `target=clash`；`target=surge` 会丢弃 VLESS / AnyTLS 节点，不适用于本订阅。订阅转换查询示例：

```text
target=clash&url=<机场订阅>&config=https://raw.githubusercontent.com/raku233/clash/main/shadowrocket.ini&emoji=false&udp=true
```

`target=clash` 会将规则集内联到生成的 YAML，无需配置 `managed_config_prefix`。
