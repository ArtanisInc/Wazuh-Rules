# Advanced Wazuh Detection Rules

> We have committed to contributing to the Open Source community. We hope you find these rulesets helpful and robust as you work to keep your networks secure.

[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![MIT License][license-shield]][license-url]

## About This Repo
The objective for this repo is to provide the Wazuh community with rulesets that are more accurate, descriptive, and enriched from various sources and integrations. Wazuh serves as a great EDR agent, but we believe the default rulesets can be strengthened. We are building a repository of strong Wazuh rules for the community to implement and expand upon.

## Supported Rules and Integrations

### Windows Security
*   [Sysmon New Events](Sysmon%20New%20Events)
*   [Sysmon](Windows_Sysmon)
*   [Powershell](Windows%20Powershell)
*   [Sigma Rules](Windows%20Sigma%20Rules)

### Linux Security
*   [Auditd](Auditd)

### Endpoint Protection & Threat Intelligence
*   [F-Secure](F-Secure)
*   [Yara](Yara)

### Operations & Management
*   [Active Response](Active_Response)
*   [Wazuh Inventory](Wazuh%20Inventory)
*   [Wazuh SCA](Wazuh%20SCA)
*   [Exclusion Rules](Exclusion%20Rules)

## Getting Started

### Prerequisites
*   Wazuh-Manager Version 4.x

### Installation
_You can either manually download the .xml rule files onto your Wazuh Manager or make use of our `wazuh_rules.sh` script._

1. Become Root User
2. Run the Script
   ```sh
   curl -so ~/wazuh_rules.sh https://raw.githubusercontent.com/ArtanisInc/Wazuh-Rules/main/wazuh_rules.sh && bash ~/wazuh_rules.sh
   ```

> :warning: **USE AT OWN RISK**: If you already have custom rules, duplicate Rule IDs might exist. Ensure there are no conflicts before adding these rules.

## Contributing
Contributions are greatly appreciated!
1. Fork the Project
2. Create your Feature Branch (`git checkout -b ruleCategory/DetectionRule`)
3. Commit your Changes (`git commit -m 'Add some DetectionRules'`)
4. Push to the Branch (`git push origin ruleCategory/DetectionRule`)
5. Open a Pull Request

[forks-shield]: https://img.shields.io/github/forks/ArtanisInc/Wazuh-Rules
[forks-url]: https://github.com/ArtanisInc/Wazuh-Rules/network/members
[stars-shield]: https://img.shields.io/github/stars/ArtanisInc/Wazuh-Rules
[stars-url]: https://github.com/ArtanisInc/Wazuh-Rules/stargazers
[license-shield]: https://img.shields.io/badge/License-MIT-blue.svg
[license-url]: https://github.com/ArtanisInc/Wazuh-Rules/blob/main/LICENSE

## Credits
*   Thanks to [SOCFortress](https://www.socfortress.co) for the initial work and inspiration.
