This project is designed to ensure that git-crypt allows us to encrypt certain plaintext files transparently, and that everything works as expected through IntelliJ and Visual Studio.

The file unencrypted.txt should say, "This is the contents of unencrypted.txt"

The file encrypted.txt should say, "This is the contents of encrypted.txt".  But it should be readable only if you are using git-crypt.

Steps to create:
- apt-get install git-crypt
- gpg --gen-key
- gpg --keyserver pgp.mit.edu --send-key 
- git-crypt add-gpg-user --trusted [use the email you used in gen-key]
- create .gitattributes and define encrypted files
- git add .gitattributes encrypted.txt unencrypted.txt README.MD
- git commit
- git push
- gpg --list-secret-keys [find your keyid]
- gpg --export-secret-keys [your keyid] > secret.key
- now put secret.key on the other machine for build, collaborate, etc.
- gpg --import /secret.key [hope you didn't forget your passphrase!]
- git clone
- git-crypt add-gpg-user --trusted [use the email you used in gen-key]
- git-crypt unlock [hope you didn't forget your passphrase!]

* There may be just a little more needed to make this work in a CI server.  See https://medium.com/@jon_gille/decrypting-secrets-in-your-ci-cd-pipeline-c57da11e1794
* Use gpg --batch --import /secret.key [to avoid the passphrase prompt]
* One last passphrase prompting nastiness.  This occurs on the git-crypt unlock.
```bash
  gpgconf --kill gpg-agent
  gpg-agent --daemon --allow-preset-passphrase --max-cache-ttl 3153600000
  /usr/lib/gnupg2/gpg-preset-passphrase --preset --passphrase $GPG_PASSPHRASE $KEY_ID
  ```