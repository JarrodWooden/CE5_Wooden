#Computer Exercise 5

------------Jarrod Wooden--------------

##Part One

```
addi $s0, $0, 44
addi $s1, $0, -37
add $s2, $s0, $s1
sw $s2, 0x54($0)
```

-load register s0 with decimal 44
-load register s1 with decimal -37
-add the two together and store at s2
-write s2 to the hex address x54

##Part Two

First I needed to create the corresponding machine code for the assembly code from Part One

First I wrote the decimal values for the assembly code from part one and changed those decimal values to binary.
Then I changed the binary values to hexidecimal.

After I had the hexidecimal I was able to write that code into the testbench for mips and simulate assembly instructions.

Below is the inserted code for the hexidecimal instructions in the testbench:

```
			instr <= X"2010002C";
			wait for clk_period;
			instr <= X"2011FFDB";
			wait for clk_period;
			instr <= X"02119020";
			wait for clk_period;
			instr <= X"AC120054";
```

After I ran the simulation I wasnt able to tell if the simulation worked with the default values shows


Therefore I had to manually insert the value I needed into the simulation.

I inserted the values I needed and the picture of the simulation is below:


![alt text](https://raw.githubusercontent.com/JarrodWooden/CE5_Wooden/master/Part2SimulationPicture.PNG "Simulation Picture for Part Two")


I knew that the simulation worked because the value stored in [18] is 7, [17] is -37, and [16] is 44

which means the correct values are stored in `$s2`, `$s1`, and `$s1`. :)



