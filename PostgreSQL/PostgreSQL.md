# [PostgreSQL](https://training.enterprisedb.com/learn/lp/19/open-source-postgresql-learning-plan-v16)

### Content Index:
- [System Architecture](#system-architecture-1)

## 1) System Architecture:
<img width="941" alt="Screenshot 2024-01-06 at 11 32 52 AM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/830c0ed2-5616-4cb7-9961-2c909d68fccf">

- Postgres uses processes, not threads(a larger process which has smaller processes running)
  - The postmaster process acts as a supervisor
    - Several utility processes perform background work (postmaster starts them, restarts them if they die)
    - One backend process per user session (postmaster listens for new connections)
   
<img width="896" alt="Screenshot 2024-01-06 at 10 07 57 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/1a20168c-ce03-44fb-a08d-f3641948466e">

<br><br>

> Understanding Postgres architecture using House architecture.
> Each instance has a different directory and port number like the kids IP number and room number

<br>

<img width="377" alt="Screenshot 2024-01-06 at 10 12 38 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/00d8bf71-24a9-4982-9b53-0b97a2c147d8">

<img width="381" alt="Screenshot 2024-01-06 at 10 13 04 PM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/ca662f75-802f-4b96-bb40-490dd819762c">



### Terminologies:

| Industry Term     | Postgres Term          | Definition                                               |
|-------------------|------------------------|----------------------------------------------------------|
| Table or Index    | Table                  | A structured collection of data organized into rows and columns. |
| Relation          | Table                  | In the context of databases, a relation is a table.       |
| Row               | Tuple                  | A single record or data entry in a table.                |
| Tuple             | Row                    | Synonymous with a row; represents a single record.       |
| Column            | Attribute              | A vertical entity in a table that represents a specific property of data. |
| Attribute         | Column                 | Synonymous with a column; represents a specific property of data. |
| Data Block        | Page (on disk)         | A block of data at the storage level, often related to disk storage. |
| Page (on disk)    | Page                   | A unit of data storage on disk or other storage media.    |
| Page             | Buffer (in memory)     | A unit of data storage in memory, often related to caching.|
| Buffer (in memory)| Buffer                 | A temporary storage area in memory used for fast access to frequently accessed data.|
