# Ansible Role: Pure-FTPd

[![Build Status](https://travis-ci.org/picturemaxx/ansible-pureftpd.svg?branch=master)](https://travis-ci.org/picturemaxx/ansible-pureftpd)

Installs Pure-FTPd on Debian/Ubuntu linux servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with other default values (see `defaults/main.yml`):

To create a ftp account define all account as follows:

```
pureftpd_users:
  - name: ftpuser
    password: '$2....40'
    home: '/var/www/site'
    uid: '1002'
    gid: '1002'

```

To allow virtual users, one single user will be created:

* `pureftpd_user`: Name of the ftp user (default 'ftpuser')
* `pureftpd_user_uid`: UID of the user (optional)
* `pureftpd_user_home`: (optional, e.g. `/home/ftp`)
* `pureftpd_group`: Name of the ftp user group (default 'ftp')
* `pureftpd_group_gid`: GID for the group (optional)


### Config Variables

Choose which flavour to install:
`pureftpd_apt_package`: `pure-ftpd`, `pure-ftpd-mysql`, `pure-ftpd-postgresql`, `pure-ftpd-ldap`

Values should be surrounded by quotation marks as otherwise `yes` becomes `True`

```
pureftpd_config:
#  AllowAnonymousFXP:           'no'
#  AllowUserFXP:                'no'
  AltLog:                      'clf:/var/log/pure-ftpd/transfer.log'
#  AltLog:                      'stats:/var/log/pureftpd.log'
#  AltLog:                      'w3c:/var/log/pureftpd.log'
#  AnonymousBandwidth:          '8'
#  AnonymousCanCreateDirs:      'no'
#  AnonymousCantUpload:         'no'
#  AnonymousOnly:               'no'
#  AnonymousRatio:              '1 10'
#  AntiWarez:                   'yes'
#  AutoRename:                  'no'
#  Bind:                         '127.0.0.1,21'
#  BrokenClientsCompatibility:  'no'
#  CallUploadScript:            'yes'
#  ChrootEveryone:              'yes'
#  ClientCharset:               'UTF-8'
#  CreateHomeDir:               'yes'
#  CustomerProof:               'yes'
#  Daemonize:                   'yes'
#  DisplayDotFiles:             'yes'
#  DontResolve:                 'yes'
#  ExtAuth:                     /var/run/ftpd.sock
#  ForcePassiveIP:              '192.168.0.1'
#  FortunesFile:                '/etc/pure-ftpd/cookie'
  FSCharset:                   'UTF-8'
#  IPV4Only:                    'yes'
#  IPV6Only:                    'yes'
#  KeepAllFiles:                'yes'
#  LDAPConfigFile:              /etc/pureftpd-ldap.conf
#  LimitRecursion:              '10000 8'
#  LogPID:                      'yes'
#  MaxClientsNumber:            '50'
#  MaxClientsPerIP:             '{{ ansible_processor_cores }}'
#  MaxDiskUsage:                '99'
#  MaxIdleTime:                 '15'
#  MaxLoad:                     '4'
  MinUID:                      '1000'
#  MySQLConfigFile:             /etc/pure-ftpd/mysql.conf
  NoAnonymous:                 'yes'
#  NoChmod:                     'yes'
#  NoRename:                    'yes'
#  NoTruncate:                  'yes'
  PAMAuthentication:           'yes'
#  PassivePortRange:            '30000 50000'
#  PerUserLimits:               '3:20'
#  PGSQLConfigFile:             /etc/pureftpd-pgsql.conf
#  PIDFile:                     '/var/run/pure-ftpd.pid'
#  ProhibitDotFilesRead:        'no'
#  ProhibitDotFilesWrite:       'no'
  PureDB:                       /etc/pure-ftpd/pureftpd.pdb
#  Quota:                       '1000:10'
#  SyslogFacility:              'ftp'
#  TLS:                         '0'
  TLSCipherSuite:              'ALL:!aNULL:!SSLv3'
#  TrustedIP:                   '10.1.1.1'
#  Umask:                       '117 007'
  UnixAuthentication:          'no'
#  UserBandwidth:                '8'
#  UserRatio:                   '1 10'
#  VerboseLog:                  'yes'
```
When `CallUploadScript` is set to `yes`, `pureftpd_upload_script` has to
be set to enable the script that should be called when an upload is
completed. If the script should be executed by a certain user and group,
also set `pureftpd_upload_script_uid` and `pureftpd_upload_script_gid`.

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: ansible-pureftpd }

## License

MIT / BSD

## Author Information

 - Tobias Schifftner, @tschifftner
 - Michael Weinrich, @micxer
