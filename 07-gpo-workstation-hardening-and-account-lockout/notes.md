# Notes

## Why the GPOs were separated

The lab intentionally separates computer hardening, user restrictions, and domain account policy.

This avoids a common mistake: placing every setting into one large GPO without considering whether the setting applies to users, computers, or the domain.

## Computer Configuration vs User Configuration

Computer Configuration settings follow the computer object. In this lab, the computer hardening GPO applied to CLIENT01 because CLIENT01 is located in the LAB/Computers OU.

User Configuration settings follow the user object. In this lab, the restrictions applied to `john.it` because the user is located in the LAB/Users OU.

## Why account lockout policy is domain-level

Account lockout policy affects domain user authentication. The domain controllers enforce it, so it belongs in the Default Domain Policy or another GPO linked at the domain root.

It should not be treated like a normal user restriction linked only to a Users OU.

## Why admin validation matters

Hardening is useful only if it is applied intentionally. The lab confirmed that `lab.admin` was not affected by standard user restrictions. This is important because accidental admin lockout can make troubleshooting and system administration harder.

## PowerShell note

Blocking Command Prompt does not block PowerShell. This lab intentionally left PowerShell unblocked. A production-grade approach would usually use AppLocker, Windows Defender Application Control, or another application control strategy.
