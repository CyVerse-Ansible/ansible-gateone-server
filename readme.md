GateOne Server
=========

Installs GateOne server. Galaxy-ized version of https://github.com/cyverse/gateone-server-ansible. May include some CyVerse-isms.

## Todo
- Set restricted file permissions on SSL private key, only accessible to Nginx and GateOne services
- Generate strong, random COOKIE_SECRET if deployer does not specify it

[![Build Status](https://travis-ci.org/CyVerse-Ansible/ansible-gateone-server.svg?branch=master)](https://travis-ci.org/CyVerse-Ansible/ansible-gateone-server)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gateone--server-blue.svg)](https://galaxy.ansible.com/CyVerse-Ansible/gateone-server/)


Requirements
------------

None

Role Variables
--------------

| Variable                | Required | Default                               | Choices | Comments                                                |
|-------------------------|----------|---------------------------------------|---------|---------------------------------------------------------|
| GATEONE_REPO            | no       | https://github.com/edwins/gateone.git |         |                                                         |
| SSL_PRIVKEY_NAME        | no       | snakeoil.key                          |         | Name of your SSL certificate private key file in files/ |
| SSL_CERT_NAME           | no       | snakeoil.crt                          |         | Name of your SSL certificate in files/                  |
| COOKIE_SECRET           | yes      | coookie-crisp                         |         | Secret to use for cookies                               |
| GATEONE_ORIGINS         | no       | '["localhost", "127.0.0.1"]'          |         | Python-style list of allowed origins (see GateOne docs) |
| GATEONE_SERVER_NAME     | yes      | myserver.com                          |         | Name of your gateone host                               |
| NOHOSTKEYCHECK_PATTERN  | yes      | 192.168.1.*                           |         | ssh_config-style host pattern to skip host key checking |
| GATEONE_API_KEY         | yes      |                                       |         | See GateOne docs                                        |
| GATEONE_API_SECRET      | yes      |                                       |         | See GateOne docs

GATEONE_ORIGINS variable is documented [here](http://liftoff.github.io/GateOne/About/configuration.html?highlight=origins#cmdoption--origins).
GATEONE_API_KEY and GATEONE_API_SECRET are documented [here]()

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - gateone-server

License
-------

See license.md

Author Information
------------------

https://cyverse.org
