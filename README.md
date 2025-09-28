# RoboShop E-commerce Store 🛒

Deploy a complete e-commerce website with one-click automation using Ansible.

## What You Get
- **Online Store**: Product catalog, cart, user registration
- **Payment System**: Order processing with payment gateway
- **Admin Features**: Inventory management, order tracking

## Quick Setup

### 1. Update Your Servers
Edit `inventory.ini` with your server IPs:
```ini
[mongodb]
your-mongodb-server.com

[frontend]
your-website.com
```

### 2. Run Commands (In Order)
```bash
# Databases first
ansible-playbook 01-mongodb.yaml -i inventory.ini
ansible-playbook 04-redis.yaml -i inventory.ini
ansible-playbook 07-mysql.yaml -i inventory.ini
ansible-playbook 09-rabbitmq.yaml -i inventory.ini

# Backend services
ansible-playbook 02-catalogue.yaml -i inventory.ini
ansible-playbook 05-user.yaml -i inventory.ini
ansible-playbook 06-cart.yaml -i inventory.ini
ansible-playbook 08-shipping.yaml -i inventory.ini
ansible-playbook 10-payment.yaml -i inventory.ini

# Frontend (last)
ansible-playbook 03-frontend.yaml -i inventory.ini
```

### 3. Open Your Website
Visit your frontend server IP - your store is ready!

## File Structure
```
├── inventory.ini          # Your servers
├── 01-mongodb.yaml        # Product database
├── 02-catalogue.yaml      # Product service
├── 03-frontend.yaml       # Website
├── 04-redis.yaml         # Cache
├── 05-user.yaml          # User accounts
├── 06-cart.yaml          # Shopping cart
├── 07-mysql.yaml         # Order database
├── 08-shipping.yaml      # Shipping service
├── 09-rabbitmq.yaml      # Message queue
└── 10-payment.yaml       # Payment service
```

## Troubleshooting
- **Service not working?** Check: `systemctl status service-name`
- **Can't place orders?** Check payment service: `journalctl -u payment -f`
- **Website not loading?** Check nginx: `systemctl status nginx`

## Requirements
- RHEL/CentOS 9 servers
- 2GB RAM per server
- Internet connection

That's it! Your e-commerce store is live! 🎉

# Roboshop 3 Tier Architecture

![Diagram](images/roboshop.png)
