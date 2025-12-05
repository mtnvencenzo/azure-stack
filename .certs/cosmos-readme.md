# Regenerate ssl
```bash
# 1. Generate the certificate with Subject Alternative Names (SANs):
openssl req -x509 -nodes -days 9999 -newkey rsa:2048 -keyout cosmos.key -out cosmos.crt -config cosmos.conf -extensions v3_req

# 2. Install to system trust store (Linux):
sudo cp ./cosmos.crt /usr/local/share/ca-certificates/cosmos.crt
sudo update-ca-certificates

# 3. Install to Chrome's certificate database (NSS):
sudo apt update && sudo apt install -y libnss3-tools
certutil -d sql:$HOME/.pki/nssdb -A -t "CP,CP," -n "cosmos" -i ./cosmos.crt

# 4. Verify it was added:
certutil -d sql:$HOME/.pki/nssdb -L | grep cosmos

# 5. Optionally convert to a pfx 
openssl pkcs12 -export -out cosmos.pfx -inkey cosmos.key -in cosmos.crt -passout pass:password

# 6. Make sure everythings readable by all users
chmod 644 ./cosmos.crt
chmod 644 ./cosmos.key
chmod 644 ./cosmos.pfx
```