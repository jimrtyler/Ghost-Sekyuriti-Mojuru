# 👻 Ghostセキュリティモジュール
**PowerShellベースのWindows & Azureセキュリティハードニングツール**

> **WindowsエンドポイントとAzure環境のためのプロアクティブセキュリティハードニング。** Ghostは、不要なサービスとプロトコルを無効化することで一般的な攻撃ベクターを削減できるPowerShellベースのハードニング機能を提供します。

## ⚠️ 重要な免責事項

**テストが必要**: 常に最初に非本番環境でGhostをテストしてください。サービスの無効化は正当なビジネス機能に影響を与える可能性があります。

**保証なし**: Ghostは一般的な攻撃ベクターを対象としていますが、どのセキュリティツールもすべての攻撃を防ぐことはできません。これは包括的なセキュリティ戦略の一つのコンポーネントです。

**運用への影響**: 一部の機能はシステムの機能性に影響を与える可能性があります。展開前に各設定を慎重に確認してください。

**専門的評価**: 本番環境では、設定が組織のニーズに適合することを確保するためにセキュリティ専門家に相談してください。

## 📊 セキュリティ状況

ランサムウェアの被害は**2025年に570億ドル**に達し、研究によると多くの成功した攻撃は基本的なWindowsサービスと設定ミスを悪用していることが示されています。一般的な攻撃ベクターには以下が含まれます：

- **ランサムウェア事件の90%**がRDPの悪用を伴う
- **SMBv1の脆弱性**がWannaCryやNotPetyaなどの攻撃を可能にした
- **文書マクロ**がマルウェア配信の主要な方法として残っている
- **USBベースの攻撃**がエアギャップネットワークを標的とし続けている
- **PowerShellの悪用**が近年大幅に増加している

## 🛡️ Ghostセキュリティ機能

Ghostは**16のWindowsハードニング機能**と**Azureセキュリティ統合**を提供します：

### Windowsエンドポイントハードニング

| 機能 | 目的 | 考慮事項 |
|----------|---------|----------------|
| `Set-RDP` | リモートデスクトップアクセスを管理 | リモート管理に影響を与える可能性 |
| `Set-SMBv1` | レガシーSMBプロトコルを制御 | 非常に古いシステムに必要 |
| `Set-AutoRun` | AutoPlay/AutoRunを制御 | ユーザーの利便性に影響を与える可能性 |
| `Set-USBStorage` | USBストレージデバイスを制限 | 正当なUSB使用に影響を与える可能性 |
| `Set-Macros` | Officeマクロ実行を制御 | マクロ有効文書に影響を与える可能性 |
| `Set-PSRemoting` | PowerShellリモーティングを管理 | リモート管理に影響を与える可能性 |
| `Set-WinRM` | Windows Remote Managementを制御 | リモート管理に影響を与える可能性 |
| `Set-LLMNR` | 名前解決プロトコルを管理 | 通常無効化しても安全 |
| `Set-NetBIOS` | TCP/IP上のNetBIOSを制御 | レガシーアプリケーションに影響を与える可能性 |
| `Set-AdminShares` | 管理共有を管理 | リモートファイルアクセスに影響を与える可能性 |
| `Set-Telemetry` | データ収集を制御 | 診断機能に影響を与える可能性 |
| `Set-GuestAccount` | ゲストアカウントを管理 | 通常無効化しても安全 |
| `Set-ICMP` | ping応答を制御 | ネットワーク診断に影響を与える可能性 |
| `Set-RemoteAssistance` | リモートアシスタンスを管理 | ヘルプデスク運用に影響を与える可能性 |
| `Set-NetworkDiscovery` | ネットワーク探索を制御 | ネットワークブラウジングに影響を与える可能性 |
| `Set-Firewall` | Windowsファイアウォールを管理 | ネットワークセキュリティに重要 |

### Azureクラウドセキュリティ

| 機能 | 目的 | 要件 |
|----------|---------|--------------|
| `Set-AzureSecurityDefaults` | 基本的なAzure ADセキュリティを有効化 | Microsoft Graphアクセス許可 |
| `Set-AzureConditionalAccess` | アクセスポリシーを設定 | Azure AD P1/P2ライセンス |
| `Set-AzurePrivilegedUsers` | 特権アカウントを監査 | グローバル管理者アクセス許可 |

### エンタープライズ展開オプション

| 方法 | 使用例 | 要件 |
|--------|----------|--------------|
| **直接実行** | テスト、小規模環境 | ローカル管理者権限 |
| **グループポリシー** | ドメイン環境 | ドメイン管理者、GP管理 |
| **Microsoft Intune** | クラウド管理デバイス | Intuneライセンス、Graph API |

## 🚀 クイックスタート

### セキュリティ評価
```powershell
# Ghostモジュールをロード
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# 現在のセキュリティ体制を確認
Get-Ghost
```

### 基本ハードニング（最初にテスト）
```powershell
# 必須ハードニング - 最初にラボ環境でテスト
Set-Ghost -SMBv1 -AutoRun -Macros

# 変更を確認
Get-Ghost
```

### エンタープライズ展開
```powershell
# グループポリシー展開（ドメイン環境）
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Intune展開（クラウド管理デバイス）
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 インストール方法

### オプション1: 直接ダウンロード（テスト用）
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### オプション2: モジュールインストール
```powershell
# PowerShell Galleryからインストール（利用可能時）
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### オプション3: エンタープライズ展開
```powershell
# グループポリシー展開用のネットワーク場所にコピー
# クラウド展開用のIntune PowerShellスクリプトを設定
```

## 💼 使用例

### 中小企業
```powershell
# 最小限の影響で基本保護
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### 医療環境
```powershell
# HIPAA重視のハードニング
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### 金融サービス
```powershell
# 高セキュリティ設定
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### クラウドファースト組織
```powershell
# Intune管理展開
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 機能詳細

### コアハードニング機能

#### ネットワークサービス
- **RDP**: リモートデスクトップアクセスをブロックまたはポートをランダム化
- **SMBv1**: レガシーファイル共有プロトコルを無効化
- **ICMP**: 偵察用のping応答を防止
- **LLMNR/NetBIOS**: レガシー名前解決プロトコルをブロック

#### アプリケーションセキュリティ  
- **マクロ**: Officeアプリケーションでのマクロ実行を無効化
- **AutoRun**: リムーバブルメディアからの自動実行を防止

#### リモート管理
- **PSRemoting**: PowerShellリモートセッションを無効化
- **WinRM**: Windows Remote Managementを停止
- **Remote Assistance**: リモートアシスタンス接続をブロック

#### アクセス制御
- **管理共有**: C$、ADMIN$共有を無効化
- **ゲストアカウント**: ゲストアカウントアクセスを無効化
- **USBストレージ**: USBデバイス使用を制限

### Azure統合
```powershell
# Azureテナントに接続
Connect-AzureGhost -Interactive

# セキュリティデフォルトを有効化
Set-AzureSecurityDefaults -Enable

# 条件付きアクセスを設定
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# 特権ユーザーを監査
Set-AzurePrivilegedUsers -AuditOnly
```

### Intune統合（v2の新機能）
```powershell
# Intuneに接続
Connect-IntuneGhost -Interactive

# Intuneポリシー経由で展開
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ 重要な考慮事項

### テスト要件
- **ラボ環境**: 最初に分離環境ですべての設定をテスト
- **段階的展開**: 問題を特定するために段階的にロールアウト
- **ロールバック計画**: 必要に応じて変更を元に戻せることを確認
- **文書化**: 環境で機能する設定を記録

### 潜在的影響
- **ユーザー生産性**: 一部の設定が日常のワークフローに影響を与える可能性
- **レガシーアプリケーション**: 古いシステムは特定のプロトコルを必要とする可能性
- **リモートアクセス**: 正当なリモート管理への影響を考慮
- **ビジネスプロセス**: 設定が重要な機能を破壊しないことを確認

### セキュリティ制限
- **多層防御**: Ghostはセキュリティの一層であり、完全なソリューションではない
- **継続的管理**: セキュリティには継続的な監視と更新が必要
- **ユーザートレーニング**: 技術的制御はセキュリティ意識と組み合わせる必要がある
- **脅威の進化**: 新しい攻撃手法は現在の保護を回避する可能性がある

## 🎯 攻撃シナリオ例

Ghostは一般的な攻撃ベクターを対象としていますが、具体的な防止は適切な実装とテストに依存します：

### WannaCryスタイル攻撃
- **軽減**: `Set-Ghost -SMBv1`が脆弱なプロトコルを無効化
- **考慮事項**: SMBv1を必要とするレガシーシステムがないことを確認

### RDPベースランサムウェア
- **軽減**: `Set-Ghost -RDP`がリモートデスクトップアクセスをブロック
- **考慮事項**: 代替リモートアクセス方法が必要な場合がある

### 文書ベースマルウェア
- **軽減**: `Set-Ghost -Macros`がマクロ実行を無効化
- **考慮事項**: 正当なマクロ有効文書に影響を与える可能性

### USB配信脅威
- **軽減**: `Set-Ghost -USBStorage -AutoRun`がUSB機能を制限
- **考慮事項**: 正当なUSBデバイス使用に影響を与える可能性

## 🏢 エンタープライズ機能

### グループポリシーサポート
```powershell
# グループポリシーレジストリ経由で設定を適用
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# GP更新後にドメイン全体で設定が適用
gpupdate /force
```

### Microsoft Intune統合
```powershell
# Ghost設定用のIntuneポリシーを作成
Set-IntuneGhost -Settings $GhostSettings -Interactive

# ポリシーが管理デバイスに自動的に展開
```

### コンプライアンスレポート
```powershell
# セキュリティ評価レポートを生成
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Azureセキュリティ体制レポート
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 ベストプラクティス

### 展開前
1. **現在の状態を文書化**: 変更前に`Get-Ghost`を実行
2. **徹底的にテスト**: 非本番環境で検証
3. **ロールバックを計画**: 各設定を元に戻す方法を知る
4. **ステークホルダーレビュー**: ビジネスユニットが変更を承認することを確認

### 展開中
1. **段階的アプローチ**: 最初にパイロットグループに展開
2. **影響を監視**: ユーザーの苦情やシステム問題を注視
3. **問題を文書化**: 将来の参照のために問題を記録
4. **変更を伝達**: セキュリティ改善についてユーザーに通知

### 展開後
1. **定期的評価**: 設定を確認するために定期的に`Get-Ghost`を実行
2. **文書化を更新**: セキュリティ設定を最新に保つ
3. **効果を確認**: セキュリティインシデントを監視
4. **継続的改善**: 脅威の状況に基づいて設定を調整

## 🔧 トラブルシューティング

### 一般的な問題
- **権限エラー**: PowerShellセッションが昇格されていることを確認
- **サービス依存関係**: 一部のサービスには依存関係がある可能性
- **アプリケーション互換性**: ビジネスアプリケーションでテスト
- **ネットワーク接続**: リモートアクセスがまだ機能することを確認

### 復旧オプション
```powershell
# 必要に応じて特定のサービスを再有効化
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 著者について

**Jim Tyler** - PowerShell Microsoft MVP
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10,000+購読者)
- **ニュースレター**: [PowerShell.News](https://powershell.news) - 週刊セキュリティインテリジェンス
- **著者**: "PowerShell for Systems Engineers"
- **経験**: PowerShell自動化とWindowsセキュリティの数十年

## 📄 ライセンス・免責事項

### MITライセンス
GhostはMITライセンスの下で無料使用、変更、配布のために提供されています。

### セキュリティ免責事項
- **保証なし**: Ghostは「現状のまま」で提供され、いかなる種類の保証もありません
- **テスト必須**: 常に最初に非本番環境でテストしてください
- **専門的ガイダンス**: 本番展開についてはセキュリティ専門家に相談してください
- **運用への影響**: 著者は運用中断について責任を負いません
- **包括的セキュリティ**: Ghostは完全なセキュリティ戦略の一つのコンポーネントです

### サポート
- **GitHub Issues**: [バグ報告や機能要求](https://github.com/jimrtyler/Ghost/issues)
- **文書化**: 詳細なヘルプは`Get-Help <function> -Full`を使用
- **コミュニティ**: PowerShellとセキュリティコミュニティフォーラム

---

**🔒 Ghostでセキュリティ体制を強化してください - ただし常に最初にテストしてください。**

```powershell
# 仮定ではなく評価から始める
Get-Ghost
```

**⭐ Ghostがセキュリティ体制の向上に役立つ場合は、このリポジトリにスターを付けてください！**