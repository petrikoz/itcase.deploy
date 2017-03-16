*************
ItCase Deploy
*************

.. image:: https://travis-ci.org/petrikoz/itcase.deploy.svg
    :target: https://travis-ci.org/petrikoz/itcase.deploy

`Ansible`_ role deploy projects to `ItCase`_ dev server.

Usage
=====

.. code-block:: yaml

    # Put this code in site.yml
    ---
    - hosts: all

      roles:
      - itcase.deploy

      vars:
        deploy_app_name: 'example'
        deploy_app_repo: 'https://github.com/petrikoz/itcase.deploy.git'

      vars_prompt:
        - name: 'deploy_pg_role_password'
          prompt: 'Password for app DB role'

        - name: 'deploy_pg_password'
          prompt: 'Password for root DB role'

For 'postgres' part required `PostgreSQL`_ on remote server.
And will be install `Psycopg2`_ on remote server.
If you need skeep this part use flag ``--skip-tags=itcase.deploy.postgres``.

You can run with command ``ansible-playbook --ask-become-pass --inventory-file inventory site.yml``

Variables
=========

.. code-block:: yaml

    deploy_user: '{{ ansible_ssh_user }}'  # Set deploy user
    deploy_group: '{{ deploy_user }}'      # Set deploy group

    deploy_app_name: 'example'
    deploy_app_repo: 'git@github.com:petrikoz/itcase.deploy.git'  # E.g. Bitbucket's repo: git@bitbucket.org:OWNER_ACCOUNT_PLACE_HERE/{{ deploy_app_name }}.git
    deploy_app_ver: 'develop'

    deploy_dir: '/home/{{ deploy_user }}/{{ deploy_app_name }}'  # Root deploy directory
    deploy_etc_dir: '{{ deploy_dir }}/etc'    # Directory where placed configuration files
    deploy_log_dir: '{{ deploy_dir }}/log'    # Directory where placed logs
    deploy_run_dir: '{{ deploy_dir }}/run'    # Directory where placed unix sockets and pid files
    deploy_src_dir: '{{ deploy_dir }}/src'    # Source's directory

    deploy_venv_root: '/home/{{ deploy_user }}/.virtualenvs'           # Directory with folders of envs
    deploy_venv_name: '{{ deploy_app_name }}'
    deploy_venv_python: python
    deploy_venv_options: ''                   # E.g. --system-site-packages

    deploy_nginx_listen: 443
    deploy_nginx_server_name: '{{ deploy_app_name }}.itcase.pro'
    deploy_nginx_extra_server_name: ['www.{{ deploy_nginx_server_name }}']
    deploy_nginx_root: '{{ deploy_dir }}'
    deploy_nginx_log: '{{ deploy_log_dir }}/nginx.error.log'

    deploy_letsencrypt_live: '/etc/letsencrypt/live/{{ deploy_nginx_server_name }}'

    deploy_uwsgi_name: '{{ deploy_app_name }}'
    deploy_uwsgi_path: '{{ deploy_dir }}'

    deploy_pg_role_name: '{{ deploy_app_name }}'
    deploy_pg_role_password: '12345'
    deploy_pg_db_name: '{{ deploy_app_name }}'
    deploy_pg_user: 'postgres'
    deploy_pg_password: '{{ deploy_pg_user }}'

License
=======

Licensed under the Apache License, Version 2.0. See the `LICENSE`_ file for details.

.. _Ansible: https://github.com/ansible/ansible
.. _ItCase: http://itcase.pro
.. _PostgreSQL: http://www.postgresql.org
.. _Psycopg2: http://initd.org/psycopg/
.. _LICENSE: LICENSE

