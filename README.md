Role Name
=========

This role creates an Ansible developement environment. It creates environment variable(s) for Ansible.  It also creates developement directory under user's Documents directory.  Lastly it create's a vimrc file catered to Ansible editing under VIM.  In addition git repo cloning and host key copying as been added.

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

# if true cloning git repos is enabled
create_ansible_dev_env_clone_repos: false
 
# git repo info to clone
# Example
# create_ansible_dev_env_git_repos:
#    - git_repo_name: apache
#      git_repo: git@github.com:streamline-it/apache.git
#      dest_dir: /home/username/git-repos
#      owner: username
#      group: username
#      host_key: rsa-github-priv

create_ansible_dev_env_git_repos:
  - git_repo_name:
    git_repo:
    dest_dir:
    owner:
    group:
    host_key:

Vars section

# used to create user aliases etc
create_ansible_dev_filepaths:
  - shell: bash
    vim_src: vimrc_bash
    vim_dest: ".vimrc"
    env_file: ".bashrc"
  - shell: bourne
    vim_src: vimrc_bourne
    vim_dest: ".vimrc"
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

    * Very simple definition

    - hosts: servers

      roles:
         - create-ansible-dev

    * Using all available options which include misc host keys
      and git repo cloning


    - hosts: servers

      vars:

	create_ansible_dev_users:
	  - name: rich
	    shell: /bin/sh
	    homedir: /home/rich

        create_ansible_dev_env_misc_keys:
          - username: rich
            user_home_dir: /home/rich
            priv_key_filename: github-priv-key
            pub_key_filename: github-priv-key.pub
            key_dest_dir: /home/rich/.ssh
            key_src_dir: /home/rich/.ssh
            mode: "0600"

        create_ansible_dev_env_ssh_user_config:
          - username: rich
            config_filepath: /home/rich/.ssh/config
            host_domain: github.com
            host_name: github.com
            identity_file: ~/.ssh/github-priv-key

        create_ansible_dev_env_clone_repos: true

        create_ansible_dev_env_clone_repos: true

        create_ansible_dev_env_git_repos:
          - git_repo_name: create-ansible-dev
            git_repo: git@github.com:streamline-it/create-ansible-dev.git
            dest_dir: /home/rich/ansible/roles/streamline-it
            owner: rich
            group: rich
            host_key: github-priv-key

      roles:
         - create-ansible-dev


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).


