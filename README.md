# Pie

[![lint](https://github.com/kdpuvvadi/pie/actions/workflows/lint.yml/badge.svg?event=push)](https://github.com/kdpuvvadi/pie/actions/workflows/lint.yml)

Playbook works on both Debian & Red Hat family hosts. Using Ubuntu 20.04 pc as control node.

You need at least 2.9 or higher version of ansible.

## Setup

1. Install pip `sudo apt install python3-pip -y`.
2. install ansible with pip `pip install ansible`.
3. Install docker sdk for ansible `pip install docker`.
4. Clone the repo  `git clone https://github.com/kdpuvvadi/pie.git pie`.
5. copy `inventory.ini.j2` to `inventory.ini`.
6. Change host ip.
7. copy `vars.yml.j2` to `vars.yml`.
8. Install requirements `ansible-galaxy collection install -r requirements.yml`
9. Change the variables based on your preferences.

## Run

Run `ansible-playbook main.yml`

> Amend `-k` incase the `ansible_user` needs password for elevation/root access.

## CloudFlare DDNS

Setup CloudFlare DDNS using Docker image by [oznu](https://github.com/oznu/docker-cloudflare-ddns).

### Variables

```yml
cf_ddns_enable: true
cf_token: "token"
cf_zone: "example.com"
cf_zone_subdomain: "home"
```

### Generate a Cloudflare API token

To create a CloudFlare API token for your DNS zone go to [https://dash.cloudflare.com/profile/api-tokens](https://dash.cloudflare.com/profile/api-tokens) and follow these steps:

1. Click Create Token
2. Provide the token a name, for example, `cloudflare-ddns`
3. Grant the token the following permissions:
    * Zone - Zone Settings - Read
    * Zone - Zone - Read
    * Zone - DNS - Edit
4. Set the zone resources to:
    * Include - All zones
5. Complete the wizard and copy the generated token into the `API_KEY` variable for the container

> source [oznu/docker-cloudflare-ddns](https://github.com/oznu/docker-cloudflare-ddns#creating-a-cloudflare-api-token)

## pihole

```yml
pihole_enable: true
pihole_hostname: pihole
pihole_timezone: Asia/Kolkata
pihole_password: "secure-password"
```

Change the timezone and pihole login password, you can skip the `pihole_password` to autogenerate the password by pihole it self and grab the password from the log. Make sure to comment out the `WEBPASSWORD` in docker compose file [/config/pihole.yml.j2](/config/pihole.yml.j2).

## Nginx Proxy Manager Login Details

```ini
Email: admin@example.com
Password: changeme
```

 More info & documentation of Nginx Proxy Manager [Official website here](https://nginxproxymanager.com/)

## Portainer

To install portainer set `portainer_enable` value to `true`.

## Support

For support, open an issue [here](/issues).

## Authors

* [@kdpuvvadi](https://www.github.com/kdpuvvadi)

## License

[MIT](/LICENSE)
