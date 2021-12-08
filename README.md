# CRA app with HTTPS configured

### Steps to run THIS REPO with HTTPS

* Edit `/etc/hosts` file and add `127.0.0.1   mysecure.localhost.app`
* Install [mkcert](https://github.com/FiloSottile/mkcert) It will create CertificateAuthority in your Keychain (in mac) and sign site certificates using that CA
* Run `mkcert -install` so the CA is added to the Keychain (password will be required)
* Run `mkcert -key-file ./.cert/key.pem -cert-file ./.cert/cert.pem "mysecure.localhost.app"` to generate site certificate for `mysecure.localhost.app`
* Run the application `yarn start`

### Steps to setup https for custom local domain from scratch for CRA app

* Pick a domain you would like to use. For this repo it is `mysecure.localhost.app`
* Edit `/etc/hosts` file and add `127.0.0.1   mysecure.localhost.app`
* Create `.cert` folder project root directory `mkdir .cert`
* Install [mkcert](https://github.com/FiloSottile/mkcert) It will create CertificateAuthority in your Keychain (in mac) and sign site certificates using that CA
* Run `mkcert -install` so the CA is added to the Keychain (password will be required)
* Run `mkcert -key-file ./.cert/key.pem -cert-file ./.cert/cert.pem "mysecure.localhost.app"` to generate site certificate for `mysecure.localhost.app`
* Create `.env` file in project root directory with following config
```
HTTPS=true
SSL_CRT_FILE=./.cert/cert.pem
SSL_KEY_FILE=./.cert/key.pem
HOST=mysecure.localhost.app
```
* Run the application `yarn start`

Now your application should have https & lock icon

### Important!

The certificate generated on my machine wouldn't work on another as you don't have the same Certificate Authority added to keychain. Because of that contents of .cert folder are ignored from GIT. Each developer needs to generate them for themself.
