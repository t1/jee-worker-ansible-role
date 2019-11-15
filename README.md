JEE-worker-role [![Build Status](https://travis-ci.org/t1/jee-worker-ansible-role.svg?branch=master)](https://travis-ci.org/t1/jee-worker-ansible-role)
===============

A [Jakarta-EE](https://jakarta.ee) container (namely [Wildfly](https://wildfly.org)) running the [Deployer](https://github.com/t1/deployer), ready to act as a worker in a [kub-ee](https://github.com/t1/kub-ee) cluster (although it doesn't know about kub-ee).

Role Variables
--------------

| var                       | description                            | default        |
| ------------------------- | -------------------------------------- | -------------- |
| deployer_version          | Version of the Deployer maven artifact | 3.0.0-SNAPSHOT |
| deployer_default_group_id | Deployer `default.group-id` config     | com.github.t1  |
| deployables               | Deployables like in the root bundle    | jolokia        |

The `deployables` look exactly like in the root bundle. E.g.:

```yaml
deployables:
  jolokia:                   # this is the deployable name
    group-id: org.jolokia    # defaults to the `default.group-id`
    artifact-id: jolokia-war # defaults to the deployable name
    version: 1.3.1           # defaults to `${jolokia.version or CURRENT}`
    state: deployed          # defaults to '${jolokia.state or «deployed»}'
  ping:                      # a second deployable with everything default
```

Dependencies
------------

* [t1.jee_app_server](https://galaxy.ansible.com/t1/jee_app_server)

Example Playbook
----------------

    - hosts: workers
      roles:
         - { role: t1.jee_worker }

License
-------

Apache 2.0
