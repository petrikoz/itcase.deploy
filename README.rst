*************
ItCase Deploy
*************

.. image:: https://travis-ci.org/petrikoz/itcase.deploy.svg
    :target: https://travis-ci.org/petrikoz/itcase.deploy

Extended fork of `Ansible`_ role `Stouts.deploy`_.
Current role deploy projects to ItCase dev server.

Usage
=====

.. code-block:: yaml

    - hosts: all

      roles:
      - itcase.deploy

      vars:
        deploy_app_repo: 'https://github.com/petrikoz/itcase.deploy.git'

Variables
=========

.. code-block:: yaml

    deploy_enabled: true                      # Enable the role

    deploy_user: '{{ ansible_ssh_user }}'     # Set deploy user
    deploy_group: '{{ deploy_user }}'         # Set deploy group

    deploy_app_name: 'example'

    deploy_dir: '/tmp/{{ deploy_app_name }}'  # Root deploy directory
    deploy_etc_dir: '{{ deploy_dir }}/etc'    # Directory where placed configuration files
    deploy_log_dir: '{{ deploy_dir }}/log'    # Directory where placed logs
    deploy_run_dir: '{{ deploy_dir }}/run'    # Directory where placed unix sockets and pid files
    deploy_src_dir: '{{ deploy_dir }}/src'    # Source's directory

    deploy_app_repo: ''                       # E.g. Bitbucket's repo: git@bitbucket.org:OWNER_ACCOUNT_PLACE_HERE/{{ deploy_app_name }}.git
    deploy_app_ver: 'develop'

    deploy_venv_root: '/tmp/.venvs'           # Directory with folders of envs
    deploy_venv_name: '{{ deploy_app_name }}'
    deploy_venv_python: python
    deploy_venv_options: ''                   # E.g. --system-site-packages

    deploy_nginx_listen: 80
    deploy_nginx_server_name: '.example.com'  # Must start with dot
    deploy_nginx_root: '{{ deploy_src_dir }}'
    deploy_nginx_meta_root: '{{ deploy_nginx_root }}/media/uploads/seo'  # Folder wich contains 'robots.txt', 'favicon.ico' and etc. 
    deploy_nginx_uwsgi_pass: 'unix://{{ deploy_run_dir }}/uwsgi.sock'
    deploy_nginx_uwsgi_options: []

    deploy_uwsgi_name: '{{ deploy_app_name }}'
    deploy_uwsgi_path: '{{ deploy_src_dir }}'

    deploy_uwsgi_options: [
      'env = LC_ALL=ru_RU.UTF-8',
      'env = LANG=ru_RU.UTF-8'
    ]

License
=======

Licensed under the Apache License, Version 2.0. See the LICENSE file for details.

.. _Ansible: https://github.com/ansible/ansible
.. _Stouts.deploy: https://github.com/Stouts/Stouts.deploy

