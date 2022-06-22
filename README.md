# Stagiu Practica
# Bandit

## Ziua 1 (14.06.2022)
Am vorbit despre ce ne-ar placea sa lucram.

## Ziua 2 (15.06.2022)
Am ales tema: __Pwn Adventures__

Am urmarit videocliptul: [Let's Play/Hack - Pwn Adventure 3: Pwnie Island](https://www.youtube.com/watch?v=RDZnlcnmPUA&list=PLhixgUqwRTjzzBeFSHXrw9DnQtssdAwgG&ab_channel=LiveOverflow) 

## Ziua 3 (16.06.2022)
Am instalat serverul privat al jocului utilizand [docker](https://github.com/LiveOverflow/PwnAdventure3) si clientul pe windows.
Nu am resuti sa instalez cientul pentru linux. Am urmarit si acest [video](https://www.youtube.com/watch?v=rOTqprHv1YE&t=720s&ab_channel=Simplilearn).

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

## Ziua 5 (20.06)

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

## Ziua 6 (21.06)

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

## Ziua 6 (21.06)

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
-picoCTF{digital_plumb3r_5ea1fbd7}

__First Find__
-find . -name uber-secret.txt -exec cat {} +
picoCTF{f1nd_15_f457_ab443fd1}

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
picoCTF{not_too_bad_of_a_problem}

__BigZip__
ls | grep -r pico
picoCTF{gr3p_15_m4g1c_ef8790dc}

__Disk, disk, sleuth!__
strings dds1-alpine.flag.img | grep pico
picoCTF{f0r3ns1c4t0r_n30phyt3_a69a712c}