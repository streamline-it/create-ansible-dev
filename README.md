Role Name
=========

This role creates an Ansible developement environment. It creates environment variable(s) for Ansible.  It also creates developement directory under user's Documents directory.  Lastly it create's a vimrc file catered to Ansible editing under VIM.

This role can also change your bash prompt if you enable the "create_ansible_dev_bash_config_promt" by making it equal to true.  You can choose the color.


This role with work on RHEL 7 OS's and up along with FreeBSD hosts versions 13 and up.
Requirements
------------

None

Role Variables
--------------

# defaults file for create-ansible-dev

# the "bash_ps1" attribute will change the bash prompt.
#
create_ansible_dev_prompt_colors:
  - black: 30
  - red: 31
  - green: 32
  - yellowbrown: 33
  - blue: 34
  - magenta: 35
  - cyan: 36
  - lightgrey: 37
  - default: 39
  - darkgrey: 90
  - white: 97

# This will help choose the color of your prompt in the bash shell, default is green
# This is the example of the end result "PS1="\e[1;32m\][\u@\h: \w]$\e[0m\]"

create_ansible_dev_chosen_color: "{{ create_ansible_dev_prompt_colors[1]['green'] }}"
create_ansible_dev_prompt_string: "\\e[1;{{ create_ansible_dev_chosen_color }}m\\][\\u@\\h: \\w]$\\e[0m\\]"
create_ansible_dev_ps_prompt: "{{ 'PS1=\"' ~ '\\e[1;32m\\][\\u@\\h: \\w]$\\e[0m\\]' ~  '\"' }}"

# if true the bash config prompt
create_ansible_dev_bash_config_prompt: true


create_ansible_dev_users:
  - name:
    os:
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
  - os: linux
    vim_src: vimrc_linux
    vim_dest: ".vimrc"
    env_file: ".bashrc"
  - os: bsd
    vim_src: vimrc_bsd
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

create_ansible_dev_bashrc_filename: .bashrc

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

    create_ansible_dev_chosen_color: "{{ create_ansible_dev_prompt_colors[4]['blue'] }}"

    create_ansible_dev_users:
      - name: rich
        os: linux
        shell: bash
        homedir: /home/rich
	bash_ps1: "{{ create_ansible_dev_ps_prompt }}"

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

