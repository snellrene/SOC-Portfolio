# Microsoft Entra ID Sign-in Investigation

## Objective

Investigate a successful sign-in from an unusual location and determine whether the activity represents credential compromise or legitimate user behaviour.

## Environment

Identity Platform: Microsoft Entra ID
User Account: Alice HR

### Security Controls
- Multi-Factor Authentication (MFA)
- Security Groups
- Sign-in Logging

## Scenario
A successful sign-in occurred from Melbourne, Victoria.
A second successful sign-in occurred shortly afterwards from a different IP address while connected through Proton VPN.
The activity was investigated to determine whether it represented a security incident.

## Evidence Collected

### Login 1

| Field | Value |
|---------|---------|
| Location | Melbourne, Victoria |
| IP Address | 203.123.105.190 |
| Result | Success |

### Login 2

| Field | Value |
|---------|---------|
| Location | West Hindmarsh, South Australia |
| IP Address | 103.216.221.95 |
| Result | Success |

<img width="1856" height="110" alt="image" src="https://github.com/user-attachments/assets/a29e4ed5-11d0-41cb-8cba-552be9534733" />

---

## Investigation

1. Reviewed Microsoft Entra ID Sign-in Logs.
2. Compared source IP addresses.
3. Reviewed location information.
4. Verified successful MFA authentication.
5. Compared timestamps.
6. Confirmed a VPN connection was used during testing.

---

## Findings

The sign-ins originated from different public IP addresses.

Although the VPN application was connected to a Singapore endpoint, Microsoft Entra ID geolocated the IP address to South Australia.

This demonstrates that geolocation data may vary depending on the IP intelligence provider being used.

MFA was successfully completed and no additional suspicious activity was observed.

---

## Conclusion

No evidence of account compromise was identified.

The activity was determined to be expected behaviour caused by testing with a VPN connection.

---

## Lessons Learned

- IP geolocation should not be used as the sole indicator of compromise.
- MFA validation is an important part of identity investigations.
- Sign-in logs provide critical evidence during account investigations.
- VPN services can create misleading location data.

---

## Skills Demonstrated

- Entra ID Sign-in Analysis
- Identity Security Monitoring
- MFA Investigation
- Incident Documentation
- Security Event Analysis
