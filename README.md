<p align="left">
  <a href="https://github.com/mrueda/convert-pheno"><img src="https://github.com/mrueda/convert-pheno/blob/main/docs/img/CP-logo.png" width="220" alt="Convert-Pheno"></a>
  <a href="https://github.com/mrueda/convert-pheno"><img src="https://github.com/mrueda/convert-pheno/blob/main/docs/img/CP-text.png" width="500" alt="Convert-Pheno"></a>
</p>
<p align="center">
    <em>A software toolkit for the interconversion of standard data models for phenotypic data</em>
</p>

[![Build and Test](https://github.com/mrueda/convert-pheno/actions/workflows/build-and-test.yml/badge.svg)](https://github.com/mrueda/convert-pheno/actions/workflows/build-and-test.yml)
[![Coverage Status](https://coveralls.io/repos/github/mrueda/convert-pheno/badge.svg?branch=main)](https://coveralls.io/github/mrueda/convert-pheno?branch=main)
[![Docker Build](https://github.com/mrueda/convert-pheno/actions/workflows/docker-build.yml/badge.svg)](https://github.com/mrueda/convert-pheno/actions/workflows/docker-build.yml)
[![Docker Pulls](https://badgen.net/docker/pulls/manuelrueda/convert-pheno?icon=docker&label=pulls)](https://hub.docker.com/r/manuelrueda/convert-pheno/)
[![Docker Image Size](https://badgen.net/docker/size/manuelrueda/convert-pheno?icon=docker&label=image%20size)](https://hub.docker.com/r/manuelrueda/convert-pheno/)
[![Documentation Status](https://github.com/mrueda/convert-pheno/actions/workflows/documentation.yml/badge.svg)](https://github.com/mrueda/convert-pheno/actions/workflows/documentation.yml)
![version](https://img.shields.io/badge/version-0.0.0_alpha-orange)
[![License: Artistic-2.0](https://img.shields.io/badge/License-Artistic%202.0-0298c3.svg)](https://opensource.org/licenses/Artistic-2.0)


**Documentation**: <a href="https://mrueda.github.io/convert-pheno" target="_blank">https://mrueda.github.io/convert-pheno</a>

**Source Code**: <a href="https://github.com/mrueda/convert-pheno" target="_blank">https://github.com/mrueda/convert-pheno</a>


# NAME

**UNDER DEVELOPMENT**

convert-pheno - A script to interconvert common data models for phenotypic data

# SYNOPSIS

convert-pheno \[-i input-type\] &lt;infile> \[-o output-type\] &lt;outfile> \[-options\]

     Arguments:                       
       (input-type): 
             -ibff                    Beacon v2 Models (JSON|YAML) file
             -iomop                   OMOP-CDM CSV files or PostgreSQL dump
             -ipxf                    Phenopacket v2 (JSON|YAML) file
             -iredcap (experimental)  REDCap (raw data) export CSV file
             -icdisc  (experimental)  CDISC-ODM v1 XML file

             (Wish-list)
             #-ifhir                  HL7/FHIR
             #-openehr                openEHR

       (output-type):
             -obff                    Beacon v2 Models JSON file
             -opxf                    Phenopacket v2 JSON file

     Options:
       -debug                         Print debugging (from 1 to 5, being 5 max)
       -h|help                        Brief help message
       -log                           Save <convert-pheno-log.json> file
       -man                           Full documentation
       -mapping-file                  Fields mapping YAML (or JSON) file
       -max-lines-sql                 Maxium number of lines read from SQL dump [500]
       -min-text-similarity-score     Minimum score for cosine similarity (or Sorensen-Dice coefficient) [0.8] (to be used with --search mixed)
       -no-color                      Don't print colors to STDOUT [>color|no-color]
       -ohdsi-db                      Use Athena-OHDSI database (~2.4GB) with -iomop
       -omop-tables                   (Only valid with -iomop) OMOP-CDM tables to be processed. Tables <CONCEPT> and <PERSON> are always included.
       -out-dir                       Output (existing) directory
       -overwrite                     Overwrite output file
       -phl|print-hidden-labels       Print original values (before DB mapping) of text fields <_labels>
       -rcd|redcap-dictionary         REDCap data dictionary CSV file
       -schema-file                   Alternative JSON Schema for mapping file
       -search                        Type of search [>exact|mixed]
       -svs|self-validate-schema      Perform a self-validation of the JSON schema that defines mapping
       -sep|separator                 Delimiter character for CSV files
       -stream                        Enable incremental processing with -iomop and -obff [>no-stream|stream]
       -sql2csv                       Print SQL TABLES (only valid with -iomop). Mutually exclusive with --stream
       -test                          Does not print time-changing-events (useful for file-based cmp)
       -text-similarity-method        The method used to compare values to DB [>cosine|dice]
       -u|username                    Set the username
       -verbose                       Verbosity on
       -v                             Print Version

# DESCRIPTION

`convert-pheno` is a command-line front-end to the CPAN's module [Convert::Pheno](https://metacpan.org/pod/Convert%3A%3APheno).

The module will be uploaded to CPAN once the paper is submitted.

# SUMMARY

A script that uses [Convert::Pheno](https://metacpan.org/pod/Convert%3A%3APheno) to interconvert common data models for phenotypic data

# INSTALLATION

## Containerized

### Method 1: From Docker Hub

Download a docker image (latest version) from [Docker Hub](https://hub.docker.com/r/manuelrueda/convert-pheno) by executing:

    docker pull manuelrueda/convert-pheno:latest
    docker image tag manuelrueda/convert-pheno:latest cnag/convert-pheno:latest

See additional instructions below.

### Method 2: With Dockerfile

Please download the `Dockerfile` from the repo:

    wget https://raw.githubusercontent.com/mrueda/convert-pheno/main/Dockerfile

And then run:

    docker build -t cnag/convert-pheno:latest .

### Additional instructions for Methods 1 and 2

To run the container (detached) execute:

    docker run -tid --name convert-pheno cnag/convert-pheno:latest

To enter:

    docker exec -ti convert-pheno bash

The command-line executable can be found at:

    /usr/share/convert-pheno/bin/convert-pheno

The default container user is `root` but you can also run the container as `$UID=1000` (`dockeruser`). 

     docker run --user 1000 -tid --name convert-pheno cnag/convert-pheno:latest
    

Alternatively, you can use `make` to perform all the previous steps:

    wget https://raw.githubusercontent.com/mrueda/convert-pheno/main/Dockerfile
    wget https://raw.githubusercontent.com/mrueda/convert-pheno/main/makefile.docker
    make -f makefile.docker install
    make -f makefile.docker run
    make -f makefile.docker enter

### Mounting volumes

Docker containers are fully isolated. If you need the mount a volume to the container please use the following syntax (`-v host:container`). 
Find an example below (note that you need to change the paths to match yours):

    docker run -tid --volume /media/mrueda/4TBT/data:/data --name convert-pheno-mount cnag/convert-pheno:latest

Then I will do something like this:

    # First I create an alias to simplify invocation (from the host)
    alias convert-pheno='docker exec -ti convert-pheno-mount /usr/share/convert-pheno/bin/convert-pheno'

    # Now I use the alias to run the command (note that I use the flag --out-dir to specify the output directory)
    convert-pheno -ibff /data/individuals.json -opxf pxf.bff --out-dir /data

## Non containerized

The script runs on command-line Linux and it has been tested on Debian/RedHat based distributions (only showing commands for Debian's). Perl 5 is installed by default on Linux, 
but we will install a few CPAN modules with `cpanminus`.

    git clone https://github.com/mrueda/convert-pheno.git
    cd convert-pheno

Now you have two choose between one of the 2 options below:

**Option 1:** Install dependencies (they're harmless to your system) as `sudo`:

    make install # (Will ask for sudo passwd)
    make test

**Option 2:** Install the dependencies in a "virtual environment" (i.e., install the CPAN modules in the directory of the application). We'll be using the module <Carton> for that:

    # NB: We're installing cpanminus and Carton as sudo. That's why you will be asked to provide sudo password.
    make install-carton
    make test

### System requirements

    * Ideally a Debian-based distribution (Ubuntu or Mint), but any other (e.g., CentOs, OpenSuse) should do as well.
    * Perl 5 (>= 5.10 core; installed by default in most Linux distributions). Check the version with "perl -v"
    * 4GB of RAM.
    * 1 core
    * At least 16GB HDD.

See note about RAM memory below.

# HOW TO RUN CONVERT-PHENO

For executing convert-pheno you will need:

- Input file(s):

    A text file in one of the accepted formats. In `--stream` mode I/O files can be gzipped.

- Optional: 

    Athena-OHDSI database

    Please download it from this [link](https://drive.google.com/drive/folders/104_Bgl3IxM3U6u-wn-1LUvNZXevD2DRm?usp=sharing) (~2.4GB) and move it inside `db/` directory.

**Examples:**

    $ bin/convert-pheno -ipxf phenopackets.json -obff individuals.json

    $ $path/convert-pheno -ibff individuals.json -opxf phenopackets.yaml --out-dir my_out_dir 

    $ $path/convert-pheno -iredcap redcap.csv -opxf phenopackets.json --redcap-dictionary redcap_dict.csv --mapping-file mapping_file.yaml

    $ $path/convert-pheno -iomop dump.sql -obff individuals.json 

    $ $path/convert-pheno -iomop dump.sql.gz -obff individuals.json.gz --stream -omop-tables measurement

    $ $path/convert-pheno -cdisc cdisc_odm.xml -obff individuals.json --rcd redcap_dict.csv --mapping-file mapping_file.yaml --search mixed --min-text-similarity-score 0.6

    $ $path/convert-pheno -iomop *csv -obff individuals.json -sep ','

    $ carton exec -- $path/convert-pheno -ibff individuals.json -opxf phenopackets.json # If using Carton

## COMMON ERRORS AND SOLUTIONS

    * Error message: CSV_XS ERROR: 2023 - EIQ - QUO character not allowed @ rec 1 pos 21 field 1
      Solution: Make sure you use the right character separator for your data. The script tries to guess it from the file extension (e.g. comma for csv), but sometimes extension and actual separator do not match.
      Example for tab separator in CLI.
       --sep  $'\t' 

    * Error message: Foo
      Solution: Bar

# CITATION

The author requests that any published work that utilizes `Convert-Pheno` includes a cite to the the following reference:

Rueda, M et al., (2023). Convert-Pheno: A software toolkit for the interconversion of standard data models for phenotypic data \[Software\]. Available from https://github.com/mrueda/convert-pheno

# AUTHOR 

Written by Manuel Rueda, PhD. Info about CNAG can be found at [https://www.cnag.crg.eu](https://www.cnag.crg.eu).

# COPYRIGHT AND LICENSE

Copyright (C) 2022-2023, Manuel Rueda - CNAG.

This program is free software, you can redistribute it and/or modify it under the terms of the [Artistic License version 2.0](https://metacpan.org/pod/perlartistic).
