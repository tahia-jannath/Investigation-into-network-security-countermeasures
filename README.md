# Investigation-into-network-security-countermeasures
# SSH, MFA & Cowrie Honeypot

## Project Description

This project demonstrates the design, implementation, testing, and evaluation of a secured Ubuntu-based network environment using the Azure Virtual Lab.

The project focuses on reducing network security risks by implementing a hardened OpenSSH server, Multi-Factor Authentication (MFA), a Cowrie SSH honeypot, and an `iptables` firewall. Security monitoring was also implemented through system and firewall logging to identify legitimate SSH activity, honeypot interactions, and blocked network traffic.

The project aligns with the CSI6202 Network Security learning outcomes:

* **ULO 2:** Evaluate a contemporary network for vulnerabilities and implement effective risk reduction strategies.
* **ULO 3:** Design a secure network to withstand contemporary cybersecurity attacks.

---

## Purpose of the Project

The main purpose of this project is to evaluate and improve the security of a network server by implementing practical security controls against common attack techniques.

The project demonstrates how multiple layers of security can work together:

* Hardened SSH configuration reduces unauthorised access risks.
* Key-based authentication removes reliance on SSH passwords.
* MFA provides an additional authentication factor.
* Cowrie acts as a honeypot to capture and monitor suspicious SSH activity.
* `iptables` restricts incoming network traffic.
* Logging provides visibility into SSH connections, honeypot activity, and blocked traffic.
* Port scanning is used to evaluate the visibility and exposure of network services.

---

## Project Scope

The project covers the following security components:

### 1. OpenSSH Security Hardening

An OpenSSH server was implemented on the Ubuntu server with a baseline security configuration.

The configuration included:

* Disabling password-based SSH authentication.
* Implementing key-based authentication.
* Changing the default SSH port to **2220**.
* Configuring a login banner containing the student's identification details.
* Disabling:

  * `AllowTCPForwarding`
  * `GatewayPorts`
  * `PermitRootLogin`
  * `HostbasedAuthentication`
  * `PermitEmptyPasswords`
  * `X11Forwarding`

### 2. Multi-Factor Authentication

MFA was implemented for OpenSSH to provide an additional authentication layer beyond the SSH key.

The configuration was subsequently tested by connecting from another VM or host.

### 3. Cowrie Honeypot

Cowrie was installed and configured as an SSH honeypot.

The honeypot was configured with:

* Hostname: `myGov`
* Two permitted users:

  * `root`
  * `staff`
* Pre-defined authentication credentials according to the assessment requirements.
* Monitoring of commands executed during honeypot sessions.

The honeypot was used to simulate an exposed SSH service and record attacker-like behaviour.

### 4. Firewall Configuration

`iptables` was implemented as the network firewall.

The firewall configuration was designed to:

* Allow incoming traffic to the OpenSSH service.
* Allow incoming traffic to the Cowrie service.
* Block other incoming traffic.
* Log SSH traffic.
* Log honeypot traffic.
* Log blocked traffic.

The required log identifiers were:

```text
SSH TRAFFIC >
HONEYPOT TRAFFIC >
BLOCKED TRAFFIC >
```

### 5. Security Monitoring

Logging was used to monitor network and application activity.

The project examined:

* SSH connection attempts.
* Cowrie login activity.
* Commands executed inside the honeypot.
* Blocked network traffic.
* Ping activity.
* Firewall detection of SSH and Cowrie connections.

### 6. Vulnerability Evaluation

The final stage involved performing different port scans against the SSH server and analysing the results.

Two weaknesses in the current configuration were also identified, with security improvements recommended to address them.

---

## Project Evolution

The project progressed through several stages, starting with basic server configuration and gradually introducing additional security controls.

### Phase 1: Initial Server Setup

An Ubuntu server was prepared in the Azure Virtual Lab environment. The initial focus was establishing the server environment and preparing it for network security configuration.

### Phase 2: SSH Hardening

OpenSSH was installed and configured using a security baseline. Password authentication was disabled and key-based authentication was introduced. The SSH service was also moved from its default port to port **2220**.

Additional SSH features that were not required were disabled to reduce the attack surface.

### Phase 3: MFA Implementation

Multi-Factor Authentication was introduced to provide another layer of protection for SSH access.

This strengthened the authentication process by requiring more than the SSH key alone.

### Phase 4: Honeypot Deployment

Cowrie was installed and configured as an SSH honeypot.

The honeypot provided a controlled environment for observing suspicious login attempts and commands without exposing the actual SSH service.

### Phase 5: Firewall Implementation

`iptables` rules were introduced to restrict incoming network traffic.

Only the required SSH and Cowrie services were permitted, while other incoming traffic was blocked and logged.

### Phase 6: Monitoring and Validation

The final configuration was tested from another VM or host.

SSH authentication, MFA, Cowrie connections, firewall behaviour, logging, and port scanning were examined to validate the security controls.

---

## Testing and Validation

Testing was performed to verify that the implemented security controls behaved as expected.

### SSH Testing

A connection was attempted from another VM or host to verify that the hardened OpenSSH service was accessible using the configured authentication method and MFA.

The SSH configuration was inspected to confirm that the required security controls were active.

### MFA Testing

An SSH connection was performed using MFA to verify that the additional authentication mechanism was functioning correctly.

### Cowrie Testing

The Cowrie service was accessed from another machine.

The following activities were performed within the honeypot:

```text
ls
cat /etc/passwd
rm ~/.bashrc_history
curl ecu.edu.au
```

The Cowrie logs were then examined to verify that the connection and commands had been recorded.

### Firewall Testing

A ping was performed against the SSH server to test the firewall's handling and logging of network traffic.

SSH and Cowrie connections were also performed and their corresponding firewall log entries were examined.

### Log Processing

The log file was processed to extract honeypot traffic and display it in the required format:

```text
HONEY MMM DD HH:MM:SS SRC DEST
```

This demonstrated the ability to extract useful security information from raw log data.

### Port Scanning

Several port scans using different parameters were performed against the SSH server.

The scan results were analysed to identify exposed services and understand how the firewall and service configuration affected network visibility.

---

## Outcome

The project resulted in a layered network security configuration incorporating multiple defensive controls.

The final environment demonstrated:

* A hardened OpenSSH server.
* Key-based SSH authentication.
* Multi-Factor Authentication.
* A Cowrie SSH honeypot.
* Restricted incoming traffic using `iptables`.
* Logging of SSH, honeypot, and blocked traffic.
* Monitoring of network and authentication activity.
* Successful validation through remote connections and port scanning.
* Identification of configuration weaknesses and recommended improvements.

The project also demonstrated how security controls can be validated through practical testing rather than relying only on configuration review.

---

## Conclusion

This project demonstrated the practical implementation of layered network security controls within an Ubuntu server environment.

OpenSSH hardening reduced unnecessary attack exposure, while MFA provided an additional authentication layer. Cowrie provided a controlled environment for observing suspicious SSH behaviour, and `iptables` restricted network access to the required services.

Security logging provided visibility into network activity and allowed SSH, honeypot, and blocked traffic to be investigated.

Testing through remote connections, firewall validation, log analysis, and port scanning provided evidence that the implemented controls were operating as intended. The final vulnerability assessment also highlighted that security configurations require ongoing review and improvement as new risks and attack techniques emerge.

Overall, the project demonstrates a practical approach to **secure network design, vulnerability evaluation, risk reduction, and security monitoring**.

