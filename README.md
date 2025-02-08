# Ansible shooting range display automation
Automated management of shooting range displays for [Jagabluat Irlbach e.V.](https://www.jagabluat-irlbach.com/) using [Ansible](https://github.com/ansible/ansible). The displays visualize results based on [Meyton](https://meyton.info/) measuring frames.

## Prerequisits
- Ansible
- ssh access to the Raspberry Pis

## Inventory groups
- `standard`: Raspberry Pis that are always in use to display websites kiosk mode.
- `replacement`: Raspberry Pis that are used for replacement if there are technical issues with devices of the standard group. The replacement devices do not automatically start chromium in kiosk mode.

## Playbooks
- [ping](./playbooks//ping.yml): Pings Raspberry Pis
- [setup](./playbooks/setup.yml): Setups Raspberry Pis to display website in kiosk mode
- [setup_replacement](./playbooks/setup_replacement.yml): Setups Raspberry Pis to display website
- [update](./playbooks/update.yml): Updates Raspberry Pis
- [reboot](./playbooks/reboot.yml): Reboots Raspberry Pis

## Usage examples
### Ping standard group:
```sh
$ ansible-playbook -i inventory.yml -e 'group=standard' playbooks/ping.yml
```
### Setup standard group:
```sh
$ ansible-playbook -i inventory.yml playbooks/setup.yml
```

### Setup replacement group:
```sh
$ ansible-playbook -i inventory.yml playbooks/setup_replacement.yml
```

### Update replacement group:
```sh
$ ansible-playbook -i inventory.yml -e 'group=replacement' playbooks/update.yml
```

### Reboot all:
```sh
$ ansible-playbook -i inventory.yml -e 'group=all' playbooks/reboot.yml
```