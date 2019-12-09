Last name of Student 1: Narlock
First name of Student 1: Dean
Email of Student 1: deannarlock@ucsb.edu
GradeScope account name of Student 1: Dean Alexander Narlock (deannarlock@umail.ucsb.edu)
Last name of Student 2:
First name of Student 2:
Email of Student 2:
GradeScope account name of Student 2: 


----------------------------------------------------------------------------
Report for Question 1 


Parallel time for n=4K, t=1K,  4x128  threads
	- 14.773 seconds

Parallel time for n=4K, t=1K,  8x128  threads
	- 7.520 seconds

Parallel time for n=4K, t=1K,  16x128 threads
	- 5.699 seconds

Parallel time for n=4K, t=1K,  32x128 threads
	- 4.406 seconds


Why there is less speedup improvement towards 32x128 threads?
	- There is an overhead of thread initialization that counters the improved speedup. 
	- As thread count increases, this overhead becames a greater percentage of the total runtime therefor reducing efficiency


----------------------------------------------------------------------------
Report for Question 2 

Parallel time for n=4K, t=1K,  8x128  threads with shared memory
	- 7.241 seconds

Parallel time for n=4K, t=1K,  32x128 threads with shared memory
	- 4.220 seconds

Explain the reason if you see an improvement compared to Question 1 code performance.  
 	- We are able to improve run-times by using shared memory. This is because threads can access shared memory with much lower latency compared to global memory.


Explain the reason if you see less improvement when the total number of threads increases. 
	- Shared memory saves time by improved latency, but there is an initial cost of copying from global to shared memory. 
	- Once this initial cost is done, each access to shared memory is saving time. The code must have a certain number of 
	accesses to break even on the initial cost. The more accesses to shared memory, the more time-saving possible.
	- With more threads, each thread needs to access the shared memory a smaller amount of times.
	- In the above test cases, we are not changing the number of threads per block, but rather changing the number of blocks.
	- Because of this, the amount of copying each thread must do is only slightly improved, but the number of accesses to
	memory is greatly decreased, in turn reducing efficiency
	- Also, there are more calls to __syncthreads() which can have a greater overhead than the improved latency


----------------------------------------------------------------------------
Report for Question 3 
The default number of asynchronous iterations is 5 in a batch.
Parallel time and the number of actual iterations executed  for n=4K, t=1K, 8x128  threads with asynchronous Gauss Seidel
	- 0.128 seconds
	- 15 iterations

Parallel time and the number of actual ierations executed  for n=4K, t=1K,  32x128 threads with asynchronous Gauss Seidel
	- 0.0952 seconds
	- 20 iterations

Does the above Gauss Seidel -Seidel method converge  faster than the Jacobi method in this case?  
Compare performance with code of Question 1 in the above setting and explain the difference.
	- The performance differences between the GS method and the Jocobi method have to do with rate of convergence.
	- The GS method convereges with far fewer iterations that the Jocobi method.
	- This is because with each iteration, we improve the accuracy in our prediction of each variable
	- On iteration k, the jacobi method uses predictions from the k - 1 round while GS will use a more accurate
	prediction from the k round.
	- By using a more updated and accurate guess, the GS is able to converge with fewer iterations




