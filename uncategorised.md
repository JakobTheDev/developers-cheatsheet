# Uncategorised

A list of commands which haven't been filed under a cheatsheet yet.

## Docker

General Docker info
```bash
# Get Docker version
docker --version

# General info about docker
docker info

# List docker images
docker image ls

# List all docker containers (running and all)
docker container ls
docker container ls --all
```

Build docker image
```bash
# Basic build
docker build --tag=REPOSITORY/IMAGE_NAME .

# Specify dockerfile
docker build --tag=REPOSITORY/IMAGE_NAME --file ./DOCKERFILE-NAME .
```

Run docker container
```bash
# Simple run
docker run -i REPOSITORY/IMAGE_NAME

# Run with interactive shell
docker run -it REPOSITORY/IMAGE_NAME

# Run container in background with port exposed
docker run -d -p LOCAL_PORT:CONTAINER-PORT REPOSITORY/IMAGE_NAME
```

Docker repository
```bash
# Login to DockerHub
docker login

# Tag image
docker image-name --tag=USERNAME/REPOSITORY:VERSION
```

Clean up
```bash
# Remove all stopped containers
docker container prune

# Remove all dangling containers
docker image prune
```

## Git

Configure git
```bash
# Configure name and email
git config --global user.name "Your Name"
git config --global user.email "email@domain.tld"

# Generate SSH key
# Note: You will need to add the public key to your git account
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

# Add key to ssh-agent
eval $(ssh-agent -s)
ssh-add ~/.ssh/id_rsa
```

Basic git
```bash
# Clone a repository
git clone URL

# Add files to staging (ready for commit)
git add .
git add foo.txt
git add src/*

# Commit staged files
git commit

# Stash changes
git stash

# Re-apply most recent stashed changes
git stash pop
```

Git Flow
```bash
# Initialise git flow
git flow init

# Available branches are:
feature   Manage your feature branches.
bugfix    Manage your bugfix branches.
release   Manage your release branches.
hotfix    Manage your hotfix branches.
support   Manage your support branches.

# Start a new branch
git flow BRANCH_TYPE start BRANCH_NAME
git flow feature start new-feature

# Finish a branch (merge back into the appropriate branch)
git flow BRANCH_TYPE finish BRANCH_NAME
git flow feature finish new-feature
```

Housekeeping
```bash
# List local branches that have been merged
git branch --merged

# List local branches that have been merged (not including master / develop)
git branch --merged | egrep -v "(^\*|master|dev)"

# Delete local branches that have been merged (not including master / develop)
git branch --merged | egrep -v "(^\*|master|dev)" | xargs git branch -d
```

## Grep

General command line arguments
```bash
# Show line numbers
grep -n foo.txt

# Exclude results with matches
grep -v dont_match_me foo.txt
```

Grep currently running processes, filtering out the grep command itself.
```bash
# Output usually matches on the grep command, filter it out with -v
ps aux | grep foo_process | grep -v grep
```

## SSL

General OpenSSL commands
```bash
# Generate a new private key and Certificate Signing Request
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key

# Generate a self-signed certificate
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt

# Generate a CSR for an existing private key
openssl req -out CSR.csr -key privateKey.key -new

# Generate a CSR based on an existing certificate
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key

# Remove a passprhase from a private key
openssl rsa -in privateKey.pem -out newPrivateKey.pem
```

Checking keys, certificates and CSRs
```bash
# Check a private key
openssl rsa -in privateKey.key -check

# Check a certificate 
openssl x509 -in certificate.crt -text -noout

# Check a CSR
openssl req -text -noout -verify -in CSR.csr

# Check a PKCS#12 file
openssl pkcs12 -info -in keyStore.p12
```

Converting with OpenSSL
```bash
# Convert DER to PEM
openssl x509 -inform der -in certificate.cer -out certificate.pem

# Convert PEM to DER
openssl x509 -outform der -in certificate.pem -out certificate.der

# Convert PKCS#12 to PEM
openssl pkcs12 -in keyStore.pfx -out keyStore.pem -nodes

# Conver PKM and private key to PKCS#12
openssl pkcs12 -export -out certificate.pfx -inkey privateKey.key -in certificate.crt -certfile CACert.crt
```

## Vi

Go to a specific line
```bash
# When opening a file
vi +100 foo.txt

# When a file is already open
:100
```

## ZSH
Set up ZSH + oh-my-zsh + powerlevel9k
```bash
# Set zsh as the default shell
chsh -s $(which zsh)

# Install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

# Install powerlevel9k
git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

# Set up your .zshrc
# (I'd recommend source controlling it and copying the file onto your machine)

# Use the .zshrc config
source ~/.zshrc
```