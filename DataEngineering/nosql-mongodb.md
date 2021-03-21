# NoSQL and MongoDB 📄

## Overview
### You Will Learn
In this section you will learn:
1. What NoSQL is and the differences between NoSQL and SQL
2. What MongoDB is
3. How to set up a MongoDB account
4. How to query data in MongoDB

### Prerequisites
None

### Introduction

In this section we're going to be chatting about some alternative forms of data storage. Don't worry if that sounds complicated, though, that's just a fancy way to say "databases other than SQL"! This section is going to cover MongoDB, which is a NoSQL database. What is "NoSQL," you ask? Well, you've come to the right place, because we're going to explain what that is too!

*Note: We'll be mainly covering how to query data that is already present in the database. To learn more about inputting and manipulating data, please refer to the [documentation](https://docs.mongodb.com/), there is a wealth of knowledge here!*

## What is NoSQL? 🗃

MongoDB is a NoSQL database, so before talking about MongoDB, it's important to understand what NoSQL is. Let's dive into that, shall we?

### An SQL Refresher 💨

You may already know a bit about SQL and what it is (if not, then you might find the [SQL section](SQLBeginner.md) to be helpful). In a nutshell, SQL stands for "Structured Query Language" and SQL databases are just that -- structured. Heavily structured. All the data is organized into tables, and all the tables have to conform to some schema. A schema is essentially an outline that defines how a database will organize its data. There are some huge benefits from this, but it also makes application development a bit difficult.

### SQL Pains 🤒

The strictness of SQL schemas is great when you know exactly what you're trying to build. You can easily define a schema that will hold all the data that your app will need. But problems start to creep up when the exact form of your app's data isn't set in stone. This happens a lot with startups or proof-of-concept projects. Sometimes the exact schema of an application's data isn't known.

As a rudimentary example, let's think about a university. In order to maintain a database of all the students, it would need to keep track of the following student information:

- Name
- Birthdate
- Home address

Now imagine that this information was used to design the schema for the student database 20 years ago. That would have worked fine back then, but in the past 20 years or so, email has become an important tool for students. In fact, email has become so important that every student needs a school-provided email address and the university needs to keep track of it in the student database. Because of rigid schemas, making these sort of changes in SQL databases are painful and difficult. Eventually, it became clear that a new solution was needed.

### NoSQL to the Rescue! 🚒

So we've talked about SQL and why it can be hard to work with sometimes. And that means the stage has been set for understanding what NoSQL is! Essentially, A NoSQL Database is any database that doesn't follow the same form as an SQL one (i.e. tables). Pretty broad, right?! There are many types of NoSQL Databases, here are a few examples:

- Graph Databases
- Key-Value Databases
- Document Databases

Today, we're going to be focusing on that last type of NoSQL database: document databases, and we're going to be looking at one specific implementation of it: MongoDB.

The beauty of NoSQL databases is that they are much less strict with their schemas. If the structure of your data is bound to change, then a NoSQL database might be the choice for you! These databases can also become pretty fast, which means they can offer a lot to products trying to use something other than SQL.

Let's dive into MongoDB to see the beauty of NoSQL databases.

*Note: NoSQL doesn't stand for what you (probably) think it stands for. It's easy to look at the name and assume that it means "No SQL," but you'd be mistaken! NoSQL actually stands for "not only SQL." The trust issues are real.*

## MongoDB and Document Basics 🐣

MongoDB is a document oriented database, which is just one of the many types of NoSQL databases out in the wild. A document is an object that holds information as a list of key-value pairs. These values of these pairs can also be nested documents, which means that documents can get very complex very fast. If you know what JSON is, then you can think of it that way; they're very similar.

It's much easier to understand documents when looking at examples, so let's do that! Here's an example document:

```
{
    "name": "Hackster the Bearcat",
    "motto": "Hack and B U"
}
```

This document has three fields, Each field has a name and value. For example, the first field has the name "`name`" and the field "`Hackster the Bearcat`", separated by a "`:`". The name of a field has to be a string, but the value can be almost any data type. Let's take a look:

```
{
    "name": "Junhson",
    "favorite-number": 24,
    "favorite foods": ["Pizza", "Cheeseburgers", "Ice Cream"],
    "favorite-movie": {
        "title": "Black Panther",
        "genre": "Action"
    }
}
```

In the above example, we use an integer as the data type for `"favorite-number"`, an array for `"favorite-foods"`, and another object for `"favorite-movie"`!

Document databases store documents in collections. A collection is simply grouping of documents. Document databases can have multiple collections.

Those are the basics of documents. If you want to know more, check out [MongoDB's documentation](https://docs.mongodb.com/). They have an incredible amount resources, including [MongoDB University](https://university.mongodb.com/), where you can take self-paced courses to master the database for the low price of *free*.

## Query Basics 🐥

Now that we've seen what the data looks like, we need to learn how to actually *query* it. To query data basically means to ask the database for some information. The database returns results based on what you requested.

For the following examples, we're going to define some sample data.

```
database (db): HackBU
collection: orgs (short for "organizers")
data:
{
    "name": "Colin",
    "age": 22,
    "role": "Executive VP",
    "specialty": "The KD Tree",
    "favorite-foods": ["burgers", "crayons"],
    "common-sayings": ["based", "malding", "most dope"]
},
{
    "name": "Junhson",
    "age": 22.5,
    "role": "Organizer",
    "specialty": "Telling awesome puns",
    "favorite-foods": ["pizza", "burgers", "ice cream"],
    "common-sayings": ["bruhh", "nah but yeah", "that's crazy"]

}
```
*Note that this isn't a 100% accurate representation of how MongoDB stores data. It's meant to show the data we're working with (in the following queries) in a (somewhat) easy-to-understand format!*

Let's look at a simple query and understand how it works!

```
// query
db.orgs.find()

// result
{
    "name": "Colin",
    "age": 22,
    "role": "Executive VP",
    "specialty": "The KD Tree",
    "favorite-foods": ["burgers", "crayons"],
    "common-sayings": ["based", "malding", "most dope"]
},
{
    "name": "Junhson",
    "age": 22.5,
    "role": "Organizer",
    "specialty": "Telling awesome puns",
    "favorite-foods": ["pizza", "burgers", "ice cream"],
    "common-sayings": ["bruhh", "nah but yeah", "that's crazy"]

}
```

`db` is MongoDB's way of representing the currently selected database. Since we can have many databases, the chosen one can be referenced by typing `db` as we see above. We'll learn how to select different databases after we set up a database cluster down below!

`orgs` is the name of the collection we've selected. As we discussed earlier, a database can have many collections. `orgs` can be anything as long as there is a collection by that same name! So when we type `db.orgs`, we're referring to our currently selected database and the collection within it that's called  `orgs`.

`find` is a function that we can call on the database. There are parameters that can be passed into it, but if we simply want to return every document, we would just call `find()` with no parameters!

So the above query would return every document within the `orgs` collection!

Here's slightly more complex query:

```
// query
db.orgs.find({"name": "Colin"})

// result
{
    "name": "Colin",
    "age": 22,
    "role": "Executive VP",
    "specialty": "The KD Tree",
    "favorite-foods": ["burgers", "pierogis", "crayons"],
    "common-sayings": ["based", "malding", "most dope"]
}
```

Whenever we're passing information into `find()`, it needs to be in the form of a document. In this case we're looking for organizers named "Colin", so we create the following document: `{"name": "Colin"}`. Based on what we learned about documents above, this document specifies a document with the name "`Colin`." The database will return any document that has "Colin" for its `name` value!

Let's look at another query:

```
// query
db.orgs.find({"age": {$gt: 22}})

// result
{
    "name": "Junhson",
    "age": 22.5,
    "role": "Organizer",
    "specialty": "Telling awesome puns",
    "favorite-foods": ["pizza", "burgers", "ice cream"],
    "common-sayings": ["bruhh", "nah but yeah", "that's crazy"]

}
```

For this query, the database returns all the documents representing organizers who are older than 22 years old. To do this, we pass the following document into the `find()` function:

```
{"age": {$gt: 22}}
```

This document contains a nested document (recall that we mentioned documents are allowed to have documents as values for fields)! The MongoDB Query Language has query operators that make it easy for us to query certain types of data. `$gt` is Mongo's query operator for "greater than." If we use this query operator, the database will return all documents where the "`age`" field has a value greater than the specified value, which is `22` in this case!

We can use MongoDB's query operators to make some very interesting queries! Check out [MongoDB's Query Operator documentation](https://docs.mongodb.com/manual/reference/operator/query/) to learn more about how to use them!

Now that we know a bit about MongoDB, let's set up our own database so we can apply what we've learned!

## Setting Up MongoDB 🍃

There are two primary ways to use MongoDB to store our data. The first option is to download MongoDB and run it on a *server* (in this case, locally on your own computer). The second option is to use MongoDB's service called *Atlas*. MongoDB Atlas is a convenient option for developers looking to focus on their code and not on managing a physical server. Atlas facilitates the management of a running MongoDB on the cloud (using AWS, GCP, or Azure) so that developers don't have to worry about it.

Both options have their pros and cons, but we're going to focus on using Atlas in this workshop. As the tech industry continues to embrace cloud computing, Atlas has continued to become a strong option for MongoDB customers.

*Note: You may be worrying about using Atlas because you don't want to pay to use it, or even input your credit card information. There's good news! Atlas has multiple tiers of the product, each of which are offered at different price points. The lowest price point is called the Free Tier! This tier allows developers to use Atlas on a shared cluster without paying at all. You don't even need to enter any payment information! This is a really great option for learning, building proof-of-concepts, or launching a product that will start with a small data footprint (you can always upgrade whenever you want — or never if you don't want to).*

### MongoDB Atlas 🌍

Here are some simple steps for getting started with MongoDB Atlas!
1. Head over to [MongoDB's Atlas Page](https://www.mongodb.com/cloud/atlas)
2. Choose the option to start for free. You'll be prompted to create an account (don't worry, you won't have to put any payment info). Fill out any account information that they may ask for.
    - If you already have an account, go ahead and log in!
3. You will prompted to choose from some options to create your cluster. The free tier options will be clearly labeled so be sure to pick those. Choose a cloud provider, one of the provider's servers, and select an **M0** cluster. You can then name your cluster and hit the "Create Cluster" button!
4. After doing this, you'll be brought to the dashboard for your cluster! Congrats, this means you have a database ready for you to use! There should be a quick tutorial on the page giving you the inside scoop on how to use the various sections. Feel free to check that out if you'd like! This workshop will also provide instructions on how to use Atlas (*but the more the merrier, right?*).

### Get Your Data On! 📚

So now we have a database cluster, but we have no data to work with. We can easily solve this problem using MongoDB's sample data.

To load the sample data, hit the "..." button on your cluster. This button will be close to the center of the screen, placed nearby the name of your cluster. The resulting menu should have an option to "load sample dataset." Hit that button and the sample data will be loaded in!

### Safe and Secure 🔐

We also need to be sure that our cluster is safe.

1. Head over to the "Network Access" page (the link should be on the left side of the screen, near the other Security pages). Here we can specify IP addresses that will be allowed to access our cluster.

2. Hit "Add IP Address." The resulting menu should allow you to enter some an IP address with a comment. If you know your desired IP address by heart, then feel free to put that in there! Don't fret if you don't remember an IP address by heart, that's not a requirement! There are also options to allow your current IP address and allow access from anywhere. We suggest allowing your current IP address. Allowing access from anywhere puts your cluster at risk of being attacked.

3. We also need to add authorized users to our cluster. Head over to the "Database Access" page (the link should be nearby the "Network Access" link) and select "Add New Database User." Enter a username and password into the form and select your preferred choices for that user's access. Feel free to stick with the default options if you want!

### Let's Get Connected ⛓

We now have a database that is ready to be used! Our final step before making some queries will be to connect to the Database!

1. Nearby the name of your cluster, there will be a button that says "Connect." Hit that button to bring up a menu for connecting to the database! There are 3 options for connecting to our cluster: the mongo shell, connecting an application (i.e. using code), and MongoDB Compass. Today we'll be using the mongodb shell, but if you are interested in the other methods, you can check out the [connection documentation](https://docs.atlas.mongodb.com/connect-to-cluster/#connect-to-a-cluster). All of the offered options are free and really cool! The mongo shell is the simplest and easiest to get started with, so we'll be using that!

2. Once you click on "mongo shell," you'll be provided with instructions for how to install and connect to the mongo shell. Follow these to get set up. If you already have the mongo shell installed, then click on "I have mongo shell installed" and follow those instructions instead. Be sure to replace the <dbname> with the name of your database (the cluster's name). You'll prompted for the password you created earlier!

### Its a *Shell*ebration! 🎊

Now that we're in shell, we're ready to start using some of queries we've learned earlier. The first thing you should do in the shell is type the following:

```
show dbs
```

This will display all the available databases that you have to choose from. Since we've loaded in the sample data, the output should look something like this:

```
MongoDB Enterprise atlas-13ap95-shard-0:PRIMARY> show dbs
admin               0.000GB
local               6.708GB
sample_airbnb       0.051GB
sample_analytics    0.009GB
sample_geospatial   0.001GB
sample_mflix        0.041GB
sample_restaurants  0.006GB
sample_supplies     0.001GB
sample_training     0.040GB
sample_weatherdata  0.002GB
```

Let's choose a database. For this example, we'll select `sample_mflix`, but you can feel free to play around whichever database you want!

Heres how we select the database:

```
use sample_mflix
```

Now that we've selected a database, we need to use `db` to reference it. Let's look at all the available collections in this database:

```
show collections
```

Your output from choosing a database and entering `show collections` should look this this:

```
MongoDB Enterprise atlas-13ap95-shard-0:PRIMARY> use sample_mflix
switched to db sample_mflix
MongoDB Enterprise atlas-13ap95-shard-0:PRIMARY> show collections
comments
movies
sessions
theaters
users
```

At this point, we've chosen a database and we can see all the associated collections. Let's run an example query using the knowledge we've gained from earlier sections:

```
db.users.find().pretty().limit(1)
```

This query is almost the same as the first example query we went over, it just has a few extra functions added onto it. Using the `.pretty()` function (which we call on the results of `find()`), we tell the database to output the results in format that is easy to read. The the `.limit(1)` call, we limit the amount of results returned to 1. This can be very useful if you don't want to flood your screen with the contents of a large collection.

Here's what your output should look like:

```
MongoDB Enterprise atlas-13ap95-shard-0:PRIMARY> db.users.find().pretty().limit(1)
{
	"_id" : ObjectId("59b99db4cfa9a34dcd7885b7"),
	"name" : "Robert Baratheon",
	"email" : "mark_addy@gameofthron.es",
	"password" : "$2b$12$yGqxLG9LZpXA2xVDhuPnSOZd.VURVkz7wgOLY3pnO0s7u2S1ZO32y"
}
```

*Note: Another useful function we can use is `.count()`. This tells the database to return the amount of matching documents instead of all the results! However, using count in the above example wouldn't be necessary since `.limit(1)` already tells us how many results we'll get for this query! See the documentation for other useful querying functions!*

You already know the basics of making queries (from earlier in this section), so go ahead and play around with the database, making queries and looking at the sample data. Feel free to try out the other databases, too!

Let's put your knowledge (and documentation research skills) to the test!

## Exercise: Scavenger Hunt! 🗺

To test out what you've learned in this section here are some questions about the data in the `sample_mflix` database. Use the mongo shell to query the data and find the answers!

- How many users are in the database? How many movies? What about comments and theaters?

- What year did `"The Poor Little Rich Girl"` come out? What genres does the movie fall under?

- Who directed the film `"Lady Windermere's Fan"`?

- How many movies are `30` minutes or less? (hint: the `"runtime"` field has a number X for the value, where X is the movie's runtime in minutes).

- How many movies are longer than `2` hours?

- How many movies fall under the following criteria (*this is a tough one!*):
  - came out between `2005` and `2010`
  - have a "rated" value of `"TV-G"`

- What is the location of `theater #1028`? (hint: use the "theaterID" field)

- Is there a user with the name `"Eggs Mclaren"`? What about the name `"Tommen Baratheon"`?

- How many comments has `"Jason Smith"` written?

- How many users are there in total?

Feel free to answer as many or as little as you want! These answers vary in difficulty, but they were all designed to incorporate the topics covered in this workshop (some have been made hard to stretch your knowledge). Have fun!
