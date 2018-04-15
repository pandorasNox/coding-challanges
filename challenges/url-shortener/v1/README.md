## assumptions
based on [challenge](./CHALLENGE.md)

- no https
- user get's always a hash
- user can't edit the short-link yet
- no lookup for existing "target-url" => adding two times example.com returns two different short-links
- no user-management necessaray => no auth mechanism needed

## decisions
- general
    - use docker
- backend
    - use express
    - use axios
    - use mongoDB
    - use jest
- frontend
    - use react
    - use redux
    - use react-static
    - use jest

### data model
- DB
    - collection: links
        - (string): reference_tag
        - (date): inital_created_at
        - (string): target
        - (date): last_assigned_at
        - (date): last_visit
        - (array): visits
            - (object): visit
                - (date): date
        - history
            - (string): target
            - (date): date
            - (object): change
                - (string): reason

1st
target = example.com
date = 1.1.2000
change = {reason: "inital created/assigned"}

2nd
target = ""
date = 1.1.2000
change = {reason: "discarded bec..."}

3st
target = my.example.com
date = 1.1.2001
change = {reason: "new assigned"}
