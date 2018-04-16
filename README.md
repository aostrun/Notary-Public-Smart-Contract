# Notary Public Smart Contract
Smart Contract serving as Notary Public

----------------------------------------------------------------------------
    Author: Andrijan Ostrun
            April, 2018.
            github.com/aostrun
----------------------------------------------------------------------------         


Smart Contract serving as Notary Public where you can protect an document 
or a file in general by storing it's hash value on the Ethereum blockchain.

Every record besides file hash has parties associated with the record (can be 
any number of parties) which can come handy if you are using this as a medium 
to store real contracts.

Every party associated with the record has to **accept** it before the record becomes
**valid**. This stands as a protection for all parties involved.

## Record Creation
**Creation of new record starts with providing:**
  * Hash value of the file that is being protected (uint256)
  * Parties associated with the record (address[])
  * Unix Timestamp for record expiration (uint256) 
    * current timestamp can be found at: https://www.unixtimestamp.com/

  * Creation of the record returns unique record ID that has to be remembered by parties
        if they want to access that record ever again.

Example of record creation:


    `createRecord(2142131241, ["address#1", "address#2", "address#3"], 2523910141)`


Parties accept record by calling function *acceptRecord* from their address. 
Function takes record ID as an argument.

## Record Verification
File can be verified by calling *verify* function. Function can be called only from
address that is party on particulat record. Function takes record ID and hash value that
we want to verify as arguments and returns boolean value, true if provided hash value
matches one on the record.

## Record Validity
**Record is valid if:**
 * timestamp *validUntil* is greater than current timestamp (time aspect)
 * all parties **accepted** the record (party aspect)
