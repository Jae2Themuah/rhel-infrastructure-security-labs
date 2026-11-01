# Project 01: Linux Identity & Access Management

## Project Overview

This project documents hands-on Linux administration exercises completed using Red Hat Enterprise Linux browser-based training labs.

The objective was to develop practical skills in managing Linux users, groups, file ownership, permissions, and access controls.

**Environment:** Red Hat Enterprise Linux (RHEL) training labs  
**Training:** RHCSA preparation  
**Status:** Guided exercises completed; independent validation ongoing  
**Date:** November 1, 2026

## 1. User and Group Administration

Practiced creating Linux users and groups.

```bash
useradd guest1
groupadd linuxadmins
usermod -aG linuxadmins guest1
```

Verified user and group membership:

```bash
id guest1
getent group linuxadmins
```

### Skills Demonstrated
- Creating local Linux users
- Creating groups
- Managing supplementary group membership
- Verifying user identities and group assignments

## 2. File Ownership Management

Practiced changing file ownership and group ownership.

```bash
chown guest1:linuxadmins /root/project.txt
chgrp linuxadmins /home/linuxprojects
```

Verified ownership using:

```bash
ls -l /root/project.txt
```

## 3. Linux File Permissions

Practiced configuring file permissions using numeric notation.

```bash
chmod 640 /root/project.txt
chmod 750 /root/project.txt
```

Permission examples:

| Mode | Owner | Group | Others |
|---|---|---|---|
| 640 | Read/Write | Read | None |
| 750 | Read/Write/Execute | Read/Execute | None |
| 770 | Full Access | Full Access | None |

## 4. Shared Directory Configuration

Created a shared directory for authorized group members.

```bash
mkdir /home/linuxprojects
chgrp linuxadmins /home/linuxprojects
chmod g+w /home/linuxprojects
chmod o-rx /home/linuxprojects
chmod g+s /home/linuxprojects
```

The setgid permission was configured so newly created files inherit the directory's group ownership.

Verified directory permissions using:

```bash
ls -ld /home/linuxprojects
```

Expected configuration:

```text
drwxrws--- root linuxadmins
```

## 5. Access Control Testing

Tested access restrictions using separate Linux accounts.

```bash
useradd guest4
id guest4
runuser -u guest4 -- touch /home/linuxprojects/guest4test.txt
```

The test returned:

```text
Permission denied
```

This demonstrated that the unauthorized user could not create files inside the restricted directory.

## 6. Permission-Based File Searches

Practiced identifying files based on their permission settings.

```bash
find /root -type f -perm 640
```

The search successfully identified:

```text
/root/project.txt
```

Also studied identifying world-writable files:

```bash
find /root -type f -perm -002
```

## 7. Troubleshooting

During the exercises, several issues were encountered and resolved.

| Issue | Resolution |
|---|---|
| Invalid group | Created the required group using `groupadd` |
| Directory not found | Created the directory using `mkdir` |
| Incorrect ownership command | Corrected `chown` syntax |
| Incorrect file path | Verified the filename and directory |
| Incorrect `find` syntax | Added the required space between command and path |

These exercises reinforced the importance of interpreting Linux error messages and verifying configurations.

## 8. Security Relevance

This project introduced several security principles:

- Principle of least privilege
- User and group-based access control
- File ownership and permission management
- Restricting unauthorized access
- Shared directory security
- Identifying potentially insecure file permissions

These concepts provide a foundation for future studies involving SELinux, DISA STIGs, and NIST SP 800-171.

## 9. Lessons Learned

Key takeaways:

1. File ownership and file permissions serve different purposes.
2. Supplementary group membership can provide access to shared resources.
3. Setgid enables group ownership inheritance in shared directories.
4. File permissions must be evaluated alongside parent directory permissions.
5. Linux error messages are useful troubleshooting tools.

## 10. Next Steps

- Reinforce numeric and symbolic permissions
- Practice independently configuring user access
- Study default permissions and umask
- Learn Linux Access Control Lists (ACLs)
- Continue RHCSA system administration training
- Recreate this project in an independently configured RHEL environment

---

**Documentation Note:** This project records guided exercises performed in temporary Red Hat training environments. It does not represent a production deployment, RHCSA certification, or a completed compliance assessment.
