# Ansible_tutorial
Make a list using new line
----------------------------
- set_fact: var_list="{{plain_var.split('\n')}}"
https://stackoverflow.com/questions/43224436/splitting-variable-not-working-in-ansible

How to append to lists in Ansible
-----------------------------------
https://blog.crisp.se/2016/10/20/maxwenzin/how-to-append-to-lists-in-ansible

Calculate and add new item a list
---------------------------------
https://stackoverflow.com/questions/44673615/ansible-add-integer-value-to-a-list

code:
- set_fact:
    list2: "{{ list2 | default([]) + [nib_blade_active | regex_search(item)] }}"
  loop: '{{nib_running_blade_regexp}}'
