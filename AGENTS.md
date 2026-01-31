# Repository Guidelines

## 项目结构与模块组织
主解决方案在 `ezorsia.sln`，核心源码与资源位于 `ezorsia/`，其中包含 DLL 入口、补丁逻辑、资源脚本与 `MapleClientCollectionTypes/`。`detours/` 提供预编译依赖库。配置文件为 `ezorsia/config.ini`。问题模板位于 `.github/ISSUE_TEMPLATE/`。

## 构建、测试与本地运行
推荐环境：VS 2019、Windows 10 SDK、工具集 v142。使用 VS 打开解决方案，选择 `Release | x86` 构建。生成后 DLL 位于 `out/Release/ijl15.dll`。部署时将客户端原 `ijl15.dll` 重命名为 `2ijl15.dll`，再复制新 DLL 和 `config.ini` 到客户端目录。当前未提供脚本化构建或测试命令。

## 编码风格与命名约定
工程为 C++/Win32，使用预编译头 `stdafx.h`/`stdafx.cpp`。缩进以 Tab 为主，保持文件现有风格。命名上保留现有习惯：类/函数多为 PascalCase，成员变量常用 `m_` 前缀，地址/大小字段常用 `dw`/`n` 前缀。若新增用户可选功能，必须通过 `config.ini` 暴露开关。

## 测试规范
仓库暂无自动化测试框架。改动需在目标客户端内手动验证，尤其是分辨率、输入法与 UI 展示相关功能。新增非分辨率类功能必须默认关闭并可配置关闭。

## 提交与 Pull Request 指南
提交信息既有 Conventional Commits（如 `feat(network): ...`）也有中文简述（如 `新增：...`）。建议保持简短清晰，并可采用 `type(scope): 描述` 或 `新增/修复/优化：描述` 格式。PR 需说明变更动机、配置项与默认值，尽量关联 issue；涉及界面或交互调整请提供截图或对比说明。

## 配置与扩展提示
`config.ini` 是功能开关与参数入口，请避免硬编码可选行为。若发现仅有地址且暂无用途的资料，可按约定以注释形式保留以便后续参考。
