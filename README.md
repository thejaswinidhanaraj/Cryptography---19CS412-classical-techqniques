
# Caeser Cipher
Caeser Cipher using with different key values

# AIM:

To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

1.	In Ceaser Cipher each letter in the plaintext is replaced by a letter some fixed number of positions down the alphabet.
2.	For example, with a left shift of 3, D would be replaced by A, E would become B, and so on.
3.	The encryption can also be represented using modular arithmetic by first transforming the letters into numbers, according to the   
    scheme, A = 0, B = 1, Z = 25.
4.	Encryption of a letter x by a shift n can be described mathematically as,
                       En(x) = (x + n) mod26
5.	Decryption is performed similarly,
                       Dn (x)=(x - n) mod26


## PROGRAM:
```
#include <stdio.h>
#include <string.h> 
#include <ctype.h>

int main() { 
char plain[10], cipher[10];
int key, i, length;
printf("\n Enter the plain text:");
scanf("%s", plain);
printf("\n Enter the key value:");
scanf("%d", &key);

printf("\n \n \t PLAIN TEXT: %s", plain);
printf("\n \n \t ENCRYPTED TEXT: ");

length = strlen(plain);

for (i = 0; i < length; i++) {
    cipher[i] = plain[i] + key;
    
    if (isupper(plain[i]) && (cipher[i] > 'Z'))
        cipher[i] = cipher[i] - 26;
        
    if (islower(plain[i]) && (cipher[i] > 'z'))
        cipher[i] = cipher[i] - 26;
        
    printf("%c", cipher[i]);
}

printf("\n \n \t AFTER DECRYPTION : ");

for (i = 0; i < length; i++) {
    plain[i] = cipher[i] - key;
    
    if (isupper(cipher[i]) && (plain[i] < 'A'))
        plain[i] = plain[i] + 26;
        
    if (islower(cipher[i]) && (plain[i] < 'a'))
        plain[i] = plain[i] + 26;
        
    printf("%c", plain[i]);
}

return 0;
}
```
## OUTPUT:

![Screenshot 2024-09-02 081624](https://github.com/user-attachments/assets/1228b24c-1dc5-4aaf-802f-c3edcc67eade)



## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.

 
## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

ALGORITHM DESCRIPTION:
The Playfair cipher uses a 5 by 5 table containing a key word or phrase. To generate the key table, first fill the spaces in the table with the letters of the keyword, then fill the remaining spaces with the rest of the letters of the alphabet in order (usually omitting "Q" to reduce the alphabet to fit; other versions put both "I" and "J" in the same space). The key can be written in the top rows of the table, from left to right, or in some other pattern, such as a spiral beginning in the upper-left-hand corner and ending in the centre.
The keyword together with the conventions for filling in the 5 by 5 table constitutes the cipher key. To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. Then apply the following 4 rules, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter. Encrypt the new pair and continue. Some   
   variants of Playfair use "Q" instead of "X", but any letter, itself uncommon as a repeated pair, will do.
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively (wrapping 
   around to the left side of the row if a letter in the original pair was on the right side of the row).
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively (wrapping around 
   to the top side of the column if a letter in the original pair was on the bottom side of the column).
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of 
   corners of the rectangle defined by the original pair. The order is important – the first letter of the encrypted pair is the one that 
    lies on the same row as the first letter of the plaintext pair.
To decrypt, use the INVERSE (opposite) of the last 3 rules, and the 1st as-is (dropping any extra "X"s, or "Q"s that do not make sense in the final message when finished).


## PROGRAM:
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define SIZE 30

// Function to convert the string to lowercase void toLowerCase(char plain[], int ps)
{
int i;
for (i = 0; i < ps; i++) {
if (plain[i] > 64 && plain[i] < 91)
 
plain[i] += 32;
}
}

// Function to remove all spaces in a string 
int removeSpaces(char* plain, int ps)
{
int i, count = 0;
for (i = 0; i < ps; i++)
if (plain[i] != ' ')
plain[count++] = plain[i];
plain[count] = '\0'; return count;
}

// Function to generate the 5x5 key square
void generateKeyTable(char key[], int ks, char keyT[5][5])
{
int i, j, k, flag = 0, *dicty;

// a 26 character hashmap
// to store count of the alphabet dicty = (int*)calloc(26, sizeof(int)); for (i = 0; i < ks; i++) {
if (key[i] != 'j')
dicty[key[i] - 97] = 2;
}

dicty['j' - 97] = 1;

i = 0;
j = 0;
for (k = 0; k < ks; k++) {
if (dicty[key[k] - 97] == 2) {
dicty[key[k] - 97] -= 1;
keyT[i][j] = key[k]; j++;
if (j == 5) {
i++; j = 0;
}
}
}

for (k = 0; k < 26; k++) {
if (dicty[k] == 0) {
keyT[i][j] = (char)(k + 97);
 
j++;
if (j == 5) {
i++; j = 0;
}
}
}
}
// Function to search for the characters of a digraph
// in the key square and return their position
void search(char keyT[5][5], char a, char b, int arr[])
{
int i, j;

if (a == 'j')
a = 'i'; else if (b == 'j')
b = 'i';
for (i = 0; i < 5; i++) {

for (j = 0; j < 5; j++) {

if (keyT[i][j] == a) {
arr[0] = i;
arr[1] = j;
}
else if (keyT[i][j] == b) {
arr[2] = i;
arr[3] = j;
}
}
}
}

// Function to find the modulus with 5 int mod5(int a)
{
return (a % 5);
}

// Function to make the plain text length to be even int prepare(char str[], int ptrs)
{
if (ptrs % 2 != 0) {
str[ptrs++] = 'z';
str[ptrs] = '\0';
 
}
return ptrs;
}

// Function for performing the encryption
void encrypt(char str[], char keyT[5][5], int ps)
{
int i, a[4];

for (i = 0; i < ps; i += 2) {
search(keyT, str[i], str[i + 1], a); if (a[0] == a[2]) {
str[i] = keyT[a[0]][mod5(a[1] + 1)];
str[i + 1] = keyT[a[0]][mod5(a[3] + 1)];
}
else if (a[1] == a[3]) {
str[i] = keyT[mod5(a[0] + 1)][a[1]];
str[i + 1] = keyT[mod5(a[2] + 1)][a[1]];
 
}
else {

}
}
}
 

str[i] = keyT[a[0]][a[3]];
str[i + 1] = keyT[a[2]][a[1]];
 

// Function to encrypt using Playfair Cipher
void encryptByPlayfairCipher(char str[], char key[])
{
char ps, ks, keyT[5][5];

// Key
ks = strlen(key);
ks = removeSpaces(key, ks); toLowerCase(key, ks);

// Plaintext
ps = strlen(str); toLowerCase(str, ps);
ps = removeSpaces(str, ps); ps = prepare(str, ps);
generateKeyTable(key, ks, keyT); encrypt(str, keyT, ps);
 
}
// Driver code int main()
{
char str[SIZE], key[SIZE];

// Key to be encrypted strcpy(key, "Monarchy"); printf("Key text: %s\n", key);

// Plaintext to be encrypted strcpy(str, "instruments"); printf("Plain text: %s\n", str);

// encrypt using Playfair Cipher encryptByPlayfairCipher(str, key);
printf("Cipher text: %s\n", str);

return 0;
}

## OUTPUT:
Output:
Key text: Monarchy Plain text: instruments Cipher text: gatlmzclrqtx

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.


## PROGRAM:
```
#include<stdio.h>
#include<string.h>
int main(){
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
int i,j, t=0;
unsigned int c[20],d[20];
char msg[20];
printf("Enter plain text: ");
scanf("%s",msg);
for(i=0;i<strlen(msg);i++)
{
c[i]=msg[i]-65;
unsigned int a[3][3]={{6,24,1},{13,16,10},{20,17,15}};
unsigned int b[3][3]={{8,5,10},{21,8,21},{21,12,8}};
printf("%d ",c[i]);
}
for(i=0;i<3;i++)
{ t=0;
for(j=0;j<3;j++)
{
t=t+(a[i][j]*c[j]);
}
d[i]=t%26;
}
printf("\nEncrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",d[i]+65);
for(i=0;i<3;i++)
{
t=0;
for(j=0;j<3;j++)
{
t=t+(b[i][j]*d[j]);
}
c[i]=t%26;
}
printf("\nDecrypted Cipher Text :");
for(i=0;i<3;i++)
printf(" %c",c[i]+65);
return 0;
}
```

## OUTPUT:

![Screenshot 2024-09-02 084916](https://github.com/user-attachments/assets/0fce0cd2-d0fd-41d2-8d2c-bbe670a033c5)

## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different Caesar ciphers based on the letters of a keyword. It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. It consists of the alphabet written out 26 times in different rows, each alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.



## PROGRAM:
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>
#include <stdlib.h>

void encrypt() {
char plaintext[128];
char key[16];
printf("\nEnter the plaintext (up to 128 characters): ");
scanf(" %[^\n]", plaintext); // Read input with spaces
printf("Enter the key (up to 16 characters): ");
scanf(" %[^\n]", key);

printf("Cipher Text: ");  
for (int i = 0, j = 0; i < strlen(plaintext); i++, j++) {  
    if (j >= strlen(key)) {  
        j = 0;  
    }  
    int shift = toupper(key[j]) - 'A';  
    char encryptedChar = ((toupper(plaintext[i]) - 'A' + shift) % 26) + 'A';  
    printf("%c", encryptedChar);  
}  
printf("\n");  
}

void decrypt() {
char ciphertext[128];
char key[16];
printf("\nEnter the ciphertext: ");
scanf(" %[^\n]", ciphertext);
printf("Enter the key: ");
scanf(" %[^\n]", key);

printf("Deciphered Text: ");  
for (int i = 0, j = 0; i < strlen(ciphertext); i++, j++) {  
    if (j >= strlen(key)) {  
        j = 0;  
    }  
    int shift = toupper(key[j]) - 'A';  
    char decryptedChar = ((toupper(ciphertext[i]) - 'A' - shift + 26) % 26) + 'A';  
    printf("%c", decryptedChar);  
}  
printf("\n");  
}

int main() {
int option;
while (1) {
printf("\n1. Encrypt");
printf("\n2. Decrypt");
printf("\n3. Exit\n");
printf("\nEnter your option: ");
scanf("%d", &option);

    switch (option) {  
        case 1:  
            encrypt();  
            break;  
        case 2:  
            decrypt();  
            break;  
        case 3:  
            exit(0);  
        default:  
            printf("\nInvalid selection! Try again.\n");  
            break;  
    }  
}  
return 0;  
}
```
## OUTPUT:

![Screenshot 2024-09-02 082609](https://github.com/user-attachments/assets/8a98ed44-18ef-4f51-8275-bc55b596b79a)

## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 
ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

## PROGRAM:

PROGRAM:
#include<stdio.h> #include<string.h> #include<stdlib.h> main()
{
int i,j,len,rails,count,code[100][1000]; char str[1000];
printf("Enter a Secret Message\n"); gets(str);
len=strlen(str);
printf("Enter number of rails\n"); scanf("%d",&rails); for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
code[i][j]=0;
}
}
count=0; j=0;
while(j<len)
{
if(count%2==0)
{
for(i=0;i<rails;i++)
{
//strcpy(code[i][j],str[j]);
code[i][j]=(int)str[j]; j++;
}

}
else
{
 
for(i=rails-2;i>0;i--)
{
code[i][j]=(int)str[j]; j++;
}
}

count++;
}

for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
if(code[i][j]!=0) printf("%c",code[i][j]);
}
}
printf("\n");
}
## OUTPUT:
OUTPUT:
Enter a Secret Message wearediscovered
Enter number of rails 2
waeicvrderdsoee
## RESULT:
The program is executed successfully
