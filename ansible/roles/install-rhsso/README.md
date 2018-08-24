Role Name
=========

install-rhsso role is intended to add a common red hat sso authentication server for workshop installation. The red hat sso container, services and routes will be added to the shared containers namespace (normally `shared-opentlc`).

In the case of workshops like the RH-PAM workshop, authentication and authorization assets keep unchanged for all students, and different users are required for the student to experiment as different personas participating through the execution of the labs, hence the student is familiarized with the product experience from different perspectives.

For projects where the student will perform changes to the authentication and authorization assets, it is best to keep the authentication server (Red Hat SSO) as a particular asset for the student workshop environment, instead of a shared resource.

Requirements
------------

* **OC Client tools**: As this is a provisioning role for an OCP workshop environment.

Role Variables
--------------

> A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

* **shared_ns**: Intended to install the rh-sso server in the shared resources for workshop environment. Normally expecting this parameter value to be `shared-opentlc`


Example Playbook
----------------

```yaml
  - hosts: masters
    roles:
    - role: "{{ ANSIBLE_REPO_PATH }}/roles/install-rhsso"
      shared_ns: "{{admin_project}}"
      when: install_sso|bool
```

Testing with workshop available master node:

  ```
  ansible-playbook -i localhost, -c local ./configs/ocp-workloads/ocp-workload.yml -e"ANSIBLE_REPO_PATH=`pwd`" -e"ocp_workload=ocp-workload-bxms-pam" -e"ocp_user_needs_quota=true" -e"guid=dtof" -e"ocp_domain=5c40.openshift.opentlc.com" -e"ACTION=create" -e"sso_required=true" -e"shared_ns=shared-opentlc"
  ```

License
-------

BSD

Author Information
------------------

dtorresf
