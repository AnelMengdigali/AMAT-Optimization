.data
array: .space 1024

.text

#Number of blocks: 1
#Cache block size: 32
#YOUR METRIC SCORE: 4616 ns
#The reasons for my optimization: 
#1. In Assembly code: I changed my implementation from working with bytes into working with words to decrease a memory access count, 
#then for success and optimal way of solution I used a fixed hex value of the cell to simulate an adding of 1 to each byte effectively. 
#Additionally, I changed some parts of the array, before I used slt also for loop condition, but then I just compared the index with loaded array limit.
#2. In the configurations of cache parameters: I chose 1 block and 32 cache block sizes as an optimal selection since it shows the best result:
#memory access count = 512, cache hit count = 504, cache miss count = 8 and cache hit rate = 98%, 
#and for my implementation such configuration really works well with only 8 times filling. 
#However, I assume that such selection will be not good since big block sizes then it will result in bad efficiency while trying to make changes as replacements, but for this task we asked to came up with the best result for our implementation.

la $s0, array
li $t0, 256
add $t1, $t1, $zero
li $t3, 16843009

Loop:	
	beq $t1, $t0, Exit
	
	lw $t2, 0($s0)
	move $t2, $t3
	sw $t2, 0($s0)
	
	addi $t1, $t1, 1
	addi $s0, $s0, 4
	
	j Loop
	
Exit:
	li $v0, 10
	syscall




