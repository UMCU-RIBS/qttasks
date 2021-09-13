# QTTASKS

## Running the task
### Installing
This program only works on Python 3. 
Required packages: `numpy` and `pyqt5`. 
Optional packages: `psutils` (strongly advised, to increase the task priority) and `pandas` (to convert log file to tsv)

Install the packages like this:

```bash
pip3 install numpy pyqt5 psutils
```

Then install this package:

```bash
git clone git@github.com:UMCU-RIBS/qttasks.git
pip3 install -e qttasks
```

It works on windows and linux (and probably MacOs but untested).

### Running the tasks
Open a command window and run:

```bash
qttasks NameOfTask ConfigurationType
```
where:
  - `NameOfTask`: name of the task, which should be similar to the name of the folder that contains the actual task settings and images! 
  - `ConfigurationType`: refers to one of the .json files that should be stored in the configurations folder. This file specifies the settings (if not otherwise specified, the default is used). 

In the words, the program reads `default.json`, then the parameters.json stored in the corresponding task folder, then the `.json` stored in the corresponding configuration folder.

Shortcuts to the tasks can also be made which allow the user to quickly run a task by double clicking on the icon. 

After running the command/clicking on the icon, wait a sec and check the command window for errors. In case of an error, you can see what’s wrong in the command window. 

### Interacting with the task
  - Starting the task: press `Enter` or double click on the right side of the screen
  - Pausing the task: press `Space` or double click on the right side of the screen
  - Minimizing the task window: double click on the left side of the screen
  - Stopping the task: press `esc` or click on the red cross of minimalized window

## Adapting the code
### File description

  - `default.json`: contains the default settings. When no other settings are specified in the configurations file, the default will be used. Specifying other settings will overwrite that specific default setting.
  - `paths.py`: sets the paths to your necessary files. 
  - `read_tsv.py`: reads the .tsv file you need to input in your tasks folder
  - `presentation.py`: contains the code that will actually presents the task
  - `dataglove.py`: enables use of the dataglove during the tasks
  - `convert_log_to_tsv.py`: says what it does (useful for BIDS, but quite unstable). 

### Tasks
If you want to add a new task, add a folder to the tasks folder. In this folder there should be:
  - an images folder including the stimuli that needs to be shown
  - a `parameters.json` file that specifies the parameters that are different from the default parameters
  - a `timing.tsv` file that specifies:
    - `onset`: time since start at which the new trial starts (e.g. stimulus is shown)
      - time between onsets – duration = inter stimulus interval (fixation cross)
    - `duration`: how long the stimulus will be visible
    - `trial_name`: condition (this should be text!)
    - `stim_file`: path to the stimulus for this trial
    - `trial_type`: number which is also send as trigger

### Configurations
You can add multiple configurations (f.e. one specific tablet or PC).
Some useful parameters to adapt:

  - `COM`:
    - `INPUT`:
      - `PORT`: port to use for input trigger (scanner trigger or button box)
      - `BAUDRATE`: baudrate of the input port
      - `START_TRIGGER`: (fMRI specific) task will start without pressing `Enter` when this trigger is received
    - `TRIGGER`:
      - `PORT`: port to use for sending triggers
      - `BAUDRATE`: baudrate of the output port
  - `SCREEN`:
    - `DOWNWARDS`: move the image down by this amount of pixels
    - `RIGHTWARDS`: move the image right by this amount of pixels
  - `TASK_TSV`: will use the file specified in this parameter (`timing_7t.tsv` f.e.). If `timing_7t.tsv` does not exist, it'll use `timing.tsv` by default. This is useful when you need to specify multiple information.


### Updating the repository
Use Git Bash to interact with git.

To pull:
  - Input path to the right folder
  - Command: git pull

To submit local change:  
  - Command: git status  shows your changed files  
  - Command: git commit -am “message what you changed”  commits all files including a message 
