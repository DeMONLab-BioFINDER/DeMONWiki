# Servers

This chapter is about our common server resources

## Bianca
Bianca is a national cluster focusing on **sensitive data**, which is part of the NAISS SENS project. There's no internet connection, so every package, software, or data should be built/collected elsewhere and then uploaded to Bianca.

Bianca provides 4480 cores in the form of 204 dual CPU (Intel Xeon E5-2630 v3) Huawei XH620 V3 nodes with 128GB memory, 75 fat nodes with 256GB of memory, 15 nodes with 512GB of memory, and ten nodes with two NVIDIA A100 40GB GPUs each.

**!!! Everything you need is the** [Detailed official guidelines](https://docs.uppmax.uu.se/cluster_guides/bianca/)

I will list out the things for you to get an easy start below

### Set up your Bianca:
1. Register an account at [NAISS SUPR](https://supr.naiss.se/person/register/) using your **Lund email** - [Step by step registration guide](https://docs.uppmax.uu.se/getting_started/supr_register/)
2. Ask Jake to add you to one of the projects lab applied to under Bianca
3. You will now have a Bianca account on your NAISS SUPR project tab, remeber to set up password for your account
<img width="222" height="199" alt="Screenshot 2026-02-25 at 00 45 45" src="https://github.com/user-attachments/assets/13e63abf-42d5-444a-b537-a16c1c6d8328" />

4. Set up second factor identification, follow this [guideline](https://docs.uppmax.uu.se/getting_started/get_uppmax_2fa/)
5. Log in to Bicanca
    1) using terminal `python ssh -A [user]@bianca.uppmax.uu.se`
    2) using website GUI: Go to https://bianca.uppmax.uu.se


### File transfer:
using `rsync`
1. Log in to Transit: `ssh [username]@transit.uppmax.uu.se`
2. Mount a Bianca project: `mount_wharf [project_id]`
3. Upload files from your local desktop to Bianca: `rsync [my_local_file] [username]@transit.uppmax.uu.se:[project_id]`
4. Download files from Bianca to your local computer: `rsync [username]@transit.uppmax.uu.se:[project_id]/[file_in_wharf] .`

More information please refer to the [Detailed Guideline](https://docs.uppmax.uu.se/cluster_guides/transfer_bianca/)

### Existing modules
Please always check whether the software/package exists before doing the installation, using:
```bash
module avail
```

### Create Conda environment
1. Create your own Conda environment on `Rackham` or `transit` /or other linux computer/
> (*computer with Internet and same amd64 architecture *)
> conda already installed or activated
```bash
$ conda create -n my_env python=x.x module_name
$ conda activate my_env
$(my_env) 
# make your installation then pack your environment
$ conda install [your required packages]
```
2. Pack your environment using `conda-pack`
```bash
# install conda-pack first
$(my_env) conda install -c conda-forge conda-pack
# Deactivate the environment
$(my_env) conda deactivate
# Pack environment my_env into out_name.tar.gz
$ conda pack -n my_env -o out_name.tar.gz
```
3. Transfer your packed conda environment (e.g. `out_name.tar.gz`) to `Bianca` (follow the File transfer guide)
4. Unpack and setup environment on Bianca
> On Bianca (computer without Internet)
```bash
# activate conda -- you can add these two lines to your ~/.bashrc file, so that you don't need to activate conda evert time
$ source /sw/apps/conda/latest/rackham_stage/etc/profile.d/conda.sh
$ export CONDA_ENVS_PATH=/proj/sensxxxxx/conda_enviroments ## this is where you put your conda environment, recommend your user home folder

# Unpack environment into directory `my_env`
#$ cd $CONDA_ENVS_PATH
$ mkdir -p $CONDA_ENVS_PATH/my_env
$ tar -xzf my_env.tar.gz -C $CONDA_ENVS_PATH/my_env

# Activate the environment. This adds `my_env/bin` to your path
$ source $CONDA_ENVS_PATH/my_env/bin/activate

# Cleanup prefixes from in the active environment.
(my_env) $ conda-unpack

# Deactivate the environment to remove it from your path
(my_env) $ source my_env/bin/deactivate
```

## Berzelius


## COSMOS-SENS
