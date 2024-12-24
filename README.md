# TFTP Enumeration

## Description

Trivial File Transfer Protocol (TFTP) is a simple lockstep File Transfer Protocol that allows a client to get a file from or put a file onto a remote host.

---

## 1. Finding Live Hosts on the Network

Start with the command below to find live hosts on a network:

```bash
nmap -sn target_ip
```

---

## 2. Finding Open Ports for Identified Hosts

Identify the TFTP port on the network. Typically, it runs on UDP port 69:

```bash
nmap -v -sU -p 69 target_ip
```

---

## 3. Connecting with the Server

Use the TFTP client tool to communicate with the TFTP server:

```bash
tftp target_ip
```

---

## 4. Attempting to List or Retrieve Files

Directory listing is not available on TFTP. However, if you know the file name, you can download or retrieve the file:

```bash
tftp> get filename
```

### Basic Commands

|  Command  |       Description       |
|:---------:|:-----------------------:|
|   `get`   |      Receive file       |
|   `put`   |       Send file         |
|  `quit`   |       Exit TFTP         |
| `verbose` |  Toggle verbose mode    |
| `binary`  |    Set mode to octet    |
|  `ascii`  |  Set mode to netascii   |

### Sample Files to Retrieve

|         File Name          |             Description             |
|:--------------------------:|:-----------------------------------:|
|       `config.txt`         |      General configuration file     |
|    `startup-config`        |      Initial startup configuration  |
|    `network-config`        |         Network configurations      |
|      `backup.cfg`          |       Backup configuration file     |
| `pxelinux.cfg/default`     | Used in PXE boot environments       |

---

## 5. Attempting to Upload Files

If nothing is found to download, try uploading a sample file. If the web directory and TFTP share the same path, you may attempt to get a reverse shell by uploading a reverse shell file.

### Example:

Upload a sample file:

```bash
put test.txt
```

Download the same file with the `get` command:

```bash
get test.txt
```

---

## 6. Analyzing Retrieved Files

Files retrieved from the TFTP server may contain sensitive information. It is crucial to analyze them thoroughly. Examples of such files include:

- Network Configuration Files
- Boot Configuration Files
- User Information and Passwords
- Log Files
- Backup Files

---

## 7. Open Source Exploits

After enumeration and version detection, search for publicly available exploits related to the identified version.

Use the following command:

```bash
nmap -sU -p 69 --script=tftp-version.nse target_ip
```

### Resources

- [Exploit Database](https://www.exploit-db.com): Exploits, Shellcode, 0days, Remote Exploits, Local Exploits, Web Apps, Vulnerability Reports.
- [CVE Details](https://www.cvedetails.com): CVE security vulnerability database, exploits, and references.

---

## 8. Using the Metasploit Framework

Metasploit provides a module to brute-force directories on TFTP.

### Steps:

1. Start Metasploit:
   ```bash
   msfconsole
   ```

2. Load the TFTP brute-force module:
   ```bash
   use auxiliary/scanner/tftp/tftpbrute
   ```

3. Set the target:
   ```bash
   set RHOSTS <target>
   ```

4. Run the module:
   ```bash
   run
   ```

---

## Reference

- [HackTricks - TFTP Enumeration](https://book.hacktricks.xyz/network-services-pentesting/69-udp-tftp)

