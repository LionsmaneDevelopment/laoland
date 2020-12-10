TAGS 

(HELPER) x() x() is a helper used by the above function 

(PARENT) x() x() uses this function as a helper 

(SETTER) x() x() is a setter function used within this function 



<strong>OffchainVotingContract.sol</strong> 


Inherits from:

    IVoting: (Voting interface)

    DaoConstants: (Stores constants, (hashes of name strings and important addresses))

    MemberGuard: (Modifiers that only allow members to interact with a function)

    AdapterGuard: (Modifiers that allow only verified Adapters to interact with a function)

***

<strong>Function Spec</strong>

    function configureDao



Allows for the modification of voting, allows the changing of the votingPeriod, grave period and fallback threshold.

(SETTER) = Changes are passed to <strong>dao.setConfiguration</strong> to actually set the changes. 

***
    function submitVoteResult



Used to pass a an off-chain voting result to __submitVoteResult, checks that the vote is passed as a majority and the grace period must have ended 
Otherwise checks if a vote override is valid to pass to _submitVoteResult

(MODIFIER/CHECKER) = _readyToSubmitResult: Is used to check if a result is in a state that is submittable

(SETTER) = _submitVoteResult: Is the setter that submits the actual vote result. 


***

    function _readyToSubmitResult



Internal function that returns a bool when a result is ready to submit based on the vote counts provided. 

(PARENT) = submitVoteResult (is a helper for this function)
***
    function _submitVoteResult  

Processes the logic and checks for submitting a voting result. Checks if the node result merkle root match and that the result weight is correct before 
processing the input and changing the vote struct. The sender will have his stake locked after processing this function. 

(PARENT)= submitVoteResult (is a setter for this function)

(HELPER) = _lockFunds: The above function has _lockFunds() as a helper function
***
    function _lockFunds 

Locks loot according to dao.getConfiguration(StakingAmount). Checks if the lockee is an active member and has enough loot to lock. 

(PARENT) = _submitVoteResult: Is a helper to this function.
***
    function _releaseFunds

Releases locked loot from a members balance. Checks they have adequate locked loot and they are an active member. 

(UNUSED) - This is an unused function currently, TODO: Back it into some other function/feature.

(HELPER) - isActiveMember() Checks if a someone is an active member, is a helper to the above function 

(HELPER) - balanceOf() Returns the balance of a particular member in a particular dao. Is a helper function to the above function. 

(SETTER) = dao.addToBalance: This function acts as a setter and does the actual balance adjustment

(SETTER) = dao.subtractFromBalance: This function acts as a setter and does the actual balance adjustment
***
    startNewVotingForProposal

Adapter only function that sets the start tine and start block for a particular proposal in a particular doa in the votes mapping by changing the respective voting struct 
start time and blocknumber attributes. This function acts as its own setter. 

(MODIFIER) = onlyAdapter() Modifier that only allows adapters to call this function. 


***
    function voteResult

Function which returns an int representing of the state of the vote; 

0: has not started

1: tie

2: pass

3: not pass

4: in progress

(HELPER) = getConfiguration() Function that returns a value (Grace Period, Voting Period etc.) of the current voting configuration. 
***
    function challengeWrongSignature

(HELPER) - verify() 

(HELPER) - _hasVoted()

(SETTER) - _challengeResult()

Checks if the challenger is part of the voting result and then builds the hash of a yes and no vote and challenges the result if the vote signature is incorrect for both.
***
    function challengeWrongWeight

Calls _challenge_result if the onchain snapshot weight is not equal to node's current weight. If so, the result is challenged and the reporter slashed.  

(HELPER) - _nodeHash() Returns the hash of a nodes attributes 

(HELPER) - getPriorAmount() 

(SETTER) - _challengeResult() 

***
    function challengeDuplicate

Checks if two nodes that are part of the merkle tree have the same voter address. If so, the result is challenged (_challengeResult())

(HELPER) _nodeHash() Returns the hash of a nodes attributes 

(HELPER) verify() VChecks if a hash is equal to its computed root 

(SETTER) _challengeResult() Sets the results state to challenged 

***
    function challengeWrongStep

This function is used to challenge a result is a step is incorrect. It checks if the data input is in fact from two consecutive nodes, if a result has been reported (in grace period) and that the proof checks for the nodes are valid. 

(HELPER) - _nodeHash() Returns the hash of a nodes attributes 

(HELPER) - verify() Checks if a hash is equal to its computed root

(HELPER) - _checkStep() Does further checks to determine is a step is incorrect and then challenges the voting result 

(SETTER) - _challengeResult() Sets the results state to challenged 
***
    requestFallback

Allows a voter to add their vote to the request_fallback tally, if enough members vote for it then on-chain voting will be used as an alternative. This function 
acts as its own setter. 


***
    function _nodeHash

This function returns the hash of all of a nodes properties (32bit)

(PARENT) _nodeHash is a helper function to all challenges functions, used widely across contract.

***
    function _checkStep

If a  challengeWrongStep is called successfully this is used to check that the reported voting statistics were incorrect and call _challengeResult(). 

(HELPER) -  _hasVotedYes() Checks if a user has voted yes on a proposal 

(HELPER) - hasVotesNo() Checks if a user has voted no on a proposal

(SETTER) - _challengeResult() Setts the results state to challenged 

***
    function _challengeResult

After a result is successfully challenged this function sets the state of the proposal to challenged and lock the loot (slashes) of the vote reporter. 

(PARENT) - _challengeResult is a setter for all challenge functions. 
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






    



