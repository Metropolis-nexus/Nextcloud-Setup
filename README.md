# Nextcloud-Setup

## Apps

### Your apps
- Disable Activity
- Disable AppAPI
- Disable Auditing/Logging
- Disable Brute-force settings
- Disable Collaborative tags
- Disable Comments
- Disable Contacts interation
- Disable Dashboard
- Disable Default encryption module
- Disable Federation
- Disable File reminders
- Disable Files download limit
- Disable First run wizard
- Disable LDAP user and group backend
- Disable Log Reader (since there are so many ridiculous errors that are not really errors)
- Disable Monitoring
- Disable Nextcloud annoucnements
- Disable Nextcloud webhook support
- Disable Password policy
- Disable Privacy
- Disable Recommendations
- Disable Related resources
- Disable Support
- Disable Suspicious login
- Disable Usage survey
- Disable User status
- Disable Weather status
- Disable Two-Factor Authentication via Nextcloud notification (Does nothing since Nextcloud cannot do 2FA with OIDC)
- Disable Two-Factor TOTP Provider (Does nothing since Nextcloud cannot do 2FA with OIDC)

### Apps to install
- Contacts
- Music
- OnlyOffice
- OpenID Connect user backend

## Administration Settings

### Overview
- Resolve issues shown in overview, skip the complaint about `X-Frame-Options` and `X-XSS-Protection`.

### Basic settings
- Background jobs -> Cron
- Profile -> Disable profile by default for new accounts
- Files compatibility -> Enforce Windows compatibility

### Sharing
- Turn off all federation features

### External storage

**Absolutely do not use this app outside of a virtual bridge or a Wireguard tunnel. 
There is no certificate verification/host fingerprint verification going on for both SFTP and FTPS.**

- Allow people to mount external storage
  - SFTP with secret key login
  - FTP (This is extremely unreliable and can even let users accidentially crash the server, so only use it mount whatever needs to be mounted over FTP and disable it. The music app interestingly cannot load album cover over SFTP so FTP is preferable for this case.)

### Theming
- Name -> Metropolis Nextcloud
- Web link -> https://metropolis.nexus
- Slogan -> More secure than Murena Workspace!
- Global default app -> Files

### ONLYOFFICE
- The default application for opening the format -> Remove pdf (Too laggy compared to the built in PDF viewer)
- Check "Keep intermediate versions when editing (forcesave)"
- Check "Enable live-viewing mode when accessing file by public link"
- Uncheck "Display Chat menu option"
- Uncheck "Display Feedback & Support menu button"
- Uncheck "Enable plugins"
- Uncheck "Run document macros"
- Enable document protection for -> All users

### OpenID Connect
- Setup property mappings in Authentik
- Connect to Authentik through Nextcloud
  - Do not use the email scope or map emails - User's can see each other's email through the contacts app otherwise
  - Add the `offline_access` scope - Authentik will not issue refresh tokens otherwise
  - Use user_id and group provisioning

## Update `config.php`

Add the following:

```
  'user_oidc' => [
    'enrich_login_id_token_with_userinfo' => true,
  ],
```

## Enforce SSO Login

```bash
docker exec nextcloud ./occ config:app:set --value=0 user_oidc allow_multiple_user_backends
```

## Note
- OIDC token invalidation currently does not work, see this [issue](https://github.com/nextcloud/user_oidc/issues/1087).
