# MYNAS – Enterprise NAS Management Tool

**Version:** 1.0.0  
**Author:** Koosha Yeganeh  
**License:** GPL-3.0 (or your preferred open-source license)

---

## 📦 Overview

`mynas` is a comprehensive Bash-based NAS (Network Attached Storage) management tool for converting any Linux machine into an enterprise-grade storage server. It includes powerful modules for:

- Storage configuration
- NFS and Samba sharing
- RAID and user management
- Backup and antivirus scanning
- Monitoring (I/O, SMART, Netdata)
- Network and firewall control
- SSHFS mounting and more...

---

## ⚙️ Features

✅ Distribution detection (Debian, Ubuntu, openSUSE)  
✅ Easy backups (tar, zip, disk clone with `dd`)  
✅ NFS, Samba, SSHFS share management  
✅ Disk health check via `smartctl`  
✅ RAID creation and maintenance with `mdadm`  
✅ Firewall rules (iptables & firewalld)  
✅ Monitoring with Netdata and `iostat`  
✅ Antivirus scanning with ClamAV, Maldet, RKHunter, chkrootkit  
✅ Network bonding, bridging, IP setup  
✅ Full service and user management support  

---

## 🚀 Quick Start

```bash
chmod +x mynas
sudo ./mynas --help        # Display help
sudo ./mynas --version     # Show version
sudo ./mynas --monitor     # Run I/O monitor
````

---

## 📘 Usage Examples

### ✅ System Update

```bash
sudo ./mynas --system
```

### ✅ Storage Format and Mount

```bash
sudo ./mynas --storage format /dev/sdb ext4
sudo ./mynas --storage mount /dev/sdb1 /mnt/storage
```

### ✅ Setup Samba Share

```bash
sudo ./mynas --samba install
sudo ./mynas --samba add-share shared_folder /mnt/storage user1
```

### ✅ Monitor Disk Health & Netdata

```bash
sudo ./mynas --monitor --disk-health
sudo ./mynas --monitor --netdata start
```

### ✅ Backup Home Directory

```bash
sudo ./mynas --backup --tar /home/user
sudo ./mynas --backup --zip /var/www
sudo ./mynas --backup --dd /dev/sda
```

---

## 🛠 Modules and Subcommands

| Module       | Subcommands                                                                                             |
| ------------ | ------------------------------------------------------------------------------------------------------- |
| `--system`   | Update packages                                                                                         |
| `--storage`  | `list`, `format`, `mount`, `umount`, `info`                                                             |
| `--backup`   | `--tar`, `--zip`, `--dd`                                                                                |
| `--av`       | `--clamav`, `--maldet`, `--rkhunter`, `--chkrootkit`, `--update-databases`                              |
| `--monitor`  | `--iostat`, `--netdata`, `--disk-health`                                                                |
| `--nfs`      | `install`, `add-share`                                                                                  |
| `--samba`    | `install`, `add-share`                                                                                  |
| `--sshfs`    | `install`, `mount`                                                                                      |
| `--firewall` | iptables/firewalld specific commands                                                                    |
| `--raid`     | `create`, `add`, `remove`, `stop`, `status`, `save`                                                     |
| `--network`  | `list-interfaces`, `set-ip`, `set-gateway`, `set-dns`, `test`, `bridge`, `bond`                         |
| `--service`  | `start`, `stop`, `restart`, `status`, `enable`, `disable`, `mask`, `unmask`                             |
| `--user`     | `add`, `remove`, `list`, `passwd`, `add-to-group`, `remove-from-group`, `list-groups`, `lock`, `unlock` |

---

## 📂 Logs

All logs are stored in:

```
/var/log/mynas/
```

Each session is timestamped for clarity and debugging.

---

## 🧩 Dependencies

* `smartmontools`
* `sysstat` (for `iostat`)
* `netdata`
* `mdadm`
* `iptables` / `firewalld`
* `clamav`, `maldet`, `rkhunter`, `chkrootkit`
* `sshfs`
* `zip`, `tar`, `dd`

Installations are handled automatically where applicable.

---

## 🔒 Security Note

Make sure to run `mynas` as root or with `sudo` for full functionality.
Always review firewall and AV rules to ensure system security.

---

## 💡 Contribution

If you'd like to contribute improvements or report bugs:

1. Fork the repository
2. Create a branch (`feature/new-feature`)
3. Submit a pull request

---

## 🧾 License

This tool is released under **GNU GPL v3.0**.
Feel free to use, modify, and distribute under the same license.

---

## 📞 Contact

For questions, contributions, or partnerships:
**Koosha Yeganeh**
📧 [kooshakooshadv@gmail.com](mailto:kooshakooshadv@gmail.com)
🌐 [kooshayeganeh.github.io](http://kooshayeganeh.github.io)

