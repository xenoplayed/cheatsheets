    ansible -i inventory/hosts all -b -m shell -a "uptime"    # runs command uptimes on all nodes

    ansible all -m ansible.builtin.user -a "name=test01 password={{ 'test' | password_hash('sha512', 'mysecretsalt')}}" -u pi --become
