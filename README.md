# __AOK_Lab5

Zad 2:
.data
vo: .asciiz "Vo interval"
nadvor: .asciiz "Nadvor od interval"

.text
li $v0, 5
syscall
add $t0, $v0, $zero
addi $s0,$zero,1
addi $s1,$zero,-5
addi $s2,$zero,105050
addi $s3,$zero,-70999

slti $t1,$t0,105
slt $t2,$s1,$t0

slt $t3, $s2, $t0
slt $t4, $t0, $s3

beq $t3,$s0, tocno
beq $t4, $s0, tocno
beq $t0, $s1, tocno
beq $t1,$s0, proveri
li $v0,4
la $a0,nadvor
syscall
li $v0, 10       
syscall  
	
	
proveri:
	beq $t2,$s0, tocno
	li $v0,4
	la $a0,nadvor
	syscall
	 li $v0, 10     
        syscall          

tocno:
	li $v0,4
	la $a0,vo
	syscall
	

___________________________________________________________________

Zad 3:

.text
li $v0, 5 
syscall
add $t0, $v0, $zero 

li $v0, 5
syscall
add $t1, $v0, $zero 

addi $s0, $zero, 4
addi $s1, $zero, 1
add $t2, $t0, $zero
addi $t3, $zero, 0

loop:
beq $t1, $t2, end
div $t2, $s0
mfhi $t4
bne $t4, $s1, skip 
addi $t3, $t3, 1
skip:
addi $t2, $t2, 1
j	loop

end:
add $a0, $t3, $zero
li $v0, 1
syscall

li $v0, 10
syscall 


______________________________________________________________

Zad 4:
 
.data
t: .space 31 

.text
la $a0, t
li $a1, 31
li $v0, 8
syscall

la $a0, t
jal BrojZnaci
add $a0, $v0, $zero
li $v0, 1
syscall

la $a0, t
li $a1, 31
li $v0, 8
syscall

la $a0, t
jal BrojZnaci
add $a0, $v0, $zero
li $v0, 1
syscall

li $v0, 10
syscall

BrojZnaci:
addi $v0, $zero, 0
la $t0, 0($a0)
ciklus:
lbu $t1, 0($t0)
beq $t1, $zero, ciklus_kraj 
addi $v0, $v0, 1
addi $t0, $t0, 1
j ciklus
ciklus_kraj:
addi $v0, $v0, -1
jr $ra
