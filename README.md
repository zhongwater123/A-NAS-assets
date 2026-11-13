# A-NAS-assets

A-NAS 开发用的大文件：模型、测试素材与发布用的运行环境。文件只存为 Release 附件，不进 Git。仓库开启了不可变 Release：发布后不修改、不替换，换文件就发新的 Release。超过 2 GiB（GitHub 单个附件的上限）的文件切成 `<文件名>.part-NN` 上传，按序号拼接。

## 模型

- 一个文件一个 Release，标签是 `sha256-<文件的 SHA-256>`，说明里是 A-NAS 仓库中固定它的清单（`deploy/models/*.json`）。
- 拉取与发布用 A-NAS 仓库的 `scripts/fetch-models.sh`，说明见 `docs/development/ai-development.md#拉取模型`。

## 测试素材

- 每套素材一个 Release，标签是素材名加版本（如 `videos-dji-v1`），附列出每个完整文件的 `SHA256SUMS`。
- 拉取方法见各 Release 的说明与 A-NAS 仓库的 `docs/development/testing.md#测试素材`。


## 伙伴动画

- 虚拟伙伴（大肥鱼）在 Safari 与 iPhone、iPad 上播放的 HEVC 动画 `dsh-pet-mov-assets-mov.zip`，一个 Release，标签同模型的规则（`sha256-<文件的 SHA-256>`）。
- 上游 dsh-pet 每次构建都同名覆盖它的 `assets-mov` 发布，编码结果每次不同，所以 A-NAS 固定的是这里的副本。
- 固定它的是 A-NAS 仓库的 `scripts/vendor-dsh-pet.py`（`MOV_ZIP`）；安装见 `docs/runbooks/install-companion-animations.md`。动画的许可是 CC BY-NC-SA 4.0，只供内部开发与测试。

## 运行环境与源码包

`make release` 从开发机的内容库取的文件中，丢了就难以原样找回的几个。一个文件一个 Release，标签同模型的规则（`sha256-<文件的 SHA-256>`），说明里写着它放到内容库的哪个目录。

- 助手试用的 Hermes 运行环境 `runtime.tar.gz`：重新构建会改变 SHA-256，A-NAS 仓库的 `ai/assistant-spike/runtime.json` 固定的是这一个文件。
- AI Worker 与网页搜索的 Python 运行环境，标题为 `ai-runtime-<ID>`、`search-runtime-<ID>`：ID 由锁文件与 Python 版本算出（`scripts/lib/content.sh`），重新构建不保证逐字节相同。锁文件一变就是新的 ID、新的 Release。
- SearXNG 源码包 `searxng.tar.gz`：GitHub 为提交生成的压缩包不保证逐字节不变，A-NAS 仓库的 `deploy/search/searxng.json` 固定的哈希与这里的副本相同。

用法见 A-NAS 仓库的 `docs/runbooks/deploy-a-nas-packages.md#步骤`。

本仓库保持私有：部分模型的许可只允许内部测试（见各清单的 `license`），测试素材只供项目内部使用。
