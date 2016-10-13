
ansible-role-python
=========

Ansible role for installing and configuring Python, pip, and virtualenv.

https://galaxy.ansible.com/singleplatform-eng/python/

Role Variables
--------------

- `logrhythm_host`: host for Mediator 1 (this is required, unless you override the entire `logrhythm_config`)

- `python_apt_key_url`: apt key for installing custom python package (Default: '')
- `python_apt_repo`: apt repo for installing custom python package (Default: '')
- `python_global_packages`: pip packages to install globally (Default: [])
- `python_package_name`: name of python package (Default: python)

- `python_pip_config`: glocal pip.conf configuration (Default: undefined)

        # Example
        global:
            index-url: http://pypi.example.com/simple
            find-links:
                - http://pypi2.example.com/simple
                - http://pypi3.example.com/simple
        search:
            index: http://pypi.example.com/simple

- `python_build_from_source`: whether to build from source or install package (Default: false)
- `python_configure_prefix`: directory to install to when building from source (Default: /usr/local)
- `python_version`: version of python to build (Default: '')

Example Playbook
----------------

Install default OS package:

    ---

    - hosts: all
      become: true
      roles:
        - python

Install custom package:

    ---

    - hosts: all
      become: true
      vars:
        python_apt_repo: deb http://example.repo/ trusty main
        python_apt_key_url: https://example.repo/Release.key
        python_package_name: python-custom
      roles:
        - python

Build Python 2 and 3 from source with custom prefix and global packages:

    ---

    - hosts: all
      become: true
      vars:
        python_build_from_source: true
        python_configure_prefix: /opt/local
        python_global_packages:
          - ansible==2.0.1.0
          - uwsgi
      roles:
        - { role: python, python_version: 2.7.7 }
        - { role: python, python_version: 3.4.4 }

Author Information
------------------

[SinglePlatform Engineering](http://engineering.singleplatform.com/)

License
-------

BSD 3-Clause
