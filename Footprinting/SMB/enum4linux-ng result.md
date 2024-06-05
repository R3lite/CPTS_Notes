target:
  host: 10.129.15.244
credentials:
  auth_method: 'null'
  user: ''
  password: ''
  domain: ''
  ticket_file: ''
  nthash: ''
  random_user: oaxksgjq
listeners:
  LDAP:
    port: 389
    accessible: false
  LDAPS:
    port: 636
    accessible: false
  SMB:
    port: 445
    accessible: true
  SMB over NetBIOS:
    port: 139
    accessible: true
domain: DEVOPS
nmblookup:
- DEVSMB          <00> -         H <ACTIVE>  Workstation Service
- DEVSMB          <03> -         H <ACTIVE>  Messenger Service
- DEVSMB          <20> -         H <ACTIVE>  File Server Service
- DEVOPS          <00> - <GROUP> H <ACTIVE>  Domain/Workgroup Name
- DEVOPS          <1e> - <GROUP> H <ACTIVE>  Browser Service Elections
- MAC Address = 00-00-00-00-00-00
smb_dialects:
  Supported dialects:
    SMB 1.0: false
    SMB 2.02: true
    SMB 2.1: true
    SMB 3.0: true
    SMB 3.1.1: true
  Preferred dialect: SMB 3.0
  SMB1 only: false
  SMB signing required: false
smb_domain_info:
  NetBIOS computer name: DEVSMB
  NetBIOS domain name: ''
  DNS domain: ''
  FQDN: nix01
  Derived membership: workgroup member
  Derived domain: unknown
sessions:
  sessions_possible: true
  'null': true
  password: false
  kerberos: false
  nthash: false
  random_user: true
rpc_domain_info:
  Domain: DEVOPS
  Domain SID: NULL SID
  Membership: workgroup member
os_info:
  OS: Linux/Unix
  OS version: '6.1'
  OS release: ''
  OS build: '0'
  Native OS: not supported
  Native LAN manager: not supported
  Platform id: '500'
  Server type: '0x809a03'
  Server type string: Wk Sv PrQ Unx NT SNT InlaneFreight SMB server (Samba, Ubuntu)
users: {}
groups: {}
shares:
  print$:
    type: Disk
    comment: Printer Drivers
    access:
      mapping: denied
      listing: n/a
  sambashare:
    type: Disk
    comment: InFreight SMB v3.1
    access:
      mapping: ok
      listing: ok
  IPC$:
    type: IPC
    comment: IPC Service (InlaneFreight SMB server (Samba, Ubuntu))
policy:
  Domain password information:
    Password history length: None
    Minimum password length: 5
    Maximum password age: 49710 days 6 hours 21 minutes
    Password properties:
    - DOMAIN_PASSWORD_COMPLEX: false
    - DOMAIN_PASSWORD_NO_ANON_CHANGE: false
    - DOMAIN_PASSWORD_NO_CLEAR_CHANGE: false
    - DOMAIN_PASSWORD_LOCKOUT_ADMINS: false
    - DOMAIN_PASSWORD_PASSWORD_STORE_CLEARTEXT: false
    - DOMAIN_PASSWORD_REFUSE_PASSWORD_CHANGE: false
  Domain lockout information:
    Lockout observation window: 30 minutes
    Lockout duration: 30 minutes
    Lockout threshold: None
  Domain logoff information:
    Force logoff time: 49710 days 6 hours 21 minutes
printers: {}
errors:
  listeners:
    enum_listeners:
    - 'Could not connect to LDAP on 389/tcp: connection refused'
    - 'Could not connect to LDAPS on 636/tcp: connection refused'
  shares:
    enum_shares:
    - 'Could not check share: STATUS_OBJECT_NAME_NOT_FOUND'