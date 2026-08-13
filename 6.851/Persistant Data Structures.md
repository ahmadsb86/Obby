# Partial persistence (only last version updatable)

Is simple under bounded in-degree assumption within pointer machine model (everything is a fixed-sized node with some fields and values; values can be pointers)

Idea is to (along with static data section) just keep a mod log of each modification and every time mod log gets full, copy contents into static sec of a new node. Use backpointers (the number of which is ofc bounded) to persistantly update pointing nodes. This could be expensive if those nodes in turn have full mod logs, but amortization works out O(1) when you set mod log capacity to 2p (p=in-degree bound)

# Full persistence (Tree of versions)

versions stored with tree encoded with matched parenthesis in an order maintainance struct (discussed in lec8) allows ancestor search of version in O(1) for any node which solves read

we also need backpointers to be versioned, because they helped with writing to a full node and now all nodes are updatable.

Updating full nodes is simillar but now we split mod log in half and put in a new node such that new node gets versions which form a subtree of the original versions in full node. Then update all forward/backward pointers of neighbors

# Confluent/Persistance
Very short explanation. TODO
# Research Space
OPEN: O(1) or even O(log (n)) space overhead per operation. for confluent
OPEN: De-amortization of full persistence.
OPEN: Is there a matching lower bound for both full and partial persistence?
OPEN: (for both functional and confluent) bigger separation? more general structure transforma-
tions?
OPEN: Lists with split and concatenate? General pointer machine?
SOLVED: by Blame Trees as described in [14], 6.851 Spring’12.
OPEN: Array with cut and paste? Special DAGs?