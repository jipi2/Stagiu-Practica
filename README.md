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