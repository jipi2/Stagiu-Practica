# Stagiu Practica


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