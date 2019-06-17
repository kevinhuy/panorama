# Configure Security Policies Panorama

This play-book takes a xls file as input to configure network objects, service objects and security polcies on Panorama

# Pre-requisites

1. requirements.txt has all the libraries that need to be installed
2. Requires you to install the Paloaltonetworks Galazy Role
    ```
    ansible-galaxy install PaloAltoNetworks.paloaltonetworks,v2.0.4 --force
    ```
3. [xls_to_facts.py](https://raw.githubusercontent.com/mamullen13316/ansible_xls_to_facts/master/xls_to_facts.py) needs to be copied onto ansible/module/files/

4. update panos_security_rule.py in galaxy roles to [this](https://raw.githubusercontent.com/PaloAltoNetworks/ansible-pan/f7cf604ab3c9c6eb2cab8f4fcc1653cb67251cee/library/panos_security_rule.py)

# Files

secrets.yaml contains the ip address of the panorama and the login credientials
variables/configuration.xlsx is the input file. 






# usefule excel formulas for Network Object Groups
=IF(ISBLANK(B2),"",CONCAT("'",B2,"'"))
=TEXTJOIN(",",TRUE,G2:K2)