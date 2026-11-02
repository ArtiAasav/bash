```bash
#!/bin/bash

# 1. Uue kasutaja loomine
read -p "Sisesta uue kasutaja nimi: " kasutaja
useradd -m "$kasutaja"
groupadd eksamgr9
usermod -aG eksamgr9 $kasutaja
echo "$kasutaja:$kasutaja" | chpasswd

echo "Kasutaja $kasutaja loodud edukalt."

# 2. Projektikataloogi loomine
kodukataloog=/home/$kasutaja

mkdir -p $kodukataloog/projekt
uname -a > "$kodukataloog/projekt/süsteem.txt"
lsb_release -a >> "$kodukataloog/projekt/süsteem.txt"

# 3. Faili olemasolu ja õiguste kontroll

if [ -f $kodukataloog/projekt/süsteem.txt ]; then
    sudo chmod 640 projekt/süsteem.txt
    echo "Faili õigused uuendatud" >> eksam9.log
else
    echo "Fail puudub!" >> eksam9.log
fi

# 4. Teenuste oleku salvestamine

sudo systemctl status ssh > "$kodukaust/projekt/teenus1.txt"
sudo systemctl status cron > "$kodukaust/projekt/teenus2.txt"
sudo systemctl status apache2 > "$kodukaust/projekt/teenus3.txt"

# 5. rm käske sisaldavate ridade otsimine
sudo touch $kodukataloog/projekt/kustutused.txt
sudo chmod 777 $kodukataloog/projekt/kustutused.txt

cat ~/.bash_history | grep "rm" > $kodukataloog/projekt/kustutused.txt

# 6. Varundamise funktsioon
mkdir -p "$kodukaust/backup"

varunda() {
    kuupaev=$(date +"%Y%m%d_%H%M%S")
    tar -cvf "$kodukaust/backup/projekt_$kuupaev.tar.gz" "$kodukaust/projekt"
}
varunda

# 7. Crontab kirje lisamine

# 8. Lõputeade
echo "Pilet 9 lõpetatud edukalt."
```
