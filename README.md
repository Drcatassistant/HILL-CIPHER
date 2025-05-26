# Cryptography---19CS412-classical-techqniques



# Hill Cipher
Hill Cipher using with different key values

**Name : Jackson Raj A**

**Reg no : 212223040071**


**Date : 27-03-2025**

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
PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define SIZE 2  // Size of the key matrix (2x2 for simplicity)

int keyMatrix[SIZE][SIZE];

void toUpperCase(char *str) {
    for (int i = 0; str[i]; i++) {
        str[i] = toupper(str[i]);
    }
}

void removeSpaces(char *str) {
    int count = 0;
    for (int i = 0; str[i]; i++) {
        if (str[i] != ' ') {
            str[count++] = str[i];
        }
    }
    str[count] = '\0';
}

void getKeyMatrix(char *key) {
    int k = 0;
    toUpperCase(key);
    removeSpaces(key);
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            keyMatrix[i][j] = key[k++] - 'A';
        }
    }
}

void encrypt(char *text, char *cipher) {
    toUpperCase(text);
    removeSpaces(text);
    int len = strlen(text);
    if (len % SIZE != 0) {
        text[len++] = 'X';  // Padding if needed
        text[len] = '\0';
    }
    
    for (int i = 0; i < len; i += SIZE) {
        for (int row = 0; row < SIZE; row++) {
            int sum = 0;
            for (int col = 0; col < SIZE; col++) {
                sum += keyMatrix[row][col] * (text[i + col] - 'A');
            }
            cipher[i + row] = (sum % 26) + 'A';
        }
    }
    cipher[len] = '\0';
}

void printKeyMatrix() {
    printf("Key Matrix:\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%d ", keyMatrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    char key[SIZE * SIZE + 1], text[100], cipher[100];
    
    printf("Enter key (4 letters): ");
    scanf("%s", key);
    getKeyMatrix(key);
    printKeyMatrix();
    
    printf("Enter plaintext: ");
    scanf("%s", text);
    
    encrypt(text, cipher);
    printf("Ciphertext: %s\n", cipher);
    
    return 0;
}
```


## OUTPUT:
OUTPUT:
Simulating Hill Cipher
![image](https://github.com/user-attachments/assets/39d653eb-34fa-4a3b-8ea5-eab5df452ebc)

------------------------------------------------------------------------------------------------------------------

## RESULT:
The program is executed successfully


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

## PROGRAM:
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

#define MAX_LENGTH 100

int main() 
{
    char input[MAX_LENGTH];
    char key[MAX_LENGTH];
    char result[MAX_LENGTH];

    printf("Enter the text to encrypt: ");
    fgets(input, MAX_LENGTH, stdin);
    input[strcspn(input, "\n")] = '\0'; 

    printf("Enter the key: ");
    fgets(key, MAX_LENGTH, stdin);
    key[strcspn(key, "\n")] = '\0'; 

    int inputLength = strlen(input);
    int keyLength = strlen(key);

    for (int i = 0, j = 0; i < inputLength; ++i) 
    {
        char currentChar = input[i];

        if (isalpha(currentChar))
        {
            int shift = toupper(key[j % keyLength]) - 'A';
            int base = isupper(currentChar) ? 'A' : 'a';

            result[i] = ((currentChar - base + shift + 26) % 26) + base;
            ++j;
        }
        else
        {
            result[i] = currentChar;
        }
    }

    result[inputLength] = '\0';
    printf("Encrypted text: %s\n", result);

    for (int i = 0, j = 0; i < inputLength; ++i) 
    {
        char currentChar = result[i];

        if (isalpha(currentChar)) 
        {
            int shift = toupper(key[j % keyLength]) - 'A';
            int base = isupper(currentChar) ? 'A' : 'a';

            result[i] = ((currentChar - base - shift + 26) % 26) + base;
            ++j;
        }
    }

    result[inputLength] = '\0';
    printf("Decrypted text: %s\n", result);

    return 0;
}
```

## OUTPUT:

![Screenshot 2025-04-23 232951](https://github.com/user-attachments/assets/50ec17f7-85b2-4563-a7e6-98715a8c2f09)



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

## PROGRAM:

```
#include<stdio.h>
#include<string.h>
#include<stdlib.h>
main()
{
int i,j,len,rails,count,code[100][1000];
 char str[1000];
 printf("Enter a Secret Message\n");
 gets(str);
 len=strlen(str);
printf("Enter number of rails\n");
scanf("%d",&rails);
for(i=0;i<rails;i++)
{
 for(j=0;j<len;j++)
 {
 code[i][j]=0;
 }
}
count=0;
j=0;
while(j<len)
{
if(count%2==0)
{
for(i=0;i<rails;i++)
{
 //strcpy(code[i][j],str[j]);
 code[i][j]=(int)str[j]; 
 j++;
}
}
else
{
for(i=rails-2;i>0;i--)
{
 code[i][j]=(int)str[j];
j++;
} 
} 
count++;
}
for(i=0;i<rails;i++)
{
for(j=0;j<len;j++)
{
 if(code[i][j]!=0)
 printf("%c",code[i][j]);
}
}
printf("\n");
}
```

## OUTPUT:

![image](https://github.com/user-attachments/assets/15133eb9-b494-498c-9cae-8a796c87bfb1)


## RESULT:
The program is executed successfully
