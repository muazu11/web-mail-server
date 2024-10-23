# muazu-s-repo
# WordPress and Mail Server Infrastructure

This repository contains the configuration and setup for a complete WordPress website infrastructure with an integrated mail server system, deployed on Ubuntu. The project demonstrates the implementation of a full-stack web and email solution.

## Project Overview

### Components
- **WordPress Installation**
  - Fully functional WordPress website
  - Custom theme and plugin configurations
  - Database integration

- **Mail Server Infrastructure**
  - Postfix (SMTP Server)
  - Dovecot (IMAP/POP3 Server)
  - PostfixAdmin (Mail Administration Interface)
  - Roundcube (Webmail Client)
  - MySQL (Database Backend)

## System Requirements

- Ubuntu Server (Latest LTS recommended)
- MySQL 8.0+
- PHP 8.3+
- Nginx 1.26+
- Minimum 2GB RAM

## Installation
## Note that the LEMP stack was installed through its repositories (not Ubuntu default repositories).
## Ubuntu 22.04
## Nginx- https://nginx.org/en/linux_packages.html
## PHP 8.3- https://www.atlantic.net/dedicated-server-hosting/how-to-install-php-8-3-on-ubuntu-22-04/
## MySQL- https://dev.mysql.com/doc/mysql-apt-repo-quick-guide/en/

### WordPress Setup
```bash
# WordPress core installation steps
apt update && apt upgrade
apt install mysql-server php php-mysql
# Additional WordPress-specific steps documented in /wordpress/README.md
```

### Mail Server Setup
```bash
# Core mail components
apt install postfix dovecot-core dovecot-imapd dovecot-pop3d
apt install postfixadmin roundcube

# Database setup
mysql -u root -p < ./sql/initial_setup.sql
```

## Configuration Files

Important configuration files are located in:

```
/etc/postfix/main.cf
/etc/postfix/master.cf
/etc/dovecot/dovecot.conf
/etc/dovecot/conf.d/
/etc/postfixadmin/
/etc/roundcube/
```

## Features

### WordPress Implementation
- Secure WordPress installation
- Custom theme integration
- Performance optimizations
- SEO configurations

### Mail Server Features
- SMTP/IMAP/POP3 support
- Virtual domains and mailboxes
- Web-based mail administration
- Webmail access
- MySQL backend for mail storage
- SSL/TLS encryption support

## Security Measures
- Firewall configurations
- SPAM protection
- Regular security updates
- Secure authentication methods

## Maintenance

### Regular Tasks
```bash
# Update system
apt update && apt upgrade

# Backup databases
mysqldump -u root -p wp_database > wordpress_backup.sql
mysqldump -u root -p postfixadmin > postfix_backup.sql

# Check mail logs
tail -f /var/log/mail.log

# Monitor mail queue
postqueue -p
```

### Monitoring
- Mail queue status
- Server resource usage
- Database performance
- Mail delivery reports

## Troubleshooting

### Common Issues and Solutions

1. Mail Delivery Issues
```bash
# Check mail queue
postqueue -p

# View mail logs
tail -f /var/log/mail.log

# Test SMTP connection
telnet localhost 25
```

2. Database Connectivity
```bash
# Check MySQL status
systemctl status mysql

# Verify database connections
mysql -u root -p -e "SHOW PROCESSLIST;"
```

3. Service Status Checks
```bash
# Check all services
systemctl status postfix
systemctl status dovecot
systemctl status mysql
systemctl status apache2
```

## Testing

### Mail Server Tests
```bash
# Test SMTP
nc -zv localhost 25

# Test IMAP
nc -zv localhost 143

# Test POP3
nc -zv localhost 110

# Test mail sending
echo "Test" | mail -s "Test Subject" user@example.com
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contact

For support or queries, please create an issue in the repository.

## Acknowledgments

- WordPress Community
- Postfix Documentation
- Dovecot Wiki
- Ubuntu Documentation

---
Last Updated: October 2024
