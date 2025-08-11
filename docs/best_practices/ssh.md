# SSH Best Practices

Securing SSH connections is critical to protect our infrastructure. Below are the recommended best practices for managing SSH access within the company.

---

## 1. Use SSH Keys

- **Prefer SSH key authentication** over password-based login.
- Generate a strong RSA or ED25519 key pair (`ssh-keygen -t ed25519`).
- Never share your private key.
- Add your public key to the target server’s `~/.ssh/authorized_keys` file.

---

## 2. Disable Direct Root Login

- Modify the SSH configuration file `/etc/ssh/sshd_config`:
  ```bash
  PermitRootLogin no
  ```

* Use a standard user account with sudo privileges for administrative tasks.

---

## 3. Change Default SSH Port

* Change the SSH port (e.g., to 2222) to reduce automated scans.
* In `/etc/ssh/sshd_config`:

  ```bash
  Port 2222
  ```
* Update firewall rules accordingly.

---

## 4. Implement Two-Factor Authentication (2FA)

* Set up multi-factor authentication (e.g., Google Authenticator, YubiKey).
* Install and configure `libpam-google-authenticator` or similar solutions.

---

## 5. Restrict SSH Access

* Limit SSH access to authorized IP ranges using firewall rules.
* Example using `iptables`:

  ```bash
  iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 2222 -j ACCEPT
  iptables -A INPUT -p tcp --dport 2222 -j DROP
  ```

---

## 6. Monitoring and Auditing

* Enable and regularly review SSH logs:

  * `/var/log/auth.log` (Debian/Ubuntu)
  * `/var/log/secure` (CentOS/RHEL)
* Set up alerts for failed login attempts.
* Use tools like `fail2ban` to block malicious IPs.

---

## 7. Additional Recommendations

* Never share private keys.
* Always protect private keys with strong passphrases.
* Revoke unused keys or accounts promptly.

---

**This documentation will be updated regularly to reflect the latest security best practices.**

---

*Sky Genesis Enterprise — Best Practices Team*
