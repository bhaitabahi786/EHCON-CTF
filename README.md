# EHCON-CTF
write ups for some chall

### 1. Forensics Chall

1. Snow White

![image](https://user-images.githubusercontent.com/69809386/140953856-d37333a2-3bfa-454c-9e9b-1d101544f0bc.png)

Solution

first we dwld the jpeg image then check strings 
``` strings -n 10 snow.jpeg ```

we can see 
```
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
```
means its steghide so fire up command

``` steghide extract -sf snow.jpeg
we got output with empty passphrase 

root@kali:~/Desktop/ehcon_ctf/forensic# steghide extract -sf snow.jpeg 
Enter passphrase: 
wrote extracted data to "secret.txt".
root@kali:~/Desktop/ehcon_ctf/forensic# 

```
we got secret.txt  after opening it we got blank file but if we try to select then we will see that we can select something 

so do ctrl + a  to select all  and copy 

then go to https://www.dcode.fr/whitespace-language   and decrypt here 

![image](https://user-images.githubusercontent.com/69809386/140957754-0b349b9b-5fb0-4b4e-87ce-6b0f85abfdc1.png)

and got the flag :)

2. Hybrid tree 

![image](https://user-images.githubusercontent.com/69809386/140959787-b159e305-e9de-41bd-97c0-92676622278a.png)

solution 

it was easy just 
```
root@kali:~/Desktop/ehcon_ctf/forensic# strings -n 10 hybrid.jpg 
((((((((((((((((((((((((((((((((((((((((((((((((((
ErVyaNLfN@}
jT'     :rU;Eg
EHACON{z1p_plu5_1m463}
```
got it 

### 2. MISCELLANEOUS

1. PikaZip

![image](https://user-images.githubusercontent.com/69809386/140960620-bc24e845-5521-46ed-aa79-7292624ac7dc.png)

Solution 

so here we got Zip file Rar file and Tar.gz file and its was zip under zip file means multiple zip file 

so written a code 
```
import os
run = os.system

for i in range(1000):
    #run('ls')
    run('mkdir zipfile_%s' % i)
    run('unzip magic.zip -d zipfile_%s' % i)
    os.chdir('zipfile_%s' % i)
    print('directory changed to zipfile_%s' % i)
    #run('cd zipfile_%s' % i)
    run('unrar e magic.rar')
    run('tar -xf magic.tar.gz')
```
this was written by me and it was a computer hanging code but i got the flag with this code 😥 

and many random directory that i have created 

but dont use above code my teammate then written simple code and here it is
```
import patoolib
import os

for i in range(1000):
    file = os.listdir("out")[-1]
    if file == "flag.txt":
        break
    patoolib.extract_archive(f"out/{file}", outdir="out")
    os.remove(f"out/{file}")
```
and my other teammate wrote code in bash
```
for VARIABLE in {1..70}
do
    unrar e magic.rar
    rm magic.zip
    tar -zxvf magic.tar.gz
    rm magic.rar
    unzip magic.zip
    rm magic.tar.gz
done
cat flag.txt
```
and then we will get flag.txt file

and when we open it its language of pikachu (very interesting language for pokemon fan hahahaha)

and searched on google will find Pikalang cipher decoder

![image](https://user-images.githubusercontent.com/69809386/140962990-93c5aaa1-341b-4b4d-9f42-897429cc51dc.png)

and got the flag 





