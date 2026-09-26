# CLine46 firmware

CLine46の分割キーボード向けZMK設定です。右側がCentralで、トラックボールとホストへのUSB/BLE接続を担当します。左側はPeripheralです。

## ビルド

1. GitHubの[Actions](https://github.com/shimcim/zmk_config_CLine46/actions/workflows/build.yml)で対象コミットの`Build`を実行するか、push後の自動実行を開きます。
2. `CLine46_R`、`CLine46_L`、`settings_reset`の3ビルドが成功したことを確認します。
3. 実行ページの`firmware`成果物をダウンロードし、ZIPを展開します。実行URLとソースコミットを控えてください。

| ファイル | 用途 |
| --- | --- |
| `CLine46_R.uf2` | 右側、Central、トラックボール側 |
| `CLine46_L.uf2` | 左側、Peripheral側 |
| `settings_reset.uf2` | 保存設定の初期化専用 |

再現したい版が[Releases](https://github.com/shimcim/zmk_config_CLine46/releases)にある場合は、その版のソースコミットと同じ成果物を使用します。

## 書き込み

1. 対象側をUSBで接続し、リセット操作でUF2ブートローダーを起動します。
2. 右側へ`CLine46_R.uf2`、左側へ`CLine46_L.uf2`を書き込みます。片側だけ更新する場合は、変更内容に応じて対象側を選びます。
3. 左右間接続とホストへのUSB/BLE接続を確認します。

通常の更新では`settings_reset.uf2`を使いません。保存済みキーマップやジェスチャー設定を消去するためです。

## 設定リセット

ファームウェア世代の切替や保存設定の初期化が必要な場合は、先に必要なキーマップと設定を退避します。その後、左へ`settings_reset.uf2`、左へ通常ファームウェア、右へ`settings_reset.uf2`、右へ通常ファームウェアの順に書き込みます。ホスト側の古いBluetooth登録を削除し、左右とホストを再ペアリングします。

初期化後は、コンパイル済みキーマップ、一時レイヤー、コンボ、ジェスチャーの初期設定に戻ります。

## ジェスチャー設定

ころころKitでジェスチャーの方向別アクションと対象レイヤーを変更できます。`GESTURE1`〜`GESTURE4`の各レイヤーで上下左右を確認し、変更後に再起動して保存状態を確認してください。保存された変更は通常のファームウェア書き込みでは保持され、`settings_reset.uf2`で消去されます。

## ファームウェア成果物

新しい配布用UF2は、ソースコミットとビルド実行を記載したGitHub Releaseに添付します。開発中のビルドはActionsの`firmware`成果物から取得します。UF2をこのリポジトリへ新たにコミットしないでください。過去にコミットされたUF2は履歴に残っています。
