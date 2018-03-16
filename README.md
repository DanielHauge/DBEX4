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
nickname VARCHAR NOT NULL,
bio VARCHAR NOT NULL,
following BIGINT NOT NULL,
follwers BIGINT NOT NULL
);
```

- Country table. Holds all country names and assigns an id. (This means, country only is one place and can therefor be easily changed with one execution. The reference can stay the same)
```
CREATE TABLE Country(
CountryID INTEGER PRIMARY KEY,
Country VARCHAR NOT NULL
);
```

- Location table. This allows for a tweet to use a pre-existing location as reference, without having to redudantly put all the information in again.
```
CREATE TABLE Location(
LocationID INTEGER PRIMARY KEY,
place VARCHAR,
CountryID INTEGER REFERENCES Country(CountryID),
latitude DOUBLE PRECISION NOT NULL,
longitude DOUBLE PRECISION NOT NULL
);
```

- Language table. Same as with coutnry. (Maybe little bit less relevant, what is the chances you want to change language and country on all. Only in case of a misspelling, but what are the chances of that?).
```
CREATE TABLE Language(
LangID INTEGER PRIMARY KEY,
Language VARCHAR NOT NULL
);
```

- Tweets table. The main table that reference other tables.
```
CREATE TABLE Tweets(
ID INTEGER PRIMARY KEY,
url VARCHAR UNIQUE,
uname VARCHAR REFERENCES Users(uname),
LangID INTEGER REFERENCES Language(LangID),
rts BIGINT NOT NULL,
favs BIGINT NOT NULL,
listed BIGINT,
date DATE NOT NULL,
hour TIME NOT NULL,
message VARCHAR NOT NULL,
picture VARCHAR,
LocationID INTEGER REFERENCES Location(LocationID)
);
```

[![https://gyazo.com/01bf21e1436ba19e4b1e194d66add591](https://i.gyazo.com/01bf21e1436ba19e4b1e194d66add591.png)](https://gyazo.com/01bf21e1436ba19e4b1e194d66add591)

### Postgres sql
- Data been used
```
docker run -p 5432:5432 --name data jegp/soft2018-data
```
- To run postgresssql
```
docker run -p 5432:5432 -d -v postgres-data:/var/lib/postgresql/data --name psql postgres:alpine
```
- To access it
```
docker exec -it psql bash
```
- Start sql terminal
```
psql -U postgres
```

- usefull postgress commands
```
\dt : List tables
\d [name] : describes the structure of a table
