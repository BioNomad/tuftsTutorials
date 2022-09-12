# Conda on the HPC

## Allocate Resources

- Please reference https://tufts.box.com/v/Pax-User-Guide to start an interactive session on the cluster on a compute node (execute every time you need to execute/run any programs on the cluster)
     - Determine if you need GUI forwarding
     - Determine if you need GPU access 
- Load modules
    - Load anaconda module

```
module load anaconda/3
```

or

```
module load anaconda/2021.05
```

The version of conda (anaconda) you use to operate on your environment needs to be

- Load other modules needed (such as $ module load cuda/11.0 )

## Create your conda environment

Now you can create your own conda env:

```
cd /cluster/tufts/XXXXlab/$USER/condaenv/
conda create -p yourenvname
```

Or if you have a specific version of python you need to use, e.g. 3.8 (Recommended!)

```
conda create -p yourenvname python=3.8 
```

!!! note 
    you will need to have python and pip installed inside the env to pip install packages inside the env.

Activate the environment (needs to be executed whenever you need to use the conda env you have created)

```
source activate yourenvname
```

If you are using system installed conda, please DO NOT use conda activate to activate your environment Install yourpackage in the conda env

```
conda install yourpackage
```

Or if you have python (comes with pip) installed

```
pip install yourpackage
```

Or follow the instruction on package website. Check what's installed in your conda environment:

```
conda list
```

When you are done, deactivate the environment

```
conda deactivate
```
## Additional Information for Jupyter Users: Run conda env as a kernel in Jupyter

If you would like to use JupyterNotebook or JupyterLab from OnDemand, you can follow the instructions below and run your conda env as a kernel in Jupyter.
Make sure with python 3.7+ and make sure you load cluster's anaconda module (this only works with py3.7+)
Activate your conda env from terminal. Install ipykernel with:

```
pip install ipykernel 
```
!!! note
    this assumes you installed python and pip in your env, otherwise, use "--user" flag
    
Add your env to jupyter with:

```
python -m ipykernel install --user --name=myenvname 
```

!!! tip
    use the name of your environment in the place of "myenvname"
    
Restart Jupyter from OnDemand 
 
