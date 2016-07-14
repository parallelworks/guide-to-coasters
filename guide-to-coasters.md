
#What are coasters?

![Image of coffee coasters]
(http://www.holycool.net/wp-content/uploads/2015/07/Coffee-Inspired-Leather-Coasters.jpg)

(Not these coasters). 

Coasters are a job submission tool used by the Swift parallel scripting language.
Coasters are written in Java.
For a detailed explanation, check [this research paper written at Argonne National Laboratory](https://www.researchgate.net/publication/216293486_Flexible_Cloud_Computing_through_Swift_Coasters)


This explanation is a very rough explanation right now, but will be updated 
later. Right now, I'm assuming you have some knowledge of parallel computing,
particularly high performance computing (batch/cluster jobs).


Typically, when submitting jobs to clusters, jobs wait a few minutes in the queue, 
almost irrespective of the job walltime. 
So if you have lots of short jobs, say 40 short jobs, you would spend most of the time waiting, 
and not much time actually running the jobs.

Coasters are designed to take a computer node in a cluster and 
then quickly run lots of small jobs--”coasting” in to the job.
Once a job completes, you can almost instantly get a second job done.

Imagine you order a bunch of small items from Amazon prime. 
Amazon doesn’t ship them individually, because there are non-trivial costs associated with every item you ship. 
You ship them all in one package, and then you can quickly unpack one after another.


#What else are coasters good for?

Coasters are a useful general job execution tool, 
since they already have an infrastructure in place for starting up instances and distributing jobs. 
Rather than reinventing the wheel, we can use coasters for starting up instances this way.

As the creators note,
“In terms of usability, it was deemed necessary to not require users to log into remote systems 
and prepare services or configure compute nodes. After all, when plugging a desk lamp into a power outlet, 
one is not required to adjust knobs inside the power plant or make a separate contract
with the electricity provider before turning the lamp on."

So, coasters make things fast and easy. Well, easy by large scale computing
standards, at least.


#What are the main parts of coasters?

There are three main parts of coasters ("the coaster system"): 
1. the coaster client
2. the coaster service
3. the coaster workers 




My explanations aren't precise (for now), but in my experience, this is how the different parts function:

When using Swift, the coaster client is built into the swift configurations. 
The coaster client is also built into the cog-job-submit CLI tool. 
The coaster client basically is the mechanism that allows coasters to be used by jobs,
"which provides an API used to establish a connection to and communicate with a service".



The coaster service refers to the service (usually) started on the head node, 
the “source” of jobs. A coaster service is started for a target cluster,
and then jobs can be submitted. It maintains an internal queue.

The coaster service has a periodic worker allocation mechanism,
which determines count, walltime, and partitioning of workers, and submits this
to the local resource manager.

### BUT WHAT ARE WORKERS?

The workers run on instances. If I start 10 workers, I can connect
these back to the coaster service. (Pictures will be inserted).


# Coasters Tutorial

# First: manually start coaster service and worker separately, on a local machine.

