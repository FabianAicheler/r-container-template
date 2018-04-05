FROM r-base:{{ cookiecutter.r_version }}

LABEL maintainer="{{ cookiecutter.author_name }}" <"{{ cookiecutter.author_email  }}">  
LABEL version="{{ cookiecutter.container_version }}"
LABEL organization="QBiC"
LABEL github="https://github.com/qbicsoftware"

# Update the OS and installed packages
RUN apt-get update -y && apt-get upgrade -y
# Install git and ca-certificates
RUN apt-get install -y git ca-certificates
# Clean up
RUN apt-get clean

# Copy the list of R packages into the container's /tmp dir
COPY rpackages.txt /tmp
ENV PKGLIST /tmp/rpackages.txt

COPY /scripts/* /usr/local/src/myscripts/
WORKDIR /usr/local/src/myscripts

# Install R packages from package list
RUN cat $PKGLIST | xargs -i sh -c 'R --vanilla <<EOF \
source("https://bioconductor.org/biocLite.R") \
biocLite("{}", ask=FALSE) \
q() \
EOF'

