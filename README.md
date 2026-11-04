# A-NAS-assets

A-NAS 开发用的大文件：模型，以后还有测试集。文件只存为 Release 附件，不进 Git。

- 一个文件一个 Release，标签是 `sha256-<文件的 SHA-256>`，说明里是 A-NAS 仓库中固定它的清单（`deploy/models/*.json`）。
- 超过 2 GiB（GitHub 单个附件的上限）的文件切成 `<文件名>.part-NN` 上传，按序号拼接后的 SHA-256 等于标签。
- 拉取与发布用 A-NAS 仓库的 `scripts/fetch-models.sh`，说明见 `docs/development/ai-development.md#拉取模型`。
- 内容按哈希寻址：发布后不修改、不替换；换文件就发新的 Release。
- 本仓库保持私有：部分模型的许可只允许内部测试，见各清单的 `license`。
