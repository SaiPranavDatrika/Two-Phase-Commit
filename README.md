# Two-Phase-Commit
The two-phase commit protocol breaks a database commit into two phases to ensure correctness and fault tolerance in a distributed database system.

The protocol
Consider a transaction coordinator that manages the commits to database stores. As the name suggests, the entire process is divided into two phases:

#Prepare phase

After each database store (slave) has locally completed its transaction, it sends a “DONE” message to the transaction coordinator. Once the coordinator receives this message from all the slaves, it sends them a “PREPARE” message.
Each slave responds to the “PREPARE” message by sending a “READY” message back to the coordinator.
If a slave responds with a “NOT READY” message or does not respond at all, then the coordinator sends a global “ABORT” message to all the other slaves. Only upon receiving an acknowledgment from all the slaves that the transaction has been aborted does the coordinator consider the entire transaction aborted.

#Commit phase

Once the transaction coordinator has received the “READY” message from all the slaves, it sends a “COMMIT” message to all of them, which ​contains the details of the transaction that needs to be stored in the databases.
Each slave applies the transaction and returns a “DONE” acknowledgment message back to the coordinator.
The coordinator considers the entire transaction to be completed once it receives​ a “DONE” message from all the slaves.

I have written this code in TLA+, which is designed by Leslie Lamport.
