---
title: Blog 1
layout: doc
---

# Blog 1: Lecture 11

Analyzing the Therac-25's UI

The Therac-25 was a radiation therapy machine controlled by software, not hardware. Unfortunately, there were many key flaws in the software’s design, which under certain conditions caused the machine to emit hundreds of times more radiation than intended. In this blog, I’ll evaluate the Therac-25’s UI based on the criteria discussed in lecture and suggest modifications that could have prevented it from administering fatal doses of radiation.

Speak User’s Language:

Operators of the Therac-25 reported that they would encounter up to 4 serious error messages per day. These error messages would simply read “MALFUNCTION X”, where X was a number from 1 to 64. No other information was provided on what the malfunction was or how to fix it. 

Error Tolerance:

Due to the frequency of these error messages, operators admitted that they ignored them and simply proceeded with treatment. It was later discovered that Malfunction 54 caused the fatal doses of radiation.

Malfunction 54 occured when operators entered information into the machine, which caused magnets inside it to move, and then changed the information during the 8 seconds it took the magnets to move into position. Since the magnets were already moving, they would not respond to the changes.

Safety:

The actual dosage of radiation was not displayed on the screen, so when operators administered radiation, they had no way of knowing if it would be 200 rads or 20,000 rads.

Solutions:

Firstly, I would handle more errors in the code rather than displaying an error every single time. Due to the sheer number of errors that operators encountered, they became desensitized to them.

Furthermore, I would also change the error message to not only explain why the error occurred, but also to indicate the current status of the machine. This would let operators know if the changes they made were actually made in the machine.

Another helpful change would be to prevent any input from being made while the magnets are moving. Although this would make the UI less efficient, as users would have to wait 8 seconds before making another change, it would drastically increase safety. 

Lastly, I would display the amount of radiation on the screen so that it would be extremely clear to users how much radiation they are adminstering.

Sources: https://www.youtube.com/watch?v=Ap0orGCiou8&t=4s&ab_channel=KyleHill 
