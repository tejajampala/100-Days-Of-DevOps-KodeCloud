# Install and Configuration Selinux

Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:

- Install the required SELinux packages.
- Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.
- No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.
- Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

## Steps

1. Install selinux packages:

   <img width="968" height="547" alt="image" src="https://github.com/user-attachments/assets/d4089a9e-56ae-4f85-b48a-d77ca8825d85" />


    ```sh
    sudo dnf install selinux-policy selinux-policy-targeted policycoreutils policycoreutils-python-utils
    ```

    <img width="667" height="745" alt="image" src="https://github.com/user-attachments/assets/d07d6ab6-9801-4482-9898-c8a94012d04c" />


2. Modify file in `/etc/selinux/config:

    

    ```sh
    sudo vi /etc/selinux/config
    ```

    updated the below line from enforced to disabled:

    ```sh
    SELINUX=disabled
    ```

<img width="957" height="710" alt="image" src="https://github.com/user-attachments/assets/f82fff0b-3918-4035-9e39-486cc496f3db" />




## Good to Know?

### SELinux (Security-Enhanced Linux)

- **Purpose**: Mandatory Access Control (MAC) security framework
- **Modes**: Enforcing, Permissive, Disabled
- **Policies**: Targeted (default), Strict, MLS (Multi-Level Security)
- **Context**: Every file/process has security context (user:role:type:level)

### SELinux States

- **Enforcing**: Policies actively enforced, violations blocked
- **Permissive**: Policies logged but not enforced (audit mode)
- **Disabled**: SELinux completely turned off

### Key Commands

- `getenforce`: Check current SELinux mode
- `setenforce 0/1`: Temporarily set permissive/enforcing
- `sestatus`: Detailed SELinux status
- `sealert`: Analyze SELinux denials

### Configuration Files

- `/etc/selinux/config`: Main configuration
- `/var/log/audit/audit.log`: SELinux violations
- `/etc/selinux/targeted/`: Policy files
