#Ankor
Ankor is a collection of php and apache install scripts that make it easy to setup and maintain

it is build to go laterally with machines and stack them high

Lets say my next project calls for several machines
for example:
* 2 web servers
* 1 mysql database
* 1 phpmyadmin
* 3 transcoding

In docker-compose.yml, I could set up something like this
````
Web        DB           PHPMYADMIN      Transcoding

                                            ___
___                                         ___
___       ___              ___              ___
````
