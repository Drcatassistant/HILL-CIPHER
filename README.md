# HILL CIPHER
HILL CIPHER
EX. NO: 3 
## AIM:
 

IMPLEMENTATION OF HILL CIPHER
 
## To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
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

## OUTPUT
![image](https://github.com/user-attachments/assets/0d00e31e-eb34-4271-a928-fc802aa3cffd)

## RESULT

The program executed successfully .
