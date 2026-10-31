# Lab-Exercise---2---Playfair-Cipher
# Aim 
To implement a program to encrypt a plain text and decrypt a cipher text using play fair Cipher substitution technique.
# Procedure
Step 1: Design of PlayFair Cipher algorithm 
Step 2: Implementation using C or python code 
Step 3: Testing algorithm with different key values.
# Program 
```
def create_matrix(key):
    key = key.upper().replace("J", "I")
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"

    matrix_list = []

    for ch in key + alphabet:
        if ch.isalpha() and ch not in matrix_list:
            matrix_list.append(ch)

    matrix = [matrix_list[i:i+5] for i in range(0, 25, 5)]

    return matrix


def prepare_message(message):
    message = message.upper().replace("J", "I")
    result = ""

    i = 0
    while i < len(message):
        a = message[i]

        if i + 1 < len(message):
            b = message[i + 1]
        else:
            b = 'X'

        if a == b:
            result += a + 'X'
            i += 1
        else:
            result += a + b
            i += 2

    if len(result) % 2 != 0:
        result += 'X'

    return result


def encrypt(message, matrix):
    message = prepare_message(message)
    result = ""

    for i in range(0, len(message), 2):
        ch1 = message[i]
        ch2 = message[i + 1]

        r1 = c1 = r2 = c2 = 0

        for r in range(5):
            for c in range(5):
                if matrix[r][c] == ch1:
                    r1, c1 = r, c
                if matrix[r][c] == ch2:
                    r2, c2 = r, c

        if r1 == r2:
            result += matrix[r1][(c1 + 1) % 5]
            result += matrix[r2][(c2 + 1) % 5]

        elif c1 == c2:
            result += matrix[(r1 + 1) % 5][c1]
            result += matrix[(r2 + 1) % 5][c2]

        else:
            result += matrix[r1][c2]
            result += matrix[r2][c1]

    return result


key = input("Enter key: ")
message = input("Enter message: ")

matrix = create_matrix(key)

print("\nPlayfair Matrix:")
for row in matrix:
    print(" ".join(row))

print("\nEncrypted message:", encrypt(message, matrix))
```
# Output
<img width="1392" height="697" alt="Screenshot 2026-10-26 101832" src="https://github.com/user-attachments/assets/8c880a5e-672a-40c3-a466-3521c54101f7" />

# Result
The program is executed successfully.
