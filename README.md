Download Link: https://assignmentchef.com/product/solved-csci251-assignment1-robots-as-toys
<br>
This assignment is to be implemented using procedural programming. The overall program should follow the processing of customer orders for robots from a robot construction company : <strong>RAT </strong>(Robots As Toys).

General code notes

These are some general rules about what you should and shouldn’t do.

<ol>

 <li>Your assignment should be organised into:

  <ul>

   <li>A driver file containing your main()</li>

   <li>A header file containing the prototypes for the functions you write.</li>

   <li>An implementation file containing the implementations of your functions.</li>

  </ul></li>

 <li>Provide a text file txt with instructions for compiling your code on capa.its.uow.edu.au into the executable RAT. The Readme.txt should actually be a text file, not a doc or pdf or rtf or something other than text, and the instruction should be a copy and pastable command.</li>

 <li><strong>If your code doesn’t compile on capa you will likely receive 0 for the assignment.</strong></li>

 <li>You are not allowed to use classes.</li>

 <li>You can use structs, but not member functions in them.</li>

 <li>Within your code, be consistent in your tabbing style. We want readable code.</li>

 <li>Include sensible volumes of commenting.</li>

 <li>Use appropriate variable names.</li>

 <li>Don’t leak memory.</li>

 <li>Your main() function should make it clear what is going on, and shouldn’t be too large.</li>

 <li>Other than the initial command line input, the program should run without user output. In particularthis means there shouldn’t be pauses waiting for the user to press a key.</li>

</ol>

<h1>Run structure</h1>

Once your program is compiled into the executable RAT, it must run as follows:

$ ./RAT Customers.txt Parts.txt Builders.txt Output-file

The files serve particular purposes and by purpose should be assumed to be in this order. The names and content of the files may differ, except for Parts.txt, so you shouldn’t hard code the content of the sample files into your program, or hard code the names of files into your program.

The expected structure of the input data files is given in the next section.

When you read from the data files you should report on the data read in. We should see a list of customers, a list of parts, and a list of builders; all appropriately formatted so it’s clear you have correctly partitioned the input data. It should be clear that you have correctly linked files, that should be clearer once you read the format of the data files. This report should go to standard out, not to Output-file.

Output-file is used to report on results.

The customer orders in the customers file are to be processed in the order they are given.

The file Output-file should be ordered by customer and contain a clear report on the build plan, success or otherwise in the multiple attempts, as necessary.

When you start each customer you should report to standard out the customer name, the name of the order they are intending to be built, and the builder assigned. You should also report to standard out when a build succeeds or fails. The process below explains how multiple builds may be attempted, and those should be reported on.

The process involved in managing a customer order is as follows:

<ul>

 <li>For the given customer randomly allocate a builder who is constructing the robot.</li>

 <li>Determine the overall robot complexity as 20 plus the sum of the part complexities. For example:</li>

</ul>

Sally:Snake:AEEEEEE.

Overall robot complexity = 20+15 + 6 * 2 = 47

If the complexity is greater than 100, it should be changed to exactly 100.

<ul>

 <li>Determine the overall robot variability as 5 plus the number of parts plus the variability of the builder. For example</li>

</ul>

Sally:Snake:AEEEEEE. Reliable Rover:70:1.

Overall robot variability = 5 + 7 + 1 = 13.

Report the customer name, project name, builder name, and the distribution parameters to the Output-file. Please report on the overall robot complexity too, that’s your target.

<ul>

 <li>The builder attempts to build the robot. Generate a random value from a normal distribution with mean equal to the builder’s ability and standard deviation equal to the overall robot variability just calculated.</li>

</ul>

If the random value is greater than or equal to the overall robot complexity, the build is successful.

If the random value is less than the overall robot complexity, the build fails.

<ul>

 <li>If the build succeeds you can move on to the next customer.</li>

 <li>If the build fails, the builder can re-attempt the build twice. For each re-attempt generate a random value from the same distribution as before, but for the first re-attempt add 5 and for the second re-attempt add 10.</li>

 <li>After three fails in total you should move to the next customer regardless of the result.</li>

 <li>The random value and success status for each attempt should be reported to the Output-file.</li>

</ul>

<h1>Inputs</h1>

Three data files are needed for each run of the program. The general syntax of those files is described here, and one example of each is provided on the Moodle site.

The three data files are as follows, with the colons used to separate fields and the full stop to end the line.

<ol>

 <li>Customers.txt: No more than 10 entries.</li>

</ol>

Customer name:Project name:List of parts.

Example:

Carly:Cat:ABCCCCE.

Dodgy Dan:Dog:BCACECC.

Ernie:Ettin:AABCCDD. Sally:Snake:AEEEEEE.

The Customer name is the name of the entity that submitted the order. It is a non-empty string of printable characters that may include spaces.

The Project name is chosen by the customer and is supposed to represent the type of robot to be built. Like the Customer name it is a non-empty string of printable characters that may include spaces.

The List of parts contains a list of letters with each letter corresponding to a part in the parts file. They do not need to be in alphabetical order. There shouldn’t be more than 10 parts for any order.

<ol start="2">

 <li>txt: This file corresponds to a publicly available catalogue for RAT so the content will be as provided here. You do not need to check the input validity but should check if the file is present.</li>

</ol>

Part code:Part name:Minimum:Maximum:Complexity.

A:Head:1:2:15.

B:Torso:0:6:5.

C:Leg:0:4:6.

D:Arm:0:4:8. E:Tail:0:6:2.

The part code will be a single capital letter. The minimum and maximum are limits on the number of that part type that is in proposed build. The complexity is used to determine how difficult a build will be depending on the parts added.

<ol start="3">

 <li>txt: No more than 5 entries.</li>

</ol>

Name:Ability:Variability.

Example:

Reliable Rover:70:1.

Sloppy Simon:20:4.

Technical Tom:90:3.

The name cannot be empty. The ability is an integer in the range 1 to 99 inclusive. The variability is an integer in the range 1 to 10 inclusive.