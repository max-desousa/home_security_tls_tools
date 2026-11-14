# What is this?
This repo is scripts to handle tls encryption and file generation used for the encryption of nodes in [home_security_client_zig](https://github.com/max-desousa/home_security_client_zig) and [home_security_server_zig](https://github.com/max-desousa/home_security_server_zig).

Since those repos are handling potentially sensitive security camera data, this repo is for:
- Generating keys for each node
- Keeping the key generation data isolated from the projects

# How to use this

The following explains how to run these scripts and what to save.

## Creating Keys and Certificates

There are two phases for generating data:
1. Generate a Certificate Authority
2. Create nodes with CA signed keys

### Generate a Certificate Authority

These are generated via script `create_certificate_authrority`. Simply run this script and all the necessary files will be created. All created files will be left in the `./ca/` path and the presence of previosu Certificate Authority will prevent the script from generating a new one. 

### Creating Subsequent CA Signed nodes

Simply run script `./generate_node [node_name] <node_type>`. 

The default node_type is a `client`, but the value `server` is also valid.

When running the script, a folder will be created that shares the node name, and all the files needed for that node to participate in a TLS secured connection will be saved. This is intended to be simply copy-paster ready for your instances of the aformentioned projects.

## Saving Your Data

Your Certificate Authority is needed for generating nodes. There is data generated that MUST remain **private** and data that is public.

No data from the ca folder should be copy/pasted. But, if you want to create nodes to add to your network later without invalidating all nodes, you need to keep all the data in the ca folder present. (or saved somewhere safe... anyone getting access to this data can create a client that can connect to the network).

The data made via generate_node should be the only data that goes into one of your zig instances. After transferring it to your instance, you can delete that from your computer. (so no one can use the private key if they stumble on it).
