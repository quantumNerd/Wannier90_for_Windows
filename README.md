# Wannier90 for Windows

## About

This respository gives a guidance of compiling **native, efficient and multi-core parallel** version of **Wannier90** code on Windows. However, similar as other programs in Windows (program compiled on one machine will likely work on all other Windows machines), you do not need to follow this procedure yourself. Rather, **download the binary (compiled) program from the release page** and you can use it directly on your Windows machine. We have tested it on several windows computers and it worked well, but in case it does not work, please file an issue on this repository.

## Folder structure of the download

There are two folders in the download: **msmpi** and **wannier90-3.1.0**. msmpi contains Microsoft MPI which supports multi-core parallel computation. wannier90-3.1.0 contains compiled wannier90 code, with wannier90.x and postw90.x being the most important in that folder. I also keep *everything* that is in the Linux version inside, but please notice that some auxiliary programs might not work due to their dependency on Linux environment. Please also file an issue in this repository if you need that, so that we can try to adapt that to Windows.

## Usage

1. Set system environment variables
   - Search "environment variables" in the Windows search bar
   - Go to "Edit the system environment variables"
   - Click "Environment Variables..."
   - From the lower scrollable list, find the variable called "Path". Select the corresponding line, and click "Edit..." in the bottom
   - In the pop-up window, click "New"
   - Paste the full directory to the folder "msmpi" in the download (you can use "Browse..." instead). Now you will see that in the end of the list, the full path to msmpi is added.
   - Click "New" again and this time paste the full directory ofthe folder "wannier90-3.1.0".
2. Open CMD (Command Prompt)
   - Run command "mpiexec". If the evironment variables are set correctly in step 1, it should output "Microsoft MPI Startup Program" with version and options.
   - Run command "wannier90.x". If the evironment variables are set correctly in step 1, it should output "Wannier90: The Maximally Localised Wannier Function Code" with options.
   - Run command "postw90.x". If the evironment variables are set correctly in step 1, it should output "postw90: Post-processing for the Wannier90 code" with options. If not, go back to step 1.
3. Go to your calculation folder using "cd" command. For example, let's say "wannier90-3.1.0_windows_x64_parallel\wannier90-3.1.0\examples\example16-noqe". Now, run
```
wannier90.x Si
```
for serial execution, or
```
mpiexec -np 6 wannier90.x Si
```
for parallel computing on 6 CPU cores. "Si" is the name of your ".win" input file.

