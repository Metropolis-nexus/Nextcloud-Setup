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

### Apps to install
- OpenID Connect user backend
- Mail
- Contacts
- Calendar
- Notes

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

### OpenID Connect
- Connect to Authentik
- Setup property mappings in Authentik
- Use user_id and group provisioning in Nextcloud

## Enforce SSO Login

```bash
docker exec nextcloud ./occ config:app:set --value=0 user_oidc allow_multiple_user_backends
```

