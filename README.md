# Repository Note:
This repositoy was formed from work done for within a course directory. To have this simulator project listed indpependently I had a new repository created, so the full commit history is not visible.


## Overview of distributed system:

In the distributed system, the users serve as the clients, in which they use the bank for their individual inquiries. The bank serves as the server as it simultaneously addresses the requests of individual clients, using separate threads. The users communicate to the bank their queries of paying a loan or depositing money, which is processed as an individual thread with the bank, which holds their shared state which is all the users’ bank accounts.

## Descriptions of the synchronization mechanisms used:

Used synchronization methods include the use of a mutex lock. In server.py, account[‘lock’] is used to ensure only one process at a time can write or access individual resources, like when the amounts of money are being modified. 

Additionally “with” in python is used alongside the account[‘lock’] to automatically acquire it and release it after the indented lines of code.

When two accounts need to have resources changed for an individual process, they are sorted by account number in order to be locked in a consistent order. This prevents deadlock issues where two different processes may try to lock two account’s locks in a way where the order interferes with unlocking.


## Discussion of challenges faced, how they were overcame:

There was a challenge of negative values not being recognized during development. So I had to go back and change the client.py function to allow support for negative values. There was also an issue of the  function pay_loan_check, where there is a conditional that checks if the type of an account is a loan account, but it didn’t address the opposite case where it was not, so the code would run indefinitely. So in response I had to go back to the code and think of a conditional check that meant the same, but covered the other case. I also had an issue of running the bash scripts, as initially I'd get an error message, but switching back to the user helped me solve this.

## An analysis of the system’s performance and potential areas for improvement

The system could run individual commands very well. All individual commands in the codingHints document were tested to work and account for the various cases. It was good that 50 thread connections were able to be run simultaneously. After run_bank.py the logs showed the balances were consistent across threads. Maybe areas for improvement could be more detailed error messages. Maybe I could include the value that is negative or the number of accounts that does not exist in the error message. I also think professional banking systems would have more verification for users, like a password, so that could be added.
