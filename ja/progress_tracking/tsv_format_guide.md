# TSV形式進捗管理ガイド

## 📊 概要

TSV (Tab Separated Values) 形式による進捗管理の標準ガイドです。
実際の運用で効果が実証されたフォーマットを提供します。

## 🎯 基本原則

### 1. **時系列順序の重要性**
- **必須**: エントリは時系列順に記録する
- **理由**: 進捗の流れと因果関係を把握するため
- **実装**: DateTime列を先頭に配置

### 2. **JST日時の標準化**
- **形式**: `YYYY-MM-DDTHH:MM:SS+09:00`
- **例**: `2025-09-11T16:32:28+09:00`
- **理由**: 日本のチームでの一貫性とソート可能性

### 3. **ステータス管理**
```
PENDING     : 未開始
INPROGRESS  : 作業中
DONE        : 完了
ERROR       : エラー発生
BLOCKED     : ブロック中（依存関係等）
READY       : 準備完了（レビュー待ち等）
```

## 📋 標準フォーマット

### ヘッダー行
```
DateTime	ServiceName	Environment	Status	DevPR	ProdPR	Notes
```

### エントリ例
```
2025-09-11T16:32:28+09:00	example-service	production	DONE		https://github.com/org/repo/pull/12345	CI SUCCESS: All checks passed after provider fix
2025-09-11T14:15:30+09:00	example-service	development	DONE	https://github.com/org/repo/pull/12340		PR merged successfully
2025-09-11T12:30:15+09:00	example-service	development	INPROGRESS	https://github.com/org/repo/pull/12340		Slack review request posted
```

## 🗂️ ファイル管理

### 命名規則
- **パターン**: `{project_name}_results_{YYYY-MM-DD}.tsv`
- **例**: `spanner_kit_upgrade_results_2025-09-11.tsv`

### 日別分割
- **推奨**: 日付が変わったら新しいファイルを作成
- **理由**: ファイルサイズ管理と検索性向上
- **保持期間**: 最新30ファイル

## 💡 ベストプラクティス

### 1. **詳細なNotes記録**
```
良い例:
"CI SUCCESS AFTER PROVIDER FIX: Google Provider upgraded to v6.3 to support 'edition' attribute"

避けるべき例:
"成功"
```

### 2. **複数環境の追跡**
- 開発環境と本番環境を明確に分離
- 依存関係を Notes で明記

### 3. **エラー情報の詳細化**
```
エラー例:
"ERROR: Google Provider version conflict - 'edition' attribute not supported in v5.37. Needs v6.3+ upgrade"
```

### 4. **ブロック状況の明記**
```
ブロック例:
"BLOCKED: Dev env CI failed with Azure Resource Provider error. Waiting for service owner fix."
```

## 🔄 更新パターン

### ステータス遷移
1. `PENDING` → `INPROGRESS` (作業開始)
2. `INPROGRESS` → `DONE` (正常完了)
3. `INPROGRESS` → `ERROR` (エラー発生)
4. `ERROR` → `INPROGRESS` (修正後再開)
5. `INPROGRESS` → `BLOCKED` (依存関係待ち)
6. `BLOCKED` → `READY` (準備完了)

### 履歴の保持
- **重要**: 過去のエントリは修正せず、新しいエントリを追加
- **理由**: 作業履歴と学習の保持

## 📈 活用効果

### 定量的効果
- **検索性**: 時系列順序により問題の因果関係を特定
- **追跡性**: PR URLによる詳細情報への直接アクセス
- **分析性**: ステータス統計による効率分析

### 定性的効果
- **透明性**: チーム全体での進捗可視化
- **学習**: エラーパターンと解決策の蓄積
- **品質**: 詳細記録による作業品質向上

## 🛠️ ツール連携

### Excel/Google Sheets
- TSV形式は直接インポート可能
- フィルタリングとソート機能活用

### Git管理
- 進捗ファイルもバージョン管理対象
- ブランチ作業との連携

### CI/CD連携
- PR URLから自動的にCI状況確認
- ステータス更新の自動化可能

---

**このガイドは実際の運用経験に基づいて作成されており、継続的に改善されます。**
