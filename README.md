Ansible role to replace all the foreman parameters of a host in Satellite/Foreman with different ones. 
Has no effect on inherited parameters (Global, domain, hostgroup etc) 

Useful for setting a "flagging" parameter such as "ansible_controlled_soe" for example. 

Call from your playbook like so: 
- name: Tell satellite to set parmeter list to only ansible_controlled_soe
      include_role:
        name: satellite-parameters
      vars:
        rolevar_fqdn: "{{ var_prov_hostname }}.{{ var_prov_domain}}"
        rolevar_list_of_dicts_with_name_and_value_fields_each:
          - name: ansible_controlled_soe
            value: true

You can now use 
`variables.icontains:ansible_controlled_soe`
as an Ansible Tower Smart Host Filter, to narrow down your Satellite-sourced dynamic inventory just to the hosts with the flagging parameter.
