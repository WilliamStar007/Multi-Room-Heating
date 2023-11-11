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

### Design of Room Model

