---
layout: post
title: Sqlalchemy hidden bug
categories: python
tags: python, orm, sqlalchemy, sql
date: 2023-08-30 11:01 +0100
excerpt: Wierd bug
---
I was working with [sqlalchemy](https://www.sqlalchemy.org/). A python orm package. I had a couple of models with relationships. Mostly one - many relationships. Everything was going alright until I met this stubborn bug. It took me hours to figure it out.  

## Replicating bug  

Let's replicate the bug here.  

### Setting up  

1. creat a directory in `/tmp` called `codespace`.  
2. create another directory in `codespace` called `models`. This will contain all our models.  
3. Create a file in models called `__init__.py` with the following content:  

    ```python
    #!/usr/bin/env python
    """Initialize the models package."""

    from sqlalchemy.ext.declarative import declarative_base


    Base = declarative_base()
    ```

4. create a file in `models` called `authors` with the content:  

    ```python
    #!/usr/bin/env python
    """Contains the Author model."""
    from sqlalchemy import Column, Integer, String
    from sqlalchemy.orm import relationship

    from . import Base


    class Author(Base):
        """Represents an author in the authors table"""
        __tablename__ = 'authors'
        id = Column(Integer, primary_key=True, autoincrement=True, nullable=False)
        firstName = Column(String(128), nullable=False)
        lastName = Column(String(128), nullable=False)

        # relationships
        books = relationship('Book', back_populates='author')
    ```
5. create a file in `models` called `books.py` with the following content:  
    ```python
    #!/usr/bin/env python
    """Contains the Book model."""

    from sqlalchemy import Column, String, Integer, ForeignKey
    from sqlalchemy.orm import relationship

    from . import Base


    class Book(Base):
        """Represents a book in the books table."""
        __tablename__ = 'books'
        id = Column(Integer, primary_key=True, autoincrement=True, nullable=False)
        name = Column(String(256), nullable=False)
        authorId = Column(Integer, ForeignKey('authors.id'), nullable=False)

        # relationships
        author = relationship('Author', back_populates='books')
    ```

6. Last file, create the main file `bookStore.py` in the current directory with the following content:  

    ```python
    #!/usr/bin/env python
    """Database for a book store"""

    from os import getenv
    from sqlalchemy import create_engine
    from sqlalchemy.orm import sessionmaker

    from models import Base
    from models import authors, books



    def getSession():
        """Initialize the database and return a session object"""
        # mysql user and password should be stored in environment variable BOOKSTORE_MYSQL_USER and BOOKSTORE_MYSQL_PWD respectively
        url = f"mysql+mysqldb://{getenv('BOOKSTORE_MYSQL_USER')}:{getenv('BOOKSTORE_MYSQL_PWD')}@localhost/bookstore"
        engine = create_engine(url, pool_pre_ping=True)
        Base.metadata.create_all(engine)
        Session = sessionmaker(bind=engine, expire_on_commit=False)
        session = Session()
        return session
    ```

7. create the database for our book store in mysql:  

    ```bash
    3:09 PM⌚arfs6 in codespace
    $ mysql -u arfs6 -p
    Enter password: 
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 13
    Server version: 8.0.33-0ubuntu0.20.04.2 (Ubuntu)

    Copyright (c) 2000, 2023, Oracle and/or its affiliates.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

    mysql> CREATE DATABASE IF NOT EXISTS bookstore;
    Query OK, 1 row affected (0.71 sec)

    mysql> 
    ```

    8. Set the `BOOKSTORE_MYSQL_USER`, and `BOOKSTORE_MYSQL_PWD` to your mysql username and password respectively. This will be used by `bookStore.py` to create the database engine.  

### Testing  

```python
3:35 PM⌚arfs6 in codespace
$ python -i bookStore.py 
>>> from models.authors import Author
>>> s = getSession()
>>> a = Author()
>>> a.firstName = 'Abdulqadir'
>>> a.lastName = 'Ahmad'
>>> s.add(a)
>>> a.id
>>> s.commit()
>>> a.id
1
>>>     
```

The Author class seems to be working, let's test the Book class.

```python
>>> from models.books import Book
>>> b = Book()
>>> b.name = 'The wierd sqlalchemy bug'
>>> b.authorId = a.id
>>> s.add(b)
>>> s.commit()
>>> b.id
1
>>> storedB = s.query(Book).all()
>>> len(storedB)
1
>>> storedB[0].id == b.id
True
>>> storedA = s.query(Author).all()
>>> len(storedA)
1
>>> storedA[0].id == storedB[0].authorId
True
>>> 
```
