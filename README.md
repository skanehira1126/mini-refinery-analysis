# Mini Refinery Analysis

目的ごとに分析を進め、根拠付きの知見と作業記録を残す軽量なCodexプラグインです。
専用CLIや中央vaultは使いません。分析環境、実行方法、データアクセス、保存・共有の制約は
利用先の `AGENTS.md` などに従います。

## インストール

```bash
codex plugin marketplace add skanehira1126/mini-refinery-analysis --ref main
codex plugin add mini-refinery-analysis@mini-refinery-analysis
```

## 使い方

- `$mini-refinery-analysis:manage-objective-knowledge`：目的フォルダの作成、現在地の更新、知見の保存・精製、明示的な別目的からの取り込み。
- `$mini-refinery-analysis:analyze-objective`：分析のHowの設計、分析の実行と結果の確認、根拠と知見の記録。

例：

> この期間差の原因を理解する目的フォルダを作ってください。

> この目的でROC曲線の期間比較を進め、結果と知見を残してください。

> objectives/other-purpose の知見を探し、今回に使えるものを出典付きで取り込んでください。

分析方法だけの相談ではファイルを作りません。実行した分析や、依頼された知見・作業の記録を保存します。
目的が変わったら別フォルダにし、同じ目的の追加分析では記録を追加します。

## 保存構成

既存の保存先を優先し、未指定なら `objectives/<目的のslug>/` を使います。

| 相対パス | 役割 |
|---|---|
| `knowledge/DESCRIPTION.md` | 目的を定義。通常の進捗では更新しない |
| `knowledge/CURRENT_STATE.md` | 現在の結論、根拠、未解決事項、次の確認 |
| `knowledge/KNOWLEDGE_INDEX.md` | 分類別の知見への索引 |
| `knowledge/<分類>/<知見>.md` | 適用条件・限界・根拠を含む知見 |
| `analyses/<記録ID>/record.md` | 分析や作業の問い、方法、結果、判断 |

テンプレートと更新規則は [目的フォルダの契約](references/workspace.md) を参照してください。
分類は必要に応じて追加します。別目的は自動で横断検索せず、取り込んだ知見は今回未検証として扱います。

## 設計の参考

- [Knowledge Refinery](https://github.com/skanehira1126/knowledge-refinery)：経験と再利用する知見の分離、条件と根拠の追跡。
- [Python Coding](https://github.com/skanehira1126/codex-plugins/tree/main/plugins/python-coding)：必要な責務境界と、リスクに対応した検証。
- [Notebook Data Analysis](https://github.com/skanehira1126/pybr/tree/main/.agents/skills/notebook-data-analysis)：問い・試行・統合した結論の分離。手順を環境に依存しない形へ整理しています。

pluginには手順だけを置き、実際の知見と分析記録は利用先へ保存します。
