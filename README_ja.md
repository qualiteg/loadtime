# LoadTimeパッケージ

[English](https://github.com/riversun/LoadTime/blob/main/README.md) | [&#26085;&#26412;&#35486;](https://github.com/riversun/LoadTime/blob/main/README_ja.md)


処理時間が不明な長時間処理中にプログレスバーを表示する Python パッケージです。1回目の実行時は処理時間を計測しておき、2回目、また同じ処理が呼ばれたときはプログレスバーを表示します。

<img src="https://riversun.github.io/loadtime/loadtime_std.gif">

例えば 事前学習済み言語モデルをGPUやCPUメモリに読み込むときに使用すると、
不確実な待ち時間を過ごすことなく読み込みプロセスの進捗を視覚化することができます。

## インストール方法

pipを使ってLoadTimeをインストールできます

```bash
pip install loadtime
```

## 主な機能

- **リアルタイムトラッキング**: LoadTimeは読み込みプロセスのリアルタイムトラッキングを提供します。

- **プログレスバー**: プログレスバーを表示し、処理がどれだけ完了し、まだどれだけ残っているかを示します。

- **過去の読み込み時間キャッシュ**:
  前回処理した時間をキャッシュしておくため、キャッシュされた情報を使用して、プログレスバーを提供します。

- **カスタマイズ可能な表示**: LoadTimeは、自分のメッセージで進捗表示をカスタマイズすることができます。

## 基本的な使い方

サンプルコードを示します

```python
import torch
from transformers import AutoTokenizer, AutoModelForCausalLM
from loadtime import LoadTime

model_path = "togethercomputer/RedPajama-INCITE-Chat-3B-v1"

tokenizer = AutoTokenizer.from_pretrained(model_path)
model = LoadTime(name=model_path,
                 fn=lambda: AutoModelForCausalLM.from_pretrained(model_path, torch_dtype=torch.float16))()
```

## 初期化パラメータ一覧

| パラメータ | 説明 |
|------------|------|
| name       | 長時間処理の名前を指定します。HuggingFace モデルの読み込み時はモデル名を指定します。 |
| message    | 表示するメッセージを指定します。省略するとデフォルトのメッセージとなります。 |
| pbar       | True に設定すると、プログレスバーとパーセンテージが表示されます。 |
| dirname    | キャッシュ保存先のディレクトリ名を指定します。 |
| hf         | True に設定すると、HuggingFace のモデル読み込み用の時間表示に使用します。まだモデルデータがディスクにダウンロードされていないときは、HuggingFace のローダーがダウンロード進捗を表示するため、本ライブラリからは表示しません。 |
| fn         | 長時間処理をする関数を指定します。 |
| fn_print   | 表示を行う関数を指定します。省略時はコンソールに出力されます。 |
