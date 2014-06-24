rest-tickets
============

RestTickets Distribution Repository

To setup:

    git clone --recursive git@github.com:farazdagi/rest-tickets.git
    vagrant up --no-provision # it is ok that it asks for password, see Vagrantfile
    vagrant provision

After everythig is done, you will end up with 3 nodes:

- Application Server (10.3.0.10)
- Database Server (10.3.0.20)
- REST API Server (10.3.0.30)

Now you should be able to ssh into any of those boxes:

    vagrant ssh app  # ssh to appserver
    vagrant ssh db   # ssh to dbserver
    vagratn ssh api  # ssh to api server

Additionally, you should be able to ping port 80 on both app and api nodes (db node listens to PostgreSQL conections
only):

    ping 10.3.0.10
    ping 10.3.0.30

To make it easier to type, add following aliases to your /etc/hosts file:

    10.3.0.10 rest.tickets
    10.3.0.20 db.rest.tickets
    10.3.0.30 api.rest.tickets

Finally, try navigating to application in your browser: https://rest.tickets (you might need to accept self-signed SSL
certificate).

