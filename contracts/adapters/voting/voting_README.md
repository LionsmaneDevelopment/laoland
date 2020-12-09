<strong>OffchainVotingContract.sol</strong> 


Inherits from:

    IVoting: (Voting interface)

    DaoConstants: (Stores constants, (hashes of name strings and important addresses))

    MemberGuard: (Modifiers that only allow members to interact with a function)

    AdapterGuard: (Modifiers that allow only verified Adapters to interact with a function)

***

<strong>Function Spec</strong>

    function configureDao

Allows for the modification of voting the votingPeriod, grave period and fallback threshold.

    function submitVoteResult

Used to pass a an off-chain voting result to __submitVoteResult, checks that the vote is passed as a majority and the grace period must have ended 
Otherwise checks if a vote override is valid to pass to _submitVoteResult


    function _readyToSubmitResult

Internal function that returns a bool when a result is ready to submit based on the vote counts provided. 

    function _submitVoteResult  

Processes the logic and checks for submitting a voting result. Checks if the node result merkle root match and that the result weight is correct before 
processing the input and changing the vote struct. The sender will have his stake locked after processing this function. 

    function _lockFunds 

Locks loot according to dao.getConfiguration(StakingAmount). Checks if the lockee is an active member and has enough loot to lock. 

    function _releaseFunds

Releases locked loot from a members balance. Checks they have adequate locked loot and they are an active member. 

    startNewVotingForProposal

Adapter only function that sets the start tine and start block for a particular proposal in a particular doa in the votes mapping by changing the respective voting struct 
start time and blocknumber attributes. 

    function voteResult

Function which returns an int representing of the state of the vote; 

0: has not started

1: tie

2: pass

3: not pass

4: in progress

    function challengeWrongSignature

    



