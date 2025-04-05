# What is Write-Ahead Logging (WAL) and Why It Is Used Internally in Databases

Write-Ahead Logging (WAL) is a standard method used in many relational databases (like SQLite and PostgreSQL) to ensure data integrity and durability. The core idea behind WAL is simple but powerful: **before any changes are made to the database, those changes are first written to a log file**. This log is then used to redo the transactions in case of a crash or power failure, ensuring that the database can recover to a consistent state.

## Why WAL is Used

1. **Atomicity and Durability**  
   WAL ensures that database changes are atomic and durable. Even if a crash occurs, any committed transactions are preserved.

2. **Faster Writes**  
   Since the log file is written sequentially, it's faster than random-access writes directly to the database. This can boost write performance.

3. **Crash Recovery**  
   On database restart, the system replays the WAL file to ensure all committed transactions are applied, helping recover from unexpected shutdowns.

4. **Concurrency**  
   WAL allows reading and writing to occur simultaneously. While data is being written to the WAL, readers can still access the main database, improving concurrency.

5. **Checkpointing**  
   Periodically, the changes from the WAL file are written to the main database file in a process called checkpointing, ensuring the log file doesn’t grow indefinitely.

## Summary

WAL is a powerful mechanism that increases reliability, performance, and concurrency in database systems. It is especially useful in mobile and embedded databases where power failure or app crashes can occur frequently.
