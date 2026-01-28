# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM

```
#include <stdio.h>
#include <string.h>

int main() {
    char text[100], enc[100], dec[100];
    int rails, len, i, j;

    printf("Enter plaintext: ");
    scanf("%s", text);

    printf("Enter number of rails: ");
    scanf("%d", &rails);

    len = strlen(text);

    char rail[rails][len];
    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            rail[i][j] = '\n';

    int row = 0, dir = 1;
    for(i = 0; i < len; i++) {
        rail[row][i] = text[i];

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }

    int k = 0;
    for(i = 0; i < rails; i++) {
        for(j = 0; j < len; j++) {
            if(rail[i][j] != '\n')
                enc[k++] = rail[i][j];
        }
    }
    enc[k] = '\0';

    printf("Encrypted: %s\n", enc);

    // Step 1: Mark zigzag positions
    for(i = 0; i < rails; i++)
        for(j = 0; j < len; j++)
            rail[i][j] = '\n';

    row = 0; dir = 1;
    for(i = 0; i < len; i++) {
        rail[row][i] = '*';

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }

    // Step 2: Fill encrypted text row-wise
    k = 0;
    for(i = 0; i < rails; i++) {
        for(j = 0; j < len; j++) {
            if(rail[i][j] == '*' && k < len) {
                rail[i][j] = enc[k++];
            }
        }
    }

    // Step 3: Read zigzag to get plaintext
    row = 0; dir = 1;
    k = 0;
    for(i = 0; i < len; i++) {
        dec[k++] = rail[row][i];

        if(row == 0)
            dir = 1;
        else if(row == rails - 1)
            dir = -1;

        row += dir;
    }
    dec[k] = '\0';

    printf("Decrypted: %s\n", dec);

    return 0;
}

```

# OUTPUT

<img width="396" height="300" alt="image" src="https://github.com/user-attachments/assets/2784bc41-ae00-4bbd-8ef3-e0f6d2877a50" />


# RESULT

A C program to implement the rail fence transposition technique has been written and executed.
