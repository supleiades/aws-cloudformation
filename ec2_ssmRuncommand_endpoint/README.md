# 要件
- ec2を作成する
- ec2への接続はssmセッションマネージャーから行う
- ssmから接続できるようにする
- ssmのrunCommandをec2に実行する

## files discription
| ファイル名 | 説明 |
| :- | :- |
| main.yml | VPC,PrivateSubnet,RT,EC2,Endpoint用SG,Endpoint(ssm系:3,s3:1)を作成 |
| main_excludeVpc.yml | main.ymlよりVPC作成のみを除外したコード |
| instance_ssm_inspector.yml | EC2作成,SsmRunCommandよりInspectorエージェントインストール実行 |
## 備考
