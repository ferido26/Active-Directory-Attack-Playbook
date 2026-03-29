# 1.Enumeration Phase

## Objective
The goal of this phase was to gather as much information as possible about the Active Directory environment using a low-privileged domain user account from the STDVM machine, which consisted of multiple domain-joined systems.


This includes identifying:
- Domain users
- Computers
- Groups
- Potential attack paths

---

## Approach

Enumeration is the most critical phase in any Active Directory attack.  
Instead of exploiting immediately, the focus was on understanding the environment and identifying misconfigurations.

---

## Tools Used

- PowerView
- BloodHound 
- SharpHound (Used to collect data for bloodhound)

---

## Domain Enumeration

Using PowerView, key domain information was extracted.

###  Enumeration Commands I used 
```powershell
- Get-DomainUser | select samaccountname
- Get-DomainComputers | dnshostname
- Get-DomainGroup -Identity DomainAdmins
- get-DomainGroupMember -Identity DomainAdmins
```

## What I Learned!
- Without enumeration you cannot plot a successfull attack path.
- Even low-privileged users can gather significant domain information.
- Tools like BloodHound simplify complex AD relationships.
  
---

## Summary

- The enumeration phase provided a clear understanding of the domain structure and revealed multiple potential attack paths, which were leveraged in later stages of the attack.
