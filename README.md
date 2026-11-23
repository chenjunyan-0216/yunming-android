# 云命 YunMing · 安卓版

<p align="center">
  <img src="www/icons/icon-192.png" width="86" alt="云命图标">
</p>

**报个生辰、一键起卦 · 完全离线 · 单文件 APK(≈340KB) · 不联网、不留数据**

不用联网、不用注册，装上一个 APK 就能用。把生辰或当下来意输进去，选一种你想问的方式，App 立刻给你起一卦、排一张盘，**每句结果都讲人话**——不用懂任何术语，看得懂就能用。

> 非生产级软件；命理内容为传统民俗推演，**仅供娱乐参考，不构成任何决策建议**。

## 能干嘛（挑个顺眼的点开就用）

| 模块 | 一句话说明 |
|---|---|
| **今日** | 打开就是今天：农历、黄道吉日、宜做什么忌做什么、吉利方位，顺手送一卦 |
| **小六壬** | 心里有件事拿不定主意，起一课看个吉凶方向，讲大白话 |
| **六爻** | 手机摇铜钱起卦，看事能不能成、吉凶如何，结果给你说人话的简断 |
| **梅花易数** | 用时间或随便想个数起卦，看这件事的来龙去脉和体用吉凶 |
| **八字四柱** | 报生辰排八字：五行旺衰、喜用神、大运流年，**同盘附送**称骨、八宅命卦、紫微斗数 |
| **合婚** | 两人八字合不合、相配程度打分，只给参考不替你下结论 |
| **黄历** | 任选一天：宜忌、冲煞、吉神方位、二十八宿，出门办事前看一眼 |
| **历史** | 最近 30 次起卦排盘都存在手机里，点开就能翻回去看 |
| **分享** | 任意结果一键生成竖版长图，存相册发给朋友 |

核心引擎源自[云命桌面版](../)(lunar-javascript 交叉验证 + 多命例回归)，本仓库已内置所用引擎源码(`core/`)，构建自包含。

## 怎么装上用

**方式一：直接装 APK** — 下载仓库里的 [`云命.apk`](./云命.apk) 传到安卓手机(7.0+)安装；系统提示「未知来源」时允许即可。应用完全离线，不联网。

**方式二：浏览器即开即用** — `npm run serve` 后手机访问电脑 IP:8730(同局域网)，或把 `www/` 部署到任意静态托管后「添加到主屏幕」。

## 从源码构建 APK

无需 Android Studio / Gradle，一条脚本走通 `javac → d8 → aapt → zipalign → apksigner`：

```bash
npm install                # 安装 esbuild / lunar-javascript / iztro / @resvg/resvg-js
node build/bundle.js       # 打包核心引擎 → www/js/core.bundle.js
node build/icons.js build/icon-src.png   # 由图标源生成 PWA + mipmap 全密度图标
bash build/apk.sh          # 产出 云命.apk(首次运行自动生成签名密钥)
```

`build/apk.sh` 需要本机工具链(约 320MB,`_toolchain/` 目录,已被 .gitignore):

| 组件 | 下载 | 解压后目录 |
|---|---|---|
| JDK 17 | [Adoptium API](https://api.adoptium.net/v3/binary/latest/17/ga/windows/x64/jdk/hotspot/normal/eclipse) | `_toolchain/jdk-17…` |
| Build-Tools 34 | [dl.google.com](https://dl.google.com/android/repository/build-tools_r34-windows.zip) | `_toolchain/android-14/` |
| Platform 34 | [dl.google.com](https://dl.google.com/android/repository/platform-34-ext7_r02.zip) | `_toolchain/android-34/` |

> 也可改走 Android Studio：打开 `android/`，把 `www/` 复制到 `app/src/main/assets/www/` 即可。

## 本地预览 / 开发

```bash
npm run serve              # → http://127.0.0.1:8730,浏览器 F12 切手机视口
```

改了 `core/` 引擎后 `node build/bundle.js` 重新打包；界面在 `www/`，逻辑入口 `www/js/app.js`。

## 目录

```
云命安卓版/
├─ 云命.apk            已签名成品(v1.1)
├─ www/                H5 应用(index.html / css / js / icons / manifest)
├─ core/               术数引擎源码(divination/bazi/huangli/hehun/ziwei/chengu/mingua)
├─ android/            WebView 壳(Manifest / MainActivity / res)
├─ build/              打包脚本(bundle/icons/apk.sh/serve.js)+ 签名密钥(本地生成)
├─ docs/               README 截图
└─ _toolchain/         本地编译工具链(不入库)
```

## 历法口径与测试

- 八字年柱以**立春**为界；紫微晚子时按**换日派**与八字口径一致；称骨按农历年计
- 六爻引擎经八宫六十四卦逐卦回归(卦名/宫位/世应/纳甲)，合婚、称骨、八宅与桌面版同源引擎
- 桌面版全量测试 32 项通过

## 作者

**陈钧炎** · GitHub [@chenjunyan-0216](https://github.com/chenjunyan-0216)

## License

[MIT](./LICENSE) © 陈钧炎 (chenjunyan-0216)