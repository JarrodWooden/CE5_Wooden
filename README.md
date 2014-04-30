#Computer Exercise 5

------------Jarrod Wooden--------------

##Part One

addi $s0, $0, 44
addi $s1, $0, -37
addi $s2, $s0, $s1
sw $s2, 0x54($0)

-load register s0 with decimal 44
-load register s1 with decimal -37
-add the two together and store at s2
-write s2 to the hex address x54
