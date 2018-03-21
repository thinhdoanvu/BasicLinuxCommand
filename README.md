Basic Linux Command for EzRAD

Assume that you have some files like this in your folder that you want to process by dDocent. 
T_VN_CX68_S69_L006_R1_001.fastq.gz

T_VN_CX68_S69_L006_R2_001.fastq.gz

T_VN_CX69_S80_L006_R1_001.fastq.gz

T_VN_CX69_S80_L006_R2_001.fastq.gz

T_VN_CX6_S63_L006_R1_001.fastq.gz

T_VN_CX6_S63_L006_R2_001.fastq.gz

T_VN_MS7_S42_L006_R1_001.fastq.gz

T_VN_MS7_S42_L006_R2_001.fastq.gz

T_VN_MS1_S38_L006_R1_001.fastq.gz

T_VN_MS1_S38_L006_R2_001.fastq.gz

T_VN_MS26_S21_L006_R1_001.fastq.gz

T_VN_MS26_S21_L006_R2_001.fastq.gz

These are your goals:

VN_CX01.F.fq.gz

VN_CX01.R.fq.gz

VN_CX02.F.fq.gz

VN_CX02.R.fq.gz

VN_CX03.F.fq.gz

VN_CX03.R.fq.gz

VN_MS01.F.fq.gz

VN_MS01.R.fq.gz

VN_MS02.F.fq.gz

VN_MS02.R.fq.gz

VN_MS03.F.fq.gz

VN_MS03.R.fq.gz

You can see that, I renamed T_VN_CX68_S69_L006_R1_001.fastq.gz, T_VN_CX68_S69_L006_R2_001.fastq.gz by VN_CX01.F.fq.gz, and VN_CX01.R.fq.gz, respectively. You can guest that what did I do for all samples.

This is tutorial to do that:
############################
@ SEQ COMMAND
Print numbers from FIRST to LAST, in steps of INCREMENT.
############################
In my case, I saw that I had 3 individuals per site, and I had 6 file totally for 1 sample location (2 locations in my case)
I will create 3 line with odering number from 1 to 3
Here is command:
seq 1 3
Result is
1
2
3

##############################
@ awk
awk '{print }' filename
##############################
I want to double lines in "seq 1 3" command before. I will do this
seq 1 3 | awk '{print $0"\n"$0}'
Here is result
1
1
2
2
3
3
???Explaination
seq 1 3 | 
I want to use the result of seq command for input awk command (this sign: |)
| : continuous command
awk '{print $0}' : $0 means for all column of input file. Because you only have 1 column in input file for awk, so you can use $1. Like this awk '{print $1}'
awk '{print $0"\n"}': "\n" means newline (Enter chracter)
awk '{print $0"\n"$0}': means for printing 1st line, then newline, then copy 1st line again. And so on...
I NEED TO SAVE THIS STEP TO A FILE
Here is fully command: seq 1 3 | awk '{print $0"\n"$0}' > stt
>: means for save output

####################################
@ nano 
####################################
Because we have many files, 1 to 32 forexample. We need to replace 1 by 01 and 9 to 09... in order to equal with length of file names
Here is command: nano stt
Your window like this
1
1
2
2
3
3
Edit line by hand with 0 character at the begining of line
This is your result:
01
01
02
02
03
03
Press Ctl + X, and then Press Y for save with the same name, and close nano window

#########################
@ ls 
list file or folde name with basic or detail information
#########################
I want to display indivials in VN_CX location. So I use
ls VN_CX*
* stand for anything on the right of the file name

#########################
@ mv
rename file or folder
mv oldname newname
#########################
I want to change T_VN_CX68_S69_L006_R1_001.fastq.gz to VN_CX01.F.fq.gz. I will use mv command. Here is command
mv T_VN_CX68_S69_L006_R1_001.fastq.gz VN_CX01.F.fq.gz
Furthermore, I want to change all my files
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
#Step 1. list all files you want to change by names
ls T_VN_CX*

Here are your results
T_VN_CX68_S69_L006_R1_001.fastq.gz

T_VN_CX68_S69_L006_R2_001.fastq.gz

T_VN_CX69_S80_L006_R1_001.fastq.gz

T_VN_CX69_S80_L006_R2_001.fastq.gz

T_VN_CX6_S63_L006_R1_001.fastq.gz

T_VN_CX6_S63_L006_R2_001.fastq.gz
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
#Step 2. Add mv at the beginning of every lines
ls T_VN_CX* | awk '{print "mv "$0}'

Here are your results
mvT_VN_CX68_S69_L006_R1_001.fastq.gz
T_VN_CX68_S69_L006_R2_001.fastq.gz

T_VN_CX69_S80_L006_R1_001.fastq.gz

T_VN_CX69_S80_L006_R2_001.fastq.gz

T_VN_CX6_S63_L006_R1_001.fastq.gz

T_VN_CX6_S63_L006_R2_001.fastq.gz
