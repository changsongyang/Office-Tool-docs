# 部署命令 {#deploy-commands}

这些命令可以在命令行和命令框中使用，命令不区分大小写。如果命令参数中含有空格，请使用 "" (英文双引号) 将其包括起来。

``` batch
deploy params
```

例如以下是一条简单的部署命令：

``` batch
deploy /add O365ProPlusRetail_zh-cn
```

| 命令 | 说明 |  |
| :-- | :-- | :-- |
| /add *values[]* | 添加一个或多个产品 | *Values*: productID_languages，**其中 productID 为必需参数**。使用方法见[部署示例](deploy.md#command-examples-for-deploying-office) |
| /Product_ID.exclapps *value* | 为产品设置排除的应用程序 | `Product_ID` 根据 `/add` 参数中的 productID 设置。使用方法见[部署示例](deploy.md#command-examples-for-deploying-office) |
| /Product_ID.mak *value* | 为产品设置 MAK | `Product_ID` 根据 `/add` 参数中的 productID 设置。使用方法见[部署示例](deploy.md#command-examples-for-deploying-office) |
| /rm *values[]* | 卸载一个或多个产品 | *Values*: productID_languages，使用方法同 `/add` |
| /rmall | 卸载全部产品 |  |
| /rmmsi | 卸载全部 Office MSI 产品 |  |
| /channel *value* | 设置更新通道 | *Value*: 通道 ID，[更多信息](/zh-cn/usage/deploy/settings/basic.md#update-channel) |
| /branch *value* | 根据分支名称设置更新通道，这个命令会覆盖 `/channel` 命令。 | *Value*: 通道的分支名，[更多信息](/zh-cn/usage/toolbox/general.md#query-office-version) |
| /edition *value* | 设置体系结构 | *Value*: `32` 或 `64`，默认值为 `32` |
| /migratearch | 迁移体系结构 |  |
| /ver *value* | 设置 Office 版本号 | *Value*: Office 版本号 |
| /srcpath *value* | 设置源路径属性 | *Value*: 本地路径、SMB 路径 |
| /fallback | 在本地找不到语言包时回退到 Office CDN | *Value*: `true` 或 `false`，默认值为 `false` |
| /display *value* | 设置是否显示 Office 安装界面 | *Value*: `true` 显示，`false` 隐藏，默认值为 `true` |
| /acpteula | 代表用户接受最终用户许可协议 |  |
| /enableupdates | 是否启用 Office 更新 | *Value*: `true` 启用，`false` 禁用 |
| /updatepath | 设置 Office 更新下载路径 | *Value*: 本地路径、SMB 路径 |
| /module *value* | 设置安装模块 | *Value*: `0`: Office 部署工具，`1`: Office Tool Plus。默认值为 `0` |
| /dlfirst | 下载后再安装 |  |
| /shortcuts | 创建桌面快捷方式 |  |

::: warning 注意

如果使用 `/srcpath` 命令指定了源路径属性，则需要同时指定 `/ver` 和 `/channel` 属性，否则 Office 安装将会失败。

:::

## 部署 Office 示例 {#command-examples-for-deploying-office}

指定多个应用程序或语言时，你需要使用「英文逗号」将其隔开，例如 `Access,Lync` 或 `zh-cn,en-us`

如果需要添加/卸载语言包或者校对工具，请使用 `LanguagePack` 或 `ProofingTools` 作为产品 ID。

部署 Office 2021 专业增强版 - 批量版，简体中文，排除 Access, Outlook, OneNote，可以这样写：

``` batch
deploy /add ProPlus2021Volume_zh-cn /ProPlus2021Volume.exclapps Access,Outlook,OneNote /channel PerpetualVL2021
```

使用本地源部署 Office 时，你需要设置 `/srcpath`，`/ver` 和 `/channel` 参数。如果安装 64 位的 Office，还需设置 `/edition` 参数：

``` batch
deploy /add O365ProPlusRetail_zh-cn /O365ProPlusRetail.exclapps Access,Outlook,OneNote /edition 64 /srcpath "D:\Test\Office Tool" /ver 16.0.xxxxx.xxxxx /channel Current
```

若要为批量产品设置 MAK，可以这样写：

``` batch
deploy /add ProPlus2021Volume_zh-cn /ProPlus2021Volume.exclapps Access,Outlook,OneNote /ProPlus2021Volume.MAK XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /channel PerpetualVL2021
```

若要添加多个产品，可以这样写：

``` batch
deploy /add "ProPlus2021Volume_zh-cn|VisioPro2021Volume_zh-cn" /ProPlus2021Volume.exclapps Access,Outlook,OneNote,OneDrive,Groove /VisioPro2021Volume.exclapps OneDrive,Groove /channel PerpetualVL2021
```

若要卸载产品，可以这样写：

``` batch
deploy /rm ProPlus2021Volume
```

卸载多个产品时，可以这样写：

``` batch
deploy /rm "ProPlus2021Volume|VisioPro2021Volume"
```

若要卸载语言包，可以这样写：

``` batch
deploy /rm LanguagePack_en-us
```
