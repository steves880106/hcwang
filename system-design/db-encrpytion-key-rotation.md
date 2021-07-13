

## Problem Statement
1. There are billion of records with PHI/PII stored in the mongoDB
2. Data encyption key haven't been changed for 5 years. The key is also the same as Transit Encryption Key.
3. Migrate to Vault as Encryption-as-a-Service <-   A new way to retrived the Encryption key
## Requirement
- Billion of documents in MongoDB collections are re-encrypted
- A system able to re encrypt billions of PII/PHI without sacrificing the performance of service in terms of latency.
- The process need to be fault-tolerant without risks of losing any data
- Test Plan
  - Correctness
  - Performance


## Scale
How many daily active users?
- 50 millions member
- Active user: 2 millions user 

How many write operations per sec?
- Every user takes a quiz/survey once a day in the form of chat / feedback UI / form ...
- In every survey / quiz, on average, we can collect 5 responses.
- How much data are there in the DB?
5 * 2000000 * 12 * 30 * 5  = 18 billions records 
How soon do we want to accomplish the key rotation?
In a month
Re-encrypt 29761 records per second

## Note

Why not just write a migrator to re-encrypt all of the data?
- Database load: write will be on primary mongodb replica.
- We have migrator for smaller data, but it is not run in an async way and it will generate blocking thread which affect services performance
- Difficult to distributed the work to different instances of the service
- A cursor style implementation works but doesn't have good resumption mechanics.

## Solution
- Create a new chronos job to execute this process and provide retry mechanism.
- Create a streaming implementation that will allow you to throttle the amount of work being performed.
  - The metadata prepended to each individual encrypted record can be inspected to determine if the record has been re-encrypted or not .
- Message passing leveraging RabbitMQ.
- Producer/Consumer implementation using Akka Actors
- Retry/Reconciliation mechanism for message resend



Why not just make a replica of DB and do key rotation there?



## Issues
1. Bad Data
2. Distribute Retry
3. Single Insert v.s. Bulk Write
4. Reencrypt data lazily or proactively?


## Data Model

JobStatus Sample Document

{
   "_id" : ObjectId,
   "collectionName" : String,
   "batchSize" : Long,    // Indicates the number of docs in batch sent over catbus.
   "consumerProcessed" : Long, // Indicates number processed successfully by re-encryption consumer
   "startId" : ObjectId,  // Indicates the start  identifier of the batch processed.
   "endId" : ObjectId, // Indicates the end identifier of the batch processed.
   "isComplete" : Boolean,  //Indicates completion of the batch.
   "creationTimeStamp" : DateTime
}



Catbus Message Format (Contract between batch Producer and Consumer):

SurveyReEncryptionRequested(
   collectionName: String,
   documentIds: Set[String],  //Documents identifiers  which need re-encryption.
   jobStatusId: String,
   isMeta: Boolean = false  //Indicates end of the batch and induces processing of the next batch when set to “true”
 )


case class EncryptionMeta(encryptionVersion: Int, encryptionTimestamp: DateTime)
case class EncryptedSurveyResponse(
  instanceId: String,
  questionId: String,
  date: Long,
  answer: EncryptedSurveyResponseAnswer,
  locale: Option[LocaleWrapper],
  lastUpdateSessionId: Option[String] = None,
  lastUpdateTimestamp: Option[DateTime] = None,
  encryptionMeta: Option[EncryptionMeta] = None,
  dbIdentifier: Option[String] = None //used for retreival of DB generated _id
)


https://cloud.google.com/kms/docs/key-rotation
https://cloud.google.com/kms/docs/re-encrypt-data
https://docs.mongodb.com/manual/core/security-encryption-at-rest/
https://info.townsendsecurity.com/mongodb-encryption-key-management-definitive-guide
