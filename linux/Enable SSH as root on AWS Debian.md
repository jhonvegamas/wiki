 ssh -i server.pem admin@remote-server.com
 
 Edit authorized_keys File
 
 ```diff
- no-port-forwarding,no-agent-forwarding,no-X11-forwarding,command="
- echo 'Please login as the user "ubuntu" rather than the user "root".';
- echo;sleep 10" 
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCPqJ2U4gidqek
  4FPQJABENkrUiLVP61LObdFAZXvs2EpCf/nBQCRg4ykMNg+8TC9lb7jC65zfIrTUcNcwongDb4
  3k6miSKu1M8fdqXDpcb8CdDRaKpM2wP8l+hTaJ2aWycXmGJ7lZKQPiwNUOhbrOLNEtDmOI9eiV
  lz7See98LVLW+6AwfzNA8Cu4riDTvEMQr/WQ9NLrS3BZE1TAAswJi9lGDfTgEvfh4Ji+eI/xT
  Xrjkkwjerkjk3jrkwejrkjwe9wASXob4rbV12TXjQIcMKaRGQAGrwOHu0nM2ibfTdgqjrTAG
  03CXKzQhF09LdxKlT7GpYe0oVU2R1kjkejwQp tecadmin.net
```

Save File

ssh -i server.pem root@remote-server.com
