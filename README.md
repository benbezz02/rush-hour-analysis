# Simulating and Modelling Train Rush Hours
### A project for the BERN02 course by Krane Kint Ediza Dabatos and  Benjamin Bezzina.  

## Overview

This project simulates how commuters travel to their workplaces by train. It estimates the concentration of commuters at a selected target station based on their desired arrival times, likely train choices, and waiting times. Using the worker database, these three times are combined to simulate commuter concentrations at a specific station. The relevant times are sampled using weighted probability distributions, with configurable modes that influence the sampling process.

For more details about the simulation methodology, see `CommuterSimulation.ipynb`.

## Usage

The simulation allows the user to select:

- **Target station:** The station at which commuter concentrations will be studied.
- **Date:** The date for the simulation, since train schedules may vary from day to day.

## Statistical Modelling

The simulated data are subsequently analysed using **Poisson regression** to model commuter concentrations at the target station. The modelling process and implementation are documented in `CommuterModelling.ipynb`.

## Workflow

1. Select the target station and simulation date, see `CommuterSimulation.ipynb`.
2. Simulate commuter behaviour using the worker database and weighted probability distributions.
3. Save the simulated results to a CSV file.
4. Load the simulated data and fit a Poisson regression model, see `CommuterModelling.ipynb`.
5. Analyse the model results to investigate commuter concentrations at the selected station.

## Data Description

All relevant data including the workers database and the train schedules is found in `skane.zip`. The simulation outputs are stored in CSV format. Descriptions of the output columns are added here to explain the meaning of each variable and how it is used in the subsequent analysis.


| Column                     | Description                                                                                                                                                             |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sex`                      | Worker’s sex, recorded as `män` (male) or `kvinna` (female).                                                                                                            |
| `residential_municipality` | Municipality where the worker lives.                                                                                                                                    |
| `workplace_municipality`   | Municipality where the worker works.                                                                                                                                    |
| `origin_station`           | Nearest station to the worker’s residence from which they commute. This station is simulated using an LLM.                                                              |
| `destination_station`      | Nearest station to the worker’s workplace to which they commute. This station is simulated using an LLM.                                                                |
| `desired_arrival`          | Worker’s planned arrival time, simulated using a weighted probability distribution. Format: `HH:MM:SS`.                                                                 |
| `commute_type`             | Indicates whether the worker is arriving at or departing from the target station. Possible values: `arrive` or `leave`.                                                 |
| `train_to_take`            | Departure or arrival time of the train the worker is likely to take, simulated using a weighted probability distribution. Format: `HH:MM:SS`.                           |
| `waiting_time`             | Amount of time the worker waits at the station before boarding their train, simulated using a weighted probability distribution. Format: `HH:MM:SS`.                    |
| `in_'target_station'`      | Simulated time when the worker is present at the target station, calculated as `train_to_take - waiting_time`. The column name includes the name of the target station. |

### Simulation Notes

* **LLM-based simulation:** The origin and destination stations are simulated based on the worker’s residential and workplace locations.
* **Weighted probability distributions:** Desired arrival times, train selections, and waiting times are generated using weighted probability distributions.
* **Time format:** Time values are represented in `HH:MM:SS` format.
* **Target station:** The `in_'target_station'` column represents the worker’s estimated presence time at the station being studied.
* The transportation data can be found here : [Skånetrafiken public transport data](https://www.trafiklab.se/api/gtfs-datasets/gtfs-regional/)
* The workers data can be downloaded here: [Statistikdatabasen](https://www.statistikdatabasen.scb.se/pxweb/sv/ssd/START__AM__AM0210__AM0210F/ArRegPend2/)
