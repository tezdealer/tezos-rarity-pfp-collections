# tezos-rarity-pfp-collections
Rarity (scores and ranks) for Tezos PFP collections and other FA2 NFT collections

The aim is to establish a rarity score and rank calculation that is used consistently across collections. Here's the process that will be followed for all collections.

## how rarity score is calculated

1. For the entire collection, all attributes and attribute values are identified e.g. Hair: Messy (Attribute: Attribute Value)
2. For tokens that don't have a specific attribute, the attribute along with a value of "None" will be applied and included in the calculation. However, attributes with value of "None" will not be counted toward the NFT's attribute count.
3. For the entire collection, all instances of an attribute value are counted
4. The total number of tokens in the collection is divided by the total count of an attribute value. 
   e.g. 1000/30 (1000 token collection, attribute value used 30 times) = rarity score of 33.33
5. Additionally, a rarity score for the number of attributes is generated and added to the sum. e.g. 5 tokens have 1 attribute, 100 tokens have 5 attributes, 300 tokens have 4 attributes, 550 tokens have 6 attributes, etc. Tokens with 1 attribute would be the most rare in this case.

Once the overall scores are determined per attribute value:

6. Per token, a sum is made of the rarity score of each attribute value that the token has. That is the token's final rarity score.

## how rank is calculated
1. Starting with the highest rarity score, tokens receive a rank, beginning with Rank #1 (most rare)
2. If multiple tokens have the same rarity score, they receive the same rank. A count is taken of tokens with the same rank, and that many is added to the next rank.

For example: if 5 tokens have highest rarity score of 1000, they will each have rank #1. But the token with the next highest rarity score will have rank of #6.

So: #1, #1, #1, #1, #1, #6 (#2-#5 are skipped).

## edge cases

### when real token metadata has yet to be revealed, ignore
For tokens whose attributes have yet to be revealed (new mints). These tokens will be excluded from the report, and total token count will ignore these tokens. For example, these tokens can be identified when these conventions are used:
* attribute name of 'Status' == 'Hidden', 'Incubating', etc (similar status values are added as needed)
* attribute name of 'Revealed' == 'False'

### remove 'meta' attributes
If summary metadata is included as an attribute like 'Rarity Score', don't evaluate it as an attribute
