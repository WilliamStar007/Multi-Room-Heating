## Project Description

### Problem Statement

The purpose of the project is to model a room heating system. Suppose there is a house with 4 rooms, and the rooms are heated with only 2 vents allowed to open at the same time. The temperature in each room is influenced by heat from the vent, if it is open, and also depends on the temperature of the adjacent rooms and the outside temperature. Each room only has one vent.

Let x<sub>i</sub> be the temperature in room i (i = 1,2,3,4), u being the outside temperature. The temperature of a room changes linearly with the difference of the temperature with the other rooms, the difference with the outside temperature, and the heater if the vent is open. Specifically, the dynamics of the system is given by:

<img width="339" alt="Screen Shot 2023-11-10 at 5 41 17 PM" src="https://github.com/JaneWu423/CS6376-FinalProject/assets/73491595/cfbc69f6-8cab-406b-9432-777129710ff1">

with constants a<sub>i,j</sub>, b<sub>i</sub>, c<sub>i</sub>. In this equation, h<sub>i</sub> ∈ {0,1} is the status of the vent in the room: h<sub>i</sub> is 0 if a vent is closed, h<sub>i</sub> = 1 if a vent is on. We assume that all the vents are identical.

### Opening of Vents

A vent will be closed in room j and open in room i (i ！= j) if all the following hold:
- Room i has its vent closed.
- Room j has its vent open.
- Temperature x<sub>i</sub> ≤ get<sub>i</sub>.
- The difference x<sub>j</sub> − x<sub>i</sub> ≥ dif<sub>i</sub>.

The get<sub>i</sub> and dif<sub>i</sub> are constants that can differ across different rooms.

### Requirement Specifications
- The temperature in all rooms is always between a given threshold (Safety 1)
- There are no more than 2 vents open at the same time (Safety 2)
- Every room will eventually get its vent opened at least once. (Liveness)

### Design of Room Heating System
The system will have h<sub>i</sub> (vent status) and u (outside temperature) as inputs. The system will be parameterized by the following constants:
- a constant matrix A = [a<sub>i,j</sub>] ∈ R<sup>4×4</sup>,
- a constant vector b = [b<sub>i</sub>] ∈ R<sup>4</sup>,
- a constant vector c = [c<sub>i</sub>] ∈ R<sup>4</sup>, 
- initial temperature of each room in a vector x<sub>0</sub> ∈ R<sup>4</sup>.

The inputs to the system will be outside temperature and output from the controller. The output will be the current temperature. The temperature of the rooms will be calculated using the room dynamics formula given above.

### Design of the Controller
The controller will have parameters
- constants on<sub>i</sub> in a vector on = [on<sub>i</sub>] ∈ R<sup>4</sup>,
- constants off<sub>i</sub> in a vector off = [off<sub>i</sub>] ∈ R<sup>4</sup>,
- constants get<sub>i</sub> in a vector get = [get<sub>i</sub>] ∈ R<sup>4</sup>, 
- constants dif<sub>i</sub> in a vector dif = [dif<sub>i</sub>] ∈ R<sup>4</sup>.

The inputs to the controller are temperatures x<sub>i</sub>. The outputs should be h<sub>i</sub> for each room i, with the constraints that h<sub>i</sub> ∈ {0,1} and at any time, at most two of these outputs can be 1 (only 2 vents can be on).

### Model Component Logic Flow
<img width="600" alt="Screenshot 2023-11-10 at 8 08 20 PM" src="https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/8c31d822-91bf-47db-bdbe-d056459fbc06">

### Model Implementation
The Python implementation of the whole system can be found in the [Google Collab notebook](https://colab.research.google.com/drive/1gZphM4oSAg27RGblI-a3MU5yguD2y-WQ?usp=sharing). Simply click "run all" in Colab, and you can see the simulation results in plots at the end of the file.

The Simulink implementation of the system is in this repo, and you can run the simulation and inspect the components by downloading the .slx file and opening it in MATLAB Simulink, simply click "Run" and you can inspect the simulation results in the display components in the model by double clicking the Display Scope blocks.

### Design in Simulink
#### Overall Design
<img width="842" alt="Screen Shot 2023-12-08 at 6 19 48 PM" src="https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/e63ea9b1-37f5-467a-9f92-0feacec8061f">

#### Room System Design
<img width="922" alt="Screen Shot 2023-12-08 at 6 20 45 PM" src="https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/388414f7-8c4d-4757-8abc-89bdc558d125">

#### Controller Design
<img width="642" alt="Screen Shot 2023-12-08 at 6 21 27 PM" src="https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/e07afe2c-5c21-4bb4-9c7f-a7becd021466">

#### Safety Monitor Design
<img width="530" alt="Screen Shot 2023-12-08 at 6 21 51 PM" src="https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/98b0276e-9776-47c5-970a-e2cddab3f320">

#### Project Demo Video
https://github.com/WilliamStar007/Multi-Room-Heating/assets/89805831/8d6a97b2-4863-4d20-b199-76be60f7cd01
