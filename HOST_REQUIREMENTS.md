# IBMi-iDive - IBM i Host Requirements

IBMi-iDive talks directly to the standard IBM i **host servers** (the same ones IBM Access Client Solutions and JTOpen/JT400 use). It does NOT use Mapepire, SSH, FTP, or any server-side install.

## Host servers and ports

| Host server (STRHOSTSVR value) | Service name | Plain port | TLS port | Server job | Used by IBMi-iDive for |
|---|---|---|---|---|---|
| `*RMTCMD` | `as-rmtcmd` | 8475 | 9475 | QZRCSRVS | CL commands, program calls, command prompter metadata. Required to connect. |
| `*DATABASE` | `as-database` | 8471 | 9471 | QZDASOINIT | SQL (Run SQL, Admin views, most lists). Required to connect. |
| `*FILE` | `as-file` | 8473 | 9473 | QPWFSERVSO | IFS browsing, viewing, upload/download. |
| `*NETPRT` | `as-netprt` | 8474 | 9474 | QNPSERVS | Spooled-file View as images (AFPDS) and related print-server features. |
| (port mapper) | n/a | 449 | n/a | n/a | Lookup of the ports above. |

Not used by IBMi-iDive: `*SIGNON` (8476/9476), `*CENTRAL` (8470/9470), `*DTAQ` (8472/9472), Mapepire (default 8076), SSH (22), FTP/Telnet. The user-profile sign-on is performed directly on each host server connection above, so the `*SIGNON` server is not contacted.

## Connection behavior

1. For each server, the app asks the **port mapper on TCP 449** for the port (`as-database`, or `as-database-s` when TLS is on).
2. If the port mapper cannot be reached or does not know the service, it falls back to the well-known port in the table (plus 1000 for TLS).
3. Connect order: Remote Command server first, then Database server. IFS and print servers are connected on first use of those features.
4. Plain connections use ports 84xx; the profile's **TLS** option switches to ports 94xx.

## What must be running on the IBM i

- TCP/IP active (`STRTCP`) and these host servers started. `*ALL` is not required; start only what is needed:
  ```
  STRHOSTSVR SERVER(*RMTCMD)
  STRHOSTSVR SERVER(*DATABASE)
  STRHOSTSVR SERVER(*FILE)      (IFS features)
  STRHOSTSVR SERVER(*NETPRT)    (spooled-file image views)
  STRHOSTSVR SERVER(*SVRMAP)    (port mapper, TCP 449)
  ```
  `SERVER(*ALL)` also works but starts servers iDive never uses (`*CENTRAL`, `*DTAQ`, `*SIGNON`). Verify with `WRKACTJOB SBS(QSYSWRK)` / `NETSTAT *CNN` (daemon jobs such as QZRCSRVSD, QZDASRVSD, QPWFSERVSD, QNPSERVD).
- Server mapper (`*SVRMAP`, 449) is recommended but optional: if it is unreachable the app falls back to the default ports.
- Autostart (optional): `CHGSVRAUTO SVR(*ALL) AUTOSTART(*YES)`.
- Firewalls must allow the ports above from the client (449 plus 8471/8473/8474/8475, or the 94xx equivalents for TLS).

## TLS

- Enable **TLS** in the connection profile only when the host servers have a certificate assigned in Digital Certificate Manager (DCM) / Service Tools for the `*SERVER` application IDs (QIBM_OS400_QZBS_SVR_*).
- The client verifies the certificate chain and host name. For self-signed or private-CA certificates either import the CA on the client or use the profile's **Trust any certificate** option (not recommended outside testing).
- Minimum TLS version is 1.2. The IBM i must have TLS 1.2 enabled in `QSSLPCL` and a matching cipher list in `QSSLCSL`.

## User profile requirements

- Valid, enabled user profile with a password (not `*NONE`) and correct case-handling for the system password level (`QPWDLVL` 0-3 are all supported; levels 2/3 use mixed-case/passphrase).
- Authority to the objects used (e.g. `*USE` to QSYS2 SQL services, spooled files, IFS paths).
- The profile must not be disabled (`*DISABLED`) or have an expired password.
- Check `QPWDLVL`, and for IFS access make sure the host's `QZLSFILE`/file server is not restricted via exit programs (`WRKREGINFO` exit points `QIBM_QPWFS_FILE_SERV`, `QIBM_QZDA_*`, `QIBM_QZRC_RMT`, `QIBM_QZSO_SIGNON`). An exit program rejecting the request shows up as a connect or authority failure.

## Troubleshooting

| Symptom | Likely cause / check |
|---|---|
| "the IBM i does not offer as-xxx (is the host server started? STRHOSTSVR)" | Server not started: `STRHOSTSVR SERVER(*xxx)`. |
| Timeout / connection refused to 8475 or 8471 | Server not started, firewall, or wrong host name. From a terminal: `nc -vz host 449` then `nc -vz host 8475`. |
| Connects but IFS list or spool images fail | `*FILE` (8473) or `*NETPRT` (8474) not started/blocked. |
| TLS error / certificate unknown | No certificate assigned to the host server in DCM, or self-signed (use Trust any certificate for testing). |
| Sign-on error (password incorrect / expired / disabled) | Check `DSPUSRPRF`; the app reports the host sign-on return code. |
| Sign-on exchange code 0100 / 0104-0108 (for example 0106 NLV not installed) | Warnings only; the connection continues. |
| Works with other tools but not iDive | iDive needs `*RMTCMD` and `*DATABASE` specifically; `*SIGNON` alone is not enough. |
