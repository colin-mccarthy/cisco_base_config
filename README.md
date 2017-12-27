Cisco_base
=========

Ansible role for configuring new 3560 switches.

Requirements
------------

A switch will need to have SSH set up first, before running this playbook.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Running config
-----------------------


```
service nagle
no service pad
service timestamps debug datetime localtime
service timestamps log datetime localtime
service password-encryption
logging buffered 15000
logging console critical
logging monitor warnings
enable secret 0 cisco
username colin privilege 15 secret 0 cisco
aaa new-model
aaa authentication login default group tacacs+ local
aaa authentication enable default group tacacs+ enable
aaa authorization config-commands
aaa authorization exec default group tacacs+ local
aaa authorization commands 1 default group tacacs+ none
aaa authorization commands 15 default group tacacs+ none
aaa accounting exec default start-stop group tacacs+
aaa accounting network default start-stop group tacacs+
aaa accounting connection default start-stop group tacacs+
aaa accounting system default start-stop group tacacs+
aaa session-id common
clock timezone MST -7
clock summer-time MDT recurring
system mtu routing 1500
vtp mode transparent
ip routing
ip domain-name thenetwork.engineer
ip name-server 10.1.0.102
ip name-server 10.1.0.101
ip name-server 10.1.0.100
login on-failure log every 5
login on-success log
archive
 log config
  logging enable
  logging size 300
  notify syslog contenttype plaintext
  hidekeys
spanning-tree mode rapid-pvst
spanning-tree extend system-id
vlan internal allocation policy ascending
ip ssh time-out 60
ip ssh version 2
ip classless
no ip http server
no ip http secure-server
ip tacacs source-interface Loopback0
ip sla enable reaction-alerts
logging source-interface Loopback0
logging 10.1.0.1
logging 10.1.0.2
snmp-server community ansibull RO 99
snmp-server trap-source Loopback0
snmp-server contact noc@yourcompany.com
snmp-server enable traps ospf state-change
snmp-server enable traps ospf errors
snmp-server enable traps ospf retransmit
snmp-server enable traps ospf lsa
snmp-server enable traps ospf cisco-specific state-change nssa-trans-change
snmp-server enable traps ospf cisco-specific state-change shamlink interface
snmp-server enable traps ospf cisco-specific state-change shamlink neighbor
snmp-server enable traps ospf cisco-specific errors
snmp-server enable traps ospf cisco-specific retransmit
snmp-server enable traps ospf cisco-specific lsa
snmp-server host 10.1.0.3 ansibull
tacacs-server host 10.1.0.4 key 7 <omitted>
tacacs-server host 10.1.0.5 key 7 <omitted>
tacacs-server timeout 3
tacacs-server directed-request
banner login ^-----------------------------------------------------------------------
<SW NAME>
 HODL CORP
 THIS IS A HODL CORP COMPUTER SYSTEM. THIS COMPUTER
 SYSTEM, INCLUDING ALL RELATED EQUIPMENT, NETWORKS AND NETWORK DEVICES
 (SPECIFICALLY INCLUDING INTERNET ACCESS), ARE PROVIDED ONLY FOR
 AUTHORIZED USE. HODL CORP SYSTEMS MAY BE MONITORED
 FOR ALL LAWFUL PURPOSES, INCLUDING TO ENSURE THAT THEIR USE IS
 AUTHORIZED, FOR MANAGEMENT OF THE SYSTEM, TO FACILITATE PROTECTION
 AGAINST UNAUTHORIZED ACCESS, AND TO VERIFY SECURITY PROCEDURES,
 SURVIVABILITY AND OPERATIONAL SECURITY. MONITORING INCLUDES ACTIVE
 ATTACKS BY AUTHORIZED COMPANY ENTITIES TO TEST OR VERIFY THE SECURITY OF
 THIS SYSTEM. DURING MONITORING, INFORMATION MAY BE EXAMINED,
 RECORDED, COPIED AND USED FOR AUTHORIZED PURPOSES. ALL INFORMATION,
 INCLUDING PERSONAL INFORMATION, PLACED ON OR SENT OVER THIS SYSTEM MAY
 BE MONITORED.
 USE OF THIS HODL CORP SYSTEM, AUTHORIZED OR UNAUTHORIZED,
 CONSTITUTES CONSENT TO MONITORING OF THIS SYSTEM. UNAUTHORIZED USE
 MAY SUBJECT YOU TO CRIMINAL PROSECUTION. EVIDENCE OF UNAUTHORIZED USE
 COLLECTED DURING MONITORING MAY BE USED FOR ADMINISTRATIVE, CRIMINAL
 OR OTHER ADVERSE ACTION. USE OF THIS SYSTEM CONSTITUTES CONSENT TO
 MONITORING FOR THESE PURPOSES.
-----------------------------------------------------------------------
^
line con 0
line vty 0 4
 exec-timeout 30 0
 privilege level 15
 transport preferred ssh
 transport input ssh
 transport output ssh
line vty 5 15
 exec-timeout 30 0
 privilege level 15
 transport preferred ssh
 transport input ssh
 transport output ssh
ntp source Loopback0
ntp server 10.1.0.6
ntp server 10.1.0.7
ntp server 10.1.0.8 prefer
port-channel load-balance src-dst-ip 
