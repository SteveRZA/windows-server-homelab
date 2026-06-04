# Notes - Lab 02

## Design Decisions

### Keep DC01 focused on core domain services

In this clean baseline lab, `DC01` is used only for:

- Active Directory Domain Services
- DNS
- Domain time synchronization

File shares, mapped drives, and NTFS permission testing are intentionally left for a future dedicated file server lab.

---

### Use DC01 as DNS for domain clients

The client initially receives DNS from VMware NAT DHCP. That is fine for general internet access, but not correct for an Active Directory domain.

For domain functionality, `CLIENT01` must use `DC01` as DNS:

```text
CLIENT01 → DC01 DNS → DNS Forwarders → Internet DNS
```

This allows the client to resolve both:

- internal AD records, such as `dc01.lab.local`
- external records, such as `google.com`

---

### Use OUs instead of default containers

The default `Users` and `Computers` containers are avoided for lab objects.

A dedicated `LAB` OU structure was created so future GPOs can be linked cleanly to users, computers, servers, or admin accounts.

---

### Use group-based admin access

The dedicated admin user is not the only object documented. The admin relationship is group-based:

```text
Lab Admin → SG_Lab_Admins → Domain Admins
```

This is cleaner than relying only on the built-in Administrator account.

---

## Troubleshooting Notes

### VMware NAT subnet correction

The original static IP plan used `192.168.10.10`, but VMware NAT was configured for:

```text
192.168.44.0/24
```

The DC was corrected to:

```text
IP: 192.168.44.10
Gateway: 192.168.44.2
DNS: 192.168.44.10
```

After this correction, external connectivity and DNS forwarding worked properly.

---

### NTP initially used Local CMOS Clock

Before configuration, `w32tm /query /status` showed:

```text
Source: Local CMOS Clock
```

The PDC Emulator was configured to use:

```text
time.windows.com,0x8
```

Final validation confirmed that the DC synchronized with the external time source.
