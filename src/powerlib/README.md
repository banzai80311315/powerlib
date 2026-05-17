## 12. ディレクトリ構成
自作アプリに使うライブラリpowerlibのディレクトリ構成は
```
src/
  powerlib/
    __init__.py

    io/ # 外部ファイルを読むだけ
      jepx_csv.py          # JEPX CSV読み込み
      schema.py            # 列名定義・標準カラム名

    preprocessing/ # 生データを分析可能な形に整える
      datetime.py          # 受渡日 + 時刻コード → datetime
      cleaning.py          # 数値変換、欠損処理、型変換
      scaling.py           # 休日・曜日補正

    features/ # 分析・モデルに使う列を作る
      time_features.py     # 時刻、曜日、休日、slot特徴量
      spike_features.py    # spike indicator, excess magnitude

    analysis/ # モデルではない集計分析
      summary.py           # 平均、分位点、基本統計
      distribution.py      # ヒストグラム用集計、分布分析
      time_profile.py      # 30分単位平均、時間帯別分析

    models/ # 予測・推定モデル
      hawkes.py            # Hawkesモデル
      threshold.py         # 閾値ベースモデル
      baseline.py          # persistenceなどベースライン

    metrics/ # 結果評価
      classification.py    # accuracy, precision, recall, F1, MCC
      forecasting.py       # MAE, WACCなど

    visualization/ # 図を作る
      timeseries.py        # plot用関数
      distribution.py      # histogram用関数
      spike.py             # spike可視化

    config.py              # 共通定数
    exceptions.py          # 独自例外
```

対応をするために、このプロジェクトディレクトリの責務も以下を意識する
```
io : 0.data_input
preprocessing : 1.data_processing
features , analysis : 2.feature_extraction
models : 3.model
metrics : 4.evaluation
```