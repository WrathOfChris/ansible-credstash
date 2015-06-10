# ansible-credstash
Ansible module for LuminalOSS/credstash

## Testing

```
credstash put testkey testsecret
ansible-playbook -i inventory/local test.yml
```

## Example

Calling credstash as a local action:

```
- name: Credstash secrets test
  connection: local
  hosts: localhost
  gather_facts: false
  vars:
  - region: "us-east-1"
  tasks:
  - local_action:
      module: credstash
      region: "{{region}}"
      unsafe: true
  - debug: msg="{{credstash.testkey}}"
```

Test Run

```
$ ansible-playbook -i inventory/local -e region=us-west-2 test.yml

PLAY [Credstash secrets test] *************************************************

TASK: [credstash] *************************************************************
ok: [127.0.0.1 -> 127.0.0.1]

TASK: [debug msg="{{credstash.testkey}}"] *************************************
ok: [127.0.0.1] => {
    "msg": "testsecret"
}

PLAY RECAP ********************************************************************
127.0.0.1                  : ok=2    changed=0    unreachable=0    failed=0
```
