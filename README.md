# Bochum Movement Data
This repository holds data from a controlled single-obstacle avoidance experiment recorded in a motion laboratory. If you are using this data, please cite the following source for the data

B. Grimme, *Analysis and identification of elementary invariants as building blocks of human arm movements*. PhD thesis, International Graduate School of Biosciences, Ruhr-Universität Bochum. (In German).


For previous analyses of this data set and a number of related experimental setups, please refer to

L.L. Raket, B. Grimme, G. Schöner, C. Igel, and B. Markussen, "Separating timing, movement conditions and individual differences in the analysis of human movement
," *PLOS Computational Biology*, (accepted).

B. Grimme, J. Lipinski, and G. Schöner, "Naturalistic arm movements during obstacleavoidance in 3D and the identification of movement primitives," *Experimental BrainResearch*. vol. 222(3), pp. 185–200, 2012.


## Experimental setup 
Ten participants performed a series of simple obstacle avoidance tasks
on a table by relocating a cylindrical object from a starting position
to a target position. Between the starting position and target,
obstacles of varying heights and positions were placed. The
participants were instructed to avoid the obstacles by lifting the cylindric object over them. Below are illustrations of the setup and trajectories for three of the 16 experimental setups included in the data. 

| Medium obstacle 15 cm from start | Tall obstacle 30 cm from start | No obstacle |
|---|---|---|
| <img src="http://i.imgur.com/UpQmWvu.png" width="300"> | <img src="http://i.imgur.com/10E0Pja.png" width="300"> | <img src="http://i.imgur.com/uRTzwLW.png" width="300"> |
|                                                        |


The movements were recorded with the Visualeyez (Phoenix Technologies Inc.) motion capture system VZ 4000. A wireless infrared light-emitting diode (IRED) was attached to the object. The trajectories of markers were recorded in three Cartesian dimensions at a sampling rate of 110 Hz based on a reference frame anchored on the table. The starting position projected to the table was taken as the origin of each trajectory in three-dimensional Cartesian space. 


Fifteen obstacle avoidance tasks were performed (one for every combination of obstacle height *Small* (20 cm), *Medium* (27.5 cm), or *Tall* (35 cm) and obstacle distance from starting position  $d\in \{15, 22.5, 30, 37.5, 45\}$) as well as a control experiment with no obstacle. The participants repeated each task ten times, giving $n=100$ functional samples per experiment, and a total of $n_f =1600$ functional samples in the dataset, with a total data size of $m_{f}=174,160$ three-dimensional observation points.

## Loading the data into R

The data can be loaded into R with the following code

``` r
repetitions <- 10
participants <- 10
experiments <- 16

y <- as.matrix(read.table('armTrajectories.dat'))
dim(y) <- c(nrow(y), 3, repetitions, participants, experiments)

yvelo <- as.matrix(read.table('armVelocity.dat'))
dim(yvelo) <- c(nrow(yvelo), 3, repetitions, participants, experiments)
```

The five-dimensional array `y` will contain all the data. The indexing `y[, c, j, p, e]` will give sequence of *c*-coordinate positions (1: x-coordinate, 2: y-coordinate, 3: z-coordinate) of the hand of participant *p*'s *j*th repetion of experimental setup *e*. `e=16` denotes the control experiment with no obstacle, the numbering of experimental setups with obstacle is given in the table below. 

| placement\obstacle height | S | M | T |
|---|---|---|---|
| 15.0 cm | 1 | 2 | 3 |
| 22.5 cm | 4 | 5 | 6 |
| 30.0 cm | 7 | 8 | 9 |
| 37.5 cm | 10 | 11 | 12 |
| 35.0 cm | 13 | 14 | 15 |


To analyze this data we recommend the [pavpop](https://github.com/larslau/pavpop) R package. 

