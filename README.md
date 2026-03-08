Role Name
=========

This role creates an Ansible developement environment. It creates environment variable(s) for Ansible.  It also creates developement directory under user's Documents directory.  Lastly it create's a vimrc file catered to Ansible editing under VIM.

This role with work on RHEL 7 OS's and up along with FreeBSD hosts versions 13 and up.
Requirements
------------

None

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

Example below includes all options.  You can control those options through the following variables.


    create_ansible_dev_env_use_misc_keys - IF true specified keys will be copied

    create_ansible_dev_env_ssh_user_config: If true, an ssh user config will be created

    create_ansible_dev_env_clone_repos: If true git repos will be cloned.

- hosts: servers

  vars:

    create_ansible_dev_users:
      - name: rich
        shell: /bin/sh
        homedir: /home/rich

    create_ansible_dev_env_use_misc_keys: true

    create_ansible_dev_env_misc_keys:
      - username: rich
        user_home_dir: /home/rich
        priv_key_filename: <private key, usually the Git repo key if you want repos to be cloned>
        pub_key_filename: <public key, usually the Git repo key if you want repos to be cloned>
        key_dest_dir: /home/rich/.ssh
        key_src_dir: /home/rich/.ssh
        mode: "0600"

    create_ansible_dev_env_ssh_user_config: true

    create_ansible_dev_env_ssh_user_config:
      - username: rich
        config_filepath: /home/rich/.ssh/config
        host_domain: github.com
        host_name: github.com
        identity_file: ~/.ssh/rsa-streamline-it

    create_ansible_dev_env_clone_repos: true

    create_ansible_dev_env_git_repos:
      - git_repo_name: apache
        git_repo: <git repo>
        dest_dir: /home/rich/ansible/roles/streamline-it
        owner: rich
        group: rich
        host_key: <git repository key>

  roles:
    - create-ansible-dev

License
-------

BSD

Author Information
------------------

Rich O'Hara

