# clash

OpenClash 使用的 subconverter 模板是 `clash.ini`。大站点名单写成单条 `GEOSITE` / `GEOIP`，subconverter 不会再把它们展开成十几万条 `DOMAIN-SUFFIX`。旧模板在 `clash.ini.bak`。

启用前在 OpenClash 中：

1. 更新 GeoSite Dat 与 GeoIP Dat（使用 MetaCubeX 的 `geosite.dat` / `geoip.dat`，Smart / Meta 核心）。`GEOIP,netflix` 依赖 GeoIP Dat；只含国家代码的 mmdb 没有 `netflix` 类别。
2. 让订阅转换重新拉取本模板并更新订阅，不要沿用路由器上已经生成的那份 6MB 配置。
3. 先跑 OpenClash 自带的配置检查，通过后再启用。检查若报未知 `netflix` 类别，打开 GeoIP Dat（geodata）并更新数据库后重试。
