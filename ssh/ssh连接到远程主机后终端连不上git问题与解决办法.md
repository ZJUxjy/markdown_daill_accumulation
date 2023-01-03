
问题描述：ssh连接到远程ubuntu后ssh的终端连github出现`git@github.com: Permission denied (publickey).`，也就是拒绝了连接。但是ubuntu上本地终端连git却没有问题。

解决方式：
用`ssh -T -v git@github.com`连github的同时查看debug信息
得到
```
OpenSSH_8.9p1 Ubuntu-3, OpenSSL 3.0.2 15 Mar 2022
debug1: Reading configuration data /home/jingyao/.ssh/config
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: /etc/ssh/ssh_config line 19: include /etc/ssh/ssh_config.d/*.conf matched no files
debug1: /etc/ssh/ssh_config line 21: Applying options for *
debug1: Connecting to github.com [20.205.243.166] port 22.
debug1: Connection established.
debug1: identity file /home/jingyao/.ssh/id_rsa type -1
debug1: identity file /home/jingyao/.ssh/id_rsa-cert type -1
debug1: identity file /home/jingyao/.ssh/id_ecdsa type -1
debug1: identity file /home/jingyao/.ssh/id_ecdsa-cert type -1
debug1: identity file /home/jingyao/.ssh/id_ecdsa_sk type -1
debug1: identity file /home/jingyao/.ssh/id_ecdsa_sk-cert type -1
debug1: identity file /home/jingyao/.ssh/id_ed25519 type -1
debug1: identity file /home/jingyao/.ssh/id_ed25519-cert type -1
debug1: identity file /home/jingyao/.ssh/id_ed25519_sk type -1
debug1: identity file /home/jingyao/.ssh/id_ed25519_sk-cert type -1
debug1: identity file /home/jingyao/.ssh/id_xmss type -1
debug1: identity file /home/jingyao/.ssh/id_xmss-cert type -1
debug1: identity file /home/jingyao/.ssh/id_dsa type -1
debug1: identity file /home/jingyao/.ssh/id_dsa-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_8.9p1 Ubuntu-3
debug1: Remote protocol version 2.0, remote software version babeld-456f9bbd
debug1: compat_banner: no match: babeld-456f9bbd
debug1: Authenticating to github.com:22 as 'git'
debug1: load_hostkeys: fopen /home/jingyao/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ssh-ed25519
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: SSH2_MSG_KEX_ECDH_REPLY received
debug1: Server host key: ssh-ed25519 SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU
debug1: load_hostkeys: fopen /home/jingyao/.ssh/known_hosts2: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts: No such file or directory
debug1: load_hostkeys: fopen /etc/ssh/ssh_known_hosts2: No such file or directory
debug1: Host 'github.com' is known and matches the ED25519 host key.
debug1: Found key in /home/jingyao/.ssh/known_hosts:1
debug1: rekey out after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey in after 134217728 blocks
debug1: Will attempt key: /home/jingyao/.ssh/id_rsa 
debug1: Will attempt key: /home/jingyao/.ssh/id_ecdsa 
debug1: Will attempt key: /home/jingyao/.ssh/id_ecdsa_sk 
debug1: Will attempt key: /home/jingyao/.ssh/id_ed25519 
debug1: Will attempt key: /home/jingyao/.ssh/id_ed25519_sk 
debug1: Will attempt key: /home/jingyao/.ssh/id_xmss 
debug1: Will attempt key: /home/jingyao/.ssh/id_dsa 
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519-cert-v01@openssh.com,ecdsa-sha2-nistp521-cert-v01@openssh.com,ecdsa-sha2-nistp384-cert-v01@openssh.com,ecdsa-sha2-nistp256-cert-v01@openssh.com,sk-ssh-ed25519-cert-v01@openssh.com,sk-ecdsa-sha2-nistp256-cert-v01@openssh.com,rsa-sha2-512-cert-v01@openssh.com,rsa-sha2-256-cert-v01@openssh.com,ssh-rsa-cert-v01@openssh.com,sk-ssh-ed25519@openssh.com,sk-ecdsa-sha2-nistp256@openssh.com,ssh-ed25519,ecdsa-sha2-nistp521,ecdsa-sha2-nistp384,ecdsa-sha2-nistp256,rsa-sha2-512,rsa-sha2-256,ssh-rsa>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey
debug1: Next authentication method: publickey
debug1: Trying private key: /home/jingyao/.ssh/id_rsa
debug1: Trying private key: /home/jingyao/.ssh/id_ecdsa
debug1: Trying private key: /home/jingyao/.ssh/id_ecdsa_sk
debug1: Trying private key: /home/jingyao/.ssh/id_ed25519
debug1: Trying private key: /home/jingyao/.ssh/id_ed25519_sk
debug1: Trying private key: /home/jingyao/.ssh/id_xmss
debug1: Trying private key: /home/jingyao/.ssh/id_dsa
debug1: No more authentication methods to try.
git@github.com: Permission denied (publickey).
```
可以看到，`debug1: Trying private key: /home/jingyao/.ssh/id_rsa`这一句在找这个路径下*id_rsa*这个文件，但是我打开这个路径却找不到这个文件，于是我将这个路径下另一个key文件重命名为*id_rsa*，再次连接，连上了，问题得到了解决。