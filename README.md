GateOne Server
=========

Installs GateOne server. Galaxy-ized version of https://github.com/cyverse/gateone-server-ansible. Intended to be used with [Atmosphere](http://github.com/iplantcollaborativeopensource/atmosphere), possibly not what you want if you are deploying GateOne for other applications.

## Todo
- Set restricted file permissions on SSL private key, only accessible to Nginx and GateOne services
- Generate strong, random COOKIE_SECRET if deployer does not specify it
- Generate and set diffie hellman parameters for Nginx
- Build test coverage beyond basic syntax checking

[![Build Status](https://travis-ci.org/CyVerse-Ansible/ansible-gateone-server.svg?branch=master)](https://travis-ci.org/CyVerse-Ansible/ansible-gateone-server)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gateone--server-blue.svg)](https://galaxy.ansible.com/CyVerse-Ansible/gateone-server/)


Requirements
------------

None

Role Variables
--------------

Note that some variables indicated as "Required" below are defined in `defaults/main.yml`, only so that this role passes automated tests. These variables still must be overridden in order to deploy a working GateOne server.

| Variable                | Required | Default                               | Choices | Comments                                                |
|-------------------------|----------|---------------------------------------|---------|---------------------------------------------------------|
| GATEONE_REPO            | no       | https://github.com/edwins/gateone.git |         |                                                         |
| SSL_CERT_NAME           | no       | snakeoil.crt                          |         | Name of your SSL certificate + CA chain in files/       |
| SSL_PRIVKEY_NAME        | no       | snakeoil.key                          |         | Name of your SSL certificate private key file in files/ |
| COOKIE_SECRET           | yes      | coookie-crisp                         |         | Secret to use for cookies                               |
| GATEONE_ORIGINS         | no       | '["localhost", "127.0.0.1"]'          |         | Python-style list of allowed origins (see GateOne docs) |
| GATEONE_SERVER_NAME     | yes      | myserver.com                          |         | Name of your gateone host                               |
| NOHOSTKEYCHECK_PATTERN  | yes      | 192.168.1.*                           |         | ssh_config-style host pattern to skip host key checking |
| GATEONE_API_KEY         | yes      |                                       |         | See GateOne docs                                        |
| GATEONE_API_SECRET      | yes      |                                       |         | See GateOne docs                                        |
| ATMO_ROOT_SSH_PUBKEYS   | no       |                                       |         | List of root public keys for Atmosphere servers         |

The code assumes that your SSL certificate and private key will be stored in files/. If you store your SSL private key in version contron, it is strongly encouraged that you encrypt it with `ansible-vault`.

GATEONE_ORIGINS variable is documented [here](http://liftoff.github.io/GateOne/About/configuration.html?highlight=origins#cmdoption--origins).
GATEONE_API_KEY and GATEONE_API_SECRET are documented [here](https://liftoff.github.io/GateOne/Developer/embedding_api_auth.html#generate-an-api-key-secret)

ATMO_ROOT_SSH_PUBKEYS, if defined, are inserted in the root user's authorized_keys file on the GateOne server. This allows Atmosphere to SSH to GateOne in order to insert users' SSH keypairs.

Dependencies
------------
Your SSL certificate + CA chain (as one PEM-encoded file), and private key (as another PEM-encoded file), should live in a location accessible from where you run the role. Refer to these paths in SSL_CERT_NAME and SSL_PRIVKEY_NAME.

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
