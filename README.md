# Docker Private Registry

## Generate User and Password

Installing the apache2-utils package

```bash
sudo apt install apache2-utils -y
```

Create a password file auth/nginx.htpasswd for “testuser” and “testpassword”.

```bash
htpasswd -Bbn testuser testpassword > ./auth/nginx.htpasswd
```

## Generate self-signed certificate

```bash
openssl req -x509 -nodes -days 365
\ -subj "/C=CA/ST=QC/O=Example,Inc./CN=example.com"
\ -addext "subjectAltName=DNS:example.com"
\ -newkey rsa:2048 -keyout ./auth/domain.key
\ -out ./auth/domain.crt;
```

## Trust Certificate

```bash
sudo mkdir /etc/docker/certs.d
sudo mkdir /etc/docker/certs.d/example.com
sudo cp /path/to/your/cert /etc/docker/certs.d/example.com
```

## Add Alias

```bash
sudo -- sh -c -e "echo '{IP_ADDRESS_OF_PRIVATE_REGISTRY}  example.com' >> /etc/hosts"
```

## Running

```bash
docker-compose up -d
```
