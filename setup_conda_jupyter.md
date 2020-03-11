## Connect to server using port forwarding

1. `ssh -L


# Download Anaconda or Miniconda
1. Connect to server using port forwarding (neccessary for running a jupyter server later)
   ```
   # Note that port number is of your choice I just decided to use 8989
   ssh -L 8989:localhost:8989 username@hostname
   ```
1. Download Anaconda or Miniconda:
   + Anaconda with Python 3.7:
     ```{bash}
     wget https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
     ```
   + Miniconda with Python 3.7:
     ```{bash}
     wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
     ```
2. Give executable persimision to dowloaded copy (example Miniconda)
   ```
   chmod u+x Miniconda3-latest-Linux-x86_64.sh
   ```
3. Make a backup of your `.bashrc` configuration file
   ```
   cp .bashrc .bashrc.bak
   ```
4. Run the executable file
   ```
   bash Miniconda3-latest-Linux-x86_64.sh
   ```
5. Follow the installation instructions:
+ Please, press ENTER to continue --> press Enter
+ Press SpaceBar until next prompt
+ Do you accept the license terms? --> yes
+ `[/home/your_username/miniconda3]` --> press Enter (install in home directory) 
+ Do you wish the installer to initialize Miniconda3 by running conda init? --> yes
6. Create a new environment
   ```
   conda create --name bionformatics
   ```
7. Update conda
   ```
   conda update -n base -c defaults conda
   ```
8. Create Python 2.7 environment
   ```
   conda create -n py27 python=2.7
   ```
9. Activate/Deactivate the new `py27` environment
   ```
   conda activate py27
   # Returns to base environment:
   conda deactivate
   ```
10. Install Jupyter in the base environment
    ```
    # Base installation of jupyter notebook
    conda install jupyter
    # Install jupyter lab upgraded interface
    conda install jupyterlab
    # Allow to run the python kernel of other environments
    conda install nb_conda_kernels
    ```
11. Setup a password for Jupyter
    ```
    jupyter notebook password
    ```

12. Install some packages to **py27**
    ```
    conda activate py27
    conda install ipykernel
    conda install numpy
    conda install pandas
    ```
13. Check the environments available
    ```
    conda info --envs
    ```
14. Show channels registered in the configuration
    ```
    conda config --show channels
    ```
15. Add a channel to the configuration
    ```
    conda config --add chaconda defaults
    conda config --add channels bioconda
    conda config --add channels conda-forge
    ```
16. Install Biopython to the **bioinformatics** environment
    ```
    conda activate bioinformatics
    conda install ipykernel
    conda ins1tall biopython
    ```

# Run Jupyter Notebook/Lab

1. Start jupyter server
   ```
   jupyter lab --port 8989 --no-browser
   ```
2. Create alias to run Jupyter
   + Open .bashrc in edit mode `vim .bashrc`
   + Create a new line in the document with this information
     ```
     alias juno="jupyter lab --port 8989 --no-browser"
     ```
3. Open browser in local machine and navigate to the following URL
   `http://localhost:8989`
4. Download some data and notebooks to try from gitHub
   ```
   # Go to the directory in which you wan to clone the repository then paste
   git clone https://github.com/fpichardom/programming-demo-test.git
   ```
## Maintain server running
1. Create new windows session with tmux
   `tmux new -s <session_name>`
3. Start jupyter notebook `juno`
4. Detach the session `CTRL+b d`
5. Re-attach session:
   `tmux attach-session -t <session_name>`


## SSH when jupyter server is already running
If you only need to open the port to connect to the jupyter server:

1. Send to background:  
   `ssh -NfL 8989:localhost:8989 username@hostname`
2. Mantain visible in console
   `ssh -NL 8989:localhost:8989 username@hostname`
## Set of useful conda commands

+ Activate/Deactivate automatic initialization of conda environment:  
  `conda config --set auto_activate_base false`
+ Delete conda environment:
  `conda env remove --name <enviro_name>`
+ List all packages in environment:
  `conda list`
+ Search for packages in registered channels:
  `conda search <searchterm>`

## Set of useful jupyter notebook commands

+ List all running notebooks (including jupyter lab):  
  `jupyter notebook list`
+ Stop a running notebook:  
  `jupyter notebook stop <port_number>`