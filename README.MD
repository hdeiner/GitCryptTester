This project is designed to ensure that git-crypt allows us to encrypt certain plaintext files transparently, and that everything works as expected through IntelliJ and Visual Studio.

The file unencrypted.txt should say, "This is the contents of unencrypted.txt"

The file encrypted.txt should say, "This is the contents of encrypted.txt".  But it should be readable only if you are using git-crypt.

Steps:
- apt-get install git-crypt
- gpg --gen-key
- gpg --keyserver pgp.mit.edu --send-key 
- git-crypt add-gpg-user --trusted howard.deiner@deinersoft.com (use the email you used in gen-key)
- create .gitattributes and define encrypted files



- gpg ––list–keys and find public $KEY_ID for your entry (it's 8 hex characters)
- gpg --armor --export --output [name].gpg [your $KEY_ID] (that's the file that needs to be sent to others to gpg --import [file])
- git-crypt init 
- git-crypt add-gpg-user [your $KEY_ID] 
- git-crypt add-gpg-user --trusted [your email]


for import:
on exporting machine...
gpg --export -a A1C63BAA > public.key
gpg --export-secret-keys -a A1C63BAA > secret.key
sudo docker cp public.key db43f9585462:/public.key
sudo docker cp secret.key db43f9585462:/secret.key
on importing machine:
gpg --import /public.key
gpg --import /secret.key
gpg --edit-key B7E58E6F3BDD142E35D33E0F35E6D2C5A1C63BAA
git clone https://www.github.com/hdeiner/GitCryptTester.git
// THIS IS WRONG IT IS FOR STARTING A GIT-CRYPT git-crypt add-gpg-user B7E58E6F3BDD142E35D33E0F35E6D2C5A1C63BAA
git-crypt unlock
