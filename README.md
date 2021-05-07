# nutanix-guest-tools

Install ngt on nuranix linux guest vm.


## Role Variables

| Variable                | Required | Default |  Comments                                 |
|-------------------------|----------|---------|------------------------------------------|
| nutanix_prism_user      | yes      |         | username for the api. You can use  format 'user@domain.local' for AD user          |
| nutanix_prism_password  | yes      |         | example variable                         |
| nutanix_prism_element_url| yes     | https://example.domain.com:9440 | Url of Prism element                      |
| vm_name                 | no      |   inventory_hostname      | VM name in Nutanix prism                       |


## Example Playbook

Prompt credentails for Nutanix Prism API

```yml
- name: Enable and install NGT
  hosts: myserver
  vars_prompt:
    - name: "nutanix_prism_user"
      prompt: "Enter Nutanix username (ex: user@domain.local)"
      private: no
    - name: "nutanix_prism_password"
      prompt: "Enter password"
      private: yes
  roles:
    - nutanix-guest-tools
```

OR source from variables file (vault or not)

```yml
- name: Enable and install NGT
  hosts: myserver
  vars_files:
    - /etc/ansible/secret/nutanix_credentials_vars.yml
  roles:
    - nutanix-guest-tools
```

OR use ansible vault inline
```yml
- name: Enable and install NGT
  hosts: myserver
  vars:
    nutanix_prism_user: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              62343632303065376633353237643735333039333934613534323238313933343133656630393734
              3862623931653136333265336235383466373961323430310a383039343561306335333134616633
              61353239383433343531633963303235623134303131656131653737653437353936363237336131
              6266666530393966620a373965626164613766323464363062646561353339383431346537346639
              65306636613363383533323465643065376461643535616234373637633136383436
    nutanix_prism_password: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              30636432303334363961346239666165336635373263663637313965653832346366616530623761
              3032333638666666656464316230363838643439353337390a623930643132663365643535326533
              66663762616530316666343962383264623764656337383536336666323533663830356438636434
              3238633138363261610a616131326261353530353738613132633965306262363863333834393064
              65323635333733383231386465363465323966626631626364313837393063373530
  roles:
    - nutanix-guest-tools
```