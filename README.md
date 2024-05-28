# GitHub Action for check the migration files if there is any potential lock to the tables on MySQL DB.

## Description
This action wil check the migration files if there is any potential lock to the tables on MySQL DB, and it will do the following:
  - fail if there is any potential lock to the tables.
  - comment in the PR the potential lock coomands.
  - add to the comment the refrence documents.

## Supported language
This action now support the migration files syntax of two languages PHP and NodeJS.
## How to use:
```
name: "Check DB Migration Files"
on:
  pull_request:
    types: [opened, edited, reopened, synchronize]
    branches:
      - master
    paths:
      - 'migrations/**'
  
jobs:
  check-new-migrations:
    runs-on: ubuntu-latest
    name: A job to check migration files
    steps:
      - uses: breadfast/db-migration-check@v1
        with: 
          FILE_LOCATION: "src/migrations/"
          GUIDE_DOC: "https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html"
          LANGUAGE: "NODEJS"
          GITHUB_TOKEN: secrets.GITHUB_TOKEN
```

## Configuration 

| Variable 	| Description 	| Default value 	| Required 	|
|---	|---	|---	|---	|
| FILE_LOCATION 	| The location of migration files 	| "src/migrations/"  	| NO 	|   
| GUIDE_DOC 	| Any documentation that you need to reference here 	| "https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html"  	| NO 	| 
| LANGUAGE 	| The programing language, we support now PHP and Nodejs 	| "NODEJS" 	| NO 	|
| GITHUB_TOKEN 	| Your Github token 	| N/A 	| YES 	|

