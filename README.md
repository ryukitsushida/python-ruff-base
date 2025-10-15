# python-ruff-base
Ruff を使ってコード整形と静的解析（リンティング）を最小構成で有効化したベースです。
※このREADMEはGPT-5君に作成してもらいました。

### 設定ファイル
- `pyproject.toml`: Ruff の共通設定（フォーマッタ＋リンタ）
- `.vscode/settings.json`: VS Code 上の拡張機能・挙動の設定

---

## `pyproject.toml` の設定解説

### [tool.ruff]
- `line-length = 120`
	- 整形時の折り返し基準。
- `target-version = "py313"`
	- 解析・自動修正時に想定する Python バージョン。

### [tool.ruff.lint]
- `select = ["E", "F", "I", "B", "UP", "S"]`
	- 有効化するルール群のプリセットを指定します。
		- `E`: pycodestyle（スタイル）
		- `F`: pyflakes（未使用変数などのバグ指向）
		- `I`: import 並び替え（isort 相当）
		- `B`: flake8-bugbear（バグを生みやすいパターンの警告、B950 を含む）
		- `UP`: pyupgrade（より新しい構文への自動提案）
		- `S`: bandit（セキュリティ）
- `ignore = ["E501"]`
	- E501（行が長すぎる）の違反を無視します。整形は `line-length` に基づいて行われますが、E501 の警告は表示しない運用です。

### [tool.ruff.format]
- `quote-style = "double"`
	- 文字列リテラルをダブルクオートで統一します。
- `indent-style = "space"`
	- インデントはスペースに統一します。
- `skip-magic-trailing-comma = false`
	- 末尾カンマ（magic trailing comma）による意図的な折り返しを有効にします。多引数での見やすい改行に寄与します。

---

## `.vscode/settings.json` の設定解説

- `editor.formatOnSave: true`
	- 保存時に自動フォーマットを実行します（フォーマッタは Ruff）。
- `editor.defaultFormatter: "charliermarsh.ruff"`
	- VS Code のデフォルトフォーマッタとして Ruff 拡張を使用します。
- `ruff.lint.enable: true`
	- VS Code 上で Ruff のリンティングを有効化します（Problems パネル等に表示）。
- `ruff.configurationPreference: "filesystemFirst"`
	- ワークスペースの `pyproject.toml` などファイル側の設定を優先します。
- `python.testing.pytestEnabled: true`
	- pytest によるテスト検出・実行を有効にします。
- `python.testing.pytestArgs: ["tests"]`
	- `tests` ディレクトリ配下をテスト探索対象にします。
