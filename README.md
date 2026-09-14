![Image text](https://github.com/EosZeph/SeeFunds/blame/main/see-funds.png)
# See Funds

See Funds 是一个本地优先的个人资金分析桌面程序，用于导入微信账单和常见银行 CSV/Excel 账单，并按照现金流口径统计资金来源、资金去向和共同交易主体。

作者：Zepy  
版本：v1.0.0  
许可证：MIT

## 功能

- 导入微信和常见银行的 CSV、XLSX、XLS、XLSB、ODS 账单。
- 自动识别交易时间、交易类型、交易对方、商品、收支、金额、支付方式、状态、交易单号和商户单号。
- 多文件合并，并按交易单号、商户单号或交易指纹去重。
- 区分外部收入、外部支出、退款、信用卡还款、转账、投资理财和内部划转。
- 退款冲抵支出，已退款原交易不重复计入消费。
- 查看资金来源、资金去向、共同交易主体、月度现金流和支出分类。
- 搜索和筛选交易明细，并手动修改交易分类。
- 数据保存在程序旁边的 `data` 目录，不上传云端。

## 适用环境

- Windows 10 或 Windows 11，64 位系统。
- 建议屏幕分辨率 `1280 × 800` 或更高。
- 程序目录需要有写入权限，建议解压到“文档”“桌面”或其他用户可写目录。
- 操作系统需要安装 Microsoft Edge WebView2 Runtime。

![Image text](https://github.com/EosZeph/SeeFunds/blob/main/see-funds-v1.0.0.png)

## 所需插件与运行环境

### 普通用户

免安装版只需要：

- Microsoft Edge WebView2 Runtime  
  下载地址：<https://developer.microsoft.com/microsoft-edge/webview2/>

Windows 10 和 Windows 11 通常已经预装 WebView2。若程序无法启动，请先安装 WebView2 Evergreen Runtime。

### 从源码构建

需要以下工具：

- Node.js LTS，建议 Node.js `20.19+` 或 `22.12+`  
  下载地址：<https://nodejs.org/>
- Rust 与 Cargo  
  下载地址：<https://rustup.rs/>
- Microsoft Visual Studio 2022 Build Tools，安装“使用 C++ 的桌面开发”工作负载  
  下载地址：<https://visualstudio.microsoft.com/visual-cpp-build-tools/>
- Microsoft Edge WebView2 Runtime  
  下载地址：<https://developer.microsoft.com/microsoft-edge/webview2/>
- PowerShell 5.1 或更高版本

## 免安装版使用方法

1. 解压 `See Funds-v1.0.0-Portable.zip`。
2. 保持 `See Funds.exe`、`README.txt`、`LICENSE.txt` 和 `DISCLAIMER.txt` 在同一个目录。
3. 双击 `See Funds.exe` 启动。
4. 打开“导入账单”，选择微信或银行导出的 CSV/Excel 文件。
5. 导入完成后，在“总览”“资金来源及去向”和“交易明细”中查看结果。
6. 首次启动后会自动创建 `data` 目录，数据库文件为 `data/see_funds.db`。

迁移时复制整个便携版目录即可。不要在程序运行时直接修改或删除数据库文件。

## 支持的账单

微信账单：

- 微信支付官方导出的 CSV 或 Excel 账单。
- 带元数据说明行的原始导出格式。
- 常见字段：交易时间、交易类型、交易对方、商品、收/支、金额、支付方式、当前状态、交易单号、商户单号、备注。

银行账单：

- 支持常见中文表头自动映射。
- 支持金额列、收入金额/支出金额分列、借贷标志等常见格式。
- 各家银行的特殊版式可能需要后续增加专用适配规则。

如果微信导出文件是加密 ZIP，请先在系统中解压并输入密码，再导入解压后的 CSV 或 Excel。

## 开发运行

```powershell
npm install
npm run tauri dev
```

## 构建 v1.0.0

```powershell
npm run portable
```

输出文件：

```text
release/See-Funds-v1.0.0-Portable/
release/See-Funds-v1.0.0-Portable.zip
release/See-Funds-v1.0.0-Portable.zip.sha256
```

## 测试

```powershell
npm run build
Set-Location src-tauri
cargo test
```

样例账单位于 `samples/wechat-sample.csv`。

## 数据与隐私

- 所有账单和数据库默认保存在本机。
- 程序不包含云同步、广告或用户行为上报。
- 备份时请关闭程序，然后复制整个 `data` 目录。
- 请自行保管便携版目录和备份文件。

## 已知限制

- v1.0.0 暂不提供删除单个导入批次的功能，以避免重叠账单导致共享交易被误删。
- 退款目前按统计范围汇总冲抵；跨账单的退款与原支出精确匹配将在后续版本增强。
- 银行格式适配以常见字段为主，特定银行仍需要脱敏样例进行回归测试。
- 收入型转账计入现金流入；支出型转账暂不直接计入消费，等待后续对账规则确认。

## 免责声明

本软件仅用于个人账单整理和资金流辅助分析，统计结果不构成财务、税务、投资或法律建议。详见 [DISCLAIMER.md](DISCLAIMER.md)。

## 许可证

本项目采用 MIT License，详见 [LICENSE](LICENSE)。
