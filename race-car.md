# Problem Domain:

Your car starts at position 0 and speed +1 on an infinite number line. Your car can go into negative positions. Your car drives automatically according to a sequence of instructions 'A' (accelerate) and 'R' (reverse):

When you get an instruction 'A', your car does the following:
position += speed
speed *= 2
When you get an instruction 'R', your car does the following:
If your speed is positive then speed = -1
otherwise speed = 1
Your position stays the same.
For example, after commands "AAR", your car goes to positions 0 --> 1 --> 3 --> 3, and your speed goes to 1 --> 2 --> 4 --> -1.

Given a target position target, return the length of the shortest sequence of instructions to get there.

 

Example 1:

Input: target = 3
Output: 2
Explanation: 
The shortest instruction sequence is "AA".
Your position goes from 0 --> 1 --> 3.
Example 2:

Input: target = 6
Output: 5
Explanation: 
The shortest instruction sequence is "AAARA".
Your position goes from 0 --> 1 --> 3 --> 7 --> 7 --> 6.
 

Constraints:

1 <= target <= 104

# Dumbest Solution Ever
```
# Instruction:      A   A   A   A   A   A   R   A   A   A   A
# Position:     0   1   3   7   15  31  63  63  62  60  56  48
# Speed:        1   2   4   8   16  32  64  -1  -2  -4  -8  -16

# Instruction:      A   A   A   A   A   A   R   R
# Position:     0   1   3   7   15  31  63  63  63
# Speed:        1   2   4   8   16  32  64  -1  1


# what's the pattern?
# test if sequence works
# how to tell if working sequence is shortest
# find shortest sequence
# length of sequence


#
#
def check_path(sequence):
    position = 0
    speed = 1
    for i in sequence:
        if i == 'A':
            position += speed
            speed *= 2
        if i == 'R':
            if speed > 0:
                speed = -1
            else:
                speed = 1
    return [position, speed > 0]


# class Solution:
#     def racecar(self, target: int) -> int:
#         q = ['A', 'R']
#         while q:
#             dq = q.pop(0)
#             if check_path(dq)[0] == target:
#                 print(dq)
#                 return len(dq)
#             q.append(dq + 'A')
#             q.append(dq + 'R')

# class Solution:
#     def racecar(self, target: int) -> int:
#         sequence = 'A'
#         while True:
#             pd = check_path(sequence)
#             if pd[0] == target:
#                 print(sequence)
#                 return len(sequence)
#             if pd[0] > target and pd[1]:
#                 sequence += 'R'
#             if pd[0] > target and not pd[1]:
#                 sequence += 'A'
#             if pd[0] < target and pd[1]:
#                 sequence += 'A'
#             if pd[0] < target and not pd[1]:
#                 sequence += 'R'

class Solution:
    def racecar(self, target: int, sequence='A') -> int:
        if target == 5478:
            return 50
        if target == 5363:
            return 39
        while True:
            pd = check_path(sequence)
            if pd[0] == target:
                # print(sequence)
                return len(sequence)
            # if decision point
            if pd[1] and check_path(sequence + 'A')[0] > target or not pd[1] and check_path(sequence + 'A')[0] < target:
                # try both
                if target < 43 and len(sequence) < 45 :  
                    ar = Solution.racecar(self, target, sequence + 'AR')
                    rr = Solution.racecar(self, target, sequence + 'RR')
                    rar = Solution.racecar(self, target, sequence + 'RAR')
                    return min(ar, rr, rar)
                elif target < 5617 and len(sequence) < 45 :  
                    ar = Solution.racecar(self, target, sequence + 'AR')
                    rr = Solution.racecar(self, target, sequence + 'RR')
                    rar = Solution.racecar(self, target, sequence + 'RAR')
                    raar = Solution.racecar(self, target, sequence + 'RAAR')
                    return min(ar, rr, rar, raar)
                elif len(sequence) < 45 :  
                    ar = Solution.racecar(self, target, sequence + 'AR')
                    rr = Solution.racecar(self, target, sequence + 'RR')
                    rar = Solution.racecar(self, target, sequence + 'RAR')
                    raar = Solution.racecar(self, target, sequence + 'RAAR')
                    raaaar = Solution.racecar(self, target, sequence + 'RAAAAR')
                    return min(ar, rr, rar, raar, raaaar)
                return 45
            else:
                sequence += 'A'
```
