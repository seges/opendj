opendj
======

A dockerized OpenDJ server.

### Prerequisites

Download OpenDJ-2.6.0 to opendj/OpenDJ-2.6.0.zip

### Build docker images

    bin/build [service] # where service is one of the directories that contains a Dockerfile

### Running opendj in development:

    bin/run [service]   # launch data and/or opendj containers

### Importing LDIFs:

The simplest aproach is to import remotely (e.g. via Apache Directory Studio). Alternatively, you can import LDIFs by injecting them into the data container:

    # Add LDIFs to /data/opendj/ldif/
    cat sample.ldif | docker exec -i data sh -c 'cat > /data/opendj/ldif/sample.ldif'
    
    # Any LDIFs in /data/opendj/ldif/ will be imported by running:
    bin/run ldap import       # requires stopping opendj_ldap_1 to import LDIFs

### Troubleshooting

    bin/run [service] shell   # launch a shell in the service container
    
    # From shell, you can run the default docker run command via:
    /start [ACTION] # where ACTION defaults to the start action

### Mac users

When run via Boot2Docker, opendj requires increasing the VM's file descriptor limit:

    echo "ulimit -n 10240" | sudo tee -a /var/lib/boot2docker/profile
