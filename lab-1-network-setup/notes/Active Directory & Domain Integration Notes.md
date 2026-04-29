# Active Directory & Domain Integration Notes

## 🧱 Domain Controller Setup

* Installed Active Directory Domain Services (AD DS)
* Promoted Windows Server 2022 to Domain Controller
* Created domain: `lab.local`

## 👤 User & Organizational Unit

* Created Organizational Unit (OU) for structure
* Created domain user: `labuser`

## 💻 Client Configuration (Windows 10)

* Renamed machine: `WIN10-CLIENT`
* Configured static IP and DNS:

  * IP: 192.168.100.10
  * DNS: 192.168.100.5

## 🌐 Domain Join Process

* Joined Windows 10 client to: `lab.local`
* Authenticated using: `LAB\labuser`

## 🧪 Validation

* Confirmed domain join via “Welcome to lab.local” message
* Verified domain login from Windows 10 client
* Tested network connectivity using ping to the Domain Controller

## 🧠 Key Learning Points

* DNS is critical for Active Directory functionality
* Static IP configuration is required in isolated lab environments
* Domain Controllers handle both authentication and DNS services
* Successful domain integration depends on proper network communication
