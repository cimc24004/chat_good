# chat_good

Ruby on Railsで制作した、ルーム形式のリアルタイムチャットアプリです。ルーム内でメッセージを送ったり、特定のメッセージに返信したりできます。メッセージの投稿・編集・削除や通知の反映に、RailsのAction Cableを使っています。

## 実装の見どころ

**接続ユーザーの識別、ルームの購読、メッセージの配信を分離**しています。WebSocket接続時にログインユーザーを識別し、ルームごとに配信先を分けます。メッセージの配信はジョブに切り出し、受信側はページを再読み込みせずに新着を確認できます。

- [connection.rb](app/channels/application_cable/connection.rb)：接続時にログインユーザーを識別
- [room_channel.rb](app/channels/room_channel.rb)：ルームへの購読と投稿処理
- [message_broadcast_job.rb](app/jobs/message_broadcast_job.rb)：投稿されたメッセージを対象ルームへ配信
- [message_notification_job.rb](app/jobs/message_notification_job.rb)：対象ユーザーに通知を配信

## 使用技術

Ruby / Ruby on Rails / Action Cable / JavaScript
