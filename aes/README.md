# AES
By Matt Prost

## Encryption
Encryption is implemented in the function

It takes into account which mode it is in (128 or 256), and sets the Nb, Nk, and Nr values accordingly.
It follows the pseudocode outlined in Figure 5 of the AES document, and implements 4 primary functions discussed in this section.
### Sub Bytes

This function uses a look up table 
### Shift Rows
### Mix Columns
### Add Round Key

## Decryption
### Inverse Sub Bytes
### Inverse Shift Rows
### Inverse Mix Columns
