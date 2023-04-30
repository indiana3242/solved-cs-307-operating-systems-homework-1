Download Link: https://assignmentchef.com/product/solved-cs-307-operating-systems-homework-1
<br>



<h1>Airline Reservation System</h1>

For this homework, you will simulate a simple Airline Reservation System which will involve accessing shared resources. In real life, there are travel agencies who try to reserve seats for their customers. When a customer asks for a seat from a specific flight, the agency checks if there is an empty seat in the aircraft and reserves it immediately (if there is any). A customer can reserve more than one seat if needed. Since there are a lot of travel agencies out there, the reservations will be done based on FCFS (first come, first served) strategy. Only one reservations can be made on a seat, so there will be no overbooking. There will be one thread per agency simulating the activities of that agency. When an agency thread is booking a seat, the rest will do busy waiting.

You will implement the following using POSIX threads:

<ul>

 <li><strong><u>The Main Reservation System:</u></strong> This is the main thread which initiates 3 other threads called TravelAgency1, TravelAgency2 and TravelAgency3 together with a 2-D array of fixed size representing the seats in a plane. It will then let the three travel agency threads access the aircraft seats and do a reservation if possible. Note that this 2-D array representing the seats is a shared data structure, so the travel agency threads can access and update it. Accessing a shared data structure may cause a race condition. If the flight is full, meaning that the shared 2-D array is fully marked, then main thread terminates the execution of travel agency threads and print the seats to the screen.</li>

 <li><strong><u>Travel Agency Thread:</u></strong> These three agencies will be the replica of each other since they are processing the same task. They will do the same routine until they are terminated. The agent thread should check the shared memory location, if it can access it, it should check if the flight is full or not, then reserve any seats and then leave the shared memory. If the reservation is done it should say “Seat Number X, Seat Number Y … are reserved by TravelAgencyTAI” where X, Y, .. is the seat numbers reserved (technically the indexes of the marked cells of the array in the shared memory) and TAI is the id of the TravelAgency, it can be 1 or 2 or 3 since we are going to have three agencies in total for the sake of simplicity. When an agent thread enters/ exits the shared memory area, it should print messages to the console to trace. <strong><u>Implementation Details and Pseudo Algorithm</u></strong>.</li>

</ul>

<u>Main thread:</u>

You will first create a Matrix M with size 2×50 and each of the cells of the matrix will represent a seat in the airplane. All the cells will initially be marked as 0.

Seat plan is done according to this convention:

<table width="555">

 <tbody>

  <tr>

   <td width="62">1</td>

   <td width="62">3</td>

   <td width="62">5</td>

   <td width="62">7</td>

   <td width="62">9</td>

   <td width="62">11</td>

   <td width="62">…</td>

   <td width="62">…</td>

   <td width="61">99</td>

  </tr>

  <tr>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="61">0</td>

  </tr>

  <tr>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="62">0</td>

   <td width="61">0</td>

  </tr>

  <tr>

   <td width="62">2</td>

   <td width="62">4</td>

   <td width="62">6</td>

   <td width="62">8</td>

   <td width="62">10</td>

   <td width="62">12</td>

   <td width="62">…</td>

   <td width="62">…</td>

   <td width="61">100</td>

  </tr>

 </tbody>

</table>

Where M<sub>11 </sub>corresponds to seat number 1, M<sub>21 </sub>corresponds to seat number 2 and M<sub>12 </sub>corresponds to seat number 3 etc.

After you create your three threads, your main thread’s job is to constantly check whether the matrix M is full or not. It is full when all the cells in the matrix are non-zero.

When Main thread sees that the Matrix is full, it will first finish the execution of the other 3 threads and then it will print the Matrix to the console.

Thread 1 &amp; Thread 2 &amp; Thread 3:

They will run concurrently, and their jobs are;

<ol>

 <li>Create a random seat number and check if that seat is reserved or not.</li>

 <li>If it is reserved create another random seat number until you find an empty seat.</li>

 <li>Reserve it and mark it as 1 or 2 or 3 according to the reserver thread number ( if thread 1 reserves it then it marks it as 1; if thread 2 reserves it, it marks it as 2 and if thread 3 reserves it, it marks it as 3).</li>

</ol>

Since they will run concurrently we need some kind of synchronization mechanism and for that, we will use busy waiting.

Remainder of the busy waiting algorithm and the pseudo code:

<table width="641">

 <tbody>

  <tr>

   <td width="214"><strong>T1</strong></td>

   <td width="214"><strong>T2</strong></td>

   <td width="214"><strong>T3</strong></td>

  </tr>

  <tr>

   <td width="214"><strong>while</strong><strong>(</strong><strong>true</strong><strong>) {   </strong><strong>while</strong><strong>(turn!=0);   </strong><strong>//Critical region </strong><strong>  //Do steps a, b and c </strong><strong>}</strong></td>

   <td width="214"><strong>while</strong><strong>(</strong><strong>true</strong><strong>) {   </strong><strong>while</strong><strong>(turn!=1);   </strong><strong>//Critical region </strong><strong>  //Do steps a, b and c </strong><strong>}</strong></td>

   <td width="214"><strong>while</strong><strong>(</strong><strong>true</strong><strong>) {   </strong><strong>while</strong><strong>(turn!=2);   </strong><strong>//Critical region </strong><strong>  //Do steps a, b and c </strong><strong>}</strong></td>

  </tr>

 </tbody>

</table>

Please refer to the POSIX thread examples in your recitation notes to see the detailed implementation of pthreads.

<strong>Submission Guides: </strong>

Solutions should be submitted in a zip achieve, name your zip achieve as: <strong><em>YourNameSurname_ID_hw1.zip</em></strong> and submit to <strong>SUcourse</strong>. Note that, your system time and SUcourse server’s time may not be synchronized so do not wait the last minutes to submit your solution. Only the solutions in the SUcourse system will be graded. Other submissions, such as emailing to instructor or assistants, will not be graded.