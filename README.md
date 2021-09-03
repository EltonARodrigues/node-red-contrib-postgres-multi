#NOT READY FOR USE!!

In Development
## node-red-contrib-postgres-multi

A [Node-RED](http://nodered.org) node to query [PostgreSQL](http://www.postgresql.org/), with multiple query support.

Original Project From [node-red-contrib-postgres-multi](https://github.com/BruceFletcher/node-red-contrib-postgres-multi) by BruceFletcher

### Compatibility

This module is designed assuming you will only use this one or Kris' original version in a project, but
not both at the same time. You can replace one with the other in your project and your flows will remain
connected.

* The configuration code is identical, so your database connection configuration should need no changes.
* The output format is identical (assuming equivalent queries)
* The input format is significantly different, and will require updates on any block generating
  queries to be passed to Postgres. (The queries shouldn't change, just the encapsulating data structure.)

### Requirements

This module uses JavaScript features only found in Node versions 12+.

### Install

Run the following command in the root directory of your Node-RED install

    npm install node-red-contrib-postgres-multi

### Usage

Assemble your queries as an array of objects on msg.payload:

    msg.payload = [
        {
            query: 'insert into mytable (id, message) values (1, $hello), (2, $world)',
            params: {
                hello: 'Hi there',
                world: 'O\'Rorke',
            },
        }
    ];

As you can see, this structure allows you to create your own transaction boundaries.

If you want the output of one or more queries, check the 'Receive output' box in the postgres node
and include an `output: true` member in the query object(s) you expect results from.
The results are then set on the msg.payload property of the outbound message.

    msg.payload = [
        {
            query: 'select message from mytable where id=$1',
            params: [1],
            output: true,
        },
        {
            query: 'select message from mytable where id=$1',
            params: [2],
            output: true,
        },
    ];

    # output:

    [
        ['Hi there'],
        ['O\'Rorke']
    ]

### Example DB

#### TO DO
### Example node-red flow

#### TO DO