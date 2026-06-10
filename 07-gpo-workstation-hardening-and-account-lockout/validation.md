# Validation Checklist

| Validation Item | Result | Screenshot |
|---|---|---|
| Computer hardening GPO applied to CLIENT01 | Success | `01-computer-hardening-gpo-applied-gpresult.png` |
| CMD blocked for standard user | Success | `02-standard-user-cmd-blocked.png` |
| User restrictions GPO applied to john.it | Success | `03-standard-user-gpo-applied-gpresult.png` |
| Control Panel blocked for standard user | Success | `04-standard-user-control-panel-blocked.png` |
| Registry Editor blocked for standard user | Success | `05-standard-user-regedit-blocked.png` |
| Admin user not affected | Success | `06-admin-user-not-affected-by-standard-user-gpo.png` |
| Domain lockout policy configured | Success | `07-domain-account-lockout-policy-configured.png` |
| Domain lockout policy validated with command line | Success | `08-domain-lockout-policy-net-accounts-validation.png` |
| Test user lockout triggered on CLIENT01 | Success | `09-test-user-account-lockout-triggered.png` |
| Test user lockout confirmed in ADUC | Success | `10-test-user-locked-out-in-aduc.png` |
| Invalid credentials delay observed | Informational | `11-invalid-credentials-delay-after-wrong-passwords.png` |

## Final Validation Summary

The lab was considered successful because:

- CLIENT01 received the computer-side hardening GPO.
- `john.it` received the standard user restriction GPO.
- `lab.admin` was not affected by the standard user restrictions.
- The domain lockout policy was visible through both GUI and `net accounts /domain`.
- A dedicated test user was locked out after repeated wrong password attempts.
