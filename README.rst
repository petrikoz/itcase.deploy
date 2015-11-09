*************
ItCase Deploy
*************

.. image:: https://travis-ci.org/petrikoz/itcase.deploy.svg
    :target: https://travis-ci.org/petrikoz/itcase.deploy

Extended fork of `Ansible`_ role `Stouts.deploy`_.
Current role deploy projects to `ItCase`_ dev server.

Usage
=====

Required `Psycopg2`_ on remote machine for PostgreSQL part.

.. code-block:: yaml

    - hosts: all

      roles:
      - itcase.deploy

      vars:
        deploy_app_repo: 'https://github.com/petrikoz/itcase.deploy.git'
      vars_prompt:
        - name: 'deploy_pg_password'
          prompt: 'password for user "postgres"'
          default: '12345'

Variables
=========

.. code-block:: yaml

    deploy_user: '{{ ansible_ssh_user }}'     # Set deploy user
    deploy_group: '{{ deploy_user }}'         # Set deploy group

    deploy_app_name: 'example'
    deploy_app_repo: ''                       # E.g. Bitbucket's repo: git@bitbucket.org:OWNER_ACCOUNT_PLACE_HERE/{{ deploy_app_name }}. ↪ git
    deploy_app_ver: 'develop'

    deploy_dir: '/tmp/{{ deploy_app_name }}'  # Root deploy directory
    deploy_etc_dir: '{{ deploy_dir }}/etc'    # Directory where placed configuration files
    deploy_log_dir: '{{ deploy_dir }}/log'    # Directory where placed logs
    deploy_run_dir: '{{ deploy_dir }}/run'    # Directory where placed unix sockets and pid files
    deploy_src_dir: '{{ deploy_dir }}/src'    # Source's directory

    deploy_venv_root: '/tmp/.venvs'           # Directory with folders of envs
    deploy_venv_name: '{{ deploy_app_name }}'
    deploy_venv_python: python
    deploy_venv_options: ''                   # E.g. --system-site-packages

    deploy_nginx_listen: 80
    deploy_nginx_server_name: '.{{ deploy_app_name }}.itcase.pro'  # Must start with dot
    deploy_nginx_root: '{{ deploy_dir }}'
    deploy_nginx_meta_sufix: '/media/uploads/seo'  # Folder wich contains 'robots.txt', 'favicon.ico' and etc. Relative from             ↪ $project_src (see /templates/nginx.conf.jinja2)
    deploy_nginx_uwsgi_pass: 'unix://$project_root/run/uwsgi.sock'
    deploy_nginx_uwsgi_options: []

    deploy_uwsgi_name: '{{ deploy_app_name }}'
    deploy_uwsgi_path: '{{ deploy_dir }}'
    deploy_uwsgi_options: [
      'env = LC_ALL=ru_RU.UTF-8',
      'env = LANG=ru_RU.UTF-8'
    ]

License
=======

Licensed under the Apache License, Version 2.0. See the `LICENSE`_ file for details.

.. _Ansible: https://github.com/ansible/ansible
.. _Stouts.deploy: https://github.com/Stouts/Stouts.deploy
.. _ItCase: http://itcase.pro
.. _LICENSE: LICENSE
.. _Psycopg2: http://initd.org/psycopg/

