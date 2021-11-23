# pulp_builder
attempt to write an ansible-role that encapsulates pulp3 specifica only.
While trying and reading through [pulp_installer](https://github.com/pulp/pulp_installer) I have  
been wondering if it's possible to have a role, which encapsulates the pulp specifica as ellegantly as  
eg [geerlingguy.postgresql](https://github.com/geerlingguy/ansible-role-postgresql).

## description of what I like in geerlingguy.postgresql
* `tasks/variables.yml` watches over all variables that have defaults and can be changed by os-specific-vars.yml
* `vars/os-specific-vars.yml's` translate os specific path's and packaga-names into variables that have meaning to role's tasks.
* `tasks/setup-os.yml's` handle os specific preperation/quirks to move them out of the way of the role's goals.
* `tasks/initialize.yml` converts the global/default/os-default/user-defined vars into facts.
  * role tasks can thereafter be restrained from running function-like evaluations based special o/s knowledge.
* `tasks/configure.yml` watches over what config is done. If role tasks needs something or has conflicts it can be settled in this file.
* The clever use of import_tasks vs include_tasks in the post-tasks (I am refering to users.yml,databases.yml,users_props.yml)
  * importing those tasks rather than including them, signifies that instead of depending on evaluations made during playbook run, they are building on idempotency guarantees made by the role.
  * that's why they can be `imported`.


