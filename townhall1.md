### CDNs

Useful for info that isn't updated much, static assets and javascript files. It hits the server first, then finds the closest CDN for the larger transfer

### LinkedIn
Lots of ways you would have workers be continuously building out the connections for a particular user when users are logged in.

Might be a good idea to know how much a redis cache can hold, rough estimate of how many users, etc. 

Need to further explore building relational data for LinkedIn. 

Rough local storage size on a browser? 

### URL Shorteners
Better to use a hashing function because iterating would create a bottle neck at scale, where at some point it has to become synchronous. 

### Sharding

Sharding makes things slower, because you have to check which shard a row is located, and you'd have to go over the network for that. Tradeoff of speed and throughput seems like the thing here. 

### SubsetAvg 

Do preprocessing so that when you compute the average it will have already been calculated when the matrix was created. This would have huge space complexity, and is a little bit of a gotcha, but could also do it with a leaner second matrix that has sums which you could then deduce averages from.