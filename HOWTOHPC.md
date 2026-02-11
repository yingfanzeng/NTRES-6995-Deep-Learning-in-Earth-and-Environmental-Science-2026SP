# NCAR HPC – Part I HOWTO

This document records the basic workflow I used to access NCAR HPC systems and run a simple job.
The purpose is to document the steps so I can reproduce them later.

---

## 1. Logging into NCAR HPC

Log into the NCAR HPC cluster Casper by entering the command line below in a terminal or through VS Code Remote-SSH:

```bash
ssh -XY <username>@casper.hpc.ucar.edu
```
Enter the password and complete the DUO two-factor authentication (2FA) to log in.
<img width="603" height="126" alt="image" src="https://github.com/user-attachments/assets/6999f920-0d3a-4b3a-8298-311551131b0e" />

<img width="345" height="71" alt="image" src="https://github.com/user-attachments/assets/b89417c4-ee70-46e9-aa3f-a84b14e5aa34" />

---

## 2. Submitting a Simple PBS Job

A PBS job script has the file suffix `.pbs`.
A simple example PBS script:

```bash
#!/bin/bash
#PBS -N SimpleJob
#PBS -l select=1:ncpus=1:mem=4GB:walltime=00:30:00
#PBS -j oe

module load python
python my_awesome_script.py
```

Submit the job by:

```bash
qsub simple_job.pbs
```

Check job status:

```bash
qstat -u <username>
```

Output and error logs are written to the working directory after the job finishes.

---

## 3. Uploading and Downloading Files

Upload a file from my local machine to Derecho:

```bash
scp local_file <username>@derecho.hpc.ucar.edu:/path/to/hpc/folder
```

Download a file:

```bash
scp <username>@derecho.hpc.ucar.edu:/path/to/hpc/folder/file .
```

---

## 4. Editing Files on the HPC

I edited scripts directly on the remote system using:

```bash
vim script.py
```

(Alternatively `nano` or VS Code Remote-SSH can be used.)

---

## 5. Monitoring Resources

Check running jobs:

```bash
qstat -u <username>
```

Check usage/accounting:

```bash
ncar_accounting_report
```

---

## 6. Cloning a Repository

The project repository can be cloned directly on the HPC system:

```bash
git clone https://github.com/<username>/<repo>.git
```

