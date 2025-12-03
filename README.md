# Nextcloud-Setup

## Apps

### Your apps
- Disable Activity
- Disable AppAPI
- Disable Brute-force settings
- Disable Collaborative tags
- Disable Comments
- Disable Contacts interation
- Disable Dashboard
- Disable Federation
- Disable File reminders
- Disable First run wizard
- Disable Monitoring
- Disable Nextcloud webhook support
- Disable Password policy
- Disable Privacy
- Disable Recommendations
- Disable Related resources
- Disable Support
- Disable Usage survey
- Disable User status
- Disable Weather status
- Two-Factor Authentication via Nextcloud notification (Does nothing since Nextcloud cannot do 2FA with OIDC)
- Two-Factor TOTP Provider (Does nothing since Nextcloud cannot do 2FA with OIDC)

### Apps to install
- OpenID Connect user backend
- Mail
- Contacts
- Calendar
- Notes
- End to end encryption (Note that the UX for this is really bad still)
- OnlyOffice

## Administration Settings

### Overview
- Resolve issues shown in overview, skip the complaint about `X-Frame-Options` and `X-XSS-Protection`.

### Basic settings
- Background jobs -> Cron
- Profile -> Disable profile by default for new accounts
- Files compatibility -> Enforce Windows compatibility

### Theming
- Name -> Metropolis Nextcloud
- Web link -> https://metropolis.nexus
- Slogan -> More secure than Murena Workspace!
- Global default app -> Files

### ONLYOFFICE
- The default application for opening the format -> Remove pdf
- Uncheck "Enable plugins"
- Uncheck "Run document macros"

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
