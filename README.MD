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