無料枠のt3.microでssh可能な環境をまとめて作成する

<img src=https://user-images.githubusercontent.com/45380191/146376500-c9556f47-7e22-4b2d-8a8d-daa3b92b008a.png width=400>

# 目的
- AWS CloudFormationを使用して開発環境を作成するymlファイルを作成する
- terraformでこれら環境は作成したが、Cfnは初見になる
- EC2にローカル環境からsshができる環境を作成する

# 準備
- 以下のurlを参考にsshする際必要になるKeyPairを作成し、pemファイルをDLしておく
https://docs.aws.amazon.com/ja_jp/servicecatalog/latest/adminguide/getstarted-keypair.html
- SGにsshポートの接続設定を付与するためターミナルからローカル（接続するPC）のグローバルIPを確認する
`curl inet-ip.info`

# 基本的な内容
- VPC、subnet...など基本的なネットワークの構成
- EC2を作成する
- 任意のローカルIPからSSHできるSGの作成
