This is the CASA pipeline for e-MERLIN data, it is designed to be fully parallelised. It is, however, very early stages and will progress rapidly. It currently does work but does not do calibration yet. Feel free to change/modify.

## Dependencies ##
- CASA v5.0+ (see https://casa.nrao.edu/)
- aoflagger v2.9+ (see https://sourceforge.net/projects/aoflagger/). v2.7+ accepted but not recommended, will be deprecated.
- python2.7

## Download ##
If you have git installed, you can get the pipeline using:  
`git clone https://github.com/e-merlin/CASA_eMERLIN_pipeline.git`

If you don't have git, you can download and unzip the files from [here](https://github.com/e-merlin/CASA_eMERLIN_pipeline/archive/master.zip).

To install other dependencies e.g. aoflagger/wsclean check out either A. Offringa's websites:
- aoflagger: https://sourceforge.net/projects/aoflagger/
- wsclean: https://sourceforge.net/projects/wsclean/

Or (**recommended!**) use the handy anaconda scripts to instantly install dependcies within the conda environment. To do this follow the instructions in this repo.: https://github.com/jradcliffe5/radio_conda_recipes

## Usage ##
To run the pipeline simply do:  
`casa -c /path/to/pipeline/eMERLIN_CASA_pipeline.py -i <input file>`

To run the parallelized version using MPI in CASA you can use:  
`mpicasa -n <num_cores> casa -c /path/to/pipeline/eMERLIN_CASA_pipeline.py -i <input file>`

To execute the pipeline from within CASA:
~~~~
> run_in_casa = True
> pipeline_path = '/path/to/pipeline_path/'   # You need to define this variable explicitly
> execfile(pipeline_path + 'eMERLIN_CASA_pipeline.py')
> inputs, msinfo = run_pipeline(inputs_path=<input file>)
~~~~

To execute the pipeline within a Jupyter Notebook:
1. Follow the instructions for installing and using the [Jupyter kernel for CASA](https://github.com/aardk/jupyter-casa) (has options for both Singularity and Docker).
2. Download the [jupyter_notebook](https://github.com/rainsworth/CASA_eMERLIN_pipeline/tree/jupyter_notebook) branch of the pipeline: `git clone -b jupyter_notebook https://github.com/rainsworth/CASA_eMERLIN_pipeline.git` .
3. Launch the Jupyter Notebook server in a Singularity or Docker container, mounting the local directory containing the pipeline and a local directory containing the data you wish to run the pipeline on:
  - Singularity: execute `singularity run -B /CASA_eMERLIN_pipeline:$HOME/pipeline -B /data:$HOME/data jupyter-casa.simg` then copy and paste the Jupyter Notebook token provided into your browser.
  - Docker: Follow [these](https://github.com/aardk/jupyter-casa) instructions. If on a Mac:
  ~~~~
  > open -a XQuartz
  > ip=$(ifconfig en0 | grep inet | awk '$1=="inet" {print $2}')
  > xhost + $ip
  > docker run --rm -p 8888:8888 -i -t -v /tmp/.X11-unix:/tmp/.X11-unix -e DISPLAY=$ip:0 -v /local/path/to/pipeline/:/home/jupyter/pipeline -v /local/path/to/data/:/home/jupyter/data penngwyn/jupytercasa /bin/sh -c "jupyter notebook"
  ~~~~
4. Open a new Casa notebook and follow the instructions for executing the pipeline from within CASA above, or see the example notebook which can be found in the pipeline directory.



## Additional information ##

- [Documentation [online]](documentation/docs.md)
- [Wiki pages](https://github.com/e-merlin/CASA_eMERLIN_pipeline/wiki)


