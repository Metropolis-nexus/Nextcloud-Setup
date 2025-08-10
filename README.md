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
- End to end encryption (Note that the UX for this is really bad still)

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
- Setup property mappings in Authentik
- Connect to Authentik through Nextcloud
  - Do not use the email scope or map emails - User's can see each other's email through the contacts app otherwise
  - Use user_id and group provisioning

## Enforce SSO Login

```bash
docker exec nextcloud ./occ config:app:set --value=0 user_oidc allow_multiple_user_backends
```
