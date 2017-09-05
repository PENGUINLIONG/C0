# 修正・実装予定の一覧

## ver 0.2.0
セルの線の編集点をなくし、3次ベジェ曲線のみで構成する。そのとき、線同士をG0またはG2連続で接続。G0は自動的に判別する。点の追加、削除を再設計、または統廃合。

点の移動と線の変形を統合。セルの追加時の線の置き換えを廃止、編集セルを廃止（これによりセル追加時の非インディケーションによるモードが除去可能）。インディケーション時に前後表示、接合表示を行う。

これらが可能ならマテリアルのコピーによるバインドを廃止、クリックでマテリアルをバインド。キャンバス操作による、暗黙的なキーフレームの分割を廃止。グループの透過表示廃止。

2017年11月リリース予定。

## ver 0.3.0
GPU描画。

## ver 0.4.0
カット単位での読み込み。カメラとイージング、ループの再設計。

## セル
**セルの線の編集点をなくし、3次ベジェ曲線のみで構成する**  
線同士をG0またはG2連続で接続。G0は自動的に判別する。

**セルのグループ間移動**  

**複数セルの重なり判定**  
複数のセルの上からセルを追加するときにもcontains判定が有効なように修正する。

**セル編集時のキーフレーム分割廃止**  
Drawingと同じように前のキーフレームのセルを編集する。

**前後表示にセルも含める**  

**セルに文字をペースト**  

**セルに画像をペースト**  

**セルの結合**  
Unionコマンドを作る。

**小さなセルを選択しやすくする**  

**重なっているセル同士の区別をつけたクリップコマンド**  
親子表示またはアニメーション表示で解決する。

**セルの間のアンチエイリアスで生じる隙間埋め**  
スーパーサンプリングなどで解決する。でもそのためには描画エンジンの変更が必要。

**セルを選択していない時のMaterialViewを背景として定義**  

**高さ優先の囲み消し**  
セルの後ろに隠れた線も選択してしまう問題の修正。

**セルグループ**  

**セルへの操作の履歴を別のセルに適用するコマンド** 

**セルを追加するときなどにある部分においてモーダルになる問題**  

**マテリアルID、カラーIDの可視性**  
indication表示で対処する。

**線の方向を排除**  
セルの回転方向を計算することで排除できますが、線の交差判定などが必要。

**同一色の重なり順飛ばし**  

**制御線コマンド**  
セルの回転などへの対応として、引いた線を制御線としてセルに適用させるもの。しかし作業の複雑性が増すため、消極的。

**自動回転補間**  

**「変形」の再設計**  
三次元変形などを導入し、枠を使った変形にする。

## 線
**線の筆圧数可変設計**  

**線の筆圧描写アルゴリズム改善**  

**線の変形表示などの改善**  

**線の分割ずれ問題**  
線にstartTとendTをつける。

**線の分割や結合**  

**定規**  

**線の端の丸み**  

**「最後の線に適用するコマンド」をすべて「最も近い線に適用するコマンド」に変更する**  

**ストロークの品質の向上**  
アニメーション補間を取り入れる。

**着色線の導入**  
原画時に簡単に塗り分けるための、線を着色線化するコマンドの導入。着色線は囲み消しの範囲と同等。ただ、原画作業の複雑化にもつながるため、消極的。

**ポリゴン化**  
GPUでの描画に切り替えるため。曲率が高い部分では分割数を増やし、低い部分では分割数を減らす。


## カメラ
**前後カメラ表示**  

**カメラと変形の統合**  

**「揺れ」の振動数の設定**  


## マテリアル
**マテリアルアニメーション**  

**コントラストなどのカラー編集**  

**アルファチェーン**  
連続する同じアルファのセル同士を同一の平面として描画。

**擬似的なセルの法線ベクトルの導入**  

**アナログ風の透過光**  

**マクロ式のライト**  

**アクションの保存**  
変形情報などをセルに埋め込む。


## セリフ
**TextViewを完成させる**  
タイムラインと同じような設計にする。

**口パク連動**  

**モードレス・テキスト入力**  
すべての状態において、キー入力を受け付ける。ただし、キー入力と衝突しているコマンドを衝突しないように変更しないといけない。おそらくハードウェアレベルでの変更が必要。

## グループ
**グループごとの線の色**  

**グループ選択による選択結合**  

**グループの半透明表示を廃止して、完成表示の上から選択グループを半透明着色する**  
描画の高速化が必要。

**グループの最終キーフレームの時間問題**  

**ループを再設計**  

**イージングを再設計**  
キーフレームではなく、セルやカメラに直接設定


## タイムライン
**キーフレームの複数選択**  

**タイムラインにキーフレーム・プロパティを統合**

**アニメーション描画**  
表示が離散的な1フレーム単位または1グループ単位のため。

**キーフレーム移動スクロール**  

**常に時間移動するトラックパッド上部スクロール**  

**カットのサムネイル導入**  
タイムラインを縮小するとサムネイル表示になるように設計する。

**カット分割設計**  
カットもキーフレームのように分割するように設計する。ただし、対になる接合アクションが必要。

## 再生
**PlayView**  
再生中のとき、isPlayingでの分岐をやめて、CutViewの上にPlayViewを配置する。

**再生ビューの分離**  
同時作業を可能にする。

**再生中のタイムライン表示更新**  

**再生中の時間移動**  


## コマンド
**コマンドヘルプ実装**  
HELP.mdの記述を利用する（HELP.mdはコマンドヘルプ及びGUIのヘルプ表示を作成後に廃止）。

**コマンドハイライト、無効コマンドの編集無効表示**  

**表示範囲内でのコマンド適用**  

**コマンド数を減らす**  
設計を根本的に変更しないといけないところがいくつかあり、習慣化の問題もあるため、消極的。

**ショートカットキー変更可能化**  
左利きのための設定を導入するなど。

**頻度の少ないコマンドをボタンまたはプルダウンボタン化**  

**コマンドのモードレス性の向上**  
コピー・ペースト対応の範囲を拡大。


## シーン
**サイズとフレームレートの自由化**  

**書き出しの種類を増やす**  

**DCI-P3色空間**  

**リニアワークフロー**  
移行した場合、「スクリーン」は「発光」に統合。


## その他のGUI
**クローン実装**  

**Union選択**  
選択の結合を明示的に行う。

**コピーオブジェクト表示**  

**コピーUndo**  

**パネルにindication表示を付ける**  
消極的。

**カーソルが離れると閉じるプルダウンボタン**  

** スロー操作時の値の変更を相対的にする** 

**ラジオボタンの導入**  

**ボタンの可視性の改善**  

**スクロールの可視性の改善・位置表示**  
元の位置までの距離などを表示。

**「調べる（QuickLook）」ジェスチャー**  

**トラックパッドなしでの対応**  
消極的。

**ペン入力デバイスでのクリック選択を廃止**  
トラックパッド操作とペン操作を完全に分けることも検討。可能な場合、トラックパッドでのドラッグを「移動」アクションに割り当てる。

**トラックパッドの環境設定を無効化**  
OSの環境設定によらず、いつでも同じジェスチャーで行えるようにする。ただ、感圧トラックパッドとの違いなどで問題が出る可能性あり。

**書き出し時間表示の精度を改善** 

**ファイルシステムのモードレス化**  

**音楽（シーケンサー）・効果音**


## ソースコードの修正

**Swift4への対応**  

**汎用性、モードレス性に基づいたオブジェクト設計にする**
ある特定の処理のためだけに設計したオブジェクトをすべて排除する。

**描画高速化**  
GPUを積極活用するように再設計する。Metal APIを利用する予定。

**CutViewのCutを不変にしてCutViewを時間に合わせて入れ替える**  

**SceneView関連の時間Undo未実装**  

**カット単位での読み込み**  

**安全性の高いデータベース設計へ移行する**  
保存が途中で中断された場合に、マテリアルの保存が部分的に行われていない状態になってしまうのを防ぐ。

**強制アンラップの抑制**  

**guard文**  

**CALayerのdrawsAsynchronouslyのメモリリーク**  
GPU描画に変更する。

**SceneViewDelegate実装**  
viewのカプセル化を強める。

**モデルのカプセル化を強める**  

**二次ベジェ曲線の長さの解析解**  
二次ベジェ曲線は廃止する可能性があり、消極的。

**保存高速化**  

**安全なシリアライズ**  
NSObject, NSCodingを取り除く。Swift4のCodableを使用することを検討中。

**Collectionプロトコル**  
allCellsやallBeziers、allEditPointsなど。

**privateを少なくし、関数のネストなどを増やす**  

**TimelineViewなどをリファクタリングする**  

**ProtocolなView**  

**永続データ構造に近づける**  

**Main.storyboard, Localizable.strings, Assets.xcassetsの廃止**

**Cocoa脱却** 