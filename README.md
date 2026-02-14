<!--
 * @Description: 
 * @version: 
 * @Author: ShowE
 * @Date: 2026-02-07 10:38:12
 * @LastEditors: ShowE
 * @LastEditTime: 2026-02-07 10:41:34
-->
# ReadSAI2：从首次提交到当前版本的改进与新功能（对比摘要）

对比范围  
- 初始提交：`5ad2195`（Init）  
- 最新提交：`ef82048`（窗口拖拽、toast 定义动画、在线更新、依赖精简）  
- 变化规模：124 个文件变更，约 +8668 / -2521 行  

---

## 1) 在线更新与发布流程（新增一整套）
- **新增在线更新核心**：`UpdateManager.cs`（基于 `manifest.json` 的增量文件更新、自更新流程）。
- **更新包构建脚本**：`scripts/pack_updates.ps1`、`scripts/generate_version.ps1`、`scripts/pack_version.cache`。
- **更新入口与页面**：`updates/index.html`、`updates/icons.svg`、`updates/preferences-color.ico`。
- **运行期配置扩展**：`ReadConfig.cs` / `config.xml` 增加 `UpdateChannel`。

## 2) 录制格式与导出管线（大幅增强）
- **录制容器与分段系统**：`RecordingContainer*.cs`、`RecordingSegmenter.cs`、`RecordingSessionWriter.cs`、`RecordingContainerReader.cs`。
- **导出逻辑**：`RrecToVideoExporter.cs`。
- **录制预览窗口**：`RecsaiPreviewForm.*`。

## 3) Windows 集成能力增强
- **Explorer 缩略图支持**：新增 `ReadSAI2.ThumbnailProvider` 子项目（`.recsai` 缩略图）。
- **文件关联 / 托盘恢复 / 单实例逻辑**：`Program.cs`、`ReadSAI2MainForm.cs` 持续扩展。

## 4) UI/UX 动画体系升级
- **统一动画系统**：`Animations.cs`、`AnimationDefinitions.cs`、`Resources/animations.json`。
- **侧边面板、DPI 适配与 UI 细节优化**：`ReadSAI2MainForm.cs`、`MuxForm.cs`。
- **自定义 Toast**：`TrayToast.cs`（淡入淡出、物理跟随）。

## 5) 窗体拖拽行为升级
- **新增物理拖拽**：`WinUtils/WindowDragPhysics.cs`。

## 6) 日志与诊断能力增强
- **诊断日志系统**：`DiagnosticLogger.cs`。
- **诊断包导出**：UI 集成导出入口。

## 7) 录制与内存读取逻辑迭代
- **核心读取适配更新**：`SAI2MemoryBridge.cs`、`Sai2Info.cs`、`BlackMemoryLib.cs`。
- **异步任务队列**：`TaskQueue.cs`。

## 8) 依赖与资源变化
- **新增依赖**：`DLLs/TransTextbox.dll`，保留 `Microsoft.WindowsAPICodePack.*`。
- **资源新增/替换**：`Resources/twi.png`、更新的 `ffmpeg.exe`。
- **工程清理**：`.gitignore` 更新，移除 `.vs/` 与 `obj/` 等构建产物。

## 9) 工程与运行环境改进
- **新增 `app.manifest`**：启用管理员权限、PerMonitorV2 DPI、长路径支持。
- **运行配置完善**：`app.config` / `ReadSAI2.csproj` 适配 DPI 与发布参数。

## 关键新增文件清单（按功能）
| 功能域 | 关键新增文件 |
| --- | --- |
| 在线更新 | `UpdateManager.cs`, `updates/*`, `scripts/pack_updates.ps1` |
| 录制容器 | `RecordingContainer*.cs`, `RecordingSegmenter.cs`, `RecordingSessionWriter.cs` |
| 录制预览 | `RecsaiPreviewForm.*` |
| 导出视频 | `RrecToVideoExporter.cs` |
| 动画系统 | `Animations.cs`, `AnimationDefinitions.cs`, `Resources/animations.json` |
| Toast | `TrayToast.cs` |
| 物理拖拽 | `WinUtils/WindowDragPhysics.cs` |
| 日志诊断 | `DiagnosticLogger.cs` |
| 缩略图扩展 | `ReadSAI2.ThumbnailProvider/*` |
