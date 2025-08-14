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

Nuvå11

**Uppgift:**  
`data.txt` innehåller text där alla bokstäver (a–z, A–Z) är ROT13-kodade. Målet är att avkoda texten och hitta lösenordet.

**Vad är ROT13?**  
ROT13 (rotate by 13) är en enkel substitutionschiffer där varje bokstav ersätts av den som ligger 13 steg fram i alfabetet.  
- A ↔ N  
- B ↔ O  
- C ↔ P  
- …  
- M ↔ Z  

Eftersom alfabetet har 26 bokstäver innebär 13 steg att samma operation fungerar åt båda hållen — ROT13 av en ROT13-sträng ger tillbaka originalet.

Använt kommando
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

Förklaring av kommandot:

cat data.txt → visar innehållet i filen.

| (pipe) skickar utdata från cat som indata till nästa kommando.

tr (translate) byter tecken baserat på två teckenuppsättningar:

'A-Za-z' = alla stora och små bokstäver i alfabetisk ordning.

'N-ZA-Mn-za-m' = samma bokstäver men med början 13 steg fram (A→N, a→n).

När tr körs på texten i filen byts varje bokstav ut enligt ROT13-regeln. Resultatet blir läsbart och innehåller lösenordet.

#Nivå12

Uppgift  
data.txt är en hexdump av en fil som har komprimerats flera gånger med olika metoder. Målet är att återskapa originalfilen och läsa lösenordet.

Arbetsmetod:
1. Skapa en temporär arbetsmapp i /tmp:
  
   cd /tmp
   mktemp -d

Kopiera sökvägen som skrivs ut, exempel: /tmp/tmp.a1B2c3D4.

    Kopiera filen data.txt till mappen:

cp ~/data.txt /tmp/tmp.a1B2c3D4
cd /tmp/tmp.a1B2c3D4

Konvertera hexdumpen tillbaka till binär fil:

xxd -r data.txt > data.bin

Identifiera filtypen:

file data.bin

Byt namn på filen utifrån filtyp och packa upp med rätt verktyg:

    Om gzip compressed data:

mv data.bin data.gz
gunzip data.gz

Om bzip2 compressed data:

mv data.bin data.bz2
bunzip2 data.bz2

Om POSIX tar archive:

    mv data.bin data.tar
    tar xf data.tar

    Om annat: anpassa efter vad file visar.

Upprepa steg 4–5 för varje ny fil som skapas, tills file visar att filen är en textfil.

Läs lösenordet:

    cat filnamn

Förklaring:

    xxd -r återskapar binärdata från en hexdump.

    file analyserar filens faktiska innehåll och avgör hur den ska hanteras.

    Rätt packningsverktyg används beroende på filtyp.

    Filtillägget ändras vid varje steg för att tydligt visa vilken typ filen har, vilket gör det lättare att välja rätt kommandon.

Lösenord:
Finns i den sista textfilen efter att alla uppackningar är klara.
