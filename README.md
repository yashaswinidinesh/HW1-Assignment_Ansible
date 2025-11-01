# SJSU HW #1 — Ansible Web Server Deployment

**Student:** Yashaswini Dinesh

Deploy Nginx on **VM1** and **VM2** to serve `Hello World from SJSU-X` on **port 8080**.
Includes **deploy** and **undeploy** tags.

## Environment (used for this demo)
- Region: `us-west-2 (Oregon)`
- Key pair: `vm-key-hw1`
- Security Group: `sjsu-hw1-sg`
  - SSH (22) from *My IP*
  - SSH (22) from *This security group*
  - TCP **8080** from `0.0.0.0/0`

## Instance details
| Name | Instance ID | Public IPv4 | Private IPv4 |
|---|---|---|---|
| VM1 | i-01c18dbb5584e32d0 | 52.88.163.142 | 172.31.26.163 |
| VM2 | i-067569cfac2c58508 | 44.252.88.193 | 172.31.17.105 |

> Replace the instance values above if they change.

## Usage

### 1) Edit inventory
`inventory/hosts.ini` is already filled with VM2's **private** IP and message strings.
If VM2's private IP changes, update the `ansible_host` value.

### 2) Deploy
```bash
ansible-playbook site.yml --tags deploy
```

### 3) Verify
- VM1: http://52.88.163.142:8080
- VM2: http://44.252.88.193:8080

### 4) Undeploy
```bash
ansible-playbook site.yml --tags undeploy
```

## Notes
- The playbook uses a `meta: flush_handlers` before verify so nginx is reloaded before the check.
- `ansible.cfg` disables host key checking for convenience in this homework.
