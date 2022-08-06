# Chess-Clock-Redesign
7 Segment display chess clock.

As of late, I have become more interested in hardware and circuit design. To help myself learn more about digital design, I am revisiting a project from my first year of college, the EENG 1910 chess clock. That was the project I came up with for our final project and presentation in that class, which was intro to electrical engineering.

My old chess clock was basically just some C++ on an arduino, 2 buttons, and an LCD. Someone had suggested to me that I just make it all out of digital ICs but back then that seemed impossible. Now that I have some experience with digital circuit design from EENG 2700 (Digital Logic), it has been relatively simple to come up with a design for the chess clock.

The general design is as follows:

Counting and Display:
I want to have two clock displays, each with 4 digits. Each digit will be a 7 segment display. Each 7 segment display will each be driven by a CD40110BE, which is a decade up-down counter that outputs directly to the pins on a seven segment display. The CD40110BE is easily cascaded. *Even though it's a fairly simple chip by modern standards, I was still so excited by all of the functionality, it's so convenient!*

Timing:
There will be a 1hz clock using a 32.768 kHz oscillator and two 4060 chips to divide it.

*A Note on Buttons: all buttons will be debounced with schmitt triggers.*

Settings Mode:
The user will be able to set the minutes of their time control from 1 minute to 99 minutes using a button underneath the minute digits on both displays. Once the user is done setting the display, the system clock will be enabled by one of the two user buttons at the start of the game. In Settings Mode the system clock will be disabled.

Game Mode:
Game Mode is entered when one of the users presses one of the two buttons. Once a button is pressed, the opposite display will begin to decrement time. This will continue until the button corresponding to the decrementing display is pressed. Once this occurs, the display will be held and the opposite display will begin to decrement. Holding each display is quite simple, it only requires a HIGH input on the HOLD pin of the CD40110BE.

Reset: 
A single reset button will be able to reset both clock displays, by sending the pulse from VCC to the reset pin on all of the counters. The reset button will send the system back to Settings Mode by also disabling the system clock.

Power:
The power supply will be a generic DC barrel jack with a linear regulator IC.
