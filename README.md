# Ed Morrow's Computer Science Portfolio

## Professional Self-Assessment

I have been studying for a B.S. in Computer Science with a concentration in Software Engineering since July 2019. During that time, I have been exposed to several topics in computer science of which I had very little knowledge previously. Most notable among those would be the fields of Database Management and Data 
Analytics: in particular, the *CS-340: Client/Server Development* course, which introduced me to non-relational databases (MongoDB, in this case) was especially interesting, as was *CS-350: Emerging Systems Architecture and Technology* class. *CS-405: Secure Coding* and *CS-410: Software Reverse Engineering* also provided a structured overview of subjects that I had some familiarity with but had not studied rigorously.

Besides exposing me to topics which I had only a piecemeal knowledge of, which I had put off in favor of other, more immediately accessible or engaging subjects, or had simply never heard of, it also developed my confidence by forcing me to quickly get up to speed with new topics and new projects each term and working to deliver work according to the deadlines prescribed by the course. While I have also learned a great deal through self-study, both prior to and during working on this degree, working according to one’s own schedule does not always give the same feeling of competence in a subject that working according to formal requirements and timelines can.

During this capstone class (*CS-499: Computer Science Capstone*) I have reviewed the work I have submitted throughout my program and selected artefacts to enhance from three categories: Software Design and Engineering, Algorithms and Data Structure and Databases. The artefacts were selected to address the following course outcomes:

1. Employ strategies for building collaborative environments that enable diverse audiences to support organizational decision making in the field of computer science;
2. Design, develop, and deliver professional-quality oral, written, and visual communications that are coherent, technically sound, and appropriately adapted to specific audiences and contexts;
3. Design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, while managing the trade-offs involved in design choices (data structures and algorithms);
4. Demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals (software engineering/design/database);
5. Develop a security mindset that anticipates adversarial exploits in software architecture and designs to expose potential vulnerabilities, mitigate design flaws, and ensure privacy and enhanced security of data and resources.

Working on these enhancements gave me the satisfaction of reflecting on what I have achieved so far but also recognizing how much more I am able to bring to these projects in light of what I have learned since. The opportunity to benefit from feedback from our instructor is also something that I have been grateful for over the duration of this final class.

## Code Review
Following is the video code review I created prior to embarking on the proposed enhancements to my code:

{% include youtube.html id="6ycBk1MSeTA" %}  
<br/>

## Category One: Software Design and Engineering
#### Morse Code Signalling Device
<a href="https://github.com/MaYingHu/CS350-Emerging-Systems-and-Architectures/">Original Code for Morse Code Signalling Program</a>

The artefact I chose to enhance for this category was a program to drive a Texas Instruments developer board (the <a href="https://www.ti.com/product/CC3220S?utm_source=google&utm_medium=cpc&utm_campaign=epd-con-null-prodfolderdynamic-cpc-pf-google-wwe_int&utm_content=prodfolddynamic&ds_k=DYNAMIC+SEARCH+ADS&DCM=yes&gclid=CjwKCAjwyqWkBhBMEiwAp2yUFiHRiiUVbY2-NhIi8TBkDs9W6MIYJajMIaiPet_6u3Or9EIftjTzCBoCpBEQAvD_BwE&gclsrc=aw.ds">*TI CS3220S*</a>) to signal one of two Morse code messages on its LEDs and to switch between them (after completing the message in progress) at the press of a button. I created this as the third and final milestone of my *CS-350: Emerging Systems and Architectures* class.

I chose this artefact because it showcases the skills I acquired writing code for embedded systems, a field of which I had next to no practical experience prior to starting the class.

As part of my *CS-499: Computer Science Capstone* class, I performed the following enhancements:

1. I simplified the functions employed to drive the LEDs from one per possible permutation to one total, taking a bit-field as function argument (with each bit corresponding to the state of a particular LED): this not only streamlined the existing code but would also make it much simpler to extend if a singalling mechanism with more than two elements were to be employed in the future;
2. I decomposed the signalling function into its most fundamental elements. In my initial submission, I had hardcoded each message as a switch statement examining every possible 500*ms* phase in the message's lifetime, an approach which was both tedious and error-prone. For the enhancement, only the individual Morse symbols (*i.e.*, the dot, the dash and the pause) were taken phase-by-phase: the message as a whole was iterated over character-by-character, each character in turn was transcribed into its Morse equivalent, and then that Morse code was iterated over with each symbol being signalled phase-by-phase;
3. I created a function containing a switch statement to transcribe characters into their Morse equivalent in order to facilitate the above enhancement. Since not all characters have a Morse equivalent, I made the decision to replace all 'unsignalable' cahracters with a space;
4. I stored the available messages in an array, and separated the button functions to cycle forwards or backwards through that array (whereas previously each had just switched from one message to the other). The user then need only add or remove strings from that array to change the selection of messages available.

While my initial attempt ran correctly, the enhancements have made the code more reusable and extendable as it is now straightforward to add an arbitrary number of messages which will be signaled in the same way, and the list can be navigated either forwards or backwards depending upon which button is pressed. This shows an ability to look beyond the most basic requirements to create a better-organized and more flexible system which not only meets the initial specifications but provides a basis for further development of the code.

This enhanced artefact demonstrates my ability to design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, because I developed it beyond the most obvious approach (at lesast, the most obvious to me) to achieve the most basic functionality required and instead abstracted the logic to the point where it can signal any message that is passed to it: all that would be required would be to add or remove strings from the array of messages, and those would then be available to signal, too. The heart of the code — which takes a message charcter-by-character, converts each character to its Morse code equivalent and then iterates over that Morse code symbol-by-symbol (symbols being dots, dashes or pauses between them), signalling each symbol by 500*ms* phases (500*ms* being the greatest common denominator between all symbols and pauses) — is reproduced below:

###### Code for the signal_message() function:
```c
/* iterate over message, character by character,
 * convert each character to Morse code, then
 * iterate over the Morse string symbol by symbol
 * and display each in turn, phase by phase, with the
 * intermediate pauses added */
void signal_message()
{
  /* initialize character and string variables */
  char character;
  char symbol;

  /* iterate over characters in message */
  character = messages[message_index][character_index];
  if (character != '\0') {

    /* assume that message is still in progress */
    message_ended = 0;

    /* iterate over symbols in character */
    symbol = get_morse(character)[symbol_index];
    if (symbol != '\0') {

      /* signal current symbol, phase by phase */
      switch (symbol) {
        case '.':
            if (phase < dot_len) {
                signal_dot(phase);
                ++phase;
            }
            else {
                ++symbol_index;
                symbol = get_morse(character)[symbol_index];
                phase = 0;
            }
          break;

        case '-':
          if (phase < dash_len) {
            signal_dash(phase);
            ++phase;
          }
          else {
              ++symbol_index;
              symbol = get_morse(character)[symbol_index];
              phase = 0;
          }
          break;

        /* space will fall through to default case, which will 
        effectively replace unknown characters with a space */
        case ' ':

        default:
          if (phase < word_pause_len) {
            word_pause(phase);
            ++phase;
          }

          /* get next symbol and reset phase to 0 */
          else {
              ++symbol_index;
              symbol = get_morse(character)[symbol_index];
              phase = 0;
          }
          break;
      }
    }

    else {
      /* pause between characters */
      if (phase <= character_pause_len) {
        character_pause(phase);
        ++phase;
      }

      /* get next character and reset symbol_index and phase to 0 */
      else {
        ++character_index;
        character = messages[message_index][character_index];
        symbol_index = 0;
        phase = 0;
      }
    }
  }

  else {
    /* pause between messages */
    if (phase <= word_pause_len) {
      word_pause(phase);
      ++phase;
    }

    /* set message_ended flag to 1 and reset phase, 
    symbol_index and character_index to 0 */
    else {
      message_ended = 1;
      phase = 0;
      symbol_index = 0;
      character_index = 0;
    }
  }
}
```

The enhanced code also demonstrates and ability to design, develop, and deliver professional-quality oral, written, and visual communications that are coherent, technically sound, and appropriately adapted to specific audiences and contexts, and also to employ strategies for building collaborative environments that enable diverse audiences to support organizational decision making in the field of computer science: the documentation for this project included a flow-chart that would allow stakeholders to understand the workings of the program without having to understand the code itself.

###### Flowchart for the enhanced Morse Code Program:
![Enhancement One Flowchart](./MorseCodeFlowchart.svg)

*It also showcases my ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals). I believe that I met those course outcomes with this artefact, as the initial code (as unwieldy as it was) would have delivered value and accomplished the goals set for it; and the enhanced code has improved the algorithm that is used to signal each message to make it flexible enough to accommodate any number of new messages with only a minimum of editing: it would required adding the new message strings to the message array and updating the variable that holds the size of the array.*

In creating and then enhancing this artefact, I was reminded again of the importance of distilling code down to the most fundamental level appropriate for the task to allow different parts of the code to be reused wherever possible: in this case I reduced four separate functions for controlling the LEDs to just one which would set them to any possible permutation based on an integer parameter which would serve as a bit-field (with each LED corresponding to a binary place in the integer, being switched on or off depending on whether that bit was one or zero). I also learned how disassembling the task to more fundamental components (in this case, iterating over the message character-by-character, then over each character’s Morse code representation symbol-by-symbol, and finally over each symbol phase-by-phase) was a little more work than my initial approach (directly hard-coding each message) but paid dividends when it came to changing or adding new messages, which is trivial in the enhanced version but would require the rather laborious creation of new switch statements for each phase of each new message. While over-abstracting can potentially lead us down a rabbit-hole which will not ever lead to useful code, there is a happy medium where foresight can prompt us to invest some extra work in the early stages of development to greatly simplify changes further down the road, and I the enhancements I made to this code represent a good example of that.

<a href="https://github.com/MaYingHu/CS350-Emerging-Systems-and-Architectures/">Enhanced Code for Morse Code Signalling Program</a>

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

###### Mockups showing Login Screen, Inventory Screen (landscape and portrait) and Add Item Screen:

![App Mockups](./appMockups.svg)
