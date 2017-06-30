FMW domain prereq
=========

Simple role to check/set required settings for EL machines.

Requirements
------------

Tested on RedHat 6.x

Role Variables
--------------
    # Linux family
    OSFamily: "RedHat"
    # Linux version
    OSVersion: "6.7"
    
    # List of packages to check/install
    installPackages:
      - binutils
      - compat-libcap1
      #- compat-libstdc++
      - gcc
      - gcc-c++
      - glibc
      - glibc-devel
      - libaio
      - libaio-devel
      - libgcc
      - libstdc++
      - libstdc++-devel
      - sysstat
    
    # List of absolute directories to create
    directoriesToCreate: []
    
    # sysctl settings
    swappiness: 0
    rmem_max: 2096304
    wmem_max: 2096304
    
    # user/group to create
    homeDir: /users
    user: oracle
    password: q1w2e3
    uid: 150
    group: oinstall
    gid: 151
    
    # pam_limits number of open files
    nofile: 61440
    
    # mount options
    nfsOptions: 'rw,bg,hard,noacl,rsize=32768,wsize=32768,vers=3,nointr,timeo=600,proto=tcp,suid'
    
    # list of mounts to add/mount to fstab
    fstab:
      - { name: '/opt/oracle/11g', src: '' }
      - { name: '/opt/oracle/admin/shared', src: 'nfs.example.com:/vol/shared' }
      - { name: '/opt/oracle/admin/aservers', src: 'nfs.example.com:/vol/aservers' }
      - { name: '/opt/oracle/admin/appfiles', src: 'nfs.example.com:/vol/appfiles' }
      - { name: '/opt/oracle/admin/logs', src: 'nfs.example.com:/vol/logs' }
    
    # list of mounts to unmount/remove from fstab
    apsend_mounts: []


Example Playbook
----------------

ansible-playbook - i hosts site.yml
    
    # site.yml
    - hosts: servers
      roles:
         - dborysenko.fmw-domain-prereq
    
    # hosts
    [servers]
    webserver.example.com
    
    
License
-------

BSD

Author Information
------------------

Dmytro Borysenko
borysenus@gmail.com
