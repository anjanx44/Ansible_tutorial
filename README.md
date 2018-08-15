# Ansible_tutorial
install ansible using pip and any virsion
-------------------------------------------
```
pip install ansible==2.5
```
### Run a ansible playbook file
-----------------------------
```
ansible-playbook -i staging day1/check_blade_status.yml
```
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

{% if vars.foo %} Ok(2)! {% endif %}

```
This also renders:
```
Ok(1)!
Ok(2)!
```
https://stackoverflow.com/questions/9486393/jinja2-change-the-value-of-a-variable-inside-a-loop


OR operator in Ansible
------------------------
```
tasks:
  - name: "shut down CentOS 6 and Debian 7 systems"
    command: /sbin/shutdown -t now
    when: (ansible_distribution == "CentOS" and ansible_distribution_major_version == "6") or
          (ansible_distribution == "Debian" and ansible_distribution_major_version == "7")
```
AND operator in Ansible
-------------------------
```
tasks:
  - name: "shut down CentOS 6 systems"
    command: /sbin/shutdown -t now
    when:
      - ansible_distribution == "CentOS"
      - ansible_distribution_major_version == "6"

```
Find all match information from a variable/register using regular expression(regex_findall)
--------------------------------------------------------------------------------------------

```
- name: Get Information from remote machine
  set_fact:
    lookup_list: "{{ register.stdout | regex_findall(a_regular_expression) }}"
```

Test Commit
--------------------------------------------------------------------------------------------

