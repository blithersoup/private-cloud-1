# run
```
ansible-playbook ansible/install.yaml -i inventory -e @values.yaml --ask-become-pass 
```
# install

```
ansible-galaxy collection install community.kubernetes
```