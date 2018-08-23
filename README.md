Encryption:

```
read -s pwd; pwd=${pwd} dk=$(cryptocli scrypt -in env:pwd -rounds $((1<<20))) sh -c 'tar -czf - htb | cryptocli aes-gcm-encrypt -derived-salt-key-in env:dk -out htb.tgz.enc'
```

Decryption:

```
read -s pwd; pwd=${pwd} cryptocli aes-gcm-decrypt -in htb.tgz.enc -derived-salt-key-in pipe:"cryptocli scrypt -in env:pwd -rounds $((1<<20)) -salt-in env:SALT" | tar -zvtf -
```

