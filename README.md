
# GoCharge Cloud Server Project

## Author

**Alyssa Foster**  

Student Project — ICT171 

Student Number - 35250097

Live Site: [https://gocharge.ink](https://gocharge.ink)

IP Adress: 3.107.197.127

## Video Explainer 


https://github.com/user-attachments/assets/fdc14928-443c-40bb-9070-4172c3e658c2 


## Project Overview

This repository contains the deployment process, website code, and configuration for **GoCharge**, a WordPress-based EV charging platform, hosted on AWS EC2 using Apache and SSL via Let's Encrypt.

---

## Homepage & Website Design

The GoCharge website is built using **WordPress (6.x)** with:

- **Theme Used**: `Carbon Agency` (customised via the Astra block system)
- **Plugin Highlighted**: `Forminator` — used to manage the contact form  

Example:
```html
<!-- wp:forminator/forms {"module_id":"27"} -->
<div class="forminator-guttenberg">[forminator_form id="27"]</div>
<!-- /wp:forminator/forms -->
```

---

## Front-End Code Highlights

The design uses **Gutenberg blocks** and pre-styled layout elements including:

- Hero Banner with background image & CTA
- Columns and Icons for services overview
- Responsive “About Us” & “Mission” sections
- Dynamic Buttons styled with custom classes

Example snippet:
```html
<h2 class="wp-block-heading has-text-align-center" style="font-size:5rem;">
  Smart. Simple. Sustainable EV Charging.
</h2>
<p class="has-text-align-center">Go Charge helps drivers connect with charging stations...</p>
```

All front-end design was created using the **WordPress Block Editor** for modular responsiveness.

---
## Domain & IP Configuration

The domain name **gocharge.ink** was purchased via [Namecheap](https://www.namecheap.com), and DNS settings were configured to point to the public EC2 IP address using **A records**:

- **Domain**: `gocharge.ink`
- **Registrar**: Namecheap  
- **Server IP**: `3.107.197.127`  
- **DNS A Records**:
  - `@` → `3.107.197.127`
  - `www` → `3.107.197.127`

This setup ensures that both `gocharge.ink` and `www.gocharge.ink` direct traffic to the same EC2 instance running the GoCharge WordPress platform.

---
## SSL Setup (HTTPS)

GoCharge uses **Let’s Encrypt** via **Certbot**:

```bash
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
```

Certbot automatically:
- Generates and installs SSL certificates
- Configures Apache for HTTPS
- Sets up auto-renewal

Check renewal:
```bash
sudo certbot renew --dry-run
```

---

## WordPress Directory Management

WordPress was moved to `/wordpress` using [SiteGround’s guide](https://au.siteground.com/kb/change-wordpress-directory/):

- Edited `wp-config.php`:
```php
define('WP_HOME', 'http://gocharge.ink');
define('WP_SITEURL', 'http://gocharge.ink/wordpress');
```

- Copied `.htaccess` and `index.php` to `/var/www/html/`
- Edited `index.php`:
```php
require( dirname( __FILE__ ) . '/wordpress/wp-blog-header.php' );
```

---

## Deployment Reference

Based on [Ali Hamza’s WordPress on Ubuntu 22.04 Guide](https://medium.com/@ali_hamza/how-to-install-wordpress-and-deploy-your-website-on-ubuntu-22-04-0a83654b7306):

- LAMP stack setup (Apache, MySQL, PHP)
- WordPress installation
- Database creation & permissions
- SSL certificate with Certbot

---

## Repository Structure

```plaintext
/var/www/html/
├── index.php                    ← Root file that redirects to WordPress
└── wordpress/
    ├── index.php
    ├── license.txt
    ├── readme.html
    ├── wp-activate.php
    ├── wp-admin/               ← WordPress admin dashboard
    ├── wp-blog-header.php
    ├── wp-comments-post.php
    ├── wp-config.php           ← Your database config
    ├── wp-config-sample.php
    ├── wp-content/             ← Themes, plugins, media uploads
    ├── wp-cron.php
    ├── wp-includes/            ← Core WordPress code
    ├── wp-links-opml.php
    ├── wp-load.php
    ├── wp-login.php
    ├── wp-mail.php
    ├── wp-settings.php
    ├── wp-signup.php
    ├── wp-trackback.php
    └── xmlrpc.php


```
---
**References**

Hamza, A. (2022, September 26). How to install WordPress and deploy your website on Ubuntu 22.04. Medium. https://medium.com/@ali_hamza/how-to-install-wordpress-and-deploy-your-website-on-ubuntu-22-04-0a83654b7306

SiteGround. (n.d.). How to change the WordPress directory. SiteGround Knowledge Base. https://au.siteground.com/kb/change-wordpress-directory/

Namecheap. (n.d.). Domain control panel: Advanced DNS for gocharge.ink. Namecheap. https://ap.www.namecheap.com/Domains/DomainControlPanel/gocharge.ink/advancedns

