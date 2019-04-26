# Como suenan los ETs?


generamos un codigo TE-fam - numero
```
cut -f2 te-categories.tab |sort|uniq |nl |awk '{print $2"\t"$1}' > tone-code.txt
```

y le ponemos play

```
awk -F'  ' 'BEGIN{while(getline < "te-categories.tab"){c[$1]=$2;} while(getline < "tone-code.txt"){t[$1]=$2}}{ for(i = $2; i < $3; i++){print t[c[$4]]} }' transposon-insertions.bed |grep -Pe'\d'| uniq |awk '{ split("0,2,4,5,7,9,11,12",a,","); for (i = 0; i < 1; i+= 0.0001) printf("%08X\n", 100*sin(1382*exp((a[$1 % 8]/12)*log(2))*i)) }' | xxd -r -p | aplay -c 3 -f S32_LE -r 10000
```

este tambien suena bien
```
awk -F'  ' 'BEGIN{while(getline < "te-categories.tab"){c[$1]=$2;} while(getline < "tone-code.txt"){t[$1]=$2}}{ for(i = $2; i < $3; i++){print t[c[$4]]} }' transposon-insertions.bed |grep -Pe'\d'| uniq |awk '{ split("0,2,4,5,7,9,11,12",a,","); for (i = 0; i < 1; i+= 0.0001) printf("%08X\n", 100*sin(1382*exp((a[$1 % 8]/12)*log(2))*i)) }' | xxd -r -p | aplay -c 1 -f S32_LE -r 90000
```

ohh y este tambien
```
awk -F'  ' 'BEGIN{while(getline < "te-categories.tab"){c[$1]=$2;} while(getline < "tone-code.txt"){t[$1]=$2}}{ for(i = $2; i < $3; i++){print t[c[$4]]} }' transposon-insertions.bed |grep -Pe'\d'| uniq |awk '{ split("0,2,4,5,7,9,11,12",a,","); for (i = 0; i < 1; i+= 0.0001) printf("%08X\n", 100*sin(1382*exp((a[$1 % 8]/12)*log(2))*i)) }' | xxd -r -p | aplay -c 8 -f S32_LE -r 10000
```
