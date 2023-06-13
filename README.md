# Ed Morrow's Computer Science Portfolio.

## Personal Statement
I have been studying for a B.S. in Computer Science with a concentration in Software Development since July 2019.

<iframe width="560" height="315"
  src="https://www.youtube.com/watch?v=6ycBk1MSeTA" 
  frameborder="0" 
  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" 
  allowfullscreen>
</iframe>

### Morse Code Signalling Device
I chose this artefact as it showcases the skills I acquired during that course as concerns writing code for embedded systems. While my initial attempt ran correctly, the enhancements have made the code more reusable and extensible as it is now straightforward to add an arbitrary number of messages which will be signaled in the same way, and the list can be navigated either forwards or backwards depending upon which button is pressed. This shows an ability to look beyond the most basic requirements to create a better organized and more flexible system which not only meets the initial specifications but provides a basis for further development of the code.

In selecting this artefact, I hoped to particularly address the third and fourth course outcomes (to design and evaluate computing solutions that solve a given problem using algorithmic principles and computer science practices and standards appropriate to its solution, and to demonstrate an ability to use well-founded and innovative techniques, skills, and tools in computing practices for the purpose of implementing computer solutions that deliver value and accomplish industry-specific goals). I believe that I met those course outcomes with this artefact, as the initial code (as unwieldy as it was) would have delivered value and accomplished the goals set for it; and the enhanced code has improved the algorithm that is used to signal each message to make it flexible enough to accommodate any number of new messages with only a minimum of editing: it would required adding the new message strings to the message array and updating the variable that holds the size of the array.

In creating and then enhancing this artefact, I was reminded again of the importance of distilling code to the most fundamental level appropriate for the task to allow different parts of the code to be reused wherever possible: in this case I reduced four separate functions for controlling the LEDs to just one which would set them to any possible permutation based on an integer parameter which would serve as a bit-field (with each LED corresponding to a binary place in the integer, being switched on or off depending on whether that bit was one or zero). I also learned how disassembling the task to more fundamental components (in this case, iterating over the message character-by-character, then over each character’s Morse code representation symbol-by-symbol, and finally over each symbol phase-by-phase) was a little more work than my initial approach (directly hard-coding each message) but paid dividends when it came to changing or adding new messages, which is trivial in the enhanced version but would require the creation of new switch statements for each phase of each message, a process which was both tedious and error-prone. While over-abstracting can potentially lead down a rabbit-hole which will not ever lead to useful code, there is a happy medium where foresight can prompt us to invest some extra work in the early stages of development to greatly simplify changes further down the road, and I believe that the enhancements I made to this code represent a good example of that.

![Enhancement One Flowchart](./MorseCodeFlowchart.svg)
