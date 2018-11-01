# cfg_aws_deploy_environment

## Description:

Issue with deploying storage for the docker registry 



## Behaviour:

**Feature:** OCP Deployment

The heketi pod was regenerating its admin secret which was causing the heketi pod to not authenticate and in turn causing the deploying the storage for the docker registry to fail

Changes are required to the following play
/usr/share/ansible/openshift-ansible/roles/openshift_storage_glusterfs/tasks/glusterfs_common.yml 


## Configuration:


- name: Set heketi admin key
  set_fact:
    glusterfs_heketi_admin_key: "{{ glusterfs_heketi_admin_secret.results.decoded.key }}"
  when:
  - glusterfs_is_native or glusterfs_heketi_is_native
  - glusterfs_heketi_admin_secret.results.results[0]




