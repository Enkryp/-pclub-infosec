# infosec
p club secy task -- infosec

### Answer:
```841f980abd04b26fe804ca0c207a574bef504cb6a3c3599a449e845ca993d2cf```

ltrace and strace didnt give anything very usefull after some crude and adhoc attempts; so i tried radare2 

running:
```
r2 -d ./rev hi
aaa
afl 
```
revealed a function ```sym.print_flag```. However sadly ```pdf @main``` further revealed that ```main``` didnt contain any entry point for the print function.

So now I just had to guide the flow of the program and make it enter print_flag to capture the flag.


Stopping main before entering printf by adding a breakpoint ``` db 0x08048581``` ; setting eip to ```sym.print_flag``` by  ```dr eip = 0x0804849c ```
(followed by respective ```dc``` s) made the program print a perfect 64 digit hexadecimal;

or a 256 bit binary which had to be the required SHA256 hash. 

### Complete Sol:
```
r2 -d ./rev hi
aaa
afl
pdf @main
db 0x08048581
dc
dr eip = 0x0804849c
dc

```
