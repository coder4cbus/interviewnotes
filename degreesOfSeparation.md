### How would you architect the feature in LinkedIn that tells you how many degrees of separation there are between you and another person?

### Basic System Design

First thought is that on a basic level this would be some kind of graph data structure. Each person is a node in the graph, and every connection represents an edge in the graph. The degrees of separation between two nodes is essentially the number of edges traversed to go from one node the other. 

One potential wrinkle (this may be a operational or business consideration) is that since you want easily tell the relationship between any two nodes,you probably only want to traverse every time a new connection is made, and then store the relationships on each node of all 1st, 2nd, and 3rd degree connections. Possibly you won't want to bother storing connections beyond the third degree. If you did, that would make it difficult to maintain since you would need to constantly be navigating the entire graph to update all of the connections. 

#### Database 

Each person is stored in the database indexed by an ID with an associated array of all the unique IDs of their direct connections. This could be possible with a simple NoSQL table, but it also lends itself well to a relational data. * This should be explored further.

Each person stored in the database would also have an array of second degree connections and third degree connections, such that you could have quick lookup to determine whether or not someone is a 1st, 2nd, or 3rd degree connection to any individual. Any node not within 3 degrees could be considered 3+ by default (although potentially there are nodes that are simply not connected at all, such that it is not possible to traverse to reach them) * Need to examine whether these related parts of the graph would be stored in array or something like a dictionary with IDs, since you would want to be able to look up very quickly to determine the degree of connection.

#### Algorithm

While the database would store the results of the algorithms work for quick and easy look up, display, and persistence, the algorithm is the generator of this information. When two nodes are connected, the algorithm would run with both nodes as inputs and it would traverse the graph. 

The degree of connection, it should be noted, is the shorted number of edges that must be traversed to reach another node. 

When a connection is made, both each node is added as a first degree connection to the other. Secondarily, all first degree connections of each node are added as second degree connections to the other (as long as they aren't already 1st degree connections). Then, all third degree connections of each node are added as second degree connections to the other (unless they were already second degree or higher connections). Lastly, all third degree or higher connections from each node are added as three plus connections to the other node. 

All of this work can be done either using a database and simply accessing the 1st, 2nd, and 3rd connections and iterating through them all, or it can be done by using an actual graph system stored in a database for clearer traversal. * Would be good to think about which is optimal. 

The key idea here is that this algorithm is run and performed at each connection and then stored as denormalized data on each node/person, rather than being calculated on each click of a perosn or node. 

#### Web Server
On the server level, when a connection request is accepted, it would route to a url path that updates invokes the algorithm to run on both nodes and update the information for each. 

### Scalability
For scalability there are a few additional factors to consider, including the ability to handle large amounts of records (billions of daily users) and potentially millions of connections made per second. One issue is also that if the algorithms are running and updating particular nodes, those nodes are probably going to have to be 'locked' for updates by other connections until they are done updating, meaning that algorithms are queued up and run on nodes. 

The avoid the bottleneck of continually pinging the database, it would be reasonable to use a memory caching service such as Redis since users are likely to add connections in spurts, such that when a user adds a connection, the initial fetch is from the database, but the connections are stored in memory for a period of 15 minutes so that subsequent connections made only need to look up the connections of the other nodes, not the node of the user. 

The webserver should also outsource the algorithm logic to a separate worker (which is itself a server), or even better a fleet of workers to continually run the algorithm without freezing up the webserver, and they just asynchronously update the data as they complete their tasks. 

In worst case scenarios, it is worth considering that a given user might have up to 1000 1st degree connections (though this is a relatively heavy user), and in the worst case each of those connections might have 1000 connections, resulting in 1 million second degree connections, and lastly if each of the 1M had 1000 connections that would quickly mean that there are 1 billion 3rd degree connections! Although this is likely a worst case, and the actual numbers would probably be smaller, it is worth considering this scenario. It should be ok for these processes to work slowly since it is not especially important for 3rd degree connections or higher to be displayed quickly. 

### Maintainability / Operation
It is worth exploring the potential benefits of various types of databases, potentially storing the information in a relational database would make more sense. * Need to explore this idea.

### Business Decisions
From a business perspective, you would want to make sure to have the capacity to scale to every person in the world, or at least every adult, but it would also be import to be able to dynamically scale horizontally, keeping costs down and not using unnecessary storage or processing power at periods of low traffic or use. 

In that sense you could turn off and on workers that run the algorithm at times of low and high traffic respectively. 