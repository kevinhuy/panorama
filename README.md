# Configure Security Policies Panorama

This play-book takes a xls file as input to configure network objects, service objects and security polcies on Panorama

# Getting Started

requirements.txt has all the libraries that need to be installed
xls_to_facts.py[https://raw.githubusercontent.com/mamullen13316/ansible_xls_to_facts/master/xls_to_facts.py] needs to be copied onto ansible/module/files/
update panos_security_rule.py in galaxy roles to this[https://raw.githubusercontent.com/PaloAltoNetworks/ansible-pan/f7cf604ab3c9c6eb2cab8f4fcc1653cb67251cee/library/panos_security_rule.py]

# files

secrets.yaml contains the ip address of the panorama and the login credientials
variables/configuration.xlsx is the input file

