# Problem with Pydio

This repository contains the Docker infrastructure for creating a fresh install of Pydio 8.0.2

This is supposed to be supplemental for the forum thread at https://forum.pydio.com/t/uploader-form-retrieval-of-config-yields-empty-response

## Usage

You should be able to run this thing using `docker-compose up --build`

## Pydio Install

After building and starting up you can navigate to
http://localhost (if you're running it locally)
and step through the Pydio install wizard.

| Install Parameter | Value |
| --- | --- |
|DB-Type:|MySQL|
|DB-Host:   | mariadb |
|DB:        | pydio  |
|User:      | pydio  |
|Password:  | pydio|

## Verify the problem

Go into on of the default repositories and try to upload ANY file. You'll get an error stating the file was too big.

## Notes

There'll be a PHPMyAdmin instance running at port 8080 so you can explore the database. Root password is `secret_haha`