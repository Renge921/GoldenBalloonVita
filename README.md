<p align="center">
  <img src="dist/web/assets/hero.jpg" alt="Golden Balloon" width="820">
</p>

<h1 align="center">Golden Balloon — PS Vita Port (日本語版ROM対応)</h1>

<p align="center">
  本リポジトリは、<a href="https://github.com/zm2283145/goldenballoon-vita-port">zm2283145/goldenballoon-vita-port</a> をベースに、<br>
  <b>Nintendo 64 日本語版ROM（Diddy Kong Racing (J) / v79）に対応させたフォーク</b>です。<br>
  エミュレータではなく、実機ネイティブクロスコンパイルにより動作します。ゲームデータ・アセットは一切含まれていません。
</p>

<p align="center">
  <a href="https://github.com/zm2283145/goldenballoon-vita-port"><b>⬆ フォーク元 (PS Vita移植版 / US版ROM対応)</b></a>
  &nbsp;·&nbsp;
  <a href="https://github.com/akratch/goldenballoon"><b>⬆ アップストリーム (PC/ブラウザ版)</b></a>
</p>

---

## 本リポジトリについて (About This Fork)

本プロジェクトは、[zm2283145/goldenballoon-vita-port](https://github.com/zm2283145/goldenballoon-vita-port) のPS Vita移植版をベースに、日本版ROMへの対応を行ったフォークです。

- **日本版ROM（v79）対応**: 日本語アセットテーブル、メニュー文字列データ、動的ストリーミング文字グリフキャッシュの描画に対応しています。
- **ゲーム内容・機能の詳細について**: ゲーム内の機能、各種設定、最適化仕様、トロフィー一覧、Save Editor等の詳細については、フォーク元リポジトリ（[zm2283145/goldenballoon-vita-port](https://github.com/zm2283145/goldenballoon-vita-port)）およびアップストリーム（[akratch/goldenballoon](https://github.com/akratch/goldenballoon)）を参照してください（今後のフォーク元のアップデート・エンハンスとの仕様乖離を防ぐため、本リポジトリでは重複した詳細説明は省略しています）。

---

## 導入手順 (PS Vita / 日本版ROM)

### 1. 前提条件 (Homebrew環境)
- **HENkaku / H-Encore** 等のCFWが導入されたPS Vita
- **[VitaShell](https://github.com/TheOfficialFloW/VitaShell)**
- **`libshacccg.suprx`**（ランタイムシェーダーコンパイラ）:
  - `ur0:data/libshacccg.suprx` に配置されている必要があります。
- **（任意）トロフィー対応**:
  - トロフィー機能を使用する場合、[NoTrpDrm](https://github.com/Rinnegatamante/NoTrpDrm)（`NoTrpDrm.suprx`）をダウンロードし、`ur0:tai/` 等に配置した上で `config.txt` の `*main` セクションに追加して本体を再起動してください。

### 2. ROMファイルの準備と配置
- ご自身で所有・吸い出した正規の **Nintendo 64 日本版ROM**（`Diddy Kong Racing (J)`、`.z64` 形式）を用意します。
- PS Vitaのストレージに以下の固定パスで配置します：
  ```text
  ux0:data/goldenballoon/baserom.jpn.v79.z64
  ```
  ※ `ux0:data/goldenballoon/baserom.z64` または `ux0:data/goldenballoon/rom.z64` でも認識されます。

### 3. VPKのインストール
- 本リポジトリの [Releases](https://github.com/Renge921/GoldenBalloonVita/releases) から最新の `GoldenBalloon-Vita-*.vpk` をダウンロードします。
- VitaShell（USB転送またはFTP）等でPS Vitaへ転送し、VitaShell上からインストールします。

### 4. 起動
- LiveAreaに追加されたバブルからゲームを起動してください。
- 起動時に問題が発生した場合は、`ux0:data/goldenballoon/mdkr_boot.log` にログが出力されます。

---

## ソースコードからのビルド (Building from source)

### GitHub Actions による自動ビルド
本リポジトリの `main` ブランチへコミットをプッシュすると、GitHub Actions（[.github/workflows/vita-build.yml](.github/workflows/vita-build.yml)）によって自動的にビルドが実行され、VPKパッケージがアーティファクトとして生成されます。

### ローカルでのビルド
[VitaSDK](https://vitasdk.org/) がインストールされた環境で以下を実行します：

```sh
cmake -S . -B build-vita -G Ninja \
    -DCMAKE_TOOLCHAIN_FILE="$VITASDK/share/vita.toolchain.cmake" \
    -DCMAKE_BUILD_TYPE=Release
cmake --build build-vita --target mdkr64
powershell tools/package_vita.ps1 -BuildDir build-vita
```

---

## クレジット・謝辞 (Credits)

- **[zm2283145/goldenballoon-vita-port](https://github.com/zm2283145/goldenballoon-vita-port)**: PS Vita移植版の開発
- **[akratch/goldenballoon](https://github.com/akratch/goldenballoon)**: アップストリームPC/Web移植版の開発
- **[DavidSM64/Diddy-Kong-Racing](https://github.com/DavidSM64/Diddy-Kong-Racing)**: N64 DKR逆コンパイルプロジェクト
- **[Rinnegatamante](https://github.com/Rinnegatamante)**: vitaGL, vitaShaRK, NoTrpDrm
- **VitaSDKコミュニティ**

---

## 免責事項 (Legal & Disclaimer)

- 本プロジェクトには、ゲームのROMデータ、テクスチャ、音声、BGM、3Dモデル等の著作権で保護されたアセットは一切含まれていません。
- 本ソフトウェアは個人利用および研究目的の非公式ファンプロジェクトであり、任天堂、レア社、その他権利者とは一切関係ありません。
- 詳細については [DISCLAIMER.md](DISCLAIMER.md) および [NOTICE.md](NOTICE.md) を参照してください。
