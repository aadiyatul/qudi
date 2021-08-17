# Installation at PhLAM        {#installation}


Windows 10, for using with Sublime Text or command line.
Qudi will not work from Spyder.


## Installing Anaconda

1. Install Anaconda from https://www.anaconda.com/download/. 
Choose register Python in the system and add to the PATH (despite it is not recommended).

2. Check that Python and Conda are in the PATH variable by typing 'where conda' and 'where python' in the command line. 
If not, add them (usually located in ...\anaconda3 and ...\anaconda3\Scripts) to the PATH.

3. Copy ``libcrypto-1_1-x64.*`` and ``libssl-1_1-x64.*`` (4 files) from ``...\anaconda3\Library\bin`` to ``...\anaconda3\DLLs``. This is needed to install requirements for qudi using a single batch file in ``...\tools\``, otherwise conda fails to look for required packages (advise found on https://github.com/conda/conda/issues/9746).



## Installin  Qudi

1. Clone or download Qudi.

2. In the Qudi folder, go to the tools folder and execute the ``install-python-modules-windows.bat`` file as administrator.
Now you have a Conda environment named ``qudi`` prepared in a dedicated folder ``...\anaconda3\envs\qudi``.



## Installing Sublime Text

1. Install Sublime Text

2. Sublime Text 4 calls system Python as ``py``, not ``python``. 
To fix this, edit Python build settings following https://stackoverflow.com/revisions/23790095/4. In ``Python.sublime-build`` change ``py`` to ``python``.
Now you will be able to run Python files in SublimeText (using ``F7`` or ``Ctrl+B``)

3. Create a new build settings ``Qudi-Python.sublime-build`` by copying ``Python.sublime-build`` from the previous step. 
Replace ``python`` by path to the ``python.exe`` in the ``qudi`` environment (i.e. ``...\anaconda3\envs\qudi\python.exe``).
This will allow to run Qudi in the dedicated environment.



## Testing

Open ``start.py`` in Sublime Text and execute it by pressing ``F7``. If everything has been installed correctly, it should launch the main window.
N.B. Use ``Ctrl+Q`` for closing Qudi, otherwise it will stay in the memory and will not be able to relaunch.



## Desktop shortcut

You can create a Desktop shortcut to launch Qudi easily on your machine.

- On your Desktop, right click and go to ``New->Shortcut``
- For the location you need to copy the following target 
    - ` %windir%\System32\cmd.exe "/K" <path-to-activation-script> "<path-to-qudi-environment>"
     && cd "<path-to-qudi-directory>" && python "start.py" `
    - In order for the shortcut to work on every windows setup, you need to specify 3 things :
        - `<path-to-activation-script>` : the path to the Anaconda activate.bat file, for example
        `C:\ProgramData\Miniconda3\Scripts\activate.bat`.
        - `<path-to-qudi-environment>` : this can be found using command `conda info --envs` in a terminal.
        - `<path-to-qudi-directory>` : the path where Qudi's `start.py` can be found.  
- Click ``Next``
- Give the name you want fot the shortcut : ``Qudi``
- Click ``Finish``
- (Optional) Right click on the newly created shortcut and go to `Proprerties`
    - Click ``Change Icon...`` and browse for the ``artwork\logo\logo_qudi.ico`` logo

	
Please note, in Windows you cannot switch directly between partitions with cd (i.e. between C: and D:).
If Qudi's program is stored in another partition, you need to change the command to :
` %windir%\System32\cmd.exe "/K" <path-to-activation-script> "<path-to-qudi-environment>" && D:
     && cd "<path-to-qudi-directory-on-D-partition>" && python "start.py" `

