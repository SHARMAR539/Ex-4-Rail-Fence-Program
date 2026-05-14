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

#define MAX 100

void encrypt(char *pt, int rails, char *ct) {
    char fence[MAX][MAX] = {0};
    int len = strlen(pt), rail = 0, dir = 1, idx = 0;

    for (int i = 0; i < len; i++) {
        fence[rail][i] = pt[i];
        if (rail == 0) dir = 1;
        if (rail == rails - 1) dir = -1;
        rail += dir;
    }
    for (int r = 0; r < rails; r++)
        for (int c = 0; c < len; c++)
            if (fence[r][c]) ct[idx++] = fence[r][c];
    ct[idx] = '\0';
}

void decrypt(char *ct, int rails, char *pt) {
    int len = strlen(ct), cnt[MAX] = {0};
    int rail = 0, dir = 1;

    for (int i = 0; i < len; i++) {
        cnt[rail]++;
        if (rail == 0) dir = 1;
        if (rail == rails - 1) dir = -1;
        rail += dir;
    }
    char rows[MAX][MAX];
    int pos = 0;
    for (int r = 0; r < rails; r++) {
        strncpy(rows[r], ct + pos, cnt[r]);
        rows[r][cnt[r]] = '\0';
        pos += cnt[r];
    }
    int idx[MAX] = {0};
    rail = 0; dir = 1;
    for (int i = 0; i < len; i++) {
        pt[i] = rows[rail][idx[rail]++];
        if (rail == 0) dir = 1;
        if (rail == rails - 1) dir = -1;
        rail += dir;
    }
    pt[len] = '\0';
}

int main() {
    char pt[MAX], ct[MAX], dt[MAX];
    int rails;

    printf("Enter Plain Text  : ");
    scanf("%s", pt);
    printf("Enter No. of Rails: ");
    scanf("%d", &rails);

    encrypt(pt, rails, ct);
    decrypt(ct, rails, dt);

    printf("\nPlain Text  : %s\n", pt);
    printf("Cipher Text : %s\n", ct);
    printf("Decrypted   : %s\n", dt);

    return 0;
}
```

# OUTPUT

<img width="1703" height="969" alt="image" src="https://github.com/user-attachments/assets/498f0842-b32a-45c4-8a55-635cdef1e176" />


# RESULT

Thus, the C program to implement the rail fence transposition technique is successfully verified
