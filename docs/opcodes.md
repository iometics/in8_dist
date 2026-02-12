
# Kamioza DFA Virtual Machine Opcode Manual

## Sections



### Blocking
- [Input](#input)  (DROP, CLICK, GRAB, WAIT, ...)
- [Sleep](#sleep)  
- [Signal](#signal)  
- [Accept](#accept)  
- REF_MACHINE  - reference another machine's registers.
- HANDOFF
- SYNCPOINT

### Conditionals
- [Branching](#branching) 
  -  [Epsilon](#epsilon)
- [Compare](#compare)  (GT, LT, EQ, EPSILON, ...)  

### Math and Logic
- [Arithmetic](#arithmetic)  (ADD,SUB,MUL,DIV)  
- [Move](#move)  (MOV a value to register)
- [Rand](#rand)  (Generate a random number into the WRAND register)


### Gameplay
- [Graphics](#graphics)   
[Loadview](#loadview)   
[Audio](#audio)         
[Spells](#spell-casting)  
[Relocate](#relocate)   
* SENDKEYI
* SENDKEY
* SENDMSGI
* SENDMSG

### Other
[Mapping](#mapping)  
- MAPi  
- MAP

[Todo](#todo)  


# Input
## System events:

|opcode |parameters     |description|
|-------|---------------|-----------|
|WAIT|sig_name|Wait for a [signal](#signal) from another machine.|

## User events:
|opcode |parameters     |description|
|-------|---------------|-----------|
|DROP|[SWAP \| IDD]|  -> wObject
|GRAB|[IDD]|wObject ->
|CLICK|
|DRAG||object_def stored in wObject
|DRAGFOCUS    

Notes:
* SWAP :DROP can take SWAP as a parameter
* GRAB object_def retrieved from wObject OR from transition wParm if specified.

# Audio
PLAYWAVE - sound id is stored in transition::wAmbient  
STOPWAVE  
PLAYMIDI  
STOPMIDI  

# Sleep

|opcode |parameters     |description               |
|-------|---------------|--------------------------|
|ESTIME |imm            |Sleep time in seconds     |
|EMTIME |imm            |Sleep time in milliseconds|

Notes:
*   the time remaining is stored in the machine::dEtime.

# Mapping

|opcode  | parameters     |description|
|--------|----------------|-----------|
|MAP     | r1=key,r2=op   |           |
|MAPi    | r1=key, op imm |           |
|MAP_OBJ |map op| depricated |
|MIX|wObject = MAP_OBJ(r1, r2) r1 = operator, r2 = operand.|
|XIM||

Mappings are modeled after prolog style facts:
```
CARD_OBJECTS(IDD_CARD00,IDD_SPELL01).
CARD_OBJECTS(IDD_CARD01,IDD_SPELL02).
CARD_OBJECTS(IDD_CARD02,IDD_SPELL03).
CARD_OBJECTS(IDD_CARD03,IDD_SPELL04).
```  
These are stored in sqlite3 map table:  
```
insert into map ([op],[key],[value]) values   
('CARD_OBJECTS','IDD_CARD00','IDD_SPELL01'),
('CARD_OBJECTS','IDD_CARD01','IDD_SPELL02'),
('CARD_OBJECTS','IDD_CARD02','IDD_SPELL03'),
('CARD_OBJECTS','IDD_CARD03','IDD_SPELL04'),
```
To perform a lookup using opcodes:
```
    ASSIGN(WOBJECT, IDD_CARD02);
    MAP(WOBJECT,CARD_OBJECTS);  
```
After MAP_OBJ WOBJECT will contain IDD_SPELL02. if the object cannot be mapped then the transition occurs w/o mapping the object.  

Note that MAP_OBJ is a special case of MAP where WOBJECT contains the item to be mapped, and receives the mapped item (object).

# Relocate

|opcode |parameters     |description|
|-------|---------------|-----------|
|SET_YOFFSET||
|SET_XOFFSET||

## Graphics
 - sprites and video

|opcode |parameters     |description|
|-------|---------------|-----------|
|SHOW|register, cursor/icon/actor| Show as sprite of the stored object.|
|ASHOW||Just like show, but play looped animate|
|ANIMATE|LOOP|
|VIDEO||Show a video clip. Remove the image after the last frame.|

# Arithmetic

|opcode |parameters     |description|
|-------|---------------|-----------|
|ADD|r1, r2 --> r1|
|SUB|r1, r2 --> r1|
|MUL|r1, r2 --> r1|
|DIV|r1, r2 --> r1|
|MOD|r1, r2 --> r1|
|ADDI|r1, value (imm) --> r1|
|SUBI|r1, value (imm) --> r1|
|MULI|r1, value (imm) --> r1|
|DIVI|r1, value (imm) --> r1|
|MODI|r1, value (imm) --> r1|

# Move

|opcode |parameters     |description|
|-------|---------------|-----------|
|ASSIGN|r1, value (imm)| imm --> r1||
|MOV|r1,r2| r2 --> r1|

Notes:
* ASSIGN(R1, 0) will clear a register so unused value is not transmitted with table updates.

# Rand

|opcode |parameters     |description  |
|-------|---------------|-------------|
|RAND   |r1,r2          | see notes   |

Notes:
* set WRAND to a value between r2 and r2+r1


# Branching
Conditionals are used to select between 2 possible transitions from a given state. The first transition is taken if the conditinal evaluate to true, the second transition is taken when the condition evalueate to false (i.e. the 'else' clause). The opcode 'Z_EPSILON' is used for the else branch. In the following example we branch from state 102 to state 0 if WTEMP1 and R_OBJECT are not equal (meaning that the supplied chem does not match the chem required by the inserted card). If the registers match, then the Z_EPSILON transition is taken:
```
-- chem1 does not match inserted card
('M08_BIN','102','0','NEQUAL','WTEMP1','R_WOBJECT', ''),
-- chem1 matches, now check for chem2:
('M08_BIN','102','103','Z_EPSILON','','','
    MOV(WTEMP1,WPARM);
    MAPi(WTEMP1,CARD_CHEM2);
    REF_MACHINE(WIP3);
'),
```



# Epsilon
   Z_EPSILON        = 0,    // Just do it.


# Compare
   IFSTATE - IFSATE state, machine_id  
   IFSTATEi- IFSATE state, machine_id  
   NOTSTATE - NOTSTATE state, machine_id  
   NOTSTATEi - NOTSTATE state, machine_id  
 

## Compare Immediate(Register , Value):

|opcode |parameters     |description      |
|-------|---------------|-----------------|
|GTi    |r1, value      |true if r1 >  r2 |
|GTEi   |r1, value      |true if r1 >= r2 |
|LTi    |r1, value      |true if r1 <  r2 |
|LTEi   |r1, value      |true if r1 <= r2 |
|EQUALi |r1, value      |true if r1 == r2 |
|NEQUALi|r1, value      |true if r1 != r2 |

## Compare registers - (Register , Register):

|opcode |parameters |description      |
|-------|-----------|-----------------|
|GT     |r1, r2     |true if r1 >  r2 |
|GTE    |r1, r2     |true if r1 >= r2 |
|LT     |r1, r2     |true if r1 <  r2 |
|LTE    |r1, r2     |true if r1 <= r2 |
|EQUAL  |r1, r2     |true if r1 == r2 |
|NEQUAL |r1, r2     |true if r1 != r2 |

   IS_A,
   NOT_A,

# Loadview

|opcode |parameters     |description|
|-------|---------------|-----------|
|LOADVIEW|view_id||

# Spell casting

|opcode  |parameters     |description|
|--------|---------------|-----------|
|SPELL    |(bParm, wParm)|
|SPELL_ME|              |dropped a spell on me|
|SPELL_YOU||Dropped a spell on you|

# Signal
|opcode |parameters     |description|
|-------|---------------|-----------|
|SIGNALri|(imm) wParm| wParm is the id of the machine to be signaled. (imm) is the signal id|
|SIGNALi|(imm) wParm| wParm is the id of the machine to be signaled. (imm) is the signal id|
|SIGNAL||(reg) bParm| reg is the register holding the id of of the machine to be signaled. wParm is the to the signaled call.|

# Accept
|opcode |parameters     |description|
|-------|---------------|-----------|
|C_ACCEPT|class|Accept objects of a specific class.|
|O_ACCEPT|idd_object|Accept specific object.|

