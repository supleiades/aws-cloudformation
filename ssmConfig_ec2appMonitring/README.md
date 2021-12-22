## 目的
- インスタンスに特定のアプリがあるかどうか監視する


## 必要な作業(GUI想定)

1. ssmフリートマネージャーの一覧に対象EC2インスタンスが表示されること
1. ssmインベントリのセットアップイベントリで、で作成
    | 項目 | パラメータ |
    | :--- | :------- |
    | ターゲット | このアカウントのすべてのマネージドインスタンスの選択 |
    | スケジュール | 30分 |
    | パラメータ | Applications のみ指定 |
1. Configルールを作成する
    | 項目 | パラメータ |
    | :--- | :------- |
    | マネージドルール | ec2-managedinstance-applications-required |
    | トリガー/リソースタイプ | AWS SSM ManagedInstanceInventory |
    | パラメータ/applicationNames | {インストール済みとして認識させたいアプリ} | 
1. 作成したルールを選択し、「修復の管理」からインストールされていない場合のアクションを作成
    | 項目 | パラメータ |
    | :--- | :------- |
    | 修復アクション | AWS-PublishSNSNotification |

## 参考
[（classmethod）EC2インスタンスに特定アプリケーションがインストールされているかチェックして通知する](https://dev.classmethod.jp/articles/config-rule-ec2-application-check-and-sns-publish/)
[ (classmethod) CloudFormationで作ったSNSトピックのメール送信先が手動変更されてたので整理した話](https://dev.classmethod.jp/articles/cloudformation-sns-topic-manual/)