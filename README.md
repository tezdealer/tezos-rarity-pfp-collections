# tezos-rarity-pfp-collections
Rarity (scores and ranks) for Tezos PFP collections and other FA2 NFT collections

The aim is to establish a rarity score and rank calculation that is used consistently across collections. Here's the process that will be followed for all collections.

## how rarity score is calculated

1. For the entire collection, all attributes and attribute values are identified e.g. Hair: Messy (Attribute: Attribute Value)
2. For the entire collection, all instances of an attribute value are counted
3. The total number of tokens in the collection is divided by the total count of an attribute value. 
   e.g. 1000/30 (1000 token collection, attribute value used 30 times) = rarity score of 33.33
4. Additionally, a rarity score for the number of attributes is generated and added to the sum. e.g. 5 tokens have 1 attribute, 100 tokens have 5 attributes, 300 tokens have 4 attributes, 550 tokens have 6 attributes, etc. Tokens with 1 attribute would be the most rare in this case.

Once the overall scores are determined per attribute value:

5. Per token, a sum is made of the rarity score of each attribute value that the token has. That is the token's final rarity score.

## how rank is calculated
1. Starting with the highest rarity score, tokens receive a rank, beginning with Rank #1 (most rare)
2. If multiple tokens have the same rarity score, they receive the same rank. A count is taken of tokens with the same rank, and that many is added to the next rank.

For example: if 5 tokens have highest rarity score of 1000, they will each have rank #1. But the token with the next highest rarity score will have rank of #6.

So: #1, #1, #1, #1, #1, #6 (#2-#5 are skipped).

## edge cases

### when attribute value == 'None'
when an attributes value has the actual value of 'None' instead of the attribute being omitted altogether from the token metadata, then the attribute will not be counted toward 'total count of attribute' calculation. however, the attribute value itself of 'None' will still be given a rarity score (how many others also have 'None' as value for this attribute) and included in overall rarity score. this calculation may change in the future, but for now this is the way it is managed. Note that most collections simply don't include the attribute in the metadata if the token doesn't have that attribute.
