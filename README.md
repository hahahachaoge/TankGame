
# 🎮 坦克大战 — Unity 3D 坦克对战模拟游戏

<div align="center">

![Unity Version](https://img.shields.io/badge/Unity-2022.3.62f3c1-blueviolet?logo=unity)
![C#](https://img.shields.io/badge/C%23-9.0-green?logo=csharp)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Android%20%7C%20iOS-lightgrey)
![License](https://img.shields.io/badge/License-MIT-orange)

**一个基于 Unity 3D 引擎、Kawaii Tanks 资源包构建的完整坦克对战模拟游戏**

</div>

---

## 📋 目录

- [项目简介](#-项目简介)
- [开发环境](#-开发环境)
- [快速开始](#-快速开始)
- [游戏操作指南](#-游戏操作指南)
- [核心架构](#-核心架构)
- [功能特性](#-功能特性)
- [模块详解](#-模块详解)
- [项目结构](#-项目结构)
- [开发日志](#-开发日志)
- [未来计划](#-未来计划)
- [许可证](#-许可证)

---

## 🎯 项目简介

本作品是一款基于 **Unity 3D** 引擎开发的坦克对战模拟游戏，综合利用了 **3ds Max** 三维建模、**Unity PhysX** 物理引擎、**Unity Audio** 音频系统与 **UGUI** 交互界面等多种技术，构建了一个具备完整驾驶、瞄准、射击、损伤反馈与视觉特效的坦克战斗系统。

项目采用 **组件式架构**，将坦克划分为驾驶系统、武器系统、炮塔瞄准系统、损伤系统、摄像机系统、音效系统、履带视觉系统等独立模块，通过 Unity 的消息机制与组件引用实现模块间低耦合通信。同时集成了 **UOS（Unity Online Service）** AES 加密保护，并支持 **Windows / Android / iOS** 多平台构建。

> **开发者**：黄彪骐 · 学号：202440025318

---

## 💻 开发环境

| 工具 | 版本 / 说明 |
|------|------------|
| **Unity 引擎** | 2022.3.62f3c1 (LTS) |
| **C# 语言** | 9.0 + .NET Standard 2.1 |
| **3ds Max** | FBX 格式模型导出 |
| **音效处理** | OGG Vorbis 格式（引擎声、开火声、爆炸声、命中声） |
| **贴图格式** | PNG（PBR 材质：Base Color / AO / Normal Bump） |
| **版本控制** | Git + GitHub |
| **IDE** | Visual Studio 2022 / VS Code |

---

## 🚀 快速开始

### 方法一：直接使用项目文件夹（推荐）

如果你已 clone 整个项目仓库：

```bash
git clone https://github.com/your-username/TankGame.git
cd TankGame
```

然后用 **Unity Hub** 打开：
1. 启动 Unity Hub
2. 点击 **"添加" → "从磁盘添加项目"**
3. 选择 `TankGame` 文件夹
4. 确保已安装 **Unity 2022.3.62f3c1** 或兼容版本
5. 在 `Project` 面板中打开 `Assets/Scenes/Tank_battle.unity`，点击 **Play** 运行

### 方法二：Assets 拷贝方式（轻量快速）

如果你只想运行游戏，不想保留整个工程文件：

1. **创建新项目**
   - 启动 Unity Hub
   - 点击 **"新建项目"**
   - 选择 **3D（Core）** 模板
   - 填写项目名称和路径，点击 **创建**

2. **拷贝 Assets**
   - 找到本项目的 `Assets` 文件夹（全部）
   - **完全覆盖** 替换到新项目的 `Assets` 文件夹中

3. **加载场景**
   - 在 Unity 编辑器中，打开 `Project` 面板
   - 导航到 `Assets/Scenes/` 目录
   - 将 **Tank_battle.unity** 拖拽到 **Hierarchy（层级面板）** 中

4. **删除默认场景**
   - 在 Hierarchy 面板中找到 `SampleScene`
   - 右键点击 → **Remove（删除）**
   - 此时场景中仅保留 Tank_battle 的内容

5. **运行游戏**
   - 点击 Unity 编辑器顶部的 **▶ Play** 按钮
   - 即可开始坦克对战！

### 附加场景

| 场景 | 路径 |
|------|------|
| 🏘️ 城镇场景 | `Assets/Kawaii_Tanks_Project/Kawaii_Tanks_Assets/Scenes/Town.unity` |
| 📦 示例场景 | `Assets/Standard Assets/Scenes/SampleScene.unity` |

---

## 🎮 游戏操作指南

### 桌面端操作（Windows）

| 按键 | 功能 |
|------|------|
| **W / ↑** | 加速前进 |
| **S / ↓** | 减速后退 |
| **A / D** | 左右转向 |
| **X** | 急停（速度归零） |
| **鼠标左键** | 开火 |
| **空格键（按住）** | 进入瞄准模式（自动锁定目标） |
| **鼠标右键（按住+拖拽）** | 旋转摄像机视角 |
| **鼠标滚轮** | 摄像机缩放（3m ~ 20m） |
| **Tab** | 切换操作坦克 |
| **P** | 暂停 / 继续 |
| **Backspace** | 重新加载场景 |
| **Enter** | 自毁（当前坦克） |
| **Esc** | 退出游戏 |

### 瞄准系统详解

1. **自由瞄准**：鼠标悬停时，炮塔自动指向鼠标位置
2. **精确瞄准**：**按住空格键** → 炮塔锁定目标 → 锁定时显示**红色 Marker** 标记
   - 锁定时右击拖拽可微调瞄准偏移量
   - 未锁定时显示**白色 Marker**
3. **炮镜视角**：瞄准模式下，当偏差角很小时自动切换到**炮管视角**，屏幕显示**十字准星**
4. **自动追踪**：锁定目标后，炮塔自动跟踪移动目标，火炮自动计算仰角

### 移动端操作（Android / iOS）

| 操作 | 功能 |
|------|------|
| 虚拟按钮 Up/Down | 加速 / 减速 |
| 虚拟按钮 Left/Right | 转向 |
| 触屏拖拽（非瞄准时） | 旋转摄像机 |
| GunCam 按钮 | 开火 + 进入瞄准模式 |
| 双指拖拽（瞄准模式） | 缩放 / 调整瞄准 |

---

## 🏗️ 核心架构

### 整体架构图

```
Game_Controller_CS（全局游戏控制器）
    │
    ▼ 管理坦克列表
ID_Control_CS（坦克身份标识 / 玩家输入管理）
    │
    ▼ BroadcastMessage / 组件引用
    ├── 🚗 Wheel_Control_CS（驾驶系统）
    │       ├── Wheel_Rotate_CS（驱动轮旋转物理）
    │       ├── Wheel_Sync_CS（从动轮同步旋转）
    │       ├── Track_Scroll_CS（履带纹理滚动动画）
    │       └── Track_Deform_CS（履带网格顶点变形）
    │
    ├── 🔫 Fire_Control_CS（射击系统）
    │       ├── Barrel_Control_CS（炮管后坐力动画）
    │       └── Fire_Spawn_CS（子弹生成 + 枪口火焰）
    │               └── Bullet_Nav_CS（子弹飞行物理 + 伤害计算）
    │
    ├── 🎯 Turret_Control_CS（炮塔瞄准系统）
    │       └── Cannon_Control_CS（火炮仰角计算 + 俯仰控制）
    │
    ├── 💥 Damage_Control_CS（损伤系统）
    │       └── Damage_Display_CS（血量 UI 显示 + 淡出效果）
    │
    ├── 📷 摄像机系统
    │       ├── Camera_Rotate_CS（摄像机环绕旋转）
    │       ├── Camera_Zoom_CS（摄像机缩放 + 自动避障）
    │       └── GunCamera_Control_CS（炮镜视角 + 准星）
    │
    ├── 🔊 SE_Control_CS（引擎音效控制）
    │
    └── 🧱 Break_Object_CS（场景物体破坏逻辑）
```

### 设计模式

- **组件模式**：每个坦克功能拆分为独立 MonoBehaviour 组件
- **广播通信**：使用 `BroadcastMessage("Get_ID_Script", ...)` 实现引用传递
- **桥接模式**：`ID_Control_CS` 作为坦克的"身份中心"，协调各子系统通信
- **策略模式**：通过 `#if UNITY_ANDROID` 条件编译实现跨平台输入策略切换

### 伤害计算流程

```
子弹命中
    │
    ▼ 计算命中角度
命中能量 = attackForce × lerp(0, 1, sqrt(命中角 / 90°))
    │
    ▼ 护甲倍率修正
    ├── 无 Armor_Collider → 倍率 = 1.0
    └── 有 Armor_Collider → 倍率 = damageMultiplier（如 0.5 = 正面装甲减半）
    │
    ▼ 扣除耐久度
Damage_Control_CS.Get_Damage()
    │
    ├── durability > 0 → 更新血量显示
    └── durability ≤ 0 → 触发销毁流程
            ├── BroadcastMessage("Destroy") → 各部件独立销毁
            ├── 生成爆炸特效预制体
            ├── 炮塔被物理击飞（AddForce）
            └── AI 坦克 → SetActive(false)
                  玩家坦克 → 完整销毁 + 残骸
```

---

## ✨ 功能特性

### 🚗 1. 真实坦克物理驾驶

- **双履带差速转向** — 左右履带独立扭矩控制，模拟真实的刹车转向效果
- **自动驻车制动** — 静止时自动锁定位置，防止滑坡
- **惯性滑行** — 基于刚体物理的加减速与转向惯性
- **车身层级管理** — 车轮、悬挂、车体使用独立物理层级，碰撞精准

```csharp
// 差速转向核心（Wheel_Control_CS）
leftRate = Mathf.Clamp(-vertical - horizontal, -1.0f, 1.0f);
rightRate = Mathf.Clamp(vertical - horizontal, -1.0f, 1.0f);
```

### 🎯 2. 高精度瞄准系统

- **SphereCast 射线球体检测** — 精确锁定任何带有 Rigidbody 的目标
- **自动追踪** — 锁定后炮塔自动跟踪，火炮根据弹道计算仰角
- **手动微调** — 右键拖拽微调瞄准偏移
- **双视角切换** — 第三人称 ↔ 炮镜第一人称，带十字准星 UI

### 🔫 3. 完整武器系统

- **装填冷却** — 射击后自动进入 reload 状态
- **炮管后坐力动画** — 使用正弦插值模拟炮管回退与复位
- **枪口火焰特效** — 每次开火生成粒子特效
- **AI 自动开火** — 非玩家坦克每 3 秒自动攻击
- **后坐力反馈** — 开火时对车体施加反方向冲量

### 💥 4. 损伤与反馈系统

- **实时血量显示** — 屏幕跟随的数值血条，带透明度淡出效果
- **护甲系统** — 不同装甲部位可设定独立伤害倍率
- **爆炸特效** — 坦克摧毁时生成 Destroyed_Effect 预制体
- **炮塔物理飞脱** — 被摧毁时炮塔被物理力击飞
- **AI 隐身** — AI 坦克被摧毁时隐藏而非销毁（方便后续复用）

### 📷 5. 多模式摄像机

| 模式 | 说明 |
|------|------|
| 第三人称跟随 | 默认视角，随坦克移动 |
| 缩放控制 | 鼠标滚轮 ±30，范围 3m ~ 20m |
| 自动避障 | 摄像机与障碍物间有碰撞时自动推近 |
| 自由环绕 | 右键拖拽旋转观察 |
| 炮镜视角 | 切换至炮管第一人称视角 + 准星瞄准 |

### 🎨 6. 视觉细节

- **履带纹理滚动** — 根据车轮转速驱动的 UV 滚动动画
- **履带网格变形** — 根据路轮位置动态修改网格顶点
- **从动轮同步** — 非驱动轮按半径比自动适配转速
- **场景物体可破坏** — 房屋（有 LOD）、树篱、树木均可被炮弹摧毁
- **枪口火焰** — 开火时的 muzzle fire 粒子特效

### 🔊 7. 音效系统（OGG）

| 音效 | 文件名 | 触发机制 |
|------|--------|---------|
| 🔧 引擎声 | SE_Engine.ogg | 持续循环，pitch/volume 随速度线性变化 |
| 💥 开火声 | SE_Fire.ogg | 每次开火触发 |
| 🛡️ 命中声 | SE_Hit.ogg | 子弹命中物体 |
| 💢 爆炸声 | SE_Explosion.ogg | 坦克被摧毁 |

### 🌐 8. 跨平台支持

- **桌面端**：完整键盘 + 鼠标操控（`#if !UNITY_ANDROID`）
- **移动端**：触屏虚拟摇杆 + 按钮（`#if UNITY_ANDROID || UNITY_IPHONE`）
- **自适应分辨率**：移动端自动限制最大分辨率 720p
- **CrossPlatformInput**：使用 Unity Standard Assets 跨平台输入系统

### 🔒 9. 资源加密（UOS）

使用 **AES-128** 加密算法保护游戏资源：
- 密钥派生：PBKDF2（1000 次迭代 + 盐值）
- 加密模式：AES-CBC（零 IV）
- 集成 Unity Online Service 启动器

---

## 🔧 模块详解

### 驾驶系统（Wheel_Control_CS + Wheel_Rotate_CS）

| 组件 | 功能 |
|------|------|
| `Wheel_Control_CS` | 附在 MainBody 上，接收输入计算左右履带转速比（leftRate/rightRate），管理自动驻车制动 |
| `Wheel_Rotate_CS` | 附在每个驱动轮上，根据 leftRate/rightRate 施加扭矩，限制最大角速度，稳定车轮角度 |
| `Wheel_Sync_CS` | 附在从动轮上，根据参考轮旋转角度和半径比同步旋转 |
| `Track_Scroll_CS` | 附在履带上，根据参考轮旋转差值偏移纹理 UV |
| `Track_Deform_CS` | 附在履带上，根据路轮位置实时修改网格顶点实现变形效果 |

### 武器系统（Fire_Control_CS → Barrel_Control_CS + Fire_Spawn_CS）

```
Fire_Control_CS（射击控制器）
    │ 接收输入、管理装填 CD、施加后坐力
    │
    ├──→ Barrel_Control_CS.Fire() → 启动 Recoil_Brake 协程
    │    （正弦插值：后坐 0.05s + 回位 0.05s，行程 0.3m）
    │
    └──→ Fire_Spawn_CS.Fire() → 协程
         ├── 实例化 MuzzleFire 预制体
         └── 实例化 Bullet 预制体 → 设置 attackForce → 等待 FixedUpdate → 施加初速度
```

### 炮塔瞄准系统（Turret_Control_CS + Cannon_Control_CS）

1. `SphereCastAll` 从鼠标位置发射射线球体检测
2. 找到目标后锁定其 Transform，每帧更新目标位置
3. 将目标位置转换到炮塔局部坐标系
4. 计算目标偏转角 → 使用 `MoveTowardsAngle` 平滑旋转
5. `Cannon_Control_CS` 根据目标距离和高度差计算仰角
6. 仰角限制：最大抬头 15°，最大低头 10°

### 子弹物理（Bullet_Nav_CS）

- **双检测机制**：射线预测 + 碰撞回调双保险
- **自碰撞忽略**：通过 LayerMask 排除自身层级
- **伤害计算**：基于命中角度线性插值 + 部位护甲倍率

---

## 📂 项目结构

```
TankGame/
├── Assets/
│   ├── Scenes/
│   │   └── Tank_battle.unity              # 🎮 主战斗场景
│   │
│   ├── Kawaii_Tanks_Project/
│   │   ├── Kawaii_Tanks_Assets/
│   │   │   ├── Scripts/                    # 📜 全部 C# 脚本（21个）
│   │   │   │   ├── Game_Controller_CS.cs   # 全局游戏控制器
│   │   │   │   ├── ID_Control_CS.cs        # 坦克身份与输入管理
│   │   │   │   ├── Wheel_Control_CS.cs     # 驾驶系统
│   │   │   │   ├── Wheel_Rotate_CS.cs      # 车轮物理旋转
│   │   │   │   ├── Wheel_Sync_CS.cs        # 从动轮同步
│   │   │   │   ├── Track_Scroll_CS.cs      # 履带纹理滚动
│   │   │   │   ├── Track_Deform_CS.cs      # 履带顶点变形
│   │   │   │   ├── Fire_Control_CS.cs      # 射击控制器
│   │   │   │   ├── Fire_Spawn_CS.cs        # 子弹生成
│   │   │   │   ├── Barrel_Control_CS.cs    # 炮管后坐力
│   │   │   │   ├── Bullet_Nav_CS.cs        # 子弹飞行物理
│   │   │   │   ├── Turret_Control_CS.cs    # 炮塔瞄准
│   │   │   │   ├── Cannon_Control_CS.cs    # 火炮仰角
│   │   │   │   ├── Damage_Control_CS.cs    # 损伤系统
│   │   │   │   ├── Damage_Display_CS.cs    # 血量 UI
│   │   │   │   ├── Camera_Rotate_CS.cs     # 摄像机旋转
│   │   │   │   ├── Camera_Zoom_CS.cs       # 摄像机缩放
│   │   │   │   ├── GunCamera_Control_CS.cs # 炮镜摄像机
│   │   │   │   ├── SE_Control_CS.cs        # 引擎音效
│   │   │   │   ├── Break_Object_CS.cs      # 物体破坏
│   │   │   │   ├── Armor_Collider_CS.cs    # 护甲碰撞体
│   │   │   │   ├── PlaceTarget.cs          # NavMesh AI 寻路
│   │   │   │   ├── Delete_Timer_CS.cs      # 延时销毁
│   │   │   │   ├── Tutorial_Text_CS.cs     # 移动端教程
│   │   │   │   └── Unity_51_Patch_CS.cs    # Unity 5.1 兼容补丁
│   │   │   │
│   │   │   ├── Prefabs/                    # 🧩 预制体
│   │   │   │   ├── SD_Firefly_1.1.prefab   # 萤火虫式坦克
│   │   │   │   ├── SD_Tiger-I_1.1.prefab   # 虎式坦克
│   │   │   │   ├── Bullet_and_Effects/     # 子弹与特效
│   │   │   │   ├── Ground_Tile/            # 地形瓦片
│   │   │   │   ├── Props/                  # 场景道具
│   │   │   │   └── Scene_Components/       # 场景组件
│   │   │   │
│   │   │   ├── Meshes/                     # 🏗️ 3ds Max 模型 (FBX)
│   │   │   │   ├── SD_Firefly/             # 萤火虫坦克
│   │   │   │   ├── SD_Tiger-I/             # 虎式坦克
│   │   │   │   ├── Bullet/                 # 子弹模型
│   │   │   │   └── Props/                  # 场景物体
│   │   │   │
│   │   │   └── Others/                     # 🎵 音效与贴图
│   │   │       ├── SE_Engine.ogg           # 引擎声
│   │   │       ├── SE_Explosion.ogg        # 爆炸声
│   │   │       ├── SE_Fire.ogg             # 开火声
│   │   │       ├── SE_Hit.ogg              # 命中声
│   │   │       └── *.png                   # UI 贴图
│   │   │
│   │   └── Scenes/
│   │       └── Town.unity                  # 🏘️ 城镇场景
│   │
│   ├── UOSLauncherEncrypt/                 # 🔒 UOS 加密模块
│   │   ├── EncryptManager.cs               # AES 加密/解密逻辑
│   │   ├── EncryptKey.cs                   # 加密密钥
│   │   └── Unity.UOS.Encrypt.asmdef        # 程序集定义
│   │
│   └── Standard Assets/                    # 📦 Unity 标准资源
│       ├── CrossPlatformInput/             # 跨平台输入系统
│       └── Scenes/
│           └── SampleScene.unity
│
├── ProjectSettings/                        # ⚙️ Unity 项目设置
├── TankGame.sln                            # Visual Studio 解决方案
└── README.md                               # 📖 本文件
```

---

## 📝 开发日志

### 阶段一：项目初始化与场景搭建

- 导入 Kawaii Tanks 资源包，搭建基础场景
- 配置 Unity 物理层级（Layer 9=车轮, Layer 10=悬挂, Layer 11=车体）
- 导入 3ds Max 模型

### 阶段二：坦克驾驶系统

- 实现 Wheel_Control_CS 双履带差速转向
- 实现 Wheel_Rotate_CS 驱动轮物理旋转
- 实现自动驻车制动（基于 RigidbodyConstraints）
- 实现 Track_Scroll_CS 履带滚动动画
- 实现 Track_Deform_CS 履带顶点变形
- 实现 Wheel_Sync_CS 从动轮同步

### 阶段三：炮塔与瞄准系统

- 实现 Turret_Control_CS SphereCast 目标锁定
- 实现 Cannon_Control_CS 火炮仰角计算
- 实现瞄准 Marker 与 UI 指示
- 实现双视角切换（第三人称 ↔ 炮镜）

### 阶段四：武器与伤害系统

- 实现 Fire_Control_CS 射击控制器（含装填 CD）
- 实现 Barrel_Control_CS 后坐力动画
- 实现 Fire_Spawn_CS 子弹与火焰生成
- 实现 Bullet_Nav_CS 子弹飞行物理
- 实现 Damage_Control_CS 损伤管理
- 实现 Damage_Display_CS 血量 UI

### 阶段五：摄像机系统

- 实现 Camera_Zoom_CS 缩放与自动避障
- 实现 Camera_Rotate_CS 自由环绕旋转
- 实现 GunCamera_Control_CS 炮镜视角

### 阶段六：音效与特效

- 集成引擎音效 SE_Control_CS
- 集成开火 / 命中 / 爆炸音效
- 集成 MuzzleFire / Destroyed_Effect 粒子特效

### 阶段七：跨平台与 AI

- 集成 CrossPlatformInput 跨平台输入
- AI 坦克自动开火逻辑
- NavMesh 寻路（PlaceTarget）

### 阶段八：加密与优化

- UOS AES 加密模块集成
- 移动端分辨率自适应
- 各模块代码注释与文档撰写

---

## 🔮 未来计划

- [ ] **联网对战** — 基于 Unity Netcode / Photon 实现多人联机
- [ ] **更多坦克种类** — 增加不同属性的坦克（重坦、轻坦、自行火炮）
- [ ] **关卡编辑器** — 让玩家自定义地图布局
- [ ] **成就系统** — 击杀计数、解锁成就
- [ ] **更丰富的 AI** — 寻路攻击、撤退、包抄等行为树
- [ ] **弹道系统** — 加入抛物线弹道与下坠
- [ ] **动态破坏** — 场景物体的物理破碎效果
- [ ] **UI 美化** — 主菜单、设置界面、载入界面
- [ ] **回放系统** — 记录并回放对局

---

## 📄 许可证

本项目基于 MIT 许可证开源 — 详见 [LICENSE](LICENSE) 文件。

---

## 🙏 致谢

- **Kawaii Tanks** — 精美的坦克模型与资源包
- **Unity Technologies** — 强大的游戏引擎与标准资源
- **3ds Max** — 专业的三维建模工具

---

<div align="center">

**Made with ❤️ by 黄彪骐 · 202440025318**

⭐ 如果这个项目对你有帮助，欢迎 star！

</div>
