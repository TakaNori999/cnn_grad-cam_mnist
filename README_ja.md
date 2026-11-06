# MNISTの学習とGrad-CAM++の可視化（Google Colab）

[English README](README.md)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakaNori999/cnn_grad-cam_mnist/blob/main/MNIST_CNN_GradCAMpp_Colab.ipynb)

## 教材の概要

MNISTの手書き数字を使ってCNNを学習し、**未知の数字画像に対して予測結果とGrad-CAM++のヒートマップ**を表示する教材です。Google Colab用で、学生がフィルタ数、畳み込み層数、エポック数、画像番号を変更できます。

## 実行方法

1. 上の **Open in Colab** からノートブックを開きます。GPUランタイムを推奨します。
2. **第2節**でフィルタ数、**第3節**でエポック数を設定して、セルを上から順に実行します。
3. **第4節**で外部の数字画像30枚をGitHubから取得し、一覧と正解率を表示します。
4. **第6節**の `INDEXES = [0]` を、例えば `[0, 7, 15]` に変更すると、選択画像の予測とGrad-CAM++を表示します。

Google Driveのマウントは不要です。画像取得元は [TakaNori999/Num_sorce_mnist](https://github.com/TakaNori999/Num_sorce_mnist) の `num_src` です。外部画像は本リポジトリに同梱しません。

## 学習・評価条件

| 項目 | 初期設定 |
| --- | --- |
| 学習画像 | Keras MNIST 60,000枚 |
| 学習中の検証 | 学習用データの10% |
| 独立テスト | MNISTテスト画像10,000枚 |
| CNN | Conv2D(32, 3×3, ReLU)、Flatten、Dense(64, ReLU)、Dense(10)、Softmax |
| 学習条件 | SGD / Categorical Crossentropy / batch size=32 / epochs=1 |
| 外部画像 | 0～9の各3枚、計30枚（コミット `c41ab788a669ad03b58b1e387b69647faa699eaf` に固定） |
| Grad-CAM++ | 指数変換した予測クラススコアの**正確な2階・3階微分を解析的に算出** |

**技術的な注意：** 特徴マップより後ろが線形層とReLUからなるため、指数クラススコアの2階・3階微分は1階勾配から数学的に正確に求められます（ReLUの折れ点を除く）。各要素について3階の自動微分を繰り返す必要はありません。ヒートマップは分類に関連する領域を示す説明であり、モデルの判断根拠の正しさを保証するものではありません。また、プーリングを使わない構造のためフィルタ数を増やすと計算負荷が大きくなります。

## データと再配布

公開対象はコードのみです。外部の数字画像は別GitHubリポジトリから実行時に取得します。これら**30枚はコードの作成者自身が制作したオリジナル画像**です。ただし、元の画像リポジトリには明示的なライセンスがないため、第三者の再利用・再配布を広く認める場合は、別途画像向けのライセンスを明記してください。

MNISTの著作権と利用条件はKerasの[公式説明](https://keras.io/api/datasets/mnist/)に従います（CC BY-SA 3.0）。このリポジトリのMIT Licenseは、当該コードにのみ適用します。

## Grad-CAM++の原論文

Chattopadhyay et al. (2018), *Grad-CAM++*, WACV. https://doi.org/10.1109/WACV.2018.00097

## 引用とDOI

`CITATION.cff` に引用情報を記載しています。GitHubリリースをZenodoに保存した後、**実際に発行されたDOI**をREADMEと引用情報に追記します。現時点でDOIは未取得です。

詳しい手順： [GitHub公開とZenodoによるDOI取得ガイド](ZENODO_RELEASE_GUIDE_ja.md)
