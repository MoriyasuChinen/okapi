# OKAPI - Polygonal Gcode Design
### OKAPIはRhinoceros+Grasshopper用のGcode作成ツールです。  
ポリゴンメッシュに基づいたツールパス生成クワッドメッシュの輪郭線に基づいてツールパスを定義することでNon-Planar3Dプリント用の複雑なツールパスの生成が可能です。
詳細はこちらの卒業論文を参照ください。( http://fab.sfc.keio.ac.jp/paper/files/2022_MoriyasuChinen.pdf )
<div align="center">
  <img src="https://github.com/user-attachments/assets/ec503611-b480-442c-af85-1c586d06177c" width="30%">
  <img src="https://github.com/user-attachments/assets/765811cb-c92b-4da8-bb61-defac346b9fe" width="30%">
  <img src="https://github.com/user-attachments/assets/d8c81162-db2b-4433-9e50-62b1759a58c5" width="30%">
</div>


![_OKAPIを利用したツールパス生成のワークフロー](https://github.com/user-attachments/assets/0a215ed9-8a13-47fe-ae22-9f6e75c6ad95)
_OKAPIを利用したツールパス生成のワークフロー_  



## ライセンス

- 本ツール（OKAPI）は、個人利用および研究目的での使用を想定して公開されています。 商用利用（営利目的での使用、販売、サービス提供等）は禁止 されていますので、ご理解の上ご利用ください。

## OKAPIの動作環境
Windows版Rhinoceros7（8は動作未検証になります）

## 3Dプリンタのセットアップ
- 本ツールはスタートコードとエンコードを調整することで一般的な卓上3Dプリンタでの利用が可能です。（動作確認済み機種：Ender3,Ender5,ZonestarZ8T)
- Non-Planar3Dプリントではノズルを上下方向に動かしながら造形を行うため長いノズルを利用する必要があります。
-  必要に応じてノズルの入手と3Dプリンタのセットアップを行ってください。Non-Planar3Dプリント用ノズル（ https://www.nonplanar.xyz/ ）

## 開発状況
本ツールは筆者が2022年に取り組んだ卒業研究において製作したものをベースとして、一般公開可能な形にアレンジしたものになります。すでに開発を止めているため、致命的な不具合以上のアップデートは予定していないことをご容赦ください。


## OKAPIの導入方法

### 1. 必要なプラグインをインストールする
- Telepathy (https://www.food4rhino.com/en/app/telepathy)
- Human UI 0.8.1.3 (https://www.food4rhino.com/en/app/human-ui)
- jSwan 1.2  (https://www.food4rhino.com/en/app/jswan)
- Pufferfish 3.0.0 (https://www.food4rhino.com/en/app/pufferfish)

※プラグインのインストール方法はこちらの記事を参考にしてください。
- https://www.applicraft.com/qanda/rhinoceros/gh_plugin_install/
- https://mt-grasshopper.blog.jp/archives/9106036.html

### 3. ダウンロード
本画面の右上のCodeからZipファイルをダウンロードしてください。
![image](https://github.com/user-attachments/assets/6cdb8e41-7abf-41a0-9945-d5a7441deb42)



## 使い方

### 1. サンプルファイルの読み込み
okapi.ghファイルをRhinocerosで開くとUIパネルが表示されます。
![image](https://github.com/user-attachments/assets/7971b15d-efb7-48b9-95fc-21c52e4551da)
- ①を選択すると、ファイルの読み込み画面が表示されます。ダウンロードファイルに同梱されているsampleTorso.objを選択すると画像のように読み込まれます。
![image](https://github.com/user-attachments/assets/4a426ba6-b847-4c02-bc0d-0b25a3ccc536)
- ③Bakeをクリックし、Bakeされたモデルを赤枠で囲われたエリアに移動します。
  この位置に基づいてスライスが行われますが、書き出し工程で位置の微調整が可能であるため、大まかな位置決めで問題ありません。
![image](https://github.com/user-attachments/assets/3729797f-af46-4e69-86ef-a07d6ac29db3)

### 2. スライス
スライス方式がNon-Planarになっていることを確認した上で輪郭抽出をクリックします。  
![image](https://github.com/user-attachments/assets/b2031c53-6cb6-4c91-bc2d-d70c7c06a42b)  
  

Rhinocerosのコマンドライン上に下図①～④に対応するダイアログが表示されるので、該当箇所を選択します。
![image](https://github.com/user-attachments/assets/e2ef85ea-1bb2-4668-961f-80c01322c9d4)

成功すると抽出されたツールパスが表示されます。
![d7469fc510b7879d1940bdb208a2b61c](https://github.com/user-attachments/assets/1885035b-10e5-4af3-aa8c-8da1977e568f)

レンダリングプレビューにすると、積層痕をシミュレーションして見ることが出来ます。
レイヤーピッチが高すぎる場合は最大レイヤーピッチ(mm)を調整することで制御出来ます。  
（詳細はP.52 http://fab.sfc.keio.ac.jp/paper/files/2022_MoriyasuChinen.pdf )
<div style="display: flex; justify-content: center; gap: 10px;">
  <img src="https://github.com/user-attachments/assets/67944c3b-faae-419d-88e5-7920c819c60e"  style="max-width: 100%; height: auto; flex: 1;">
  <img src="https://github.com/user-attachments/assets/7b36cf08-780b-4e4b-8202-c995e4a9a472"  style="max-width: 100%; height: auto; flex: 1;">
</div>

### 3. テクスチャ編集
網目模様とランダム模様のテクスチャを付与することが出来ます。
網目の間隔はポリゴンメッシュの縦線の間隔に依存しています。
![image](https://github.com/user-attachments/assets/b5e53eeb-b659-462e-81ba-4c07f747db59)

### 4. 書き出し
この工程で一般的なスライサーと同様にプリントの設定を行います。  
※ender3以外のプリンターを利用してる方はStart Script とEnd Scriptを必ず書き換えてください。  
※温度設定はマニュアル操作となります。

プロジェクト名と保存先を入力した上でexportをします。  
指定した場所にプロジェクトフォルダが作られ、gcodeと設定ファイルが格納されます。  
![image](https://github.com/user-attachments/assets/645fd214-6ea5-4e5b-9a07-25da3c6ebd03)  
設定ファイルはExportパネルのSettingから読み込むことが出来ます。  
![image](https://github.com/user-attachments/assets/e889a2aa-415e-4489-b84f-976798919ab0)  


### モデルの作成方法
（詳細はP.52 http://fab.sfc.keio.ac.jp/paper/files/2022_MoriyasuChinen.pdf )

