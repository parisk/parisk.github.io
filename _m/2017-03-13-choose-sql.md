---
layout: post
title: Choose SQL
medium_url: https://stateofprogress.blog/choose-sql-d017cfc08870
---

Let’s get straight to the point; **choose an SQL database for your web application**. I think I can’t make my self clearer.

Again; don’t go with a NoSQL, key-value, distributed-whatever-data-store as the main database for your application. You will regret it — as we did with [SourceLair](https://www.sourcelair.com/home) — I promise.

Now, let’s deconstruct my statement and explain why choosing a NoSQL data store as the database of your web application is the wrong choice, while the typical boring SQL is the right one.

### The wrong reasons to choose NoSQL

What is worse than just using a NoSQL data store as your database, is doing it for the wrong reasons, because this implies superficial understanding of this choice.

The main wrong reasons I see people choosing NoSQL, instead of a typical SQL DBMS are the following.

#### It’s easier for programmers

The typical example you will see that compares the easiness of use of each NoSQL solution vs SQL is how you write a document into the data store vs. how you write a new database record with `INSERT`. And indeed writing a raw JSON object straight to a data store is easier than an `INSERT` SQL query.

And this is where all that “it’s easier for programmers” fuss stops.

Now, let’s compare for example how you can fetch the users that signed up for an example application within the last 24 hours using:

**MySQL**

```sql
SELECT  *
FROM    users
WHERE   signup_time >= CURDATE() - INTERVAL 1 DAY
```

vs. **Mongo**

```javascript
db.users.find({
  "signup_time": {
    $gt: new Date(Date.now() - 24*60*60 * 1000)
  }
})
```

In the first case there is a language using words that humans use to talk to each other, while in the second one there is pure JavaScript, where you have to build your query using a JSON object and even convert the 24 hours to milliseconds on your own.

**It’s not over!** The funniest part is when you want to ask your database to provide you with something like all users that signed up last week and also have signed in my website at least two times.

While a simple relational query like this just cannot be expressed directly in a NoSQL data store, it can be expressed in a single SQL (or [pure ORM](https://docs.djangoproject.com/en/1.10/topics/db/aggregation/#following-relationships-backwards)) query. To do this in NoSQL you have to rely either on [denormalization](https://en.wikipedia.org/wiki/Denormalization) (keeping aggregated data stored in it’s own field, rather than calculating them on demand) or the [fucking map-reduce](https://en.wikipedia.org/wiki/MapReduce) everyone used to go crazy about.

Do not forget also that nowadays SQL has been pulled to the background thanks to dead-easy and super secure ORMs (e.g. [Django’s built-in ORM](https://docs.djangoproject.com/en/1.10/topics/db/) and [Rails’ Active Record](http://guides.rubyonrails.org/active_record_basics.html)), which let you avoid SQL completely in most cases ([even when altering your tables](https://docs.djangoproject.com/en/1.10/topics/migrations/)).

And no, if you are building a web application nowadays you won’t avoid to use something like an ORM, even with NoSQL, since [there](https://github.com/MongoEngine/mongoengine) [are](https://github.com/couchbaselabs/node-ottoman) [tons](https://github.com/mongodb/pymodm) [of](https://github.com/mongodb/mongoid) [“ODMs”](https://github.com/Automattic/mongoose) [out](https://github.com/mongodb/morphia) [there](https://docs.phalconphp.com/en/latest/reference/odm.html) promoting usage of a language-native object model instead of pure JSON.

#### It scales better

OK this is a sneaky trap, as it breaks down in two false assumptions:

1. Scaling is actually a problem for you
2. NoSQL scales better than existing SQL solutions

First, scaling is not and most probably won’t be your problem. Unless you start having a few thousand of queries per second and terrabytes of data in your database, this won’t be a problem at all. And in case it does, you can go with a fully managed solution like [AWS’ RDS](https://aws.amazon.com/rds).

Second, no; NoSQL does not scale better than SQL. At least not in the manner you think. MySQL is being used from top-traffic websites like Facebook and Twitter, to high traffic websites like GitHub and Basecamp and almost every PHP installation out there. If this is not scaling, then what is it?

#### It writes faster

In general that’s true, but is “fast writes” what your application needs? Unless you aim to run a logging service or something like that chances are that your web application is like most out there:

A person puts content to be consumed by other people.

This is how Facebook, Twitter, YouTube, blogs, e-shops, file sharing services, and the vast majority of the web work. Chances are your application is not an exception.

This is where all the “wrong reasons to choose NoSQL” thing stops. It’s quite sad that one of the main sources of the NoSQL > SQL claim comes [straight from MongoDB’s website](https://www.mongodb.com/compare/mongodb-mysql#feature-comparison), because I am pretty sure that it has played a vital role in this delusion.

### The right reasons to choose an SQL database

Exposing the down parts of NoSQL is not enough. Every kind of technology has it’s pros and cons and now we will see why SQL is the right choice for almost every web application out there.

#### The ecosystem
You simply cannot beat the ecosystem of SQL. SQL is a language that exists since 1974. This is more than 40 fucking years of existence. It’s only natural that options you have for SQL people, tools and services are enormous.
SQL is being taught in every computer science school across the world. You can find SQL software from mature pieces like [PHPMyAdmin](https://www.phpmyadmin.net/) and [SQLAlchemy](http://www.sqlalchemy.org/) to more bleeding edge pieces like the [Pony ORM](https://ponyorm.com/). And don’t forget that all cloud provider’s nowadays provide SQL databases as a service that you can use with zero effort (e.g. [Amazon RDS](https://aws.amazon.com/rds/), [Google Cloud SQL](https://cloud.google.com/sql/) and [Azure SQL Database](https://azure.microsoft.com/en-gb/services/sql-database/)).

This might not sound quite important but the progress and evolution of software has strong foundation on not reinventing the wheel and using solutions provided by others to solve common problems.

#### Transactions and ACID compliance

SQL offers something that all people responsible for web applications running in production crave about; peace of mind about their data.

That’s because almost every SQL solution in the market lets you group multiple SQL queries into [ACID](https://en.wikipedia.org/wiki/ACID) compliant units of work called **transactions**.

In practice, this means that you can perform multiple changes in your database grouped into a single *transaction*, which you can *commit* and *rollback*, while being guaranteed about your transaction’s [**Atomicity**](https://en.wikipedia.org/wiki/Atomicity_%28database_systems%29), [**Consistency**](https://en.wikipedia.org/wiki/Consistency_%28database_systems%29), [**Isolation**](https://en.wikipedia.org/wiki/Isolation_%28database_systems%29) and [**Durability**](https://en.wikipedia.org/wiki/Durability_%28database_systems%29).

In simple words; **with SQL you can be 100% certain that either your exact intent gets reflected in the database or nothing happens at all**.

#### Storage

Another important “feature” of SQL database systems that is super important for production applications is that it saves you hell of a storage.

This feature comes for free because SQL needs a predefined table structure (schema) to store data in it. This allows storing only the contents of each row’s columns on the disk. On the contrary, with NoSQL solutions you have to store the whole document (all keys and all values) on the disk, since there is not predefined structure of the *documents* stored in each *collection*.

As your data set grows this issue gets even bigger as you can easily have many GBs of NoSQL data, which could be easily **less than half**, if you used an SQL database system.

### Conclusion

This article is not a rant against NoSQL data stores. Most famous NoSQL data stores in the market are great solutions that are being used also by almost every production web application out there.

[Redis](https://redis.io/) is possibly one of the very few NoSQL data stores that has not attempted to claim any space from SQL databases and this is why it is thriving big fucking time in it’s space with universal acclaim.

This article is against using NoSQL as panacea to our data storing problems, because of their “simple” look and attempting to replace established, mature solutions that already suit the needs of our job, with them.

---

🆓 **BONUS**: If you really need to store unstructured data into your database, this does not mean you have to go with a NoSQL data store. Take a look at [MySQL’s JSON data type](https://dev.mysql.com/doc/refman/5.7/en/json.html), [Postgres’ JSON types](https://www.postgresql.org/docs/9.6/static/datatype-json.html) and [SQLite’s JSON extension](https://www.sqlite.org/json1.html).