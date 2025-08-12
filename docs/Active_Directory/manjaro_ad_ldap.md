# Querying Active Directory from Manjaro (Non-Domain-Joined)

## Install Required Tools
```bash
sudo pacman -S --needed openldap krb5 ca-certificates ca-certificates-mozilla
```

## Set Your Values
```bash
DC_HOST="dc01.domain.local"
BASE_DN="DC=domain,DC=local"
BIND_USER="user@domain.local"      # or full DN like CN=User,OU=...,DC=domain,DC=local
```

## Find a User by Name

-> Match any name containing `"john"`
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(cn=*john*)' sAMAccountName displayName
```

-> Match names starting with `"john"`
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(cn=john*)' sAMAccountName displayName
```

-> Match names ending with `"john"`
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(cn=*john)' sAMAccountName displayName
```

-> Match exactly `"John"`
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(cn=John)' sAMAccountName displayName
```

-> Return specific attributes (faster than "everything")
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(cn=*john*)' sAMAccountName displayName mail
```

## List Disabled Accounts (AD Bitwise Filter)
```bash
ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" '(&(objectCategory=person)(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=2))'   sAMAccountName displayName userAccountControl
```

## Users Not Logged In for 90 Days (Using `lastLogonTimestamp`)
```bash
# Windows FileTime cutoff for "now - 90 days"
CUTOFF=$(python3 - <<'PY'
import time
print(int((time.time()-90*86400+11644473600)*10_000_000))
PY
)

ldapsearch -LLL -x -H "ldaps://${DC_HOST}:636" -D "${BIND_USER}" -W   -b "${BASE_DN}" "(lastLogonTimestamp<=$CUTOFF)"   sAMAccountName displayName lastLogonTimestamp
```

## Notes
- Prefer `ldaps://...:636`. If you must use plain `ldap://`, add StartTLS with `-ZZ` and ensure the DC supports it.
- Kerberos SSO is possible on Manjaro:
```bash
sudo pacman -S --needed krb5
kinit user@DOMAIN.LOCAL
ldapsearch -LLL -Y GSSAPI -H "ldap://${DC_HOST}" -b "${BASE_DN}" '(cn=*john*)' sAMAccountName displayName
```
- `cn` ≈ the "Name" in `Get-ADUser -Filter "Name -like ..."`.
- You can also search `displayName`, `givenName`, `sn`, or `sAMAccountName` depending on what you want.
