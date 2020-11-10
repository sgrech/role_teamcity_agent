Role Name
=========

Ansible role used to install teamcity agent as a service.

Requirements
------------

Needs teamcity server running as a service, see [sgrech.role_teamcity](https://galaxy.ansible.com/sgrech/role_teamcity).
Also requires agent repository `buildAgentFull.zip` downloaded from running teamcity server instance.
The playbook using this role also needs to define `agent_archive_host_path` variable to define where
the build agent archive is stored on the host.

Role Variables
--------------

The following variables can be overridden to customize service installation

- archive_path: "/tmp"
- agent_archive: "buildAgentFull.zip"
- teamcity_server_url: "http://localhost:8111"
- service_path: "/opt/teamcity-agent"
- teamcity_group: teamcity
- teamcity_agent_user: teamcity_agent
- teamcity_agent_service: teamcity-agent
- teamcity_agent_port: 9090
- teamcity_agent_index: 1

Dependencies
------------

sgrech.role_teamcity

Example Playbook
----------------

```yml
---
- hosts: any
  become: yes

  vars:
    teamcity_user: teamcity
    teamcity_group: teamcity
    agent_archive_host_path: ~/Software/buildAgentFull.zip

  tasks:
    - import_role:
        name: sgrech.role_teamcity
      tags: teamcity_server

    - import_role:
        name: sgrech.role_teamcity_agent
      vars:
        teamcity_agent_user: teamcity_agent_1
        teamcity_agent_service: teamcity-agent-1
        teamcity_agent_port: 9091
        service_path: /opt/teamcity-agent-1
        teamcity_agent_index: 1
      tags: teamcity_agent
```  

License
-------

GPL

Author Information
------------------

TODO
