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
| instanceCent6-64bit_ssm_inspector.yml | centos6.9にuserdataを利用してssmAgentインストール＆セッションマネージャーで接続確認完了 |

### instance_ssm_inspector.yml
- インストーラー

| No | OS | ダウンロードリンク |
| :- | :- | :- |
| 1 | Cent8-Intel64, Cent7-Intel64 | https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_amd64/amazon-ssm-agent.rpm |
| 2 | Cent8-arm64, Cent7-arm64 | https://s3.region.amazonaws.com/amazon-ssm-region/latest/linux_arm64/amazon-ssm-agent.rpm |
| 3 | Cent6-Intel64 | https://s3.region.amazonaws.com/amazon-ssm-region/3.0.1390.0/linux_amd64/amazon-ssm-agent.rpm |
| 4 | Cent6-Intel32 | https://s3.region.amazonaws.com/amazon-ssm-region/3.0.1390.0/linux_386/amazon-ssm-agent.rpm |

- パラメータ
  - AMIOSバージョン
    - ["CentOS 6.x", "CentOS 7.x", "CentOS8.x"]
  - AMIcpuタイプ
    - ["Intel 64-bit (x86_64)", "ARM 64-bit (arm64)", "Intel 32-bit (x86)"]

- 分岐

| OS | CPU | インストーラーNo |
| :- | :- | :- |
| "CentOS8.x" | "Intel 64-bit (x86_64)" | 1 |
| "CentOS8.x" | "ARM 64-bit (arm64)" | 2 |
| "CentOS7.x" | "Intel 64-bit (x86_64)" | 1 |
| "CentOS7.x" | "ARM 64-bit (arm64)" | 2 |
| "CentOS6.x" | "Intel 64-bit (x86_64)" | 3 |
| "CentOS6.x" | "Intel 32-bit (x86)" | 4 |


## 備考


