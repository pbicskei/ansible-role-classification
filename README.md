<img title="a title" alt="Alt text" src="https://app.travis-ci.com/pbicskei/ansible-role-classification.svg
">

Role Name
=========

A role that simplifies simple classification from ansible_facts.

Classification Proxmox `p24.xlarge` stands for a `Proxmox` host with `ansible_processor_count` equals `24` and `ansible_memtotal_mb` greater than `32456`.
Classification Raspberry `a4.large` stands for a `Arm` host with `ansible_processor_count` equals `4` and `ansible_memtotal_mb` between `4096` and `8096`.
Classification Generic `g4.nano` stands for a `Generic` host with `ansible_processor_count` equals `4` and `ansible_memtotal_mb` between `4096` and `8096`.

In the Proxmox example the leading letter is based on `ansible_kernel` like this:

```yaml
  - name: Proxmox Hypervisor
    set_fact:
      type: p
      type_desc: "{{ ansible_distribution }} Proxmox"
    when: '"pve" in ansible_kernel'
```

These maps are generated base on 2 variables: `size_map` and `type_map` which both can be found in defaults/main.yml.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

Using the default table:

```yaml
    - hosts: servers
      roles:
         - pbicskei.classify
```

Using a Custom table:

```yaml
    - hosts: servers
      roles:
         - pbicskei.classify
      vars:
        type_map:
          - { name: "Hypervisor", letter: "hv", kernel_match: "pve" }
          - { name: "Compute(ARM)", letter: "a", kernel_match: "raspi" }
          - { name: "Generic", letter: "g", kernel_match: "default" }

        size_map:
          - { name: "nanite", min: 1, max: 1024 }
          - { name: "microbe", min: 1024, max: 2048 }
          - { name: "insect", min: 2048, max: 4092 }
          - { name: "hamster", min: 4092, max: 8184 }
          - { name: "dog", min: 8184, max: 16368 }
          - { name: "horse", min: 16368, max: 32736 }
          - { name: "elephant", min: 32736, max: 65472 }
          - { name: "whale", min: 65472, max: 130944 }  

      roles:
        - pbicskei.classify
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
