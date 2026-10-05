# Microsoft Entra ID Suspicious Sign-in Investigation

## Objective

Investigate a successful sign-in from an unusual location and determine whether the activity represents credential compromise or legitimate user behaviour.

## Environment
| Field | Value |
|---------|---------|
| Identity Platform | Microsoft Entra ID |
| User Account | Alice HR |
| VPN | Proton VPN |

### Security Controls
- Multi-Factor Authentication (MFA)
- Security Groups
- Sign-in Logging

## Scenario
A successful sign-in occurred from Melbourne, Victoria.
A second successful sign-in occurred shortly afterwards from a different IP address while connected through Proton VPN.
The activity was investigated to determine whether it represented a security incident.

## Evidence Collected

<img width="1815" height="113" alt="image" src="https://github.com/user-attachments/assets/378e6ac3-97ff-49fa-8076-d2355028a7e6" />

### Login 1

| Field | Value |
|---------|---------|
| Location | Melbourne, Victoria |
| IP Address | 203.123.105.190 |
| Result | Success |

<img width="943" height="746" alt="image" src="https://github.com/user-attachments/assets/f80de5ed-7582-473f-8f48-af5f6293a83d" />

<img width="806" height="362" alt="image" src="https://github.com/user-attachments/assets/ce5ce130-33b8-4244-855d-25f23fcdf8ff" />

### Login 2

| Field | Value |
|---------|---------|
| Location | West Hindmarsh, South Australia |
| IP Address | 103.216.221.95 |
| Result | Success |

<img width="834" height="753" alt="image" src="https://github.com/user-attachments/assets/25578dfb-ab8f-4709-a8db-c29a28fdf079" />

<img width="836" height="407" alt="image" src="https://github.com/user-attachments/assets/8d6a206a-d9e6-439a-8a63-0aa8037d25ac" />

## Investigation

1. Reviewed Microsoft Entra ID Sign-in Logs.
2. Compared source IP addresses.
3. Reviewed location information.
4. Verified successful MFA authentication.
5. Compared timestamps.
6. Confirmed a VPN connection was used during testing.

## Findings

The sign-ins originated from different public IP addresses.

Although the VPN application was connected to a Singapore endpoint, Microsoft Entra ID geolocated the IP address to South Australia.

This demonstrates _that geolocation data may vary depending on the IP intelligence provider being used_.

MFA was successfully completed and no additional suspicious activity was observed.

## Conclusion

No evidence of account compromise was identified.

The activity was determined to be expected behaviour caused by testing with a VPN connection.

## Lessons Learned

- IP geolocation should not be used as the sole indicator of compromise.
- MFA validation is an important part of identity investigations.
- Sign-in logs provide critical evidence during account investigations.
- VPN services can create misleading location data.

## Skills Demonstrated

- Entra ID Sign-in Analysis
- Identity Security Monitoring
- MFA Investigation
- Incident Documentation
- Security Event Analysis
