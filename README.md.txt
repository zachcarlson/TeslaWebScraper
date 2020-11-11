# Tesla Supercharger Station Locations

## Project description

The overall goal is for the user to be able to press buttons randomly using the InputData scene. This data requires security (i.e. encrypted in transmission and at rest). In other words, you cannot store this information in a plain txt but can remain in RAM. Once the user has pressed the buttons, they can see their results in the StatsDisplay scene. Here, the user can clear their data and/or return to the InputData scene to add more data. 

### Requirements:
- Accurately collect user inputs from the buttons.
- Manage user data between scenes securely.
- Display the user's button pressing "progress" in some way besides just text.

### Notes:
- You can use any free asset you want.
- You can add to the README to justify any design decisions you made.
- Feel free to ask me questions if you have them. Our team will typically work like this, just message me whenever you need.
- You can tear apart/redo the scenes, they're just placeholders for clarity of project requirements. 


### Design

- Collection of user input is handled solely by the ButtonInputRecorder. This object communicates with the InputStorage object via the IInputStorage interface to store input data. ButtonInputRecorder requires references to objects that implement the IButtonInput interface. This interface exposes an id which is used by InputStorage.

- This interface driven approach allows us to easily add or remove button inputs. InputStorage doesn't care where the input comes from, it only requires an id to keep track of inputs.

- InputStorage is a persistent singleton that maintains a dictionary of stored inputs. I assigned each input an id (enforced by IButtonInput) that can be utilized throughout the app. Users' input data lives in InputStorage and is destroyed when a session ends.

- I implemented InputStorage as a singleton to make dependency resolution simpler. This object is used in two different scenes (one stores data, the other retrieves it).

- Upon fetching input data, InputStatsTextDisplay creates 'rows' of data via a prefab I set up. It only requires a reference to IInputStorage which can be retrieved via the singleton.

- InputStatsDotDisplay utilizes the DOTween library of animations to display a pictograph of the user's input data.