## 使い方  

### 準備  
inventory.ini.exampleをコピーしてinventory.iniを作成。
[target]にnfsサーバーを設置するホストを記述する。
[clients]にはnfsサーバーに接続するホストを記載する。

roles/install-server/files/allowed_ports.yml.example
をコピーしてallowed_ports.ymlを作成します。
nfsサーバーではデフォルトでipが固定されない通信が発生するようなので(mountd, lockdなどで)
このファイルのポートを編集して任意のポートに固定してください。ポートの開放はプレイブックないで行われます。

playbook.yml内の  
```playbook.yml
vars:  
  nfs_dir_path: /export/shared  
```
を変更するとマウント先のディレクトリを変更できます。  


### 実行  
プロジェクトルートで  
ansible-playbook -i inventory.ini playbook.yml  
を実行するとnfs-kernel-serverが設置され、クライアントにはnfs-commonがインストールされます。

クライアント側で  
sudo mount -t nfs [server_ip]:/path/to/nfsdir /path/to/mountdir  
でマウントできるか確認してください。