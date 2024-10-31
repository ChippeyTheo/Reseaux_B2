# TP5 INFRA : Intégration

## I. Tester

**🌞 Récupérer l'application dans la VM hosting.tp5.b1**

```shell
[theo@localhost ~]$ curl -O https://gitlab.com/it4lik/b2-network-2024/-/raw/main/tp/net/5/server.py?inline=false
```

**🌞 Essayer de lancer l'app**

```shell
[theo@localhost ~]$ python server.py
[theo@localhost ~]$ ss -lutnp
Netid   State    Recv-Q   Send-Q     Local Address:Port      Peer Address:Port  Process                                                                                     
tcp     LISTEN   0        1                0.0.0.0:13337          0.0.0.0:*      users:(("python",pid=1425,fd=3))  
```

**🌞 Tester l'app depuis hosting.tp5.b1**

changer le bash du server : sudo vim /etc/passwd  pas nessessaire d'avoir un shell bash un nologin est tres bien 
definir un user pour le service sinon c'est root automatiquement pas bien 
firewall filtrer les sorties pour empecher les connections extérieurs. un server ne doit rien laisser sortir
syscalls : "strace" --> cmd 

SystemCallFilter= white list les syscalls autorisé
SystemCallFilter=~ black list les syscalls que l'ont empeche

dans important :
[Service]
User=
SystemCallFilter=