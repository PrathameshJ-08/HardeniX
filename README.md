# 🛡️ HardeniX – Security-as-Code Linux Hardening Framework

HardeniX is a Ansible-based framework designed to automate the security hardening of Linux systems in alignment with industry best practices such as the CIS Benchmarks.

## 🚀 Features

- ✅ CIS-based system hardening
    
- 🔒 SSH hardening (custom port, disable root login, no password auth)
    
- 🔥 UFW firewall configuration (default deny, allow HTTP/S & SSH)
    
- 🧩 Password policy enforcement (expiration, age)
    
- 🛠️ Security tools installation:
    
    - Lynis (automated weekly scan)
        
    - Fail2Ban (brute-force protection)
        
    - auditd and AIDE (file integrity and auditing)
        

## 📁 Project Structure

```
hardeniX/
├── inventory/
│   └── hosts.yml
├── playbooks/
│   └── main.yml
├── roles/
│   ├── hardening/
│   │   └── tasks/main.yml
│   ├── ssh/
│   │   ├── tasks/main.yml
│   │   └── templates/sshd_config.j2
│   ├── firewall/
│   │   └── tasks/main.yml
│   ├── tools/
│   │   └── tasks/main.yml
│   └── auditing/
│       └── tasks/main.yml
└── README.md
```

## 🛠️ Prerequisites

- Two Linux VMs (e.g., Ubuntu 22.04)
    
    - Control Node (Ansible + Git installed)
        
    - Target Node (reachable via SSH)
        
- Ansible installed on control node
    
- Passwordless SSH setup between control and target
    

## 🔧 Setup Instructions

1. Clone the repo on the control node:
    
    ```bash
    git clone https://github.com/PrathameshJ-08/hardenix.git
    cd hardenix
    ```
    
2. Edit inventory/hosts.yml with your target IP and SSH user.
    
3. Run the playbook:
    
    ```bash
    ansible-playbook -i inventory/hosts.yml playbooks/main.yml --ask-become-pass
    ```
    

## 🔍 Post-Deployment Checks

- SSH on new port:
    
    ```bash
    ssh -p 2222 user@<target_ip>
    ```
    
- Check UFW:
    
    ```bash
    sudo ufw status verbose
    ```
    
- Trigger Lynis scan:
    
    ```bash
    sudo lynis audit system
    ```
    
- Verify Fail2Ban and AIDE:
    
    ```bash
    sudo systemctl status fail2ban
    ls /var/lib/aide/
    ```
    
