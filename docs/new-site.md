# Adding a new site/firm

## Prerequisites

Make sure you can remote into the prod server. If you do not have access, please review [setting up ssh access](./ssh.md).

## Open an interactive terminal on the prod server

```sh
docker exec -it rafnav-backend-1 bash
```

### Add a new site on the server

```sh
bench new-site [site_name].rafnav.co.za --mariadb-user-host-login-scope='%' --admin-password [pwd] --verbose
```

Replace [site_name] with the firm's name. no spaces allowed and all lower case letters. See examples below:
> raf-nav-raf-attorneys.rafnav.co.za \
> selegal.rafnav.co.za

Replace [pwd] with admin password for the site. Please save the admin password in the excel file located at:
**Make sure the password is very secure

>Z:\112-RAFNAV\Production Users Credentials.xlsx

See full example:

```sh
bench new-site selegal.rafnav.co.za --mariadb-user-host-login-scope='%' --admin-password !SomeStrongPassword@ --verbose
```

### Initial Setup

Log in to the new site as the administrator user with the site name as the url. For example a site with site name _selegal.rafnav.co.za_ will have the url <https://selegal.rafnav.co.za>. Follow the on screen steps to complete the initial Frappe setup.

#### Install RAFNav

>**Important: Make sure you have done the initital setup before installing and setting up RAFNav**

After the initial set up was done for the new site, install rafnav using the command below.

```sh
bench --site [site_name] install-app rafnav_core matter_management filing documentation raf_finance
```

#### RAFNav Setup

Please review the _RAFNav Admin Portal Overview.mp4_ video under ```Z:\112-RAFNAV\06.Support & Maintanence\04.Admin Portal User Guide```

### Enable Scheduler for all sites

After RAFNav has been installed, enable the background job scheduler using the command below.

```sh
bench --site all enable-scheduler
```
