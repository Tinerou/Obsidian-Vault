#ComputerOrganization 

```Assembly
# Code Section

# Activation record for main
# 0. choice
# 1. head - Corresponds to addFront()
# 2. sum - Corresponds to sum()

# r6 frame pointer
# r7 stack pointer
main: lli r6 0x00
lui r6 0x80
addi r7 r6 3

# head in main
lli r1 &heapPtr
lui r1 &heapPtr
lw r2 r1 0
sw r2 r6 1     # initial head = first val of heap

# choice = user input
choose: in r1
sw r1 r6 0
lli r2 4
sub r3 r1 r2
beq r3 &quit          # choice = 4
addi r2 r2 -1
sub r3 r1 r2
beq r3 &callSum       # choice = 3
addi r2 r2 -1
sub r3 r1 r2
beq r3 &callPrint     # choice = 2
addi r2 r2 -1
sub r3 r1 r2
beq r3 &callAddFront  # choice = 1
beq r0 &choose        # choice is invalid

# call addFront(Node *head, int val)
callAddFront: lw r1 r6 1 # r1: head
sw r1 r7 1 # head --> param 1
in r1      # get val from user
sw r1 r7 2 # val --> param 2 
lli r1 &addFront
lui r1 &addFront

jalr r1 r5

# head = < return value (r4) >
sw r4 r6 1 # r4 will return a pointer to the head
beq r0 &choose

# call print(Node* head)
callPrint: lw r1 r6 1  # r1: head
sw r1 r7 1 # head --> param 1

lli r1 &print
lui r1 &print
jalr r1 r5
beq r0 &choose

# remember to incorporate RECURSIVELY
# call sum(Node* head)
callSum: lw r1 r6 1
sw r1 r7 1 # head --> param 1

lli r1 &sum
lui r1 &sum
jalr r1 r5

# sum = < return value (r4) >
sw r4 r6 2
out r4
beq r0 &choose

# End main
quit: .halt 

# Activition record for addFront
# 0. previous frame pointer
# 1. head
# 2. value

addFront: sw r6 r7 0 # store previous frame ptr
addi r6 r7 0         # move frame ptr to stack ptr
addi r7 r7 3         # move stack ptr to end

lw r1 r6 1    # r1: head
lw r2 r6 2    # r2: value

addi r3 r1 2  # r3: new head location
sw r1 r3 0    # head->next
sw r2 r3 1    # set value

# head = < return val (r4) >
addi r4 r3 0

addi r7 r6 0
lw r6 r7 0
jalr r5 r0    # return 

# Activation record for print
# 0. previous frame pointer
# 1. head
# Value is not passed in but Node + 1

print: sw r6 r7 0    # store previous frame ptr
addi r6 r7 0         # move frame ptr to stack ptr
addi r7 r7 2         # move stack ptr to end

lw r1 r6 1   # r1: head

pWhile: lw r2 r1 0
beq r2 &pReturn
lw r2 r1 1
out r2
lw r2 r1 0
addi r1 r2 0
beq r0 &pWhile

pReturn: addi r7 r6 0
lw r6 r7 0
jalr r5 r0 # return

# Activation record for sum
# 0. previous frame pointer
# 1. head
# 2. return address
# Value is not passed in but Node + 1

sum: sw r6 r7 0      # store previous frame ptr
addi r6 r7 0         # move frame ptr to stack ptr
addi r7 r7 3         # move stack ptr to end
sw r5 r6 2           # save return address

lw r1 r6 1   # r1: head

lw r2 r1 0     # check if head == NULL
beq r2 &then   # if NULL go to &then
beq r0 &else

then: lli r4 0  # set return val to 0
beq r0 &sReturn

# r2 is stll head->next here
else: sw r2 r7 1   # set r2 as param 1 in next call
lli r1 &sum
lui r1 &sum
jalr r1 r5      # call sum(head->next)

lw r1 r6 1
lw r2 r1 1
add r4 r4 r2    # r4 = r4 + currVal

sReturn: lw r5 r6 2  # restore return address
addi r7 r6 0         # move stack ptr to frame ptr
lw r6 r7 0           # load prev frame ptr
jalr r5 r0           # pReturn

# Heap Section
# Holds linked list
heapPtr: .fill &heap
heap: .fill 0
```

