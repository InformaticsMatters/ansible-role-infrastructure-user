Ansible Role - informaticsmatters.infrastructure_user
=====================================================

[![Build Status](https://travis-ci.com/InformaticsMatters/ansible-role-infrastructure-user.svg?branch=master)](https://travis-ci.com/InformaticsMatters/ansible-role-infrastructure-user)

A Kubernetes-based Role for the configuration of a pre-deployed infrastructure.
This role provides actions to add and remove Keycloak users in the
infrastructure deployment.

Requirements
------------

-   None

Role Variables
--------------

    # The user action.
    # One of 'create' or 'delete'
    iu_action: create
    
    # The Keycloak hostname (https:// is assumed)
    iu_hostname: example.com
    # The Realm, realm manager and manager's password...
    iu_realm: ''
    iu_realm_manager: ''
    iu_realm_manager_password: ''
    
    # A list of users.
    # The list contains users and passwords: -
    #
    #   iu_users:
    #   - username: alan
    #     password: blob1234
    #   - username: nala
    #     password: blob5678
    iu_users: []
    
Dependencies
------------

-   (none)

Example Playbook
----------------

**NOTE** The example below assumes that you have a Keycloak installation.

    - hosts: servers
      tasks:
      - include_role:
          name: informaticsmatters.infrastructure_config
        vars:
          iu_action: create
          iu_hostname: keycloak.example.com
          iu_realm: my-realm
          iu_realm_manager: manager
          iu_realm_manager_password: abc0000000
          iu_users:
          - username: alan
            password: blob1234

License
-------

Apache 2.0 License

Author Information
------------------

alanbchristie
