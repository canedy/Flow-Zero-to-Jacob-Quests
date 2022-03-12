1. What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")
   - Uhmmm. Provide a `destroy` function

2. Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.
   - Idea #1: Do we really want everyone to be able to mint an NFT? (insert thinking emoji here).
     - I would think in most cases you would want a admin to mint new NFTs. So we would have to figure out how to restrict it to only certain accounts.

   - Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?
     - Yeah, that is no fun. As we learned, it's easier to reference resources and then work with them with reference. I would imagine having to do something similar with getting to the NFT metadata. 
