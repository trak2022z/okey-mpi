# Alpine MPICH

Docker image of Alpine Linux with  [MPICH](http://www.mpich.org/) -- portable implementation of Message Passing Interface (MPI) standard. Designed for MPI program development and deployment.

Provide solution for MPI Cluster Automation with Docker containers using either Docker Compose or Docker Swarm Mode.

----

        Best Paper Award at IEEE CCWC 2017

**N. Nguyen** and **D. Bein**, "[Distributed MPI cluster with Docker Swarm mode](http://ieeexplore.ieee.org/document/7868429/)," 2017 IEEE 7th Annual Computing and Communication Workshop and Conference (CCWC), Las Vegas, NV, USA, 2017, pp. 1-7.

----

Image usage instruction: 
[https://hub.docker.com/r/nlknguyen/alpine-mpich](https://hub.docker.com/r/nlknguyen/alpine-mpich)


Distributed MPI cluster setup instruction: [https://github.com/NLKNguyen/alpine-mpich/tree/master/cluster](https://github.com/NLKNguyen/alpine-mpich/tree/master/cluster)  
* **[Single Host Orchestration](https://github.com/NLKNguyen/alpine-mpich/wiki/Single-Host-Orchestration)**
* **[Multi Host Orchestration](https://github.com/NLKNguyen/alpine-mpich/wiki/Multi-Host-Orchestration)**



----

Automated build with Travis CI and push to Docker Hub [https://hub.docker.com/r/nlknguyen/alpine-mpich](https://hub.docker.com/r/nlknguyen/alpine-mpich/)

**TODO Feb 23, 2019**: Current failed checks are due to new style rules for shell scripts using *shellcheck* tool. All shell scripts need to be updated to pass the build. Most of shellcheck's recommendations are legit. 

[![Build Status](https://travis-ci.org/NLKNguyen/alpine-mpich.svg?branch=master)](https://travis-ci.org/NLKNguyen/alpine-mpich)

[![Docker Hub](http://dockeri.co/image/nlknguyen/alpine-mpich)](https://hub.docker.com/r/nlknguyen/alpine-mpich)


`base image` ([Dockerfile](https://github.com/NLKNguyen/alpine-mpich/blob/master/Dockerfile)) : contains MPICH and essential build tools. Intended to be used as development environment for developing MPI programs.

`onbuild image` ([Dockerfile](https://github.com/NLKNguyen/alpine-mpich/blob/onbuild/Dockerfile)) : inherits base image with network setup for cluster. Can be used like base image but intended to be used to build image that contains compiled MPI program in order to deploy to a cluster.

`cluster` ([project scaffolder](https://github.com/NLKNguyen/alpine-mpich/tree/master/cluster)) : is a directory containing a setup for deploying MPI programs to a cluster of containers. Include a runner script to automate Docker commands.


*Below is instruction for building the Docker image yourself if you don't want to use the pre-built base or onbuild image.*

----

## Build Instruction

The images are prebuilt and hosted at Docker Hub, but in case you want to build them yourself:

```sh
$ git clone https://github.com/NLKNguyen/alpine-mpich

$ cd alpine-mpich

$ docker build -t nlknguyen/alpine-mpich base/

$ docker build -t nlknguyen/alpine-mpich:onbuild onbuild/
```

Since the onbuild image inherits the base image, if you use a different tag name (`nlknguyen/alpine-mpich`), you must change the first line in `onbuild/Dockerfile` to inherits `FROM` your custom tag name.

----

## Build Customization

In order to customize the base image at build time, you need to download the Dockerfile source code and build with optional build arguments (without those, you get the exact image as you pull from DockerHub), for example:

```sh
$ git clone https://github.com/NLKNguyen/alpine-mpich

$ cd alpine-mpich

$ docker build --build-arg MPICH_VERSION="3.2b4" -t my-custom-image base/
```

These are available **build arguments** to customize the build:
- `REQUIRE` *space-separated names of packages to be installed from Alpine main [package repository](http://pkgs.alpinelinux.org/packages) before downloading and installing MPICH. Default=`"sudo build-base openssh"`*
- `MPICH_VERSION` *to find which version of MPICH to download from [here](http://www.mpich.org/static/downloads/). Default=`"3.2"`*
- `MPICH_CONFIGURE_OPTIONS` *to be passed to `./configure` in MPICH source directory. Default=`"--disable-fortran"`* (let me know if you need Fortran, I can certainly add it by default)
- `MPICH_MAKE_OPTIONS` *to be passed to `make` after the above command. Default is empty*
- `USER` *non-root user with sudo privilege and no password required. Default=`mpi`*
- `WORKDIR` *main working directory to be owned by default user. Default=`/project`*

*See MPICH documentation for available options*

Should you need more than that, you need to change the Dockerfile yourself or send suggestion/pull requests to this GitHub repository.


# Feedback

Feedbacks are always welcome. For general comments, use the comment section at the bottom of this [image page](https://hub.docker.com/r/nlknguyen/alpine-mpich) on Docker Hub

## Issue

Use this GitHub repository [issues](https://github.com/NLKNguyen/alpine-mpich/issues)

## Contributing

Suggestions and pull requests are awesome.

# License MIT
Copyright ?? Nikyle Nguyen
# okey, tutorial dla student??w PRZ

INSTRUKCJA INSTALACJI NA WINDOWS 10
1. Uruchom powershell z uprawnieniami administratora
2. Uruchom poni??sze instrukcje

wsl --install

Lub, gdy istnieje wsl1:

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform

wsl --set-default-version 2

Zainstaluj wybran?? dystrybucj?? linuxa np. debian.
W wybranej dystrybucji utw??rz konto u??ytkownika a nast??pnie wykonaj:

sudo apt-get update

sudo apt-get upgrade

sudo apt-get install git
Wy????cz debiana/ubuntu/whatever.

ZAINSTALUJ DOCKER
Po instalacji wejd?? w opcje i zaznacz w general "Use Docker Compose V2" je??li jest odznaczone
Wejd?? w opcjach w resources-> wsl integration i w????cz integracj?? WSL oraz zaznacz zainstalowan?? dystybucj??.

UWAGA
je??li posiadasz ju?? docker, nale??y przekszta??ci?? go do wsl2. Wy????cz dockera a nast??pnie wpisz poni??sze instrukcje.

wsl --shutdown

wsl --unregister docker-desktop

wsl --unregister docker-desktop-data

W????cz docker.
W????cz wybran?? dysrtybucj?? linuxa.
W wybranym miejscu pobierz projekt:

git clone https://github.com/B-Paluch/okey.git

W WSL wklejasz za pomoc?? prawego klawisza myszy.


Jak dzia??a:
wejd?? w katalog cluster. Zawarty tam jest plik ./cluster.sh

Wykonuj??c komend?? ./cluster.sh size=10
zostanie uruchomiony klaster z 10 procesami pracuj??cymi.

Wpisz ./cluster.sh aby zapozna?? si?? z komendami

Po????czysz si?? z klastrem przez ./cluster.sh login


UWAGA niekt??re dystrystrybucj?? wymagaj?? zmiany chmod dla folderu i uruchamiania pozosta??ych polece?? z konta administratora(sudo komenda).


Komenda chmod:

sudo chmod 777 cluster -R

Po zalogowaniu wydaj polecenie ls i odpal dowolny program dla przyk??adu

mpirun ./mpi_hello_world

Przerwiesz dzia??anie programu przy pomocy ctrl+c

od????czysz si?? od klastra przy pomocy polecenia exit


# JAK PISA?? PROGRAMY

Pod wybran?? dystrybucj?? utw??rz kod programu kt??ry chcesz napisa??.
Mo??liwe jest w eksploratorze windows(klawisz windows+e) wpisanie w ??cie??k??:


\\wsl$

i przegl??danie zawarto??ci linuxa.
Wejd?? w ??cie??k?? gdzie zawarte s?? programy, na przyk??ad:

\\wsl.localhost\Debian\home\bartek\alpine-mpich\cluster\project

nazwa bartek\alpine-mpich ma by?? nazw?? twojego u??ytkownika oraz projektu

W tym miejscu dodaj pliki napisane w C.

Po wykonaniu tego, wejd?? katalog ni??ej

\\wsl.localhost\Debian\home\bartek\alpine-mpich\cluster\

I w pliku Dockerfile(otw??rz na przyk??ad notatnikiem) dopisz po poni??szej linijce:

RUN mpicc -o bingo bingo.c

linijk??:

RUN mpicc -o nazwaprogramu nazwaprogramu.c

Po dodaniu tego wykonaj przebudow?? obrazu na dystrybucji linuxa za pomoc?? ./cluster.sh up size=10

gdzie size to parametr kt??ry samemu dobieramy, zale??nie od tego ile chcemy mie?? worker??w w klastrze.

Po po????czeniu si?? z klastrem - ./cluster.sh login

wykonaj polecenie mpirun ./nazwaprogramu

Je??eli program zosta?? napisany poprawnie, zostanie on wykonany zgodnie z zaleceniami.

Przy ka??dej zmianie w programie nale??y przebudowa?? ponownie obraz przez ./cluster.sh up...

Aby doda?? kolejne pliki powt??rz w pliku Dockerfile linijk?? RUN mpicc -o...
