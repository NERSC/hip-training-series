# HIP Lecture Series

## Introduction to HIP Exercises

For the HIP Lecture Series, the examples can be retrieved from this repository.

`git clone https://github.com/NERSC/hip-training-series`

Then check out the perlmutter branch:
`git checkout perlmutter`

This markdown document is located at `'Lecture1/01 Exercises for HIP Introduction.md'` contains 
the instructions to run the examples. 

During the training session node reservation hours, get a slurm interactive session
`salloc -N 1 -q shared -c 32 -G 1 -t 30:00 -A ntrain8 --reservation=hip_aug14`

Outside the reservation hours,
`salloc -N 1 -q interactive -c 32 -G 1 -t 30:00 -A <a project>`
use your own project instead of ntrain8 if you have a NERSC regular project.

```
module load hip
make
```

### Basic examples

`cd hip-training-series/Lecture1/HIP/vectorAdd `

For Makefile system
```
module load hip
make vectoradd
```

We can use a SLURM submission script, let's call it `hip_batch.sh`. 

```
#!/bin/bash
#SBATCH -q shared
#SBATCH -N 1
#SBATCH --gpus=1
#SBATCH -G 1
#SBATCH -t 10:00
#SBATCH -A <your project id>

module load hip
cd $HOME/HPCTrainingExamples/HIP/vectorAdd 

make vectoradd
srun -n 8 ./vectoradd
```

Submit the script
`sbatch hip_batch.sh`

Check for output in `slurm-<job-id>.out` or error in `slurm-<job-id>.err`
