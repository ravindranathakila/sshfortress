# SSH-Fortress

## 1. What does it do?

1. Make your cluster servers be more safe by expose your SSH connection through SSH-Fortress server
2. Login your SSH server through the SSH-Fortress Web Interface and record all input and output history commands.
2. Manage your cluster server's SSH Account by SSH-Fortress with Web Account
3. Manage a server's files by SSH-Fortress's SFTP-web-interface
4. Easily login into your private Cluster by SSH Proxy provided by SSH-Fortress-Proxy


## 2. build and run
```bash
git clone https://github.com/mojocn/sshfortress.git && cd sshfortress;
go build
echo "run the app with SQLite database"
./sshfortress sqlite -v --listen=':3333'
echo "run the app with Mysql database, you need a config.toml file in your sshfortress binary folder"
./sshfortress run -v --listen=':3333'

```
### 2.1 config.toml
The config.toml file should in sshfortress binary folder.  config.toml works with command `sshfortress run`. Command `sshfortress sqlite` can run with the config file.

```toml
[app]
    name="frotress.mojotv.cn"
    addr=":8360"
    verbose= true
    jwt_expire=240 #hour
    secret="asdf4e8hcjvbkjclkjkklfgki843895iojfdnvufh98" #jwt secret
[db]
    # mysql database connection
    host = "127.0.0.1"
    user = "root"
    dbname = "sshfortress"
    password = "your_mysql_password"
    port = 3306

[github] #github.com OAuth2
    client_id="d0b29360a088d0c4dc18"
    client_secret="89b272eeb22f373d8aa688986a8dbbc4edbfc64a"
    callback_url="http://sshfortress.mojotv.cn/#/"
```
## 3. Online demo

[https://sshfortress.mojotv.cn/#/login](https://sshfortress.mojotv.cn/#/login)

just click the login button, the default password has input for you, user `admin@sshfortress.cn` password: `admin`,


## 4. Run With supervisor

sshfortress.ini
```ini
[program:sshfortress.mojotv.cn]
command=/data/sshfortress/bin/sshfortress sqlite
autostart=true
autorestart=true
startsecs=10
user=root
chmod=0777
numprocs=1
redirect_stderr=true
stdout_logfile=/data/sshfortress/supervisor.log
```

## 5. Reference

1. [idea from my another repo: libragen/felix](https://github.com/libragen/felix)
2. [How to run SSH-Terminal in browser](https://mojotv.cn/2019/05/27/xtermjs-go)