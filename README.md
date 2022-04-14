# ansible-sshkeys
This is a simple playbook that copies your public SSH keys to remote systems, you could use this either with a public key already on the system or specify the password via the `-e` parameter below.

[![GA](https://github.com/sadsfae/ansible-sshkeys/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/sadsfae/ansible-sshkeys/actions)

### Setup

* Clone Ansible repository
```
git clone https://github.com/sadsfae/ansible-sshkeys
cd ansible-sshkeys
```

* Add the names of your servers to the inventory file under the servers inventory group.

```
vi hosts
```

```
[servers]
host01.example.com
host02.example.com
```

* By default this will copy `id_rsa.pub` found in your local user home directory where you run Ansible.

* Add any additional public SSH keys as needed
  - copy (append) your pubkey to ```install/roles/sshkeys/files/authorized_keys```
```
cat ~/.ssh/id_dsa.pub >> install/roles/sshkeys/files/authorized_keys
```

### Running the Thing

  - Run playbook, pass `-e "ansible_ssh_pass=PASSWORD"` for the default root password.

```
ansible-playbook -i hosts install/sshkeys.yml -e "ansible_ssh_pass=PASSWORD"
```

  - Alternatively, if you already have your public key on remote systems but want to copy a bunch of other keys then just run `ansible-playbook` without the `-e` parameter.

