<strong>OffchainVotingContract.sol</strong> 


Inherits from:

    IVoting: (Voting interface)

    DaoConstants: (Stores constants, (hashes of name strings and important addresses))

    MemberGuard: (Modifiers that only allow members to interact with a function)

    AdapterGuard: (Modifiers that allow only verified Adapters to interact with a function)

***

<strong>Function Spec</strong>

    function configureDao

***

Allows for the modification of voting the votingPeriod, grave period and fallback threshold.

    function submitVoteResult

***

Used to pass a an off-chain voting result to __submitVoteResult, checks that the vote is passed as a majority and the grace period must have ended 
Otherwise checks if a vote override is valid to pass to _submitVoteResult


    function _readyToSubmitResult



Internal function that returns a bool when a result is ready to submit based on the vote counts provided. 
***
    function _submitVoteResult  

Processes the logic and checks for submitting a voting result. Checks if the node result merkle root match and that the result weight is correct before 
processing the input and changing the vote struct. The sender will have his stake locked after processing this function. 
***
    function _lockFunds 

Locks loot according to dao.getConfiguration(StakingAmount). Checks if the lockee is an active member and has enough loot to lock. 
***
    function _releaseFunds

Releases locked loot from a members balance. Checks they have adequate locked loot and they are an active member. 
***
    startNewVotingForProposal

Adapter only function that sets the start tine and start block for a particular proposal in a particular doa in the votes mapping by changing the respective voting struct 
start time and blocknumber attributes. 
***
    function voteResult

Function which returns an int representing of the state of the vote; 

0: has not started

1: tie

2: pass

3: not pass

4: in progress
***
    function challengeWrongSignature

Checks if the challenger is part of the voting result and then builds the hash of a yes and no vote and challenges the result if the vote signature is incorrect for both.
***
    function challengeWrongWeight

Calls _challenge_result if the onchain snapshot weight is not equal to node's current weight. If so, the result is challenged and the reporter slashed.  
***
    function challengeDuplicate

Checks if two nodes that are part of the merkle tree have the same voter address. If so, the result is challenged (_challengeResult())
***
    function challengeWrongStep

This function is used to challenge a result is a step is incorrect. It checks if the data input is in fact from two consecutive nodes, if a result has been reported (in grace period) and that the proof checks for the nodes are valid. 
***
    requestFallback

Allows a voter to add their vote to the request_fallback tally, if enough members vote for it then on-chain voting will commence, 
***
    function _nodeHash

This function returns the hash of all of a nodes properties (32bit)
***
    function _checkStep

If a  challengeWrongStep is called successfully this is used to check that the reported voting statistics were incorrect and call _challengeResult(). 
***
    function _challengeResult

After a result is successfully challenged this function sets the state of the proposal to challenged and lock the loot (slashes) of the vote reporter. 
***
    function getSignedHash

This function returns a hash of the snapshot root, dao and proposal ID. 
***
    function getSignedAddress
This function recovers the address associated with the hash of the proposal hash and "\x19Ethereum Signed Message:\n32" and the calldata signature 
***
    function _hasVotedYes

Checks if a user has voted yes on a particular proposal, returns true for if they have votes yes and false if they have voted no. If they have signed for neither 
then the function will revert. 
***
     function _hasVoted

Function that checks, similar to above, if a user has voted on a particular proposal at all. Returns 1 if they have, 2 if they have not and 0 otherwise. 
***
    function recover

Returns the signers address given the hash of a signed message and the ethereum signature. If the address cannot be returned the key is returned instead with ecrecover. 
***
    function verify

Checks if a computed hash is equal to the provided root. 
***






    



