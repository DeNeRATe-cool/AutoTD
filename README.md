> [!IMPORTANT]
> 北航 TD 官方截止时间一般是 14 周周日
> 
> 但每学期均会延长一周（15 周周日）
> 
> 需要打卡的同学注意打卡时间，默认一天打卡三次（每学期要求共 32 次）

📡 **产品集**

> **[AutoTD](https://github.com/DeNeRATe-cool/autoTD)**: BUAA TD PyPI 实现 TD 自由
> 
> **[AutoBoya](https://github.com/DeNeRATe-cool/AutoBoya)**: 北航博雅课程命令行工具，支持后台运行、自动选课、签到与签退，实现博雅自由
>
> **[AutoSign](https://github.com/DeNeRATe-cool/AutoSign)**: 北航 BUAA iClass 多账号自动签到 CLI（开机自启、自动签到、多账号配置、跨平台支持、免费全天托管服务）

# AutoTD

[![PyPI](https://img.shields.io/pypi/v/autotd-buaa)](https://pypi.org/project/autotd-buaa/)
[![Python](https://img.shields.io/pypi/pyversions/autotd-buaa)](https://pypi.org/project/autotd-buaa/)

`autoTD` 是一个用于 BUAA TD 打卡流程管理与执行的 Python CLI 工具。

> [!NOTE]
> 仅支持**校园网**直连环境，不支持 VPN。

## Quickstart

```bash
# 1) 安装 PyPI 包
pip install autotd-buaa

# 2) 初始化本地配置目录（默认 ~/.autoTD）
autotd init
```

## CLI 端

```
# 3) 准备至少一张打卡图片并导入
autotd image add ~/images/image1.jpg

# 4) 添加用户（quick 模式自动填充学院路机位组合）
autotd user add 2xxxxxxx --quick 学院路

# 5) 启动打卡流程
#    - autotd run       : 后台持续运行
#    - autotd run --once: 前台仅执行一轮
autotd run [--once]
```

**状态与 TD 次数查询**

```bash
# 查看当前后台运行状态与今日执行进度
autotd status

# 查看某个学号当前缓存的 TD 次数（不访问服务器）
autotd user count 2xxxxxxx

# 实时查询服务器并刷新本地 TD 次数缓存
autotd user count 2xxxxxxx --refresh
```

## Web 端

```bash
autotd ui
```

`autotd ui` 会打开本地 Web 管理端，可查看用户列表、今日打卡进度、TD 数和后台 PID，支持 quick 新增/删除用户、运行或停止后台进程、今日打卡，以及上传、预览和删除图片。

<img src="https://files.seeusercontent.com/2026/05/27/u5bO/pasted-image-1779896740022.webp" alt="pasted-image-1779896740022.webp" title="pasted-image-1779896740022.webp">

## PATH（Windows / macOS / Linux）

若安装后提示 `... is not on PATH` 且 `autotd` 不可用，可先用：

```bash
python -m auto_td.cli init
```

再按系统把用户脚本目录加入 PATH（执行后重开终端）：

```powershell
# Windows (PowerShell)
$d = py -c "import sysconfig; print(sysconfig.get_path('scripts','nt_user'))"; [Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path","User") + ";" + $d, "User")
```

```bash
# macOS (zsh)
echo 'export PATH="$(python3 -m site --user-base)/bin:$PATH"' >> ~/.zprofile && source ~/.zprofile
```

```bash
# Linux (bash)
echo 'export PATH="$(python3 -m site --user-base)/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

验证：

```bash
autotd --help
```
