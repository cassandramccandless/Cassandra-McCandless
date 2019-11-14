# Cassandra-McCandless
import sys
#open file specified by user
keywordfile=open(sys.argv[1], 'r')
for line in keywordfile:
    keyword = line.strip()
    
    MIN_WORDLEN = 5
     # check min word length
    if len(keyword) < MIN_WORDLEN: 
        continue      
    #open the output file    
    matrixfile = open(sys.argv[2], 'w')
    #the weight calculation; loop fro the 5th to 2nd character in the word
    for i in range(4, 0, -1):
        charValue = ord(keyword[i])
        shiftValue = (i-1)*8 #shift index 4 24 bits, 3rd 16 bits, 2nd 8 bits, 1st 0 bits
        charWeight = charValue << shiftValue
        wordWeight = (wordWeight | charWeight)
        matrixfile.write(hex(wordWeight) + '\n')
        keywordfile.close()
        matrixfile.close()
    
