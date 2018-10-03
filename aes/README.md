# AES
By Matt Prost

## Instructions For Running
Step 1: gcc -o aes aes.c 

Step 2: ./aes [KEY SIZE] [KEY FILENAME] [INPUT FILENAME] [OUTPUT FILENAME] [MODE]

KEY SIZE = {128,256}

MODE = {encrypt,decrypt}

Example:

gcc -o aes aes.c

./aes 256 key256 input256 output256 encrypt
## Encryption
Encryption is implemented in the function

uint8\_t\* encrypt(uint8\_t\* key, uint8\_t\* plaintext, uint16\_t Nb, uint16\_t Nk, uint16\_t Nr)

It takes into account which mode it is in (128 or 256), and sets the Nb, Nk, and Nr values accordingly.
It follows the pseudocode outlined in Figure 5 of the AES document, and implements 4 primary functions discussed in this section.
### Sub Bytes
uint8\_t\*\* subBytes(uint8\_t\*\* state)

This function uses a look up table to substitute given Byte values. S-Box values were sourced from online and put into an array. 
### Shift Rows
uint8\_t\*\* shiftRows(uint8\_t\*\* state)

This function swaps the column position of a state entry, based on the row value. This is done pretty succinctly with a nested for loop and a small amount of math.
### Mix Columns
uint8\_t\*\* mixColumns(uint8\_t\*\* state)

This function transforms entries in a column, based on the sum of several multiplication operations on the entries in that column. The sum is simply implemented by XORing the values, and the multiplication is accomplished using lookup tables provided by instructors. The lookup tables used for this function are 2 and 3 as outlined in the specs. Note that 1 is also used, but it requires no additional math.
### Add Round Key
uint8\_t\*\* mixColumns(uint8\_t\*\* state)

This function simply adds the round key to a column of the state. It relies on the key expansion to obtain these values.
#### Key Expansion 
uint32\_t\* keyExpansion(uint8\_t\* key, uint16\_t size, uint16\_t Nk)

This function implements logic as defined by the pseudocode in Figure 11 of the AES document. It creates a key schedule to be used during the Add Round Keys function by filling the first values of the key schedule with the values of the key, and appending XORed values from earlier in the key schedule, until the key schedule is full. Which values get XORed is dependent on how many Bytes the original key was, and every 4th word is scrambled by some variance of an S-Box lookup, rotating the Bytes in the word, and XORing the values with a lookup table sourced from the Internet. The exact scrambling of the 4th word is dependent on where the key schedule is in the sequence, and what size the original key was.

## Decryption
Decryption is implemented in the function

uint8\_t\* decrypt(uint8\_t\* key, uint8\_t\* ciphertext, uint16\_t Nb, uint16\_t Nk, uint16\_t Nr)

It takes into account which mode it is in (128 or 256), and sets the Nb, Nk, and Nr values accordingly.
It follows the pseudocode outlined in Figure 12 of the AES document, and implements 3 primary functions discussed in this section. These functions are simply inverses of functions discused in the encryption section. Decryption also uses Add Round Key, which is the same in encryption.
### Inverse Sub Bytes
uint8\_t\*\* subBytesInv(uint8\_t\*\* state)

This function uses a look up table to substitute given Byte values. Inverse S-Box values were sourced from online and put into an array. 
### Inverse Shift Rows
uint8\_t\*\* shiftRowsInv(uint8\_t\*\* state)

This function swaps the column position of a state entry, based on the row value. This is done pretty succinctly with a nested for loop and a small amount of math. The direction of the swap is opposite of the Shift Rows function used for encryption.
### Inverse Mix Columns
uint8\_t\*\* mixColumnsInv(uint8\_t\*\* state)

This function transforms entries in a column, based on the sum of several multiplication operations on the entries in that column. The sum is simply implemented by XORing the values, and the multiplication is accomplished using lookup tables provided by instructors. The lookup tables used for this function are 9, 11, 13, and 14 as outlined in the specs.

