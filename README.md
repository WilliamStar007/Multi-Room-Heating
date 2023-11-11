# CS6376-FinalProject
Repo for final project for the class CS6357 hybrid &amp; embedded systems at Vanderbilt University

# Project Proposal
[Project Initial Choice.pdf](https://github.com/JaneWu423/CS6376-FinalProject/files/13272777/Project.Initial.Choice.pdf)

# Intermediate Update

### Problem Statement

The purpose of the project is to model a room heating system. Suppose tehre is a house with 4 rooms, and the rooms are heated by only 2 heaters. The temperature in each room is controlled by a heater, if there is one in it, and also depends on the temperature of the adjacent rooms and the outside temperature. Each room can have at most one heater.

Let x<sub>i</sub> be the temperature in room i (i = 1,2,3,4), u being the outside temperature. The temperature of a room changes linearly with the difference of the temperature with the other rooms, the difference with the outside temperature, and the power of the heater if there is one in it. Specifically, the dynamics of the system is given by:

<img width="339" alt="Screen Shot 2023-11-10 at 5 41 17 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/cfbc69f6-8cab-406b-9432-777129710ff1">

with constants a<sub>i,j</sub>, b<sub>i</sub>, c<sub>i</sub>. In this equation, h<sub>i</sub> ∈ {0,1} is the power status of the heater in the room: h<sub>i</sub> is 0 if there is no heater or the heater is off, h<sub>i</sub> = 1 if there is a heater and is on. We assume that all the heaters are identical. If a<sub>i, j</sub> > 0 then rooms i and j are adjacent.

### Movement of heaters

A heater is moved from room j to room i (i ！= j) if all the followings hold:
- Room i has no heater (each room can have at most one heater)
- Room j has a heater
- Temperature x<sub>i</sub> ≤ get<sub>i</sub>
- The difference x<sub>j</sub> − x<sub>i</sub> ≥ dif<sub>i</sub>.

The get<sub>i</sub> and dif<sub>i</sub> are constants that can differ across different rooms.

### Requirement Specifications
- The temperature in all rooms is always between a given threshold (Safety)
- Every room will eventually get a heater that is on. (Liveness)

### Design of Room Heating System
The system will have h<sub>i</sub> (power status of the header in the room) and u (outside temperature) as inputs. The system will be parameterized by the following constants:
- a constant matrix A = [a<sub>i,j</sub>] ∈ R<sup>4×4</sup>,
- a constant vector b = [b<sub>i</sub>] ∈ R<sup>4</sup>,
- a constant vector c = [c<sub>i</sub>] ∈ R<sup>4</sup>, 
- initial temperature of each room in a vector x<sub>0</sub> ∈ R<sup>4</sup>.

A simple model of the room is built in the [Google Collab notebook](https://colab.research.google.com/drive/1gZphM4oSAg27RGblI-a3MU5yguD2y-WQ?usp=sharing). 
More modification of current model will be made to work with the designed controller.

### Design of the Controller
The controller will have parameters
- constants on<sub>i</sub> in a vector on = [on<sub>i</sub>] ∈ R<sup>4</sup>,
- constants off<sub>i</sub> in a vector off = [off<sub>i</sub>] ∈ R<sup>4</sup>,
- constants get<sub>i</sub> in a vector get = [get<sub>i</sub>] ∈ R<sup>4</sup>, 
- constants dif<sub>i</sub> in a vector dif = [dif<sub>i</sub>] ∈ R<sup>4</sup>.

The inputs to controller are temperatures x<sub>i</sub>. The outputs should be h<sub>i</sub> for each room i, with the constraints that h<sub>i</sub> ∈ {0,1} and at any time, at most two of these outputs can be 1 (only 2 heaters can be on).


### Model Component Logic Flow
<img width="600" alt="Screenshot 2023-11-10 at 8 08 20 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/89805831/755ef469-a4cc-4cb5-beb8-72a008ddcdc6">
