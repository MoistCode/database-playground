# General
1. Not only SQL
2. Dynamic / flexible / non-structured
3. Document-oreiented
4. One document is inside of a collection
   1. First name, last name, email in User collection
   2. First name, middle name, age in User collection
   3. Document is sorta like a row
   4. Key is the field
   5. Value is the value
   6. BSON; binary JSON
5. `mongod` is server
6. `mongo` is how we talk to db
7. If you try to work with something that doesn't exist, it will just create it
   1. `use subscribe` will create db subscribe
   2. ```
        db.users.insertOne({
          name: "Amy",
          age: "23",
          status: "A",
          groups: ["editor", "manager"]
        });
      ```