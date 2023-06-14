# Ed Morrow's Computer Science Portfolio

## Professional Self-Assessment
I have been studying for a B.S. in Computer Science with a concentration in Software Development since July 2019.

{% include youtube.html id="6ycBk1MSeTA" %}  
<br/>
## Code Review
Following is the video code review I created prior to embarking on the proposed enhancements to my code:

<!-- [![Code Review](https://img.youtube.com/vi/6ycBk1MSeTA/0.jpg)](https://www.youtube.com/watch?v=6ycBk1MSeTA) -->

## Category One: Software Design and Engineering
#### Morse Code Signalling Device
<a href="https://github.com/MaYingHu/CS350-Emerging-Systems-and-Architectures/">Original Code for Morse Code Signalling Program</a>

This project was originally created as a milestone in my *CS-350: Emerging Systems and Architectures* class: 
I chose this artefact as it showcases the skills I acquired during that course as concerns writing code for embedded systems. While my initial attempt ran correctly, the enhancements have made the code more reusable and extensible as it is now straightforward to add an arbitrary number of messages which will be signaled in the same way, and the list can be navigated either forwards or backwards depending upon which button is pressed. This shows an ability to look beyond the most basic requirements to create a better organized and more flexible system which not only meets the initial specifications but provides a basis for further development of the code.

In selecting this artefact, I hoped to particularly address the third and fourth course outcomes (to design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, and to demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals). I believe that I met those course outcomes with this artefact, as the initial code (as unwieldy as it was) would have delivered value and accomplished the goals set for it; and the enhanced code has improved the algorithm that is used to signal each message to make it flexible enough to accommodate any number of new messages with only a minimum of editing: it would required adding the new message strings to the message array and updating the variable that holds the size of the array.

In creating and then enhancing this artefact, I was reminded again of the importance of distilling code to the most fundamental level appropriate for the task to allow different parts of the code to be reused wherever possible: in this case I reduced four separate functions for controlling the LEDs to just one which would set them to any possible permutation based on an integer parameter which would serve as a bit-field (with each LED corresponding to a binary place in the integer, being switched on or off depending on whether that bit was one or zero). I also learned how disassembling the task to more fundamental components (in this case, iterating over the message character-by-character, then over each character’s Morse code representation symbol-by-symbol, and finally over each symbol phase-by-phase) was a little more work than my initial approach (directly hard-coding each message) but paid dividends when it came to changing or adding new messages, which is trivial in the enhanced version but would require the creation of new switch statements for each phase of each message, a process which was both tedious and error-prone. While over-abstracting can potentially lead down a rabbit-hole which will not ever lead to useful code, there is a happy medium where foresight can prompt us to invest some extra work in the early stages of development to greatly simplify changes further down the road, and I believe that the enhancements I made to this code represent a good example of that.

<a href="https://github.com/MaYingHu/CS350-Emerging-Systems-and-Architectures/">Enhanced Code for Morse Code Signalling Program</a>

###### Flowchart for the enhanced Morse Code Program:
![Enhancement One Flowchart](./MorseCodeFlowchart.svg)

## Category Two: Data Structures and Algorithms 
#### Linked List

The artefact I chose for this category was code for a linked list which was written in C++. I created this as a milestone in the Data Structures and Algorithms (CS260) class.

I chose to include this artefact in my portfolio because it offers an example of the knowledge I have gained of working with data structures and manipulating them using appropriate algorithms. In this case, I enhanced the code to implement additional methods that were not included originally: I added methods to insert an item into the list at a given index; to clear the list and leave it empty; to delete the list entirely; to remove an item; to delete an item at a given index; to find an item and return its index or to get an item at a particular index; to reverse the list in-place or to return a new list which is a reversal of the original; to convert the list to a C++ vector; and to sort the list in-place. For the last method mentioned, I opted for a merge sort as its worst-case runtime is O(nlogn), as it is not subject to pathological cases of the sort that reduce quicksort to O(n2) time; and the sequential-access nature of linked lists means it is better suited to those applications than quicksort anyway. However, it might be worthwhile to also implement a quicksort-by-conversion-to-array in the future, as this could perform better in some situations. 

These enhancements have resulted in code which is more modular and reusable. It was also improved over the original by addressing memory leaks in the original. These enhancements address course outcomes three and four (to design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing the trade-offs involved in design choices and to demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals) because they demonstrate my ability to consider the proper implementation of algorithms for a particular task, and to consider how code (the linked list, in this case) could be reused across multiple applications, and how the code itself should be modularized as much as possible to facilitate that end.

The biggest challenge I encountered when modifying the code was implementing the sort methods, and in fact I am still ironing out some issues with that. I also practised thinking in terms of algorithmic efficiency when working on the enhancements: for example, in the code to reverse the list in-place, I was able to come up with a solution that would work in O(n) time by making a single pass through the list and reversing the direction of the links, rather than a much more time-consuming process that would have involved beginning by navigating to the end of the list (i.e., sequentially accessing each node in turn) before redirecting them. I also had an opportunity to further practise employing pointers, which I am much more comfortable with after working on tasks like this.

## Category Three: Databases
#### Inventory Management App for Android

<a href="https://github.com/MaYingHu/CS-360-Inventory-App/tree/master">Original Code for Android Inventory App</a>

The artefact I chose for this category was code for an Android inventory management app which I developed as my final project in CS-360 (Mobile Architecture and Programming).

I chose to include this artefact in my portfolio because it offers an example of an Android app which I coded to meet user requirements for a client (albeit a fictitious one, in this case). As mobile app development is a field that I hope to move into, it seemed a suitable choice for my personal portfolio. The artefact as a whole demonstrates my ability to code simple apps in Android studio, to work to an existing specification, and to incorporate the use of a database into the app together with the appropriate security considerations. To enhance the artefact, I added two-factor authentication to the login process (requiring that the user input a six-digit one-time passcode texted to their ’phone in addition to their user name and password in order to be authenticated) and incorporated salted and hashed passwords to help to protect user credentials even in the case of a data breach.

I planned to address course outcome number five (to develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources) with this artefact, and the enhancements that I have made do indeed show an awareness of potential security concerns and an ability to overcome them. I also addressed course outcome number four (to develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources) by utilizing existing libraries (such as the Java SHA256 hashing library) to achieve my goals with this enhancement. 

In enhancing this artefact, the main obstacle I had was with reacquainting myself with the original code and then determining which additional methods and (in the case of two-factor authentication) activities I would need to add to the existing code. While that was fairly straightforward to do because I was careful to document the code in the first place, it was time-consuming. The other major challenge lay in incorporating existing Java libraries to perform the tasks I could not do myself: while I was able to write my own method to generate a 32-character alphanumeric ‘salt’ I thought it unwise to attempt to create hashes of the passwords myself, so I used the MessageDigest library instead. My main takeaway from working on this was being more systematic about debugging my code: the bugs that took the most time to detect were all very simple (in one case I was trying to write an alphanumeric salt to the database as an integer rather than as text, for example) and I could have saved myself a lot of time if I had been more patient about ensuring that these things were correct from the beginning.

###### Mockups showing Login Screen, Inventory Screen (landscape and portrait) and Add Item Screen:</p>

![App Mockups](./appMockups.svg)

Oldskool:

<p float="left">
  <img src="./appMockupsLogin.svg" width="200" />
  <img src="./appMockupsInventoryLandscape.svg" height="200" /> 
  <img src="./appMockupsInventoryPortrait.svg" width="200" />
  <img src="./appMockupsAddItem.svg" width="200" />
</p>

