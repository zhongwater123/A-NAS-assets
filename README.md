# A-NAS-assets

A-NAS 开发用的大文件：模型与测试素材。文件只存为 Release 附件，不进 Git。仓库开启了不可变 Release：发布后不修改、不替换，换文件就发新的 Release。超过 2 GiB（GitHub 单个附件的上限）的文件切成 `<文件名>.part-NN` 上传，按序号拼接。

## 模型

- 一个文件一个 Release，标签是 `sha256-<文件的 SHA-256>`，说明里是 A-NAS 仓库中固定它的清单（`deploy/models/*.json`）。
- 拉取与发布用 A-NAS 仓库的 `scripts/fetch-models.sh`，说明见 `docs/development/ai-development.md#拉取模型`。

## 测试素材

- 每套素材一个 Release，标签是素材名加版本（如 `videos-dji-v1`），附列出每个完整文件的 `SHA256SUMS`。
- 拉取方法见各 Release 的说明与 A-NAS 仓库的 `docs/development/testing.md#测试素材`。

本仓库保持私有：部分模型的许可只允许内部测试（见各清单的 `license`），测试素材只供项目内部使用。
