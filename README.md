Vytvořeno za účelem reakce na pracovní příležitost ve společnosti inizio

Default user je nastaven "admin", pokud se Váš user liší, změnte ho v hosts.ini.


Postup:
1. sudo apt install openssh-server
2. Přidejte ssh klíč, pokud již máte svůj stačí ho přidat do authorized keys. Pokud možno tak použijte rsa klíč s default jménem. Klíč by měl být v ~/.ssh./id_rsa.pub 
3. sudo apt install ansible
4. git clone git@github.com:UURadekP/inizio_test.git. Naklonovat do /home/<username>
5. cd inizio_server/ansible_inizio/
6. ansible-playbook -i inventory/hosts.ini playbooks/site.yml -K
7. Po skončení playbooku by mělo fungovat ssh webapp@<ip adresa vaši VM>

Co playbook dělá:
1. Vytvoří usera "webapp"
2. Vytvoří web root directory
3. Vytvoří ssh directory pro uživatele webapp a zkopíruje Váš ssh klíč do authorized_keys.
4. Nainstaluje nebo zkontroluje unattended-upgrades, poté je zapne.
5. Updatne package cache and a upgradne všechny packages.
6. Nainstalluje nginx
7. Smaže default nginx config
8. Deployne vlastní nginx config.
9. Stáhne index.html.j2 z git repozitáře (https://github.com/UURadekP/inizio_webpattern).
10. Vytvoří index.html skrze template funkci a uloží ho do web rootu. Pokud se index.html změnil, reloadne nginx.
11. Kontrola nginx
12. Installace ufw
13. Přídání portů 22 a 80 do allow listu.
14. Změní default ufw policy na deny.
15. Nainstaluje fail2ban
16. Deployne custom sshd_config
17. Vypne heslovou authentikaci při použití SSH klíče.
18. Kontrola, zda li server běží.
19. Kontrola skrze uri modul.
