# HILL CIPHER
HILL CIPHER
EX. NO: 3 

```
Name     : Shivaram M.
Reg. No. : 212223040195
```

AIM: 

IMPLEMENTATION OF HILL CIPHER
 
## To write a program to implement the hill cipher substitution techniques.

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
import numpy as np
from sympy import Matrix

def mod_inverse(matrix, mod):
    det = int(round(np.linalg.det(matrix))) % mod
    det_inv = pow(det, -1, mod)  # Modular inverse of determinant
    adjugate = Matrix(matrix).adjugate()
    return (det_inv * np.array(adjugate) % mod).astype(int)

def text_to_matrix(text, size):
    text = text.upper().replace(" ", "")
    while len(text) % size != 0:
        text += 'X'
    values = [ord(char) - ord('A') for char in text]
    return np.array(values).reshape(-1, size)

def matrix_to_text(matrix):
    return "".join(chr(int(round(num)) % 26 + ord('A')) for num in matrix.flatten())

def hill_cipher_encrypt(text, key_matrix):
    text_matrix = text_to_matrix(text, key_matrix.shape[0])
    encrypted_matrix = np.dot(text_matrix, key_matrix) % 26
    return matrix_to_text(encrypted_matrix)

def hill_cipher_decrypt(ciphertext, key_matrix):
    try:
        key_inverse = mod_inverse(key_matrix, 26)
    except ValueError:
        return "Error: Key matrix is not invertible mod 26. Choose a different key."
    cipher_matrix = text_to_matrix(ciphertext, key_matrix.shape[0])
    decrypted_matrix = np.dot(cipher_matrix, key_inverse) % 26
    return matrix_to_text(decrypted_matrix)

# Get user input
message = input("Enter the message: ").strip()
key_values = list(map(int, input("Enter the key matrix values (space-separated): ").split()))
size = int(len(key_values) ** 0.5)
key_matrix = np.array(key_values).reshape(size, size)

encrypted_text = hill_cipher_encrypt(message, key_matrix)
decrypted_text = hill_cipher_decrypt(encrypted_text, key_matrix)

print("Encrypted:", encrypted_text)
print("Decrypted:", decrypted_text)

```

## OUTPUT

<img width="1680" alt="hill_cipher" src="https://github.com/user-attachments/assets/0327743c-7b33-4699-8761-441bf9ba228b" />

## RESULT

The program is executed successfully.
