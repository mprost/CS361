# AES
By Matt Prost

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

