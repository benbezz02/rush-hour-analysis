# Rush Hour Analysis

## Group Members

Benjamin Bezzina  
Krane Kint Ediza Dabatos

## DataFrame Column Descriptions

The DataFrame contains information about workers and their simulated commuting behavior for a certain date.

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
* The transportation data can be found here : [Skånetrafiken public transport data (Google Drive)](https://drive.google.com/drive/folders/1dk5nIUQvKuFdWP_bqHSTBLJ0musdubZt?usp=drive_link)
* The workers data can be downloaded here: [Statistikdatabasen](https://www.statistikdatabasen.scb.se/pxweb/sv/ssd/START__AM__AM0210__AM0210F/ArRegPend2/)
