# Screenshot Index

| File | Description |
|---|---|
| `01-computer-hardening-gpo-applied-gpresult.png` | `gpresult /r /scope computer` showing the computer hardening GPO applied to CLIENT01 |
| `02-standard-user-cmd-blocked.png` | Command Prompt blocked for `john.it` |
| `03-standard-user-gpo-applied-gpresult.png` | `gpresult /r /scope user` showing user restrictions applied to `john.it` |
| `04-standard-user-control-panel-blocked.png` | Control Panel / Settings blocked for `john.it` |
| `05-standard-user-regedit-blocked.png` | Registry Editor blocked for `john.it` |
| `06-admin-user-not-affected-by-standard-user-gpo.png` | `lab.admin` can open Command Prompt and Control Panel |
| `07-domain-account-lockout-policy-configured.png` | Account lockout policy configured in Default Domain Policy |
| `08-domain-lockout-policy-net-accounts-validation.png` | `net accounts /domain` validating the domain lockout settings |
| `09-test-user-account-lockout-triggered.png` | CLIENT01 showing the locked-out account message |
| `10-test-user-locked-out-in-aduc.png` | ADUC showing `test.lockout` is locked out |
| `11-invalid-credentials-delay-after-wrong-passwords.png` | Windows delaying the next attempt after repeated wrong passwords |
