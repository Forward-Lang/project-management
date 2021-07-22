# project-management
Create a Gantt Chart from Github issues

## Gantt charts

A Gantt chart is a type of horizontal bar chart,  
where the X-axis is each task,  
while the Y-axis is the timeline (could be days, weeks, months, etc.).  
The magnitude of each bar is the duration of the task.  

A task may have a start- and end-date,  
it may also have an indication of its progress, [TODO]  
and its dependencies.  

> NB: A task's start- and end-date,  
> are __not__ the same as its creation- and due-date. [TODO]

For defining dependencies and in turn progress,  
Gantt charts usually rely on a work-breakdown structure.  

### Work-breakdown structure (WBS) 

In a WBS, a parent task is 100% completed when all (ie. 100%) of its children are completed.  
This is the 100% rule,
and has the important property that a parent task may __not__ be more than the sum of its parts.  
In other words,
a project definition should contain 100% of the necessary actions to complete the project.

### Time-dependencies


* Start to Start: When Task A starts then Task B starts
* [TODO: StF]
* Finish to Start: When Task A finishes then Task B starts
* Finish to Finish: When Task A finishes then Task B finishes 

Finish to Start, is the traditional sequential approach to task management.  
Start to Start, and Finish to Finish, allow for parallel execution of tasks.
[TODO: StF]

![GanttChartAnatomy](https://upload.wikimedia.org/wikipedia/commons/5/57/GanttChartAnatomy.svg)


#### Examples with no sub-tasks

In a traditional approach, you might have:

1. Step one
2. Step two
3. Step three

Doing them sequentially:  
Step two is started when Step one is done,  
Step three is started when Step two is done;  
ie this is an __ordered__ list.  

-----------------------------------------------------

Here is another example that perhaps better represents github issues:

* Task A 
* Task B
* Task C

This is an __un-ordered__ list.  
Tasks are completed in any order,  
no dependency between them is specified.  

-----------------------------------------------------

Finally here is an example using StS and FtS

1. Step one, start here, no dependencies
2. Step two, FtS, depends on Step one being finished 
3. Step three, StS, depends on Step two starting

#### Examples with sub-tasks

Here is an example with sub-tasks:

* Task A 
  * Task B
  * Task C
* Task D
* Task E

Using the 100% rule,
Task A wouldn't be complete until both Task B and C are completed.

Ignoring the 100% rule,


-----------------------------------------------------

Here is an example using StS, FtS, and FtF

1. Project A
  1. Step one, start here, no dependencies
  2. Step two, FtS, depends on Step one being finished 
  3. Step three, StS, depends on Step two starting
2. Celebrate Project A's completion, FtF, depends on Step one being finished 


#### Implications of Start- and End-dates

* Start to Start: Start-date depends on another task
* Start to Finish: End-date depends on another task
* Finish to Start: Start-date depends on another task
* Finish to Finish: End-date depends on another task

|Dependency|Start       |End         |
|----------|------------|------------|
|None      | YYYY-MM-DD | YYYY-MM-DD |
|StS       | Depends on |            |
|StF       |            | Depends on |
|FtS       | Depends on |            |
|FtF       |            | Depends on |


#### Format

Issue `#25`

```yml
depends on: #14 completion
start: YYYY-MM-DD
end:   YYYY-MM-DD

Explanation of issue
```

## Graph

A naive implementation would set the duration of a parent task  
to the sum of the duration its children, due to the 100% rule.  
Unfortunately this doesn't take into account slack/buffer time, eg weekends.

A parent task has an implied StS and FtF relationship with its children.  
A parent task starts when the first child task starts, and  
ends when the last child task ends.

### Every task has a dependency?

If I had to create a Gantt chart from a simple markdown list,
this is how I would specify it:

1. Task A: Starts with Task B, Ends with Task D
  1. Task B: 
  2. Task C: Starts on completion of Task B 
  3. Task D: Starts on completion of Task C
2. Task E: Starts on completion of Task A & Starts with Task F, Ends with Task G
  1. Task F: 
  2. Task G: Starts on completion of Task F
3. Task H: Starts on completion of Task E
  * Task I
  * Task J
  * Task K




## Github issues
https://docs.github.com/en/rest/reference/issues#list-repository-issues


## For more info see:
- https://en.wikipedia.org/wiki/Gantt_chart
- https://en.wikipedia.org/wiki/Work_breakdown_structure
- https://en.wikipedia.org/wiki/Dependency_(project_management)
- https://en.wikipedia.org/wiki/ISO_8601
