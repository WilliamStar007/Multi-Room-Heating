# CS6376-FinalProject
Repo for final project for the class CS6357 hybrid &amp; embedded systems at Vanderbilt University

# Project Description
[Project_Description.pdf](https://github.com/JaneWu423/CS6376-FinalProject/files/13532765/description.pdf)


# Project Proposal
[Project Initial Choice.pdf](https://github.com/JaneWu423/CS6376-FinalProject/files/13272777/Project.Initial.Choice.pdf)

# Project Presentation Slides
[Presentation Google Slides](https://docs.google.com/presentation/d/11mU_nW_fXvMXEo77R5Aph6IkYLEQ7t2BdWsd3m9e64o/edit?usp=sharing)

### Problem Statement

The purpose of the project is to model a room heating system. Suppose there is a house with 4 rooms, and the rooms are heated with only 2 vents allowed to open at the same time. The temperature in each room is influenced bu heat from the vent, if it is open, and also depends on the temperature of the adjacent rooms and the outside temperature. Each room only has one vent.

Let x<sub>i</sub> be the temperature in room i (i = 1,2,3,4), u being the outside temperature. The temperature of a room changes linearly with the difference of the temperature with the other rooms, the difference with the outside temperature, and the heater if vent is open. Specifically, the dynamics of the system is given by:

<img width="339" alt="Screen Shot 2023-11-10 at 5 41 17 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/cfbc69f6-8cab-406b-9432-777129710ff1">

with constants a<sub>i,j</sub>, b<sub>i</sub>, c<sub>i</sub>. In this equation, h<sub>i</sub> ∈ {0,1} is the status of the vent in the room: h<sub>i</sub> is 0 if vent is closed, h<sub>i</sub> = 1 if vent is on. We assume that all the vent are identical.

### Openning of Vents

A vent will be closed in room j and open in room i (i ！= j) if all the followings hold:
- Room i has vent closed
- Room j has vent open
- Temperature x<sub>i</sub> ≤ get<sub>i</sub>
- The difference x<sub>j</sub> − x<sub>i</sub> ≥ dif<sub>i</sub>.

The get<sub>i</sub> and dif<sub>i</sub> are constants that can differ across different rooms.

### Requirement Specifications
- The temperature in all rooms is always between a given threshold (Safety 1)
- The there is no more than 2 vents open at the same time (Safety 2)
- Every room will eventually get its vent opened at least once. (Liveness)

### Design of Room Heating System
The system will have h<sub>i</sub> (vent status) and u (outside temperature) as inputs. The system will be parameterized by the following constants:
- a constant matrix A = [a<sub>i,j</sub>] ∈ R<sup>4×4</sup>,
- a constant vector b = [b<sub>i</sub>] ∈ R<sup>4</sup>,
- a constant vector c = [c<sub>i</sub>] ∈ R<sup>4</sup>, 
- initial temperature of each room in a vector x<sub>0</sub> ∈ R<sup>4</sup>.

The inputs to the system will be outside temperature and output from the controller. The output will be current temperature. The temperature of the rooms will be calculated using the room dynamics formula given above.

### Design of the Controller
The controller will have parameters
- constants on<sub>i</sub> in a vector on = [on<sub>i</sub>] ∈ R<sup>4</sup>,
- constants off<sub>i</sub> in a vector off = [off<sub>i</sub>] ∈ R<sup>4</sup>,
- constants get<sub>i</sub> in a vector get = [get<sub>i</sub>] ∈ R<sup>4</sup>, 
- constants dif<sub>i</sub> in a vector dif = [dif<sub>i</sub>] ∈ R<sup>4</sup>.

The inputs to controller are temperatures x<sub>i</sub>. The outputs should be h<sub>i</sub> for each room i, with the constraints that h<sub>i</sub> ∈ {0,1} and at any time, at most two of these outputs can be 1 (only 2 vents can be on).

### Model Component Logic Flow
<img width="600" alt="Screenshot 2023-11-10 at 8 08 20 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/89805831/755ef469-a4cc-4cb5-beb8-72a008ddcdc6">

### Model Implementation
The python implementation of the whole system can be found in the [Google Collab notebook](https://colab.research.google.com/drive/1gZphM4oSAg27RGblI-a3MU5yguD2y-WQ?usp=sharing). Simply click "run all" in Colab, and you can see the simulation results in plots in the end of the file.

The Simulink implementation of the system is in this repo, and you can run the simulation and inspect the components by downloading the .slx file and open it in MATLAB Simulink, simply click "simulate" and you can inspect the simulation results in the display components in the model.

### Design in Simulink
#### Overall Design
<img width="842" alt="Screen Shot 2023-12-08 at 6 19 48 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/3ffdf087-bf2f-4ec8-b4ae-33390969ae98">

#### Room System Design
<img width="922" alt="Screen Shot 2023-12-08 at 6 20 45 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/5265df5a-e12b-4af3-bb86-a310d50dbf2c">

#### Controller Design
<img width="642" alt="Screen Shot 2023-12-08 at 6 21 27 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/a18e236b-f2f6-4062-b456-fab58fa9e0c6">

#### Safety Monitor Design
<img width="530" alt="Screen Shot 2023-12-08 at 6 21 51 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/1d6ad9cd-58df-49b8-a3b1-08883507a30d">

#### Project Demo Video
https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/05fec211-dad7-4efa-819f-117b7846dc86

