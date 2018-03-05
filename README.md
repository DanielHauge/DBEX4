# DBEX4





### 
```
CREATE TABLE Users(
uname VARCHAR PRIMARY KEY,
nickname VARCHAR,
bio VARCHAR,
following BIGINT,
follwers BIGINT,
);
```

```
CREATE TABLE Country(
CountryID INTEGER PRIMARY KEY,
Country VARCHAR
);
```


```
CREATE TABLE Location(
LocationID INTEGER PRIMARY KEY
place VARCHAR NULLABLE,
CountryID INTEGER REFERECES Country(CountryID),
latitude DOUBLE PRECISION,
longitude DOUBLE PRECISION,
);
```

```
CREATE TABLE Language(
LangID INTEGER PRIMARY KEY,
Language VARCHAR
```

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
