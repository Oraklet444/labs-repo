#Dokumentation för nivåer i leveln bandit på overthewire.


Nivå 1  
Anslöt med `ssh bandit1@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta lösenordet i filen `-` i hemkatalogen  
Körde `ls -1` för att lista filerna  
Körde `cat ./-` för att läsa innehållet (`./` används eftersom `-` annars tolkas som en växel) och få lösenordet (sparas separat)  

Nivå 2  
Anslöt med `ssh bandit2@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta lösenordet i filen `spaces in this filename` i hemkatalogen  
Körde `ls -1` för att lista filerna  
Körde `cat "spaces in this filename"` för att läsa innehållet (citationstecken krävs för att hantera mellanslag i filnamn) och få lösenordet (sparas separat)  

Nivå 3  
Anslöt med `ssh bandit3@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta lösenordet i en dold fil i katalogen `inhere`  
Körde `ls -a inhere` för att visa även dolda filer (prefix `.`)  
Körde `cat inhere/.hidden` för att läsa innehållet och få lösenordet (sparas separat)  

Nivå 4  
Anslöt med `ssh bandit4@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta en human-readable fil i katalogen `inhere`  
Körde `file inhere/*` för att kontrollera filtyper  
Körde `cat` på den fil som identifierades som ASCII text för att få lösenordet (sparas separat)  

Nivå 5  
Anslöt med `ssh bandit5@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta en fil i `inhere` som är human-readable, 1033 bytes och inte är executable  
Körde `find inhere/ -type f -size 1033c ! -executable` för att filtrera rätt fil  
Körde `cat` på den fil som hittades för att få lösenordet (sparas separat)  

Nivå 6  
Anslöt med `ssh bandit6@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta en fil på hela systemet som ägs av användaren `bandit7`, gruppen `bandit6` och är 33 bytes stor  
Körde `find / -user bandit7 -group bandit6 -size 33c 2>/dev/null` för att undvika felmeddelanden  
Körde `cat` på filen som hittades för att få lösenordet (sparas separat)  

Nivå 7  
Anslöt med `ssh bandit7@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta lösenordet i `data.txt` där raden innehåller ordet "millionth"  
Körde `grep millionth data.txt` för att visa raden och få lösenordet (sparas separat)  

Nivå 8  
Anslöt med `ssh bandit8@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta raden i `data.txt` som förekommer exakt en gång  
Körde `sort data.txt | uniq -u` för att sortera och filtrera unika rader och få lösenordet (sparas separat)  

Nivå 9  
Anslöt med `ssh bandit9@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att hitta en human-readable sträng i `data.txt` som är föregången av `=`  
Körde `strings data.txt | grep =` för att extrahera textsträngar och filtrera på mönstret och få lösenordet (sparas separat)  

Nivå 10  
Anslöt med `ssh bandit10@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att dekoda innehållet i `data.txt` som var base64-kodat  
Körde `base64 -d data.txt` för att dekoda och få lösenordet (sparas separat)  

Nivå 11  
Anslöt med `ssh bandit11@bandit.labs.overthewire.org -p 2220`  
Uppgiften var att dekryptera innehållet i `data.txt` som var krypterat med ROT13  
Körde `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'` för att dekryptera texten och få lösenordet (sparas separat)  

