# 2.Initial Access

##  Objective
The goal of this phase was to gain elevated access on the initial foothold machine by identifying and leveraging exposed credentials within the environment.

---

## Approach

After completing enumeration, the focus shifted to identifying potential misconfigurations that could lead to privilege escalation or credential exposure.

Network shares were specifically targeted, as they often contain sensitive information due to improper access controls.

---

##  Network Share Enumeration

The following command was used to identify accessible shares on a domain system:

```cmd
net view \\<TARGET_MACHINE> /all
```
- The above command revealed all the available shared resources on the network.

---

## Findings

Credentials for a local administrative account were exposed in a shared directory.

## Impact

- This allowed escalation from a standard domain user to a privileged user on the system.

---

## Privilege Abuse

The discovered credentials were used to spawn a new session with elevated privileges.

```cmd
runas /user:<admin_user> cmd
```
- Using this command we gained access to a command prompt with administrative privileges.
