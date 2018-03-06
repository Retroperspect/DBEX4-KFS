# DBEX4-KFS
> by Kristian Flejsborg Sørensen (cph-kf96)

## intro
this is the handin assignment that was descriped in [this](https://github.com/datsoftlyngby/soft2018spring-databases-teaching-material/blob/master/lecture_notes/07-DBMSs%20and%20normal%20forms.ipynb) slide.
the full table have been cut up into smaller bits to follow the third normal forms requirements.
## Tweets table
The first table tweets have been reduced to only describe the attributes that's unrelated to the other tables, while keeping references to the other tables, note two new id's have been introduced called LangID and LocationID.
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
## Users table
the User is defined with ther uname attribute which is essentially a unique value that can be used as the primary key, all other attributes don't describe the other so third normal form is maintained.
```
CREATE TABLE Users(
uname VARCHAR PRIMARY KEY,
nickname VARCHAR,
bio VARCHAR,
following BIGINT,
follwers BIGINT,
);
```
## Language table
it was chosen to have a identification, while allowing different entries of a language, say british english and american english.
```
CREATE TABLE Language(
LangID INTEGER PRIMARY KEY,
Language VARCHAR
);
```
## Location table
there can be multiple tweets from the same position, but there can only be 1 of each position was the logic for having this table be reference from and not too with the tweets table.
```
CREATE TABLE Location(
LocationID INTEGER PRIMARY KEY
place VARCHAR NULLABLE,
CountryID INTEGER REFERECES Country(CountryID),
latitude DOUBLE PRECISION,
longitude DOUBLE PRECISION,
);
```
## Country
it was chosen to introduce a table of countries, to reduce redundancy in the Location table.
```
CREATE TABLE Country(
CountryID INTEGER PRIMARY KEY,
Country VARCHAR
);
```
