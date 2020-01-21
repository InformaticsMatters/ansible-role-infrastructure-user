Ansible Role - informaticsmatters.infrastructure_user
=====================================================

[![Build Status](https://travis-ci.com/InformaticsMatters/ansible-role-infrastructure-user.svg?branch=master)](https://travis-ci.com/InformaticsMatters/ansible-role-infrastructure-user)
![GitHub release (latest by date)](https://img.shields.io/github/v/release/informaticsmatters/ansible-role-infrastructure-user)
![Ansible Role](https://img.shields.io/ansible/role/45913)

A Kubernetes-based Role for the configuration of a pre-deployed infrastructure.
This role provides actions to add and remove Keycloak users in the
infrastructure deployment.

Requirements
------------

-   None

Role Variables
--------------

    # The role action.
    # One of 'create' or 'delete', used in conjunction with 'iu_type'
    iu_action: create
    # The type of item to create,
    # One of 'realm', 'role' or 'user'
    iu_type: user
    
    # The Keycloak hostname (https:// is assumed)
    iu_hostname: example.com
    # The Realm, realm manager and manager's password.
    # The manager user is 'manager' by default
    # and password is randomly generated if not supplied.
    iu_realm: ''
    iu_realm_manager: 'manager'
    iu_realm_manager_password: "{{ lookup('password', '/dev/null length=14 chars=ascii_letters,digits') }}"
    # The namespace of the Keycloak's instance,
    # required if creating or deleting a realm.
    iu_namespace: ''
    
    # The keycloak admin user name and password
    # (required to create and delete realms)
    iu_admin: admin
    iu_admin_password: ''
    
    # A list of users to add to a realm.
    # The list contains usernames and passwords: -
    #
    #   iu_users:
    #   - username: alan
    #     password: blob1234
    #   - username: nala
    #     password: blob5678
    iu_users: []
    
    # A list of roles to add to an existing realm.
    # It is simply a list of role names: -
    #
    #   iu_roles:
    #   - standard-user
    iu_roles: []
    
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
          iu_type: user
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
