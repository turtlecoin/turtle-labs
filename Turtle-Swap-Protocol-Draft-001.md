# Turtle Swap Protocol
Draft 0





*RockSteady, Soregums, Fexra, Zpalm, IBurnMyCD*

Create a protocol for publishing and consuming swap offers, cross-network via p2p daemon advertisement.

Summary: It is possible for daemons to opt-in to a secondary protocol allowing management and interaction with a pool of orders for cross-chain atomic transfer.
By designing a method for connecting to, surveying, and consuming orders from other Cryptonote and TRTL flavored networks, we hope to create opportunities for decentralized atomic transfer.

Example Scenario: Jenny is on the TRTL Network and she wants to transfer 1,000,000.00 TRTL for 1,000,000,000.00 DATA on the Karai network. Paul is on the Karai Network, and he has 1,000,000,000.00 DATA to swap for TRTL.

1. Jenny launches her TRTL Network daemon with swap enabled ```./TurtleCoind --swap DATA 123.222.222.222```
The syntax enables her to `--swap` enable swap mode, `DATA` specify a receiving instrument for surety that this is the network she wishes to transact on, and `123.333.333.333`, a seed node (reliable entry) to the neighbor network.
2. Jenny's daemon has connected to the TRTL Network, and has received a heartbeat or indicator from the neighbor network's seed that she is engaged in a connection currently.
3. Jenny can then issue commands like `list` or `consume` or `offer`:
  - `list` would list current swap offers of the neighbor network with swap offers for Jenny's native currency at the top of the list.
  - `consume ####` would allow Jenny to consume an order for swap on the neighbor network
  - `offer 1000000 TRTL 1000000000 DATA 90 PARTIAL` where she posts an offer of 1MM TRTL in exchange for 1BB DATA, she'd like the data to persist for 90 blocks on the neighbor network, and "partial" rather than "full" means that partial swaps are okay.
  
Diagram:

Listings should be easily viewable from the terminal, and should supply API endpoints for explorers to consume the offer data. This enables open swap offers to be browsed from websites instead of needing a different sync'd daemon for each network.

ID(int), publisheraddress(string), numberofnativecurrency(int), swapcurrencyamount(int), expirationdate
```
==========================================================================================================================
=  ID  =  Publisher Address  =  Amt. Publisher Currency  =  Amt. Consumer Currency  =  full/partial  =  expiration time  =
==========================================================================================================================

 FFF111   TRTLv2iu84jgje...         1,000,000 TRTL               5,000 XMLC            Partial        1,000 TRTL Blocks
 AD2B34   TRTLv2iu84jgje...           500,000 TRTL               2,500 XMLC            Partial          500 TRTL Blocks
 FED277   TRTLv2er34634e...         9,000,000 TRTL              45,000 XMLC             FULL          8,000 TRTL Blocks
 CBCDA4   TRTLv2iu84jgje...         1,000,000 TRTL               5,000 XMLC            Partial        1,000 TRTL Blocks
 5D8BAC   TRTLv2iu84jgje...         1,000,000 TRTL               5,000 XMLC            Partial        1,000 TRTL Blocks
 
 ```
 
 TODO: Border interaction
