MOOSE is a tool that allows the use of many physics and maths libraries to run simulations of finite elements of any shape, including unstructured meshes.

My purpose is to run simulations in parallel. My laptop that already is using Fedora 32, has four cores to process calculations.

According to the official MOOSE Website, we can install MOOSE using Conda.

1. In case you already have installed Conda, and its configuration; please go to the step 3.

You might install conda on Linux, by executing the following command:
```
curl -L -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p ~/miniconda3
```
2. Then, please set the global environment in our system to use conda:

export PATH=$HOME/miniconda3/bin:$PATH

3. Let’s add the channel conda-forge that will allow us to create the moose environment:
```
conda config --add channels conda-forge
conda config --add channels https://mooseframework.org/conda/moose
conda create --name moose moose-libmesh moose-tools
```
4. You need to activate the new moose env to use it. Do an update if it is possible:
```
conda activate moose
conda update --all
```
5. Clone the moose code and the examples provided in the new moose environment:
```
mkdir ~/projects
cd ~/projects
git clone https://github.com/idaholab/moose.git
cd moose
git checkout master
```
6. You can run the project in parallel, in this case we are using only four cores:
```
cd ~/projects/moose/test
make -j 4
./run_tests -j 4
```
If everything is a success, a message that the passed tests done in parallel, is displayed:Now, were are ready to run our first MOOSE program. I followed this workshop
```
cd ~/projects/moose/tutorials/darcy_thermo_mech/step01_diffusion
make -j 4 # use number of processors for your system
cd problems
../darcy_thermo_mech-opt -i step1.i
```
Remember to copy the content of sept1.i, and execute the output with Peacock, as follows:
```
~/projects/moose/python/peacock/peacock -r step1_out.e
```
Now, we have our simulation in action 🙂
