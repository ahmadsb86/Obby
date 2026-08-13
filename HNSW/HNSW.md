# How it works

this is how it works

Builds off of pughs probability skip linked lists structure. More dynamic vesion of sorted array (log update) . Boils down to a sorted linked list with some (probability based) elements elevated to higher levels. For search, higher level is scanned (linearly not thru bin search because linked list) then when best found at that level, we search recursively in the next level.  

Random skips instead of even spread helps dynamify and good emperical perf 

HNSW  is a hierchy of multiple NSW, navigable small worlds which are basically proximity graphs where verticies close to each other are linked 

The probability of a vector insertion at a given layer is given by a probability function, and it must be cascaded downwards (layer 0 gets everyone)

Structure made with one-by-one insertions

To insert, greedily walk towards vector to new vector while searching into multiple candidates (ef_consutrction param defines how many) 

then when that sets stops getting better, choose M (another param) of the best ones to be linked.


# My thoughts

It seems like 