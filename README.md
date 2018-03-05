# Database exercise 4 (SQL Introduction & 3 normal forms)
This repository is a exercise project for Software development (PBA) Database course. Daniel (cph-dh136)

## Description
This exercise is to introduce SQL and how to get datastructure into 3rd normal form. The exercise requires to make tables from pre-existing example, that is in 3rd normal form.

The exercise can be found in the buttom of this ressource: [Here](https://github.com/datsoftlyngby/soft2018spring-databases-teaching-material/blob/master/lecture_notes/07-DBMSs%20and%20normal%20forms.ipynb)


## Assignment
Below can be seen the tables which has been split up and done with to get the example table into 3rd normal form. To greatly reduce redundancy, and amount of data needed to store.

- Users table. This greatly reduces redundancy, example. Bio doesn't need to go in every single tweet. etc.
```
CREATE TABLE Users(
uname VARCHAR PRIMARY KEY,
nickname VARCHAR,
bio VARCHAR,
following BIGINT,
follwers BIGINT,
);
```

- Country table. Holds all country names and assigns an id. (This means, country only is one place and can therefor be easily changed with one execution. The reference can stay the same)
```
CREATE TABLE Country(
CountryID INTEGER PRIMARY KEY,
Country VARCHAR
);
```

- Location table. This allows for a tweet to use a pre-existing location as reference, without having to redudantly put all the information in again.
```
CREATE TABLE Location(
LocationID INTEGER PRIMARY KEY
place VARCHAR NULLABLE,
CountryID INTEGER REFERECES Country(CountryID),
latitude DOUBLE PRECISION,
longitude DOUBLE PRECISION,
);
```

- Language table. Same as with coutnry. (Maybe little bit less relevant, what is the chances you want to change language and country on all. Only in case of a misspelling, but what are the chances of that?).
```
CREATE TABLE Language(
LangID INTEGER PRIMARY KEY,
Language VARCHAR
```

- Tweets table. The main table that reference other tables.
```
CREATE TABLE Tweets(
ID INTEGER PRIMARY KEY,
url VARCHAR UNIQUE,
uname VARCHAR REFERECES Users(uname),
LangID INTEGER REFERECES Language(LangID)
rts BIGINT,
favs BIGINT,
listed NULLABLE,
date DATE,
hour TIME,
message VARCHAR,
picture VARCHAR NULLABLE,
LocationID REFERECES Location(LocationID)
);
```
