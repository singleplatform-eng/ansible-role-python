In addition to installing Python, this role also installs `pip` and `virtualenv` globally.

Install default OS package:
```
---

- hosts: all
  become: true
  roles:
    - python
```

Install custom package:
```
---

- hosts: all
  become: true
  vars:
    python_apt_repo: deb http://example.repo/ trusty main
    python_apt_key_url: https://example.repo/Release.key
    python_package_name: python-custom
  roles:
    - python
```

Build Python 2 and 3 from source with custom prefix and global packages:
```
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
```
