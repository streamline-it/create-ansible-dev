Role Name
=========

This role creates an Ansible developement environment. It creates environment variable(s) for Ansible.  It also creates developement directory under user's Documents directory.  Lastly it create's a vimrc file catered to Ansible editing under VIM.

Requirements
------------


Role Variables
--------------

# defaults file for create-ansible-dev

create_ansible_dev_users:
  - name:
    shell:
    homedir:
    wallpaper: 
    devuser_src_key_path:
    devuser_priv_key_file:
    devuser_pub_key_file:

# directories to create for ansible developement
create_ansible_dev_directories:
  - Documents/ansible_dev/playbooks

# environment variable(s) to create
create_ansible_dev_env_vars_line:
  - "export ANSIBLE_FORCE_COLOR=True"

# other pub/private keys to add
create_ansible_dev_env_misc_keys:
  - username:
    user_home_dir:
    priv_key_filename:
    pub_key_filename:
    key_dest_dir:
    key_src_dir:
    mode: 

# hold /home/<user>/.ssh/config values to allow user
# of keys such as github keys
create_ansible_dev_env_ssh_user_config:
  - username: 
    config_filepath: 
    host_domain:
    host_name:
    identity_file:


Vars section

# used to create user aliases etc
create_ansible_dev_filepaths:
  - shell: bash
    vim_src: vimrc_bash
    vim_dest: ".vimrc"
    env_file: ".bashrc"
  - shell: bourne
    vim_src: vimrc_bourne
    vim_dest: "vimrc"
    env_file: ".profile"



FreeBSD.yml

create_ansible_dev_additional_pkgs:
  - git

RedHat.yml

create_ansible_dev_additional_pkgs:
  - git
  - git-core
  - git-core-doc
Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - create-ansible-dev

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).


