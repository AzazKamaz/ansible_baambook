# Ansible playbook to deploy baambook to some VPS

Ansible playbook allows to easily deploy [baambook](https://github.com/AzazKamaz/baambook) (written in Elixir) under Docker using Traefik as TLS Reverse Proxy with auto Let's Encrypt certificate acquiring & updating

Tested with Yandex.Cloud

## Guide
1. Install Ansible
2. Install Ansible requirements: `ansible-galaxy install -r ./requirements.yml`
3. Set some vars in `./hosts.yml`
4. Execute playbook: `ansible-playbook ./baambook.yml`

## Tips
- Ssh keys without password in one command: `ssh-keygen -t ecdsa -b 521 -f ./id_ecdsa -N ''`
- Yandex.Cloud cli cmd to create suitable vps: `yc compute instance create --name [NAME] --ssh-key ./id_ecdsa.pub --public-address [ADDRESS] --create-boot-disk type=network-ssd,size=16,image-id=fd8vgqmrilk8dchj1ccf` (16GB SSD with Ubuntu 20.04 LTS)
- Watch vps serial output to wait it to complete cloud-init: `watch -c "yc compute instance get-serial-port-output --name [NAME] | tail -n $(($LINES - 4))"`
