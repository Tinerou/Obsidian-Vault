```Assembly
#Activation record for main
# 0. a
# 1. b
# 2. c
# 3. total
lli r1 2
sw r1 r6 0
lli r1 3
sw r1 r6 1
lli r1 4
sw r1 r6 2

# call foo(a, b, c)
lw r1 r6 0
sw r1 r7 1
lw r1 r6 1
sw r1 r7 2
lw r1 r6 2
sw r1 r7 3
lli r1 &foo
lui r1 &foo
jalr r1 r5
sw r4 r6 3 # return total

# call bar(b, c)
lw r1 r6 1
sw r1 r7 1
lw r1 r6 2
sw r1 r7 2
lli r1 &bar
lui r1 &bar
jalr r1 r5

# total = total + bar(b, c)
lw r1 r6 3
add r1 r1 r4
sw r1 r6 3
out r1

# end of main
.halt

# Activation record for bar
0. Previous frame pointer
1. parameter a
2. parameter b
3. c

bar: sw r6 r7 0
addi r6 r7 0
addi r6 r7 4

# c = a + b
lw r1 r6 1 # r1 = a
lw r2 r6 2 # r2 = b
add r1 r1 r2 # r1 = c

addi r4 r1 2

addi r7 r6 0
lw r6 r7 0
jalr r5 r0


# Activation record for foo
# 0. Previous frame ptr
# 1. a
# 2. b
# 3. c
# 4. sum1
# 5. sum2

addi r6 r7 0
addi r7 r7 6

# Activation record for bar
# 1. a
# 2. b

```