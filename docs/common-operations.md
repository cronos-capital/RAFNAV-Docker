# Common bench operations

## Prerequisites

1. Ensure you have [ssh](./ssh.md) access to the live server.
2. Ensure that you have an interactive terminal on the prod image. If not please create a new interactive terminal using the command below:

```sh
docker exec -it rafnav-backend-1 bash
```

## Common Commands

### Interactive terminal for RAFNav bench

```sh
docker exec -it rafnav-backend-1 bash
```

### CSRF Issues

Sign out all users on all sites. Forcing users to relogin is good for security but also resolves CSRF issues especially after an update.

```sh
docker exec -it rafnav-backend-1 bash
bench --site all destroy-all-sessions
```

### New Site

```sh
bench new-site [site_name] --mariadb-user-host-login-scope='%' --admin-password [pwd] --verbose
```

### Installing RAFNav

```sh
bench --site [site_name] install-app rafnav_core matter_management filing documentation raf_finance
```

### Migrations

```sh
bench --site all migrate
```

### Enable Scheduler

#### For a Specific Site

```sh
bench --site [site] enable-scheduler
```

#### For All Sites

```sh
bench --site all enable-scheduler
```
