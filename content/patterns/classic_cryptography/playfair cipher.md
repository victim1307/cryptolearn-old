+++
title = "Playfair Cipher"
weight = 4
+++

The Playfair Cipher is a polygraphic substitution cipher that encrypts pairs of letters instead of single letters. It uses a 5x5 grid of letters (called the key square or tableau) to encrypt pairs of letters.

To encrypt a message, the first step is to create the key square. This is done by choosing a keyword and writing it in a 5x5 grid, filling the remaining spaces with the remaining letters of the alphabet in alphabetical order, omitting the letter 'J'.

For example, using the keyword "PLAYFAIR", the grid would be:
{{<code>}}
P L A Y F
I R B C D
E G H K M
N O Q S T
U V W X Z
{{</code>}}
Then the plaintext message is divided into pairs of letters, if the message has an odd length, the last letter is padded with an "X" or any other letter.

#### The encryption process is done by following these steps:

- If both letters of the pair are the same, an "X" or any other letter is added to the second letter to make them different.
- If the letters are in the same row of the key square, the letters to the right of each one are used (wrapping around to the left side of the row if necessary)
- If the letters are in the same column of the key square, the letters below each one are used (wrapping around to the top of the column if necessary)
- If the letters are in different rows and columns, the letters at the intersections of the same row and column as each letter are used.
For example, using the key square above and the plaintext "HELLO", the ciphertext would be "CENNR".

The Playfair Cipher decryption process is similar to the encryption process, but the opposite operations are applied.

To decrypt a message that was encrypted using the Playfair Cipher, the first step is to create the key square using the same keyword that was used to encrypt the message.

Then, the ciphertext message is divided into pairs of letters, just as it was done during the encryption process.

#### The decryption process is done by following these steps:

- If the letters are in the same row of the key square, the letters to the left of each one are used (wrapping around to the right side of the row if necessary)
- If the letters are in the same column of the key square, the letters above each one are used (wrapping around to the bottom of the column if necessary)
- If the letters are in different rows and columns, the letters at the intersections of the same row and column as each letter are used.
For example, using the key square created with the keyword "PLAYFAIR" and the ciphertext "CENNR", the plaintext would be "HELLO".

It's important to note that this decryption process assumes that the key square was created using the same keyword as the one used to encrypt the message and that the plaintext message was padded with "X" or any other letter if necessary.

### Code
{{<code>}}
import re


def textCleaning(text):
    text = text.upper()
    text = re.sub(r'\s*\d+\s*', '', text)
    text = re.sub(r'[^\w\s]', '', text)
    text = text.replace(' ', '')
    return text


def postProcess(text):
    text = [text[i:i+5] for i in range(0, len(text), 5)]
    text = ' '.join(text)

    return text


def matrix(x, y, initial):
    return [[initial for i in range(x)] for j in range(y)]


def locateIndex(c, playFairMatrix):  # get location of each character
    loc = list()
    if c == 'J':
        c = 'I'
    for i, j in enumerate(playFairMatrix):
        for k, l in enumerate(j):
            if c == l:
                loc.append(i)
                loc.append(k)
                return loc


def encrypt(text, playFairMatrix):
    text = textCleaning(text)
    cipher = ''
    i = 0
    for s in range(0, len(text)+1, 2):
        if s < len(text)-1:
            if text[s] == text[s+1]:
                text = text[:s+1]+'X'+text[s+1:]

    if len(text) % 2 != 0:
        text = text[:]+'X'

    # print("CIPHER TEXT:", end='')

    while i < len(text):
        loc = list()
        loc = locateIndex(text[i], playFairMatrix)
        loc1 = list()
        loc1 = locateIndex(text[i+1], playFairMatrix)
        if loc[1] == loc1[1]:
            cipher += playFairMatrix[(loc[0]+1)%5][loc[1]] + playFairMatrix[(loc1[0]+1)%5][loc1[1]]
            # print("{}{}".format(playFairMatrix[(loc[0]+1)%5][loc[1]],playFairMatrix[(loc1[0]+1)%5][loc1[1]]),end=' ')
        elif loc[0] == loc1[0]:
            cipher += playFairMatrix[loc[0]][(loc[1]+1) % 5] + playFairMatrix[loc1[0]][(loc1[1]+1) % 5]
            # print("{}{}".format(playFairMatrix[loc[0]][(loc[1]+1)%5],playFairMatrix[loc1[0]][(loc1[1]+1)%5]),end=' ')
        else:
            cipher += playFairMatrix[loc[0]][loc1[1]] + playFairMatrix[loc1[0]][loc[1]]
            # print("{}{}".format(playFairMatrix[loc[0]][loc1[1]],playFairMatrix[loc1[0]][loc[1]]),end=' ')
        i = i+2

    cipher = postProcess(cipher)

    return cipher


def decrypt(cipher, playFairMatrix):  # decryption
    cipher = textCleaning(cipher)
    plainText = ''
    # print("PLAIN TEXT:", end=' ')
    i = 0
    while i < len(cipher):
        loc = list()
        loc = locateIndex(cipher[i], playFairMatrix)
        loc1 = list()
        loc1 = locateIndex(cipher[i+1], playFairMatrix)
        if loc[1] == loc1[1]:
            plainText += playFairMatrix[(loc[0]-1) % 5][loc[1]] + \
                playFairMatrix[(loc1[0]-1) % 5][loc1[1]]
            # print("{}{}".format(playFairMatrix[(loc[0]-1)%5][loc[1]],playFairMatrix[(loc1[0]-1)%5][loc1[1]]),end=' ')
        elif loc[0] == loc1[0]:
            plainText += playFairMatrix[loc[0]][(loc[1]-1) %
                                                5] + playFairMatrix[loc1[0]][(loc1[1]-1) % 5]
            # print("{}{}".format(playFairMatrix[loc[0]][(loc[1]-1)%5],playFairMatrix[loc1[0]][(loc1[1]-1)%5]),end=' ')
        else:
            plainText += playFairMatrix[loc[0]][loc1[1]
                                                ] + playFairMatrix[loc1[0]][loc[1]]
            # print("{}{}".format(playFairMatrix[loc[0]][loc1[1]],playFairMatrix[loc1[0]][loc[1]]),end=' ')
        i = i+2

    plainText = postProcess(plainText)

    return plainText


def generatePlayfairSquare(key):
    key = key.upper()
    result = list()

    for c in key:  # storing key
        if c not in result:
            if c == 'J':  # replacing j with i
                result.append('I')
            else:
                result.append(c)

    flag = 0

    for i in range(65, 91):  # storing other character
        if chr(i) not in result:
            if i == 73 and chr(74) not in result:
                result.append("I")
                flag = 1
            elif flag == 0 and i == 73 or i == 74:
                pass
            else:
                result.append(chr(i))
    k = 0
    my_matrix = matrix(5, 5, 0)  # initialize matrix
    for i in range(0, 5):  # making matrix
        for j in range(0, 5):
            my_matrix[i][j] = result[k]
            k += 1

    return my_matrix

def main():
    while(1):
        choice=int(input("\n 1.Encryption \n 2.Decryption: \n 3.EXIT \n"))
        key=input("Enter key : ")
        key = textCleaning(key)

        PS = generatePlayfairSquare(key)
        if choice==1:
            plainText = input("Enter Plaintext : ")
            plainText = textCleaning(plainText)
            print(encrypt(plainText, PS))
        elif choice==2:
            cipher = input('Enter cipher : ')
            cipher = textCleaning(cipher)
            print(decrypt(cipher,PS))
        elif choice==3:
            exit()
        else:
            print("Choose correct choice")
    return 0

if __name__ == '__main__':
    main()
{{</code>}}

