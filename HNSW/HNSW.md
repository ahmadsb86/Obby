# How it works

this is how it works

Builds off of pughs probability skip linked lists structure. More dynamic vesion of sorted array (log update) . Boils down to a sorted linked list with some (probability based) elements elevated to higher levels. For search, higher level is scanned (linearly not thru bin search because linked list) then when best found at that level, we search recursively in the next level.  

Random skips instead of even spread helps dynamify and good emperical perf 

HNSW  is a hierchy of multiple NSW, navigable small worlds which are basically proximity graphs where verticies close to each other are linked 

The probability of a vector insertion at a given layer is given by a probability function, and it must be cascaded downwards (layer 0 gets everyone)

Structure made with one-by-one insertions

Insertion:

The probability of a vector insertion at a given layer is given by a probability function normalized by the _‘level multiplier’ m_L_, where _m_L = ~0_ means vectors are inserted at layer 0 only and 1/lnM is generally optimal.

To insert a vector `q`, first search for its `ef` nearest neighbors (ef=1 in paper and most implementations), moving down layer by layer (same as search, taking the local minimum at each layer) until reaching the chosen _insertion layer_. From there, phase two begins: `ef` is raised to `efConstruction`, so more neighbors come back. These neighbors are candidates for links to `q` and also entry points to the next layer down. `M` of the candidates are linked to `q`, most simply the closest ones. efconstruction must be bigger than m so that you get true closest neighbors linked, otherwise youll just be linking approx neighbors. `M_max` caps the links per vertex, and `M_max0` is the same cap for vertices in layer 0.

`M_max` / `M_max0` are enforced by pruning: when linking `q` pushes a neighbor `e` over its cap, `e` re-runs selection over its neighbors plus `q` and keeps the best `M_max` (`M_max0` at layer 0), so the graph ends up directed. 

The graph is directed because if it is connected to at 
# My thoughts

It seems like 