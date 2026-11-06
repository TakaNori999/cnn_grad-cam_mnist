# GitHub公開とZenodoでのDOI取得（日本語）

対象リポジトリ： `https://github.com/TakaNori999/cnn_grad-cam_mnist`

## 第1段階：公開前の確認

- [x] 修正版ノートブックをColabで上から実行し、MNISTの学習、外部画像30枚の取得、Grad-CAM++の表示を確認する（利用者による動作確認）。
- [x] [外部画像の既存リポジトリ](https://github.com/TakaNori999/Num_sorce_mnist) の30枚は著者本人が制作したオリジナル画像（著者による申告）。元リポジトリに利用許諾の記載はまだないため、画像の第三者による再利用を認める場合は別途明記する。
- [ ] 著者氏名・所属する権利者・共著者の扱いを確認する（仮設定：Norihiro Takahashi）。ORCIDがあれば `CITATION.cff` に追記する。
- [ ] `.ipynb` に実行画像・個人情報・機密情報が埋め込まれていないことを確認する。

## 第2段階：GitHub公開ファイルを確認する

1. リポジトリ `TakaNori999/cnn_grad-cam_mnist` はすでにPublicで公開済みです。今後の更新時も、データ・画像・実行出力を含めないでください。
2. `.ipynb`、README、LICENSE、CITATION.cff、requirements.txt、`.gitignore`、ガイドがリポジトリ直下にあることを確認してください。
3. **Open in Colab** のリンク `https://colab.research.google.com/github/TakaNori999/cnn_grad-cam_mnist/blob/main/MNIST_CNN_GradCAMpp_Colab.ipynb` でNotebookが開き、実行できることを確認する。

## 第3段階：Zenodoと連携（GitHub Releaseより前）

1. [Zenodo](https://zenodo.org/) にログイン（必要ならアカウント作成）。
2. GitHubアカウントを連携する。Zenodoのプロフィールメニュー → GitHub → Sync now → リポジトリ `cnn_grad-cam_mnist` を探し、連携スイッチをONにする。
3. 必要な著者・タイトル・ライセンスが Zenodo側に適切に登録されるよう `CITATION.cff` を確認する。
4. GitHubで **Releases → Draft a new release** を開き、タグ `v1.0.0`、タイトル `MNIST CNN & Grad-CAM++ v1.0.0` を指定して公開する。
5. Zenodoでアーカイブの完了・DOIの発行を確認する。GitHub Releaseは自動でZenodoに取り込まれる設定です。

Zenodo公式：[Enable a repository](https://help.zenodo.org/docs/github/enable-repository/)、[Archive a release from GitHub](https://help.zenodo.org/docs/github/archive-software/github-upload/)

## 第4段階：DOI反映

- Zenodoで発行された**特定バージョンのDOI**をREADMEに追記し、`CITATION.cff` に `doi: "10.5281/zenodo.実際の番号"` を記載する（番号を推測・捏造しない）。
- Zenodoに保存されたv1.0.0の内容は公開時点のスナップショットです。DOI追記後のGitHubの変更は、既存のZenodoアーカイブには自動で反映されないので注意してください。
- 将来v1.1.0をリリースする際は、それに対応する新しいバージョンDOIを記録します。

## 注意点

- 今回は**元の学生向けコードを基に技術的な誤りを修正**しています。Grad-CAM++は、指数クラススコアの2階・3階微分を、線形＋ReLUの分類部という構造を利用して**解析的に正確に評価**しています（ReLUの折れ点を除く）。全要素の高階自動微分は行わず、1階勾配から高階微分を解析的に求めます。研究論文にはこの計算方式を明記してください。
- MNISTデータはKerasが実行時に取得します。外部画像は固定した別GitHubリポジトリから取得するため、Zenodoに画像そのものは含まれません。元リポジトリの削除・非公開化などが起こると将来の実行に影響します。
- 外部の30枚は著者の制作物ですが、今回のソフトウェアパッケージには同梱せず既存リポジトリから取得します。画像の二次利用を認める場合は、画像用ライセンスを明記すると利用者に親切です。
