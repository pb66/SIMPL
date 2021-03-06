# SIMPL

A serial interpreted minimal programming language toolkit - adapted for various microcontrollers including Arduino, ARM and MSP430.

The SIMPLinterpreter is about 300 lines of C code that allow you to control the peripherals of a microcontroller from a serial terminal connection.

It enables interaction with the hardware and peripherals using a set of serial commands - for example typing 13h will set digital pin 13 high and typing 13l will set it low. 

There are commands to access the ADC channels, perform integer arithmetic and print numerical results and strings to the terminal.

SIMPL uses single ascii characters as commands to control the hardware - and commands can be strung together to make new commands - a litte bit like FORTH.

There are 96 printable ascii characters, so this limits SIMPL to 96 unique commands.


Most recently - SIMPL runs under Arduino on STM32L433 on the myStorm BlackIce open source FPGA board  - September 2017

Previously coded in under 1024 bytes of MSP430 assembly language - Runs on MSP430G2553 Launchpad



; Serial Interpreted Microcontroller Programming Language

;-------------------------------------------------------------------------------

; SIMPL - a very small Forth Inspired Extensible Language 



; Type ? to get list of commands

; Type H or M to get a test message

; Ken Boak   May to September 2017

; Loops, I/O, Strings and Delays added

Here are some quick instructions - it uses lower case commands usually preceded by an integer number 32767 max

1234p   Print the number 1234

14sp    Take an ADC sample from pin 14 and print it as an integer

_Hello World_   Print the text string contained between the underscores

47d     Define the GPIO pin to be used for input or output

1o      Output logic 1 to the previously defined output pin

0o      Output logic 0 to the previously defined output pin

1000m   A delay of 1000 milliseconds

100u    A delay of 100 microseconds

b       Print the current value of the millisecond counter

c       Print the current valule of the microsecond counter

{ }     Create a loop structure

k       The current value of the loop counter - decrements each time around the loop

Make a LED on pin 47 flash 10 times

47d10{1o100m0o100m}

1o and 0o can be replaced with h and l (HIGH and LOW)

47l Initially set LED pin low

10{h200ml200m}      Flash the LED



1000{1o250u0o250u}  Create a short audio tone on pin 47

100{14sp}    Take 100 ADC samples on pin 14 (AN0) and print them out

10 11+p      Add 10 and 11 and print the result


;		Upper case letters are used to define Users "words"

;		User Routines are defined by capital letters starting  with colon : and end with semicolon ;

;		eg  :F10(100mh200ml);		;	Flash the led 10 times - high for 100mS and low for 200mS

;		You can play sequences of notes through a small speaker  ABC etc

;   :A40{h1106ul1106u);		 musical note A

;   :B5{h986ul986u);			 musical note B

;   :C51{h929ul929u);			 musical note C

;   :D57{h825ul825u);			 musical note D

;   :E64{h733ul733u);			 musical note E

;   :F72{h690ul691u);			 musical note F

;   :G81{h613ul613u);			 musical note G

;   :H_Hello World, and welcome to SIMPL_;   A Banner Message

;   Examples of SIMPL phrases

; 	eg add 123 and 456 and print the result to the terminal

; 	123 456+p

;	  Loop 10 times printing "Spurs are Fab!"

; 	10(_Spurs are Fab!_)

;   Flash a LED 10 times 100mS on 200mS off

;   10(h100ml200m)

;   Toggle a port pin at 1MHz   1000(hlhlhlhlhlhlhlhlhlhl)



;	Lower case letters are used for more complex commands

; a

; b      print the milliseconds counter - for timing durations

; c      print the microseconds counter

; d      Define an I/O pin

; e

; f

; g

; h       set port pin high

; i       input byte from port

; j

; k       access the loop counter variable

; l       set port pin low

; m       milliseconds delay

; n

; o       output bit to port

; p       print the top of stack to terminal

; q       print the ascii character at given RAM location

; r       read input pin

; s       sample the ADC

; t

; u       microseconds delay

; v

; w

; x

; y

; z

; Maths operators +  - * and / are recognised




