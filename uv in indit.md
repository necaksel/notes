# uv in indit

## UV_EXTRA_INDEX_URL
https://github.com/search?q=repo%3AOncoImmunity%2Fansible-server-automation+index+url&type=code
If we want to set it on the servers we can have oiml work out of the box.
Without any direnv.
See if you can figure that out.

https://github.com/OncoImmunity/ansible-server-automation/tree/f935f1b563f88490b18cd42ee6428c06eb25d140
Could even install uv on all the servers?
And set the token for uv.

https://adamj.eu/tech/2024/09/18/python-uv-development-setup/
Uv pre commit hook and uv for tox.
Showt how he uses uv to install python vi ansible

Got an intro to [[ansible-server-automation]] from which has an example
of how to do what I want for setting this on the servers.
It might fail to run due to the deadsnakes apt error.


Sets the `UV_INDEX` env var that uv needs to read our gemfury packages.
With this I have what I need to enable uv in indit.

I wanted to also install uv on all of the servers, but had trouble deciding how to install uv.
The uv installer is the most appealing option on https://docs.astral.sh/uv/getting-started/installation/, because with that we can run `uv self update`. Uv is under very active
development so it would be nice to be able to update easily.
The installer does a local install by default to `~/.local/bin/uv, running the installers
for all users on all servers to install and update uv feels a bit bonkers (but maybe it isn't?).

In the end I'm happy with just the index env var being set now, that simplifies all the uv
commands and we can do local installs of uv in the indit team now to see how it works first.



Commit message for my attempt at a script.
```diff
    Add task to install uv
    
    This installs uv with the install script.
    Uv could also be installed vi apt or even
    via pip.
    I'm installing it via the install script
    because this enables running `uv self update`
    https://docs.astral.sh/uv/reference/cli/#uv-self-update
    which is not availabe if installed vi pip or apt.
    
    Let me know if manging apt packages is better
    for some reason.
    I don't have experience with what the tradeoffs
    are when managing servers via ansible is.
    
    I haven't set up any task to update uv because
    I wanted to see if this would work before I add to it.
    But a regular update task seems nice to have.

new file   pip/tasks/install_uv.yml
@@ -0,0 +1,19 @@
+---
+- name: "Download UV installation script"
+  get_url:
+    url: https://astral.sh/uv/install.sh
+    dest: /tmp/uv_install.sh
+    mode: '0755'
+  become: true
+
+- name: "Install UV globally"
+  shell: /tmp/uv_install.sh
+  args:
+    creates: /usr/local/bin/uv
+  become: true
+
+- name: "Clean up installation script"
+  file:
+    path: /tmp/uv_install.sh
+    state: absent
+  become: true 
modified   pip/tasks/main.yml
@@ -1,4 +1,8 @@
 ---
+- name: "Install UV Package Manager"
+  include_tasks: install_uv.yml
+  loop: "{{ pip_users }}"
+
 - name: "Install PIP"
   include_tasks: user_config.yml
   loop: "{{ pip_users }}"
```