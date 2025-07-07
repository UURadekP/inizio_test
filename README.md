Vytvořeno za účelem reakce na pracovní příležitost ve společnosti inizio

For english version scroll down.

Default user je nastaven "admin", pokud se Váš user liší, změnte ho v hosts.ini.

Postup:
1. sudo apt install openssh-server
2. Přidejte ssh klíč, pokud již máte svůj stačí ho přidat do authorized keys skrze "ssh-copy-id -i ~/.ssh/id_rsa.pub admin@<ip adresa>. Klíč by měl být v ~/.ssh./id_rsa.pub 
3. sudo apt install ansible
4. git clone git@github.com:UURadekP/inizio_test.git. Naklonovat do /home/<username>
5. cd inizio_test/ansible_inizio/
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

___________________________ ENGLISH BELOW ___________________________

Procedure:
1. sudo apt install openssh-server
2. Add an SSH key — if you already have your own, simply add it to the authorized_keys with "ssh-copy-id -i ~/.ssh/id_rsa.pub The key should be in ~/.ssh/id_rsa.pub.
3. sudo apt install ansible
4. git clone git@github.com:UURadekP/inizio_test.git — Clone it into /home/<username>/
5. cd inizio_test/ansible_inizio/
6. ansible-playbook -i inventory/hosts.ini playbooks/site.yml -K
 
After the playbook finishes, SSH access should work with ssh webapp@<your VM's IP address>

What the playbook does:
1. Creates the user "webapp"
2. Creates the web root directory
3. Creates the SSH directory for the "webapp" user and copies your SSH key into authorized_keys
4. Installs or verifies unattended-upgrades, then enables it
5. Updates the package cache and upgrades all packages
6. Installs Nginx
7. Removes the default Nginx configuration
8. Deploys a custom Nginx configuration
9. Downloads index.html.j2 from the Git repository https://github.com/UURadekP/inizio_webpattern
10. Creates index.html using the template function and saves it to the web root. If index.html has changed, it reloads Nginx
11. Verifies Nginx is working
12. Installs UFW (firewall)
13. Adds ports 22 and 80 to the allow list
14. Changes the default UFW policy to deny
15. Installs Fail2Ban
16. Deploys a custom sshd_config
17. Disables password authentication when using an SSH key
18. Checks that the server is running
19. Performs a check using the uri module
