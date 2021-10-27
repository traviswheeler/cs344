cs344
=====

Introduction to Parallel Programming class code, tied to this Udacity course:
https://classroom.udacity.com/courses/cs344



Running on the mtech cluster
============================

Instructions to get Cuda problem set 1 working on mtech:

(1) Log in to the mtech head node  (you need to have an account!)

(2) Add the following two lines to ~/.bashrc 

module load cuda
module load opencv

(this will keep you from needing to type those commands every time you log into the system or start an interactive shell)


(3) Clone my copy of the Udacity github repo. It contains the 
changes required to make it run on mtech:

    % cd wherever/you/want/cs344/to/be
    % git clone https://github.com/traviswheeler/cs344.git  
    
This will create a directory called cs344, which contains all of
the problem sets (plus more)

(4) Edit ProblemSet1's student_func.cu (only!)

    % cd cs344/ProblemSets/ProblemSet1/
    # Edit code for problem set 1 to your heart's content

(5) Compile; you should be in cs344/ProblemSets/ProblemSet1/

    % make
    # note: you'll get a warning about "unused parameter h_rgbaImage"
    ... Don't worry about. A note in the code explains the warning

(6) Run

    #interactive login to gpu node  
    % msub -I -l nodes=1:ppn=1 -l feature=gpunode 

    #use this command; it's the one I'll use (including the tolerance values 3 & 15)
    % ./HW1 cinque_terre_color.jpg mine.jpg cinque_terre_bw.jpg 3 15


You'll iterate over 4 - 6 until everything is working well. Mine runs like this: 

    % ./HW1 cinque_terre_color.jpg mine.jpg cinque_terre_bw.jpg 3 10
    Your code ran in: 0.060224 msecs.
    PASS

While troubleshooting, you may find it useful to see what your code 
has produced. This can be easily done by copying it from the cluster
onto your machine. Do this with (from your machine):
    % scp username@hpc.mtech.edu:/path/to/ProblemSet1/mine.jpg .  
    include the "." at the end of the line above!

... then open the jpg with your favorite viewer


Good luck!    




# Building on OS X

These instructions are for OS X 10.9 "Mavericks".

* Step 1. Build and install OpenCV. The best way to do this is with
Homebrew. However, you must slightly alter the Homebrew OpenCV
installation; you must build it with libstdc++ (instead of the default
libc++) so that it will properly link against the nVidia CUDA dev kit. 
[This entry in the Udacity discussion forums](http://forums.udacity.com/questions/100132476/cuda-55-opencv-247-os-x-maverick-it-doesnt-work) describes exactly how to build a compatible OpenCV.

* Step 2. You can now create 10.9-compatible makefiles, which will allow you to
build and run your homework on your own machine:
```
mkdir build
cd build
cmake ..
make
```

