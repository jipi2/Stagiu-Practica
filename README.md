# Stagiu Practica
# Bandit

## Ziua 1 (14.06.2022)
Am vorbit despre ce ne-ar placea sa lucram.

## Ziua 2 (15.06.2022)
Am ales tema: __Pwn Adventures__

Am urmarit videocliptul: [Let's Play/Hack - Pwn Adventure 3: Pwnie Island](https://www.youtube.com/watch?v=RDZnlcnmPUA&list=PLhixgUqwRTjzzBeFSHXrw9DnQtssdAwgG&ab_channel=LiveOverflow) 

## Ziua 3 (16.06.2022)
Am instalat serverul privat al jocului utilizand [docker](https://github.com/LiveOverflow/PwnAdventure3) si clientul pe windows.
Nu am reusit sa instalez clientul pentru linux. Am urmarit si acest [video](https://www.youtube.com/watch?v=rOTqprHv1YE&t=720s&ab_channel=Simplilearn).

## Ziua 4 (17.06.2022)
Am incercat in continuare sa finalizez instalarea clientului pentru linux, am incercat site-urile: 

1. [link_github](https://github.com/LiveOverflow/PwnAdventure3)
2. [PwnAdventure](https://www.pwnadventure.com/)
3. [Stack](https://askubuntu.com/questions/339364/libssl-so-10-cannot-open-shared-object-file-no-such-file-or-directory)

Nu am reusit, de aceea m-am reprofilat pe *CTF-uri*.

Am facut de pe [overthewire](https://overthewire.org/wargames/) urmatoarele:

## Bandit:
0 := ssh bandit0@bandit.labs.overthewire.org -p 2220

0->1 := __boJ9jbbUNNfktd78OOpsqOltutMc3MY1__
		am dat un ls si un cat pt a citit ce scria in readme
		
1->2 := cat ./- (asa se pot deschide fisierele cu -)
		__CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9__
		
2->3 := cat "spaces in this filename"
		__UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK__
		
3->4 := cat .hidden
		__pIwrPrtPN36QITSp3EQaw936yaFoFgAB__
		
4->5 := find . -type f -exec file {} +	
		cat ./-file07
		__koReBOKuIDDepwhWk7jZC0RTdopnAYKh__

5->6 := find . -size 1033c -exec file {} +
		__DXjZPULLxYr17uwoI01bNLQbtFemEgo7__
		cat maybehere07/.file2
		
6->7 := find . -user bandit7 -group bandit6 -size 33c 2>/dev/null
		cat var/lib/dpkg/info/bandit7.password
		__HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs__
		
7->8 := cat data.txt | grep millionth
		__cvX2JJa4CFALtqS87jk27qwqGhBM9plV__
		
8->9 := sort data.txt | uniq -u
		__UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR__
		
9->10 := strings data.txt | egrep "[=]+"
		__truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk__
		
10->11 := cat data.txt | base64 -d
		  __IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR__

11->12 := cat data.txt | tr "[a-m][A-M][n-z][N-Z]" "[n-z][N-Z][a-m][A-M]"
			__5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu__

## Ziua 5 (20.06.2022)

12->13 := am tot dezarhivat pana am ajuns la rezultat
		  comenzi folosite:
1. gunzip <Nume_Fis>
2. bunzip2 <Nume_Fis>
3. tar xf <Nume_Fis>		 
		 __8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL__

13->14 := ssh -i sshkey.private bandit14@localhost
		  __4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e__

14->15 := nc localhost 30000 (dupa am introdus parola de mai sus)e
		  __BfMYroe26WYalil77FoDi9qh59eK5xNr__	

15->16 := ncat localhost 30001 --ssl
		  __cluFn7wTiGryunymYOu4RcffSxQluehd__
		  
16->17 := nmap -p 31000-32000 localhost (asa am vazut ce porturi sunt activa si care nu sunt active)
		  ncat localhost 31790 --ssl (si am introdus parola de mai sus)
		  ssh -i piv_pass bandit17@bandit.labs.overthewire.org -p 2220
		  (in piv_pass am copiat cheia obtinuta anterior)

17->18 := diff passwords.new passwords.old
 __kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd__
		  
18->19 := ssh -t bandit18@bandit.labs.overthewire.org -p 2220 /bin/sh
		  cat readme
	__IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x__
		  
19->20 := ./bandit20-do cat /etc/bandit_pass/bandit20 (ne folosim de acel executabil pentru a executa comenzi cu drepturile ownerului care a creat fisierul)

__GbKksEFF4yrVs6il55v6gwY5aVje5f0j__
	
20->21 :=  (este nevoie de 2 terminale);
	       nc -lvp 4452 (serverul asculta pe portul 4452, se pot face doar conexiuni locale);
		  ./suconnect 4452 (ma conectez ; pe un alt terminal);
		  (copiez parola );
		   (de pe primul terminal scriu parola pt bandit 20, adica cea mai sus)	;
		   (obtin parola pe al doilea terminal);
		   __gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr__

## Ziua 6 (21.06.2022)

21->22 := m-am uitat la: [link](https://www.youtube.com/watch?v=UlVqobmcPuM&ab_channel=OneByteAtATime) , [link](https://www.youtube.com/watch?v=v952m13p-b4&t=56s&ab_channel=Linode).

		  cd /etc/cron.d
		  cat cronjob_bandit22
		  cat /usr/bin/cronjob_bandit22.sh
		  cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
		  Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
		  (m-am uitat in scriptul care ruleaza si am luat fisierul in care se scria outputul)
		  
22->23 := comenzi

		  cd /etc/cron.d
		  cat cronjob_bandit23
          cat /usr/bin/cronjob_bandit23.sh
		  echo I am user bandit23 | md5sum | cut -d ' ' -f 1
          cat /tmp/8ca319486bfbbc3663ea0fbe81326349
		  jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
		  (m-am uitat in scriptul care se ruleaza si am accesat fisierul in care se salveaza parola cautata)
		  
23->24 := comenzi

		  cd /etc/cron.d
	      cat cronjob_bandit24
		  cat /usr/bin/cronjob_bandit24.sh
		  (dupa analizarea scriptului, observam ca putem crea un script care sa citeasca parola aferenta contului bandit24, deoarece noi nu avem permisiunea sa o citim direct)
		  (creeam un folder in /tmp pentru a putea scrie scriptul)
		  mkdir /tmp/work
		  cd /tmp/work
		  nano s.sh
		  ------------
		  #!/bin/bash
		  cat /etc/bandit_pass/bandit24 > /tmp/work/pass
	      ----------------------
		  touch pass
		  chmod 777 -R /tmp/work (dam permisiuni de executie)
		  cp s.sh /var/spool/bandit24
		  (dupa aprox un minut parola este disponibil in fisierul pass)
		  UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

24->25 := 
#!/bin/bash

pass=UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
num_list=(0 1 2 3 4 5 6 7 8 9)
```
for i1 in ${num_list[@]}
do
	for i2 in ${num_list[@]}
	do
		for i3 in ${num_list[@]}
		do
			for i4 in ${num_list[@]}
			do
				pin=$i1$i2$i3$i4
				echo "$pass $pin" > fis.txt
			done
		done
	done
done
```	
		  nc localhost 30002 < fis.txt
		  uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
		  
25->26 := (trebuie sa micsoram terminalul pentru a se putea executa comanda "more"0)

		  ssh -i bandit26.sshkey bandit26@localhost
		  (apasam pe "v" pentru a porni editorul de text vim)
		  :set shell? (pt a edea ce shell se foloseste)
		  :set shell=/bin/bash
		  :shell
		  cat /etc/bandit_pass/bandit26
		  5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
		  
26->27 := ./bandit27-do cat /etc/bandit_pass/bandit27

		  3ba3118a22e93127a4ed485be72ef5ea

## Ziua 7 (22.06.2022)

27->28 := comenzi

		  git clone ssh://bandit27-git@localhost/home/bandit27-git/repo
		  cd repo
		  cat README
		  0ef186ac70e04ea33b4c1853d2526fa2
		  
28->29 := comenzi

		  git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
		  git log (putem vedea toate commit-urile facute pana in momentul de fata)
		  git checkout c086d11a00c0648d095d04c089786efef5e01264 (putem vedea cum arata README.md la momentul celui de-al doilea commit)
		  cat README.md
		  bbc96594b4e001778eee9975372716b2
		  
29->30 := comenzi

	      git branch -a (vedem alte branch-uri)
		  git checkout dev (schimbam branchul)
		  cat README.md
		  5b90576bedb2cc04c86a9e924ce42faf

30->31 := comenzi

		  git tag
		  git show secret
		  47e603bb428404d265f59c42920d81e5
		  
31->32 := comenzi

		  (am creat fisierul key.txt)
		  (nu am putut pune pe git nimic pt ca in fisier .gitignore erau fisiere de tipul *.txt)
		  (am modificat .gitignore)
		  git add key.txt
		  git commit -m "key"
		  git push origin master
		  56a9bf19c63d650ce78e6ec0354ee45e
		  
32->33 := comenzi

		  (shellul nu recunoaste comenzile deoarece litere sunt majuscule)
		  $0 (revenim la lowercase)
		  cat /etc/bandit_pass/bandit33
		 c9c3199ddf4121b10cf581a98d51caee

# Natas

0->1 := __gtVrDuiDfck831PqWsLEZy5gyDz1clto__
		(parola era intr-un comentariu din sursa paginii)
		
1->2 := __ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi__
		(parola era intr-un comentariu din sursa paginii) + (ctrl+U pentru a vedea sursa)
		  
2->3 := __sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14__
		(am accesat index of files)

# PicoCTF

__flag_shop__:

-am introdus un numar mare de flaguri false astfel incat acel numer inmultit cu 900 sa fie negativ

-fiind negativ, scazand acel numar din balanta, de fapt am adunat la balanta

-asa am avut bani pt flag

__plumbing__

-nc jupiter.challenges.picoctf.org 4427 | grep pico

*picoCTF{digital_plumb3r_5ea1fbd7}*

__First Find__

-find . -name uber-secret.txt -exec cat {} +

*picoCTF{f1nd_15_f457_ab443fd1}*

__The numbers__
```
#!/bin/bash

letters=(A B C D E F G H I J K L M N O P Q R S T U V W X Y Z)
numbers=(16 9 3 15 3 20 6 \{ 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 \})

for i in ${numbers[@]}
do
	if [[ $i == \{ || $i == \} ]]
	then
		echo $i >> temp.txt
	else
		echo ${letters[$i-1]} >> temp.txt
	fi

done
cat temp.txt | tr -d "\n"
rm temp.txt
```
__13__

tr "[a-m][A-M][n-z][N-Z]" "[n-z][N-Z][a-m][A-M]"

*picoCTF{not_too_bad_of_a_problem}*

__BigZip__

ls | grep -r pico

*picoCTF{gr3p_15_m4g1c_ef8790dc}*

__Disk, disk, sleuth!__

strings dds1-alpine.flag.img | grep pico

*picoCTF{f0r3ns1c4t0r_n30phyt3_a69a712c}*

## Ziua 8 (23.06.2022)

__So Meta__
identify -verbose pico_img.png | grep pico

*picoCTF{s0_m3ta_d8944929}*

__extensions__

atril flag.txt

*picoCTF{now_you_know_about_extensions}*

__basic-file-exploit__

trebuia introdus "0" la intrarea in tabel (era un if in codul sursa)

*picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_1B9F5942}*

__basic-mod1__
```
#!/bin/bash

vect=`cat $1`
cont=0
for i in ${vect[@]}
do
	res=`expr $i % 37`
	vect_mod[$cont]=$res
	let cont++
done 

map=(A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 0 1 2 3 4 5 6 7 8 9 \_)

for i in ${vect_mod[@]}
do
	echo ${map[$i]} >> temp.txt
done

cat temp.txt | tr -d "\n"
rm temp.txt
```
*picoCTF{R0UND_N_R0UND_79C18FB3}*

__basic-mod2__
```
#!/usr/bin/env python3

import string

flag = []

with open("message.txt") as fis:
	vect = fis.read()
	vect_mod = [int(val) for val in vect.split()]

	for number in vect_mod:
		modulus = pow(number, -1, 41)

	if modulus in range(1,27):
		flag.apppend(string.ascii_uppercase[modulus-1])
	elif modulus in range (27,37):
		flag.apppend(string.digits[modulus-27])
	else:
		flag.apppend("_")

print ("picoCTF{%s}" % "".join(flag))
```
__fixme1.py__

(era o problema la identare)

*picoCTF{1nd3nt1ty_cr1515_6a476c8f}*

__fixme2.py__

(trebuia la un if (==))

*picoCTF{3qu4l1ty_n0t_4551gnm3nt_4863e11b}*

__Glitch Cat__
```

flag_enc='picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32) + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'
print(flag_enc)

```
*picoCTF{gl17ch_m3_n07_9c42a45d}*

__HashingJobApp__

*picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}*

__PW Crack 1__

(am luat parola din codul sursa)

*picoCTF{545h_r1ng1ng_1b2fd683}*

__PW Crack 2__
```

flag_enc=chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36)
print(flag_enc)

```
*picoCTF{tr45h_51ng1ng_489dea9a}*

__PW Crack 3__

am incercat fiecare parola din lista aceea,
parola era: *1ea2*

*picoCTF{m45h_fl1ng1ng_6f98a49f}*

__PW Crack 4__
```
#!/bin/bash

list=("6288", "6152", "4c7a", "b722", "9a6e", "6717", "4389", "1a28", "37ac", "de4f", "eb28", "351b", "3d58", "948b", "231b", "973a", "a087", "384a", "6d3c", "9065", "725c", "fd60", "4d4f", "6a60", "7213", "93e6", "8c54", "537d", "a1da", "c718", "9de8", "ebe3", "f1c5", "a0bf", "ccab", "4938", "8f97", "3327", "8029", "41f2", "a04f", "c7f9", "b453", "90a5", "25dc", "26b0", "cb42", "de89", "2451", "1dd3", "7f2c", "8919", "f3a9", "b88f", "eaa8", "776a", "6236", "98f5", "492b", "507d", "18e8", "cfb5", "76fd", "6017", "30de", "bbae", "354e", "4013", "3153", "e9cc", "cba9", "25ea", "c06c", "a166", "faf1", "2264", "2179", "cf30", "4b47", "3446", "b213", "88a3", "6253", "db88", "c38c", "a48c", "3e4f", "7208", "9dcb", "fc77", "e2cf", "8552", "f6f8", "7079", "42ef", "391e", "8a6d", "2154", "d964", "49ec")
count=0

for i in ${list[@]}
do
	pass[$count]=`echo $i | egrep -o "[0-9a-zA-Z]+"`
	let count++
done

for i in ${pass[@]}
do
		echo $i > pass.txt
		python3 level4.py < pass.txt | grep pico
done
rm pass.txt
```
*picoCTF{fl45h_5pr1ng1ng_ae0fb77c}*

__PW Crack 5__

(am modificat codul astfel incat sa nu mai fie nevoie de introducerea de la tastaura a parola)
(toate parolele sunt citite direct din fisier si se verifica daca este cea buna)
(de asemenea nu se mai printeaza decat flagul, nu si faptul ca o anumita parola a fost incorecta)
```
import hashlib

### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level5.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level5.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_5_pw_check(line):
    user_pw = line
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    #print("That password is incorrect")



with open("/home/jipi/work/newDown/dictionary.txt") as dict:
    lines = dict.readlines()
    for line in lines:
        line = line.strip()
        level_5_pw_check(line)
```

*picoCTF{h45h_sl1ng1ng_fffcda23}*

__runme.py__

python3 runme.py

*picoCTF{run_s4n1ty_run}*

__Serpentine__

(am modificat rezultatul uni if)
```
 elif choice == 'b':
      print('\nOops! I must have misplaced...wait a second, here it is:')
      print_flag()
      print("\n\n")
```
*picoCTF{7h3_r04d_l355_7r4v3l3d_8e47d128}*

__Scavenger Hunt__

 Here's the first part of the flag: picoCTF{t (era in source code)

CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0  (era in CSS)

Part 3: t_0f_pl4c (era in robots.txt)

Part 4: 3s_2_lO0k (era in .htaccess)

Congrats! You completed the scavenger hunt. Part 5: _a69684fd} (era in .DS_Store)

__Enhance!__

am folosit comanda strings, flagul era in ultimele linii

*picoCTF{3nh4nc3d_aab729dd}*

__Lookey here__

cat anthem.flag.txt | grep pico

*picoCTF{gr3p_15_@w3s0m3_4c479940}*

__patchme.py__

(am modificat parola in interiorul codului)

*picoCTF{p47ch1ng_l1f3_h4ck_c4a4688b}*

__Vigerne__

(am folosit site-ul: [boxentrig](https://www.boxentriq.com/code-breaking/vigenere-cipher) pentru decodificare)

*picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_ae82272q}*

__RPS__

(pentru a stabili cine a castigat, programul verifica daca utilizatorul a introdus instrumentul care distruge instrumentul ales de computer)

(aceasta verficare se face cu strstr, fiind o vulnerabilitate)

(pt a castiga de fiecare data trebuie sa introducem "rockpaperscissors" pentru ca astfel, strstr mereu va returna ceva diferit de null, ceea ce inseamna runda castigata pentru noi)

__information__

(am folosit un tool numit exiftool pentru a vedea metadate despre poza)

(se poate observa ca in dreptul licentei este un sir de caractere care ar putea fi o codificare base64)

(am decodificat si am obtinut flagul)

exiftool cat.jpg | grep License | cut -f2 -d":" | egrep -o "[a-zA-Z0-9]+" | base64 -d

*picoCTF{the_m3tadata_1s_modified}*