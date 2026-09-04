# Configure-Named-Standard-IPv4-ACLs

# Packet Tracer – Configure Named Standard IPv4 ACLs

## Overview

This lab demonstrates how to configure a **named standard IPv4 Access Control List (ACL)** on a Cisco router to control access to a File Server. Only **PC1 (192.168.20.4)** and the **Web Server (192.168.100.100)** are allowed to access the File Server, while all other devices are denied.

## Objectives

* Configure a named standard IPv4 ACL.
* Allow only authorized hosts to access the File Server.
* Apply the ACL to the correct router interface.
* Verify the ACL configuration and operation.

## Configuration

```bash
enable
configure terminal

ip access-list standard File_Server_Restrictions
 permit host 192.168.20.4
 permit host 192.168.100.100
 deny any

interface fastEthernet 0/1
 ip access-group File_Server_Restrictions out

end
copy running-config startup-config
```

## Verification

Use the following commands to verify the ACL:

```bash
show access-lists
show run
show ip interface fastEthernet 0/1
```

## Testing

| Source             | Web Server | File Server |
| ------------------ | ---------- | ----------- |
| PC0 (192.168.20.3) | ✅ Allowed  | ❌ Denied    |
| PC1 (192.168.20.4) | ✅ Allowed  | ✅ Allowed   |
| PC2 (192.168.10.3) | ✅ Allowed  | ❌ Denied    |
| Web Server         | N/A        | ✅ Allowed   |

## Result

The named ACL successfully restricts access to the **File Server** by permitting only **PC1** and the **Web Server**, while denying all other hosts. This demonstrates how standard ACLs filter traffic based on the **source IP address** to improve network security.
