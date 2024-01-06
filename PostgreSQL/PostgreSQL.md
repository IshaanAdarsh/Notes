# [PostgreSQL](https://training.enterprisedb.com/learn/lp/19/open-source-postgresql-learning-plan-v16)

## Index:
### [System Architecture](https://github.com/IshaanAdarsh/TIL/blob/main/PostgreSQL/PostgreSQL.md#system-architecture-1)




## System Architecture:
<img width="941" alt="Screenshot 2024-01-06 at 11 32 52 AM" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/830c0ed2-5616-4cb7-9961-2c909d68fccf">

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
