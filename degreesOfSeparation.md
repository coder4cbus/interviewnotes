### How would you architect the feature in LinkedIn that tells you how many degrees of separation there are between you and another person?

Brainstorm

Things to hit: 
* Naive Working Solution
* Scalability
* Maintainability
* Business Considerations
* Diagrams

### Basic System Design

First thought is that on a basic level this would be some kind of graph data structure. Each person is a node in the graph, and every connection represents an edge in the graph. The degrees of separation between two nodes is essentially the number of edges traversed to go from one node the other. 

One potential wrinkle (this may be a operational or business consideration) is that since you want easily tell the relationship between any two nodes,you probably only want to traverse every time a new connection is made, and then store the relationships on each node of all 1st, 2nd, and 3rd degree connections. Possibly you won't want to bother storing connections beyond the third degree. If you did, that would make it difficult to maintain since you would need to constantly be navigating the entire graph to update all of the connections. 

#### Database 

Each person is stored in the database indexed by an ID with an associated array of all the unique IDs of their direct connections. This could be possible with a simple NoSQL table, but it also lends itself well to a relational data. * This should be explored further.

Each person stored in the database would also have an array of second degree connections and third degree connections, such that you could have quick lookup to determine whether or not someone is a 1st, 2nd, or 3rd degree connection to any individual. Any node not within 3 degrees would be considered 3+ by default. * Need to examine whether these related parts of the graph would be stored in array or something like a dictionary with IDs, since you would want to be able to look up very quickly who is in

#### Algorithm

I would design an algorithm that will 