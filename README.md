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


