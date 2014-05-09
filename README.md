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


##Part3


First to be able to start on part three I needed to make the truth table for what signals the `ori` instruction would 
assert.

It was plain to see from looking at the truth table that I was making and thinking about the control path and how the
`ori` instruction would fit into the path, I would need another control signal and another multiplexer.

Below you can see that I added the `ExtOp` to determine when a multiplexer would choose between the zero extend or the 
sign extend from the control path graph.

Below you can see my truth table:

![alt text](https://raw.githubusercontent.com/JarrodWooden/CE5_Wooden/master/Truth_Table.jpg "The Truth Table")


Next step to my design process was figuring out how to implement the truth table on the control path graph.

First what I went ahead and did was added the control signal, `ExtOp`, the zero extend symbol, and a multiplexer.

The only other thing I needed to figure out was how to hook up all the new parts I put into the control path.

First I connected the control signal to the multiplexer to choose between the signextend (assert a zero) and the
zero extend (assert a one). Then I connected the 15 downto 0 to both the sign extend and the zero extend. I then
connected the new multiplexer to the `1` of the old multiplexer of sign extend.

Below is a picture of the control path I made to implement the `ori` instruction:

![alt text](https://raw.githubusercontent.com/JarrodWooden/CE5_Wooden/master/Datapath_Drawing.jpg "Datapath Drawing")

After I had everything hooked up I wrote out what the instruction would be to make the `ori` work and wrote out the 
machine code and OR'd the values together and changed it to a hexidecimal number to test what the value should be
after I implement my design into the vhdl mips design.

The simple easy story of how I implemented the design was that I used what I drew on the control path graph to
determine sections of the vhdl that I would need to change to implement my design. I also semi followed the jump
instruction because that was the last thing added and I wanted to see how the instruction was implemented as well.

***Basically, I followed the graph of what signal and wires I needed and where I needed to hook those wires up to.

You can reference the VHDL mips code above if you would like to see exactly the syntax I used for everything looked like.
Just remember to try to find names for things that reference the zero extender because that is mostly what I named
my wires to.

After I got the code figured out, it was time to test my design with the testbench. I inserted the instruction into
the test bench which looked like this because the instructions were inserted with hexidecimal:

			```
			instr <= X"2010002C";
			wait for clk_period;
			instr <= X"2011FFDB";
			wait for clk_period;
			instr <= X"02119020";
			wait for clk_period;
			instr <= X"AC120054";
			wait for clk_period;
			instr <= X"36538000";
			```

Then I ran the simulation. The waverform that Captian Silva supplied our class with didn't work and how we all got it to
work was to change the name of the testbench to the same name that was referenced in the VHDL.

Someone sent out that tid bit of information for the whole class to fix, but his name I forgot... which is bad because he
is in my class :/

After the waveform worked though, I could locate where the value would match the OR'd value that I calculated writing
out.


![alt text](https://raw.githubusercontent.com/JarrodWooden/CE5_Wooden/master/Part3SimPic.PNG "Simulation Picture for Part Three")


As you can see above. The hex value that I should have got after `ori` was 00008007, which matches up with the simulaiton
picture and tells me that my design worked!

#The End
