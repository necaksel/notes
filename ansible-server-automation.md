# ansible-server-automation
https://github.com/OncoImmunity/ansible-server-automation

Uses ![[Ansible]]

main.yaml is the main playbook.
This is run on merges to main and on sundays via a cron job.

[[Stian Lagstad]] says take ownership, feel free to rename and improve things.
[[Moritz von Stetten]] and stian tried to set up nix and deven recently.
This role could be a good example to copy if you need to set up an ansible role
https://github.com/OncoImmunity/ansible-server-automation/tree/main/setup-nix-devenv
It even has an ansible test https://github.com/OncoImmunity/ansible-server-automation/blob/main/setup-nix-devenv/molecule/default/verify.yml

Tasks can loop over things.
Fex the pip task loops over all `pip_user`s which executes script to set env vars for all users.

Ansible vault. Some things are encrypted.
Fex the `pip-keys.yaml` file which has all our users and their gemfury keys.

The readme links a guide for setting up gemfury tokens for new users https://neconcoimmunity.atlassian.net/wiki/spaces/OP/pages/1043202175/IT+on-boarding+flow#Create-gemfury-tokens-and-add-them-to-the-ansible-setup

