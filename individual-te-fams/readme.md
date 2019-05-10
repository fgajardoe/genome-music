
zcat danRer10.fa.out.gz|grep Merlin-1_DR  > Merlin-1_DR.out
awk '{print $5"\t"$6"\t"$7"\t"$10"\t.\t"$2}' Merlin-1_DR.out >Merlin-1_DR.bed
bedtools subtract -b Merlin-1_DR.bed -a danRer10.chrom.bed  |awk '{print $0"\t.\t.\t0"}' > subtractMerlin-1_DR.bed
cat subtractMerlin-1_DR.bed Merlin-1_DR.bed |grep chr13 |sort -k2,2 -g|awk '{print "play -n synth "($3-$4)/5000000" sine "$6*50}'|xargs -I%s sh -c 'echo "%s" && %s'
# el anterior esta malo, pero suena mejor. este seria el correcto
cat subtractMerlin-1_DR.bed Merlin-1_DR.bed |grep chr13 |sort -k2,2 -g|awk '{print "play -n synth "($3-$2)/100000" sine "$6*50}'|xargs -I%s sh -c 'echo "%s" && %s'

zcat danRer10.fa.out.gz |grep -Fwf te-genome-contrib.tab.lst |awk 'BEGIN{while(getline < "te-genome-contrib.tab.tone"){tone[$1]=$2}}{print $5"\t"$6"\t"$7"\t"$10"\t.\t"tone[$10]}' |awk '{print "play -n synth "0.1" sine "$6/5}'|xargs -I%s sh -c 'echo "%s" && %s'

# el mejor
zcat danRer10.fa.out.gz |grep -Fwf te-genome-contrib.tab.lst |awk 'BEGIN{while(getline < "te-genome-contrib.tab.tone"){tone[$1]=$2}}{print $5"\t"$6"\t"$7"\t"$10"\t.\t"tone[$10]}' |cut -f6 |grep -Pe'\d'| awk '{ split("0,2,4,5,7,9,11,12",a,","); for (i = 0; i < 1; i+= 0.0001) printf("%08X\n", 100*sin(1382*exp((a[$1 % 8]/12)*log(2))*i)) }' | xxd -r -p | aplay -c 8 -f S32_LE -r 5000

# radiohead
zcat danRer10.fa.out.gz |grep -Fwf te-genome-contrib.tab.lst |awk 'BEGIN{while(getline < "te-genome-contrib.tab.tone"){tone[$1]=$2}}{print $5"\t"$6"\t"$7"\t"$10"\t.\t"tone[$10]}' |cut -f6 |grep -Pe'\d'| awk '{ split("0,2,4,5,7,9,11,12",a,","); for (i = 0; i < 1; i+= 0.0001) printf("%08X\n", 100*sin(1382*exp((a[$1 % 8]/12)*log(2))*i)) }' | xxd -r -p | aplay -c 3 -f S32_LE -r 2000
