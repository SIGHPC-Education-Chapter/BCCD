# BCCD
## One-Liner Description:
Show examples of parallel computing codes with visualizations running in a
Linux cluster environment without needing to obtain special hardware or manage
complicated software configurations.

## Extended Description:
The Bootable Cluster CD (BCCD) allows for the creation of a Linux cluster out of
any x86-based computers without requiring special hardware, separate disks or
partitions, or complicated software installations or setup.

There are a number of example codes included that can be run in parallel. Some
of them have visualizations that display as the code is running. Two of these in
particular are the N-body simulation named GalaxSee and the disease simulation
named Pandemic.

As an outreach tool, BCCD can be used to demonstrate examples of scientific,
parallel computing and basic performance benchmarking and scaling.

## Concepts
- N-body simulations
- Disease simulations
- Parallel computing
- Performance benchmarking
- Speedup
- Scaling

## Learning Outcomes
- Recognize examples of simulations for computational science
- Understand that the speed of programs can be measured
- Understand that parallel programs are run on multiple processors
- Understand that using a parallel program can be either faster or slower than
using a serial program

## Pre-Requisites
The person giving the demo will need to boot the cluster ahead of time. This
person will also need to be comfortable using a command line interface to enter
commands ahead of time to:

1. Compile the examples
~~~
make build-all
~~~
2. Distribute the executables to each computer (this only needs to be done if
more than one computer is used)
~~~
bccd-snarfhosts
bccd-syncdir . ~/machines-openmpi
~~~
3. Change directories to one of the examples (e.g. GalaxSee or Pandemic)
- If only running on one computer,
~~~
cd GalaxSee
~~~
- If running on more than one computer,
~~~
cd /tmp/node000-bccd/GalaxSee
~~~

Then the person giving the demo can run the GalaxSee simulation as follows
- Default
~~~
./GalaxSee.cxx-mpi
~~~
- 1,000 stars (adjustable parameter)
~~~
./GalaxSee.cxx-mpi 1000
~~~
- 1,000 stars that are 10 solar masses each (adjustable parameter)
~~~
./GalaxSee.cxx-mpi 1000 10
~~~
- 1,000 stars that are 10 solar masses each, for 10,000 time steps (adjustable
parameter)
~~~
./GalaxSee.cxx-mpi 1000 10 10000
~~~
- 1,000 stars that are 10 solar masses each, for 10,000 time steps with
visualization turned off
~~~
./GalaxSee.cxx-mpi 1000 10 10000 0
~~~
- Timing the simulation
~~~
time ./GalaxSee.cxx-mpi 1000 10 10000 0
~~~
- Timing the simulation with 2 cores (adjustable parameter)
~~~
time mpirun -np 2 ./GalaxSee.cxx-mpi 1000 10 10000 0
~~~
- Running on multiple computers
~~~
time mpirun -np 8 -machinefile ~/machines-openmpi ./GalaxSee.cxx-mpi 1000 10 10000 0
~~~

In the other terminal window, you can run this command to see how many pieces
of the program are being run and what percentage of a single core each is using 
(%CPU).
~~~
top
~~~

The person giving the demo can run the Pandemic simulation as follows
- Default
~~~
./Pandemic.serial
~~~
- 100 people (adjustable parameter)
~~~
./Pandemic.serial -n 100
~~~
- An environment with a width of 100 (adjustable parameter) and a height of 3
(adjustable parameter)
~~~
./Pandemic.serial -w 100 -h 3
~~~
- A simulation of 10 days (adjustable parameter)
~~~
./Pandemic.serial -t 10
~~~
- 100 people (adjustable parameter), 10 of whom are infected (adjustable
parameter)
~~~
./Pandemic.serial -n 100 -i 10
~~~
- Editing the Makefile to comment out the line that shows the visualization
~~~
vi Makefile
... (line 13)
#CFLAGS+=-DX_DISPLAY -L/usr/X11R6/lib -lX11
...
:wq
~~~
- Timing the simulation with 50,000 people
~~~
time ./Pandemic.serial -n 50000
~~~
- Timing the simulation with 2 cores (adjustable parameter)
~~~
time mpirun -np 2 ./Pandemic.c-mpi -n 50000
~~~
- Running on multiple computers
~~~
time mpirun -np 8 -machinefile ~/machines-openmpi ./Pandemic.c-mpi 50000
~~~

As with GalaxSee, in the other terminal window, you can run this command to see
how many pieces of the program are being run and what percentage of a single
core each is using (%CPU).
~~~
top
~~~

## Required Equipment
BCCD can run on any x86-based machine as a virtual machine or as a live image
booted from a CD or USB drive. For example, it can run on a single multi-core
laptop, or if you have networking gear (e.g. Ethernet cables and a switch), you
can connect multiple laptops or desktops; each one needs to run a virtual
machine or boot from a CD or USB drive.

A .iso image file should be downloaded from bccd.net. This .iso file should
be used either as a virtual CD in a virtual machine or burned to a CD or USB
drive.

It is helpful to include a small physical cluster nearby, e.g. a Raspberry Pi
cluster or a LittleFe (http://littlefe.net) to help visualize the idea of using
multiple processors at once.

## Duration
As few as 5 minutes, as much as an hour.

## Group Size
This demonstration can be given to groups of any size provided there is
sufficient screen projection and voice amplification.

## Contact
Aaron Weeden, aweeden@shodor.org
