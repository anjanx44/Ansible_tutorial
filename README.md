# Ansible_tutorial
### Run a ansible playbook file
-----------------------------
ansible-playbook -i staging day1/check_blade_status.yml

Regular expression serarch for one time
---------------------------------------
```
- name: Get some info
  set_fact:
    some_info: "{{ result.stdout | regex_search(regex_var) }}"
```

Make a list using new line
----------------------------
```
- set_fact: var_list="{{plain_var.split('\n')}}"
```
https://stackoverflow.com/questions/43224436/splitting-variable-not-working-in-ansible

How to add new item into lists using loop
------------------------------------------
```
- set_fact:
    kk_list: "{{ kk_list | default([]) + [another_var | regex_search(item)] }}"
  loop: '{{loop_var}}'
```
https://blog.crisp.se/2016/10/20/maxwenzin/how-to-append-to-lists-in-ansible

Calculate and add new item a list
---------------------------------
https://stackoverflow.com/questions/44673615/ansible-add-integer-value-to-a-list

code:
```

- set_fact:
    list2: "{{ list2 | default([]) + [nib_blade_active | regex_search(item)] }}"
  loop: '{{nib_running_blade_regexp}}'
```
difference two list and create one like error list
--------------------------------------------------
```

- name: Create error list
  set_fact:
    error_list: "{{ current_situation | difference(expected_situaltion) }}"
```
Jinja2: Change the value of a variable inside a loop
-----------------------------------------------------
Try also dictionary-based approach. It seems to be less ugly.
```
{% set vars = {'foo': False} %}

{% for item in items %}
  {% if vars.update({'foo': True}) %} {% endif %}
  {% if vars.foo %} Ok(1)! {% endif %}
{% endfor %}

{% if vars.foo %} Ok(2)! {% endif %}```

```
This also renders:
```
Ok(1)!
Ok(2)!
```
