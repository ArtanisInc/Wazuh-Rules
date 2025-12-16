# Auditd - Linux Security Rules

> The Linux Audit system provides a way to log events that happen on a Linux system. The recording options offered by the Audit system is extensive — process, network, file, user login/logout events, etc.
> Must have Auditd installed.

## Overview

This directory contains **346 Linux security rules** in a single unified file:

| File | Rules | IDs | Description |
|------|-------|-----|-------------|
| **200110-auditd.xml** | 346 | 200110-200468 | Unified Linux security rules (manual + Sigma auto-generated) |

## 📄 200110-auditd.xml Structure

The file contains two types of rules merged together:

### Manual Rules (200110-200186) - 64 rules
**Characteristics:**
- ✅ Hand-crafted rules optimized for specific detection patterns
- ✅ 58/64 rules with MITRE ATT&CK mappings (91%)
- ✅ Uses precise field matching (`audit.execve.a0`, `audit.directory.name`)
- ✅ 1 CDB list integration for bash_profile monitoring
- ✅ Based on 41 Sigma rules, manually converted and enhanced
- ✅ Includes Sigma source links in XML comments

**Coverage:**
- Process execution (SYSCALL, EXECVE)
- File system operations (PATH)
- Configuration changes (CONFIG_CHANGE)
- User and credential management (USER_AND_CRED)

**Example Rule:**
```xml
<!-- https://github.com/SigmaHQ/sigma/blob/master/rules/linux/auditd/lnx_auditd_coinminer.yml -->
<rule id="200132" level="12">
  <if_sid>200111</if_sid>
  <field name="audit.execve.a1">--cpu-priority</field>
  <description>Detects command line parameter used by mining software.</description>
  <mitre>
    <id>T1496</id>
  </mitre>
</rule>
```

### Sigma Auto-Generated Rules (200187-200468) - 282 rules
**Characteristics:**
- ✅ Auto-generated from SigmaHQ repository using [StoW converter](https://github.com/ArtanisInc/StoW)
- ✅ 260/282 rules with MITRE ATT&CK mappings (92%)
- ✅ All rules have Sigma source links (`<info type="link">`)
- ✅ 92/282 rules configured for email alerts (33%)
- ✅ Uses PCRE2 regex patterns for flexible matching
- ✅ Comprehensive metadata (Author, Created, Modified, Sigma ID, Status)

**Coverage Categories:**
- **Auditd/Execve**: Process execution, command-line analysis
- **Clamav**: Antivirus log detection
- **Cron**: Scheduled task manipulation
- **Guacamole**: Remote access detection
- **Modsecurity**: Web application firewall logs
- **Sshd**: SSH daemon activity
- **Sudo**: Privilege escalation monitoring
- **Syslog**: System log analysis
- **Process Creation**: Linux process creation detection
- **Vsftpd**: FTP server security

**Example Rule:**
```xml
<rule id="200187" level="12">
  <info type="link">https://github.com/SigmaHQ/sigma/tree/master/rules/linux/auditd/execve/lnx_auditd_binary_padding.yml</info>
  <!--     Author: Igor Fits, oscd.community-->
  <!--Description: Adversaries may use binary padding to add junk data...-->
  <!--   Sigma ID: c52a914f-3d8b-4b2a-bb75-b3991e75f8ba-->
  <mitre>
    <id>T1027.001</id>
  </mitre>
  <description>Binary Padding - Linux</description>
  <options>no_full_log</options>
  <options>alert_by_email</options>
  <group>linux,auditd,</group>
  <field name="audit.type" type="pcre2">(?i)EXECVE</field>
  <field name="full_log" type="pcre2">(?i)truncate</field>
  <field name="full_log" type="pcre2">(?i)-s</field>
</rule>
```

## 🔄 Rule Overlap

**Some rules exist with different detection approaches** between manual and Sigma sections. This is intentional - having multiple detection methods increases coverage.

## [Auditd Configuration](https://github.com/ArtanisInc/Wazuh-Rules/blob/main/Auditd/auditd.conf)

Use the provided auditd rules to get started. These rules configure the Linux kernel to generate audit events.

### Custom Decoders

Use custom decoders rather than the ones provided by Wazuh. There were issues during testing with default decoders.

Remember to exclude Wazuh's default auditd decoder and rules within the `ossec.conf` of the manager:

```xml
<ruleset>
    <!-- Default ruleset -->
    <decoder_dir>ruleset/decoders</decoder_dir>
    <decoder_exclude>ruleset/decoders/0040-auditd_decoders.xml</decoder_exclude>
    <rule_dir>ruleset/rules</rule_dir>
    <rule_exclude>0215-policy_rules.xml</rule_exclude>
    <rule_exclude>0365-auditd_rules.xml</rule_exclude>

    <!-- Required CDB Lists -->
    <list>etc/lists/audit-keys</list>
    <list>etc/lists/bash_profile</list>

    <!-- User-defined ruleset -->
    <decoder_dir>etc/decoders</decoder_dir>
    <rule_dir>etc/rules</rule_dir>
</ruleset>
```

## 📊 Statistics Summary

| Metric | Manual (200110-200186) | Sigma (200187-200468) | Total |
|--------|------------------------|----------------------|-------|
| **Total Rules** | 64 | 282 | **346** |
| **MITRE Coverage** | 58 (91%) | 260 (92%) | 318 (92%) |
| **Field Matching** | 54 (84%) | 282 (100%) | 336 (97%) |
| **Email Alerts** | 0 | 92 (33%) | 92 (27%) |
| **Format** | Field-based | PCRE2 regex | Mixed |

## 🎯 Recommended Usage

1. **Deploy 200110-auditd.xml** for comprehensive Linux coverage
2. **Monitor alerts** initially for false positives
3. **Tune email alerts** by adjusting rules with `<options>alert_by_email</options>`
4. **Create exclusions** in Exclusion Rules directory as needed
5. **Update periodically** - Sigma rules can be regenerated with StoW

## 📈 Coverage Breakdown

### By Detection Category
- **Process Execution**: ~180 rules (auditd execve, process creation)
- **File System**: ~40 rules (path monitoring, file modifications)
- **Authentication**: ~30 rules (SSH, sudo, user/cred)
- **Configuration**: ~25 rules (cron, system config, auditing)
- **Network**: ~20 rules (guacamole, FTP, network tools)
- **Logging**: ~15 rules (syslog, clamav, modsecurity)
- **Other**: ~36 rules (various Linux security events)

### By Severity Level
- **Critical (15)**: Webshell RCE, critical exploits
- **High (12-13)**: Privilege escalation, credential access, persistence
- **Medium (10)**: Suspicious activities, potential threats
- **Low (7)**: Reconnaissance, information gathering
- **Info (3-5)**: Baseline events, informational

## 🔗 References

- [Linux Auditd Documentation](https://man7.org/linux/man-pages/man8/auditd.8.html)
- [SigmaHQ Rules Repository](https://github.com/SigmaHQ/sigma)
- [StoW Sigma Converter](https://github.com/ArtanisInc/StoW)
- [MITRE ATT&CK for Linux](https://attack.mitre.org/matrices/enterprise/linux/)
- [Wazuh Auditd Integration](https://documentation.wazuh.com/current/proof-of-concept-guide/detect-unauthorized-processes-netcat.html)

## 📝 Notes

- The file size is 189KB - within Wazuh's recommended limits
- Manual rules use standard Wazuh field matching
- Sigma rules use PCRE2 regex for more flexible pattern matching
- Both styles are valid and supported by Wazuh 4.x+
- Consider splitting into multiple files if performance issues arise (>500 rules per file is recommended maximum)
