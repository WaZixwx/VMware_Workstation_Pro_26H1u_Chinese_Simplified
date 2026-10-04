# VMware Workstation Pro 26H1u1 简体中文语言包

为 **VMware® Workstation Pro 26H1u1 (26.0.1.25688693)** 制作的社区简体中文语言包。

官方从 25H2 版本起移除了内置简体中文支持，本语言包基于官方遗留的西班牙语语言包（ES）**从零翻译**而来，让新版 VMware Workstation 重新拥有完整的中文界面。

---

## ✨ 特性

- ✅ **菜单栏**：文件、编辑、查看、虚拟机、帮助等全部菜单中文化
- ✅ **对话框**：48 个 Dialog（设置、向导、错误提示等）全部翻译
- ✅ **托盘菜单**：USB、快照、消息、下载等状态栏图标右键菜单
- ✅ **动态文本**：`vmware.vmsg` 中 686KB 的状态提示、错误信息、任务进度全部翻译
- ✅ **String Table**：底层字符串表全部翻译
- ✅ **排版优化**：针对中文长度调整了控件宽度和高度，避免文字截断
- ✅ **术语统一**：使用 VMware 官方中文术语（虚拟机、快照、克隆、数据存储等）

**汉化覆盖率约 99%**，仅极少数硬编码在主程序中的英文字符串无法翻译（详见"已知问题"）。

---

## 📦 安装方法

### 1. 备份原文件

进入你的 VMware Workstation 安装目录下的语言包文件夹：

```
<安装目录>\messages\zh_CN\
```

> 默认路径通常是 `C:\Program Files\VMware\VMware Workstation\messages\zh_CN\`。
> 如果 `zh_CN` 文件夹不存在，请手动创建。

**在替换前，请务必备份原有的 3 个文件**（如果存在）：

- `vmui_zh_CN.dll`
- `vmappsdk_zh_CN.dll`
- `vmware.vmsg`

### 2. 复制语言包文件

将本仓库中的 3 个文件复制到 `messages\zh_CN\` 目录：

| 文件 | 说明 | 大小参考 |
| :--- | :--- | :--- |
| `vmui_zh_CN.dll` | 主界面资源（菜单、对话框） | ~170 KB |
| `vmappsdk_zh_CN.dll` | 底层 SDK 资源（向导、属性页） | ~13 MB |
| `vmware.vmsg` | 动态文本资源（提示、错误、进度） | ~600 KB |

### 3. 设置语言

有两种方式让 VMware 加载中文：

**方式 A：修改 `preferences.ini`（推荐）**

打开文件：`%APPDATA%\VMware\preferences.ini`

在文件末尾添加一行：

```ini
pref.locale = "zh_CN"
```

**方式 B：修改快捷方式**

右键 VMware Workstation 桌面快捷方式 → 属性 → 在"目标"栏末尾添加：

```
 --locale zh_CN
```

（注意：`--locale` 前面有一个空格）

### 4. 重启 VMware

完全关闭 VMware Workstation（包括托盘图标），重新启动即可看到中文界面。
有时候不用杀死进程，只用关闭 UI 界面重新打开也可以（我这里可以），似乎语言是支持热更新的

---

## ⚠️ 已知问题

### 1. 个别字符串仍为英文

由于部分字符串**硬编码在主程序 `vmware.exe` 或底层 DLL 中**，不在语言包覆盖范围内，无法通过替换语言包翻译。已知的例子：

- 新建虚拟机向导"典型"页的描述文字：`Workstation 25H2 or later`

这是所有第三方语言包的共同限制，包括官方本地化团队也需要修改 C++ 源码才能处理。

### 2. 极少数界面可能存在排版微调

翻译时已尽量调整控件尺寸避免中文截断，但由于无法实际运行所有界面进行测试，可能仍有个别地方存在排版问题。欢迎提交 Issue 反馈。

### 3. 版本匹配

本语言包**仅适用于 VMware Workstation Pro 26H1u1 (26.0.1.25688693)**。

其他版本可能因资源 ID 不匹配而出现菜单错乱、功能缺失等问题，请勿混用。

---

## 🔧 制作方法

本语言包采用"资源级汉化"方案，不修改任何程序代码，仅替换 `.rsrc` 段中的资源数据。

### 流程

1. 从官方安装包中解压提取西班牙语语言包（`vmui_es.dll`、`vmappsdk_es.dll`、`vmware.vmsg_es`）
2. 将西班牙语文件重命名为简体中文对应文件名（`vmui_zh_CN.dll`、`vmappsdk_zh_CN.dll`、`vmware.vmsg`）
3. 使用 **Resource Hacker** 逐条翻译以下资源（共 14 个 Menu、48 个 Dialog、1 个 String Table）：
   - `vmui_zh_CN.dll`：**4 个 Menu** + 10 个 Dialog
   - `vmappsdk_zh_CN.dll`：**10 个 Menu** + 38 个 Dialog + String Table
4. 使用 **VS Code** 手动翻译 `vmware.vmsg` 中 686KB 的动态文本
5. 针对中文长度逐一调整控件宽度和高度，避免文字截断
6. 编译保存，替换回 `messages\zh_CN\` 目录

### 使用的工具

- [Resource Hacker](http://www.angusj.com/resourcehacker/) — 资源编辑
- [VS Code](https://code.visualstudio.com/) — 文本编辑
- [7-Zip](https://www.7-zip.org/) — 解压官方安装包

### 为什么选择资源级汉化？

- **不修改程序逻辑**：只动 `.rsrc` 段，不碰 `.text` 段，不会破坏功能
- **可逆**：备份原文件即可完全恢复
- **无需源码**：官方没有开放源码，资源级汉化是唯一可行的方案

---

## 📜 许可

- 本语言包仅供**学习交流**使用，请勿用于商业用途
- VMware Workstation 版权归 **Broadcom Inc.** 所有
- 本仓库中的翻译文本（`.vmsg` 文件和 `.rc` 脚本）以 **MIT License** 授权

---

## 🐛 反馈

如果发现遗漏的西班牙语、英文残留，或者中文排版问题，请提交 Issue 并附上：

- 截图
- 触发路径（如：文件 → 新建虚拟机 → 下一步）
- VMware 版本号

---

**如果这个语言包对你有帮助，欢迎 Star ⭐ 支持！**
