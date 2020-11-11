# Tesla Supercharger Station Locations

## Project Overview

The overall of this project is to scrape the Tesla website for Supercharger station locations and create a `.csv` file of these data points.  This repository was created for the DSCI 511 course at Drexel University

### Team Members

- Ashley Zuir,

- Shoshone Smith,

- Wesley Marshall, 

- Zach Carlson, zc378@drexel.edu

### Design

- Collection of user input is handled solely by the ButtonInputRecorder. This object communicates with the InputStorage object via the IInputStorage interface to store input data. ButtonInputRecorder requires references to objects that implement the IButtonInput interface. This interface exposes an id which is used by InputStorage.

- This interface driven approach allows us to easily add or remove button inputs. InputStorage doesn't care where the input comes from, it only requires an id to keep track of inputs.

- InputStorage is a persistent singleton that maintains a dictionary of stored inputs. I assigned each input an id (enforced by IButtonInput) that can be utilized throughout the app. Users' input data lives in InputStorage and is destroyed when a session ends.

- I implemented InputStorage as a singleton to make dependency resolution simpler. This object is used in two different scenes (one stores data, the other retrieves it).

- Upon fetching input data, InputStatsTextDisplay creates 'rows' of data via a prefab I set up. It only requires a reference to IInputStorage which can be retrieved via the singleton.

- InputStatsDotDisplay utilizes the DOTween library of animations to display a pictograph of the user's input data.
