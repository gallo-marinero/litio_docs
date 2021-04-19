.. _script:

Submit jobs
===========

Jobs in litio should not be executed interactively, but rather through a script
that efficiently takes care of the queue and resources. Litio uses `OpenPBS
<https://www.openpbs.org/>`_.

1. Copy the script below and save it as (for example) *sendjob.pbs*.

2. Submit it from the terminal with:

   ``qsub sendjob.pbs``


This is a working script to submit jobs in litio.

.. code-block:: bash

   #!/usr/bin/env bash

   ## Define the name for this job
   #PBS -N test1
   ## Define the number of cores (ncpus)
   #PBS -l nodes=1:ppn=1
   ## Merge standard output and error files
   #PBS -j oe
   ## (Optional) Define the maximum time you want the job to be running. Default: unlimited
   ###PBS -l walltime=71:59:00
   ## (Optional) Mail is sent to you when the job starts and when it terminates or aborts
   ###PBS -m bea
   ## (Optional) Specify your email address
   ###PBS -M <username@cicenergigune.com>

   ## Create scratch directory if it does not exist
   if ! [ -d /scratch/$USER ]; then
    mkdir /scratch/$USER
   fi
   
   ## Using the job id ($PBS_JOBID), create the specific scratch directory 
   ## and hold its name as $SCRDIR
   export SCRDIR=/scratch/$USER/$PBS_JOBID
   mkdir $SCRDIR

   ## Go to scratch directory and copy everything from working directory
   cd $SCRDIR
   cp $PBS_O_WORKDIR/* .

   ## Run the code
   your_program your_input.inp

   ## Copy back the results
   cp * $PBS_O_WORKDIR/

   ## Tell PBS to wait till all files are copied
   if [ 0 == 0 ]; then
    cd $PBS_O_WORKDIR
    rm -rf $SCRDIR
   fi

.. note:: Comments and instructions
    
   ``#`` This is an instruction for the queue system

   ``##`` This is a comment

Note that lines starting with # are instructions for the queue manager (they
are not comments). You need to add more than one # to write a comment.


