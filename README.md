# GVE_DevNet_ISE_9K_Ansible_Config
prototype ansible playbook that pushes configurations for Catalyst 9k to setup radius configuration with Cisco ISE


## Contacts
* Jorge Banegas

## Solution Components
* ISE
* Ansible
* Catalyst 9000 series

## Installation/Configuration

```python
pip install -r requirements.txt
```

Fill out all the values of the variables inside the vars/main.yml file. Below is a sample, make sure to change accordingly. 

```python
variables:
  description: Test Loopback
  sc1_ip :  '*.*.*.*'
  sc1_pac_key :  ********
  sc1_key_server_key : ********
  rid_ip : '*.*.*.*'
  rid_key_pac_key : ********
  rid_key_server_key : ********
  access_vlan_list : '521-522'
  voice_vlan_list : '1076'
  ise_password : ********
  interfaces : 
    - 'GigabitEthernet1/1/1-2'
  rollback_version: myconfiguration-Nov-10-18-06-21.697-8
```

## Usage rollback.yml playbook (playbook that adds rollback functionalities (setup,save,restore)

* To initialize rollback feature:
    $ ansible-playbook -i inventory.yml rollback.yml --tags=setup_rollback
* To save current running configuration into the flask memory (will save image with a timestamp)
    $ ansible-playbook -i inventory.yml rollback.yml --tags=save_version
    
* To rollback to a specific image version, include the rollback version into the rollback_version variable in vars/main.yml file. Inside the rollback folder, you will see all the devices rollback versions named [hostname]_rollback.txt. 
    ```python
      rollback_version: myconfiguration-Nov-10-18-06-21.697-8
    ```
    $ ansible-playbook -i inventory.yml rollback.yml --tags=rollback
    
 ## Usage cisco-9k.yml playbook (playbook that contains several configurations templates - check out templates folder)

* To run specific play, include the tag name on which play you want to execute:
    $ ansible-playbook -i inventory.yml cisco-9k.yml --tags=aaa_config
    
# Screenshots

![/IMAGES/0image.png](/IMAGES/0image.png)

### LICENSE

Provided under Cisco Sample Code License, for details see [LICENSE](LICENSE.md)

### CODE_OF_CONDUCT

Our code of conduct is available [here](CODE_OF_CONDUCT.md)

### CONTRIBUTING

See our contributing guidelines [here](CONTRIBUTING.md)

#### DISCLAIMER:
<b>Please note:</b> This script is meant for demo purposes only. All tools/ scripts in this repo are released for use "AS IS" without any warranties of any kind, including, but not limited to their installation, use, or performance. Any use of these scripts and tools is at your own risk. There is no guarantee that they have been through thorough testing in a comparable environment and we are not responsible for any damage or data loss incurred with their use.
You are responsible for reviewing and testing any scripts you run thoroughly before use in any non-testing environment.
