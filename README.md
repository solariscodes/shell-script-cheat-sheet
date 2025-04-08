# 🚀 Bash Scripting Cheat Sheet

---

## 📋 Conditional Statements (if, elif, else)
Check if a number is positive, negative, or zero:
```bash
num=3
if [ $num -gt 0 ]
then
    echo "Positive"
elif [ $num -lt 0 ]
then
    echo "Negative"
else
    echo "Zero"
fi
```

---

## 📊 Comparison Operators
Operators for comparing values in conditions:

**Integer Comparison:**

| Operator | Meaning | Example |
|----------|---------|---------|
| `-eq` | Equal to | `[ $a -eq $b ]` |
| `-ne` | Not equal to | `[ $a -ne $b ]` |
| `-lt` | Less than | `[ $a -lt $b ]` |
| `-le` | Less than or equal to | `[ $a -le $b ]` |
| `-gt` | Greater than | `[ $a -gt $b ]` |
| `-ge` | Greater than or equal to | `[ $a -ge $b ]` |

**String Comparison:**

| Operator | Meaning | Example |
|----------|---------|---------|
| `=` or `==` | Equal to | `[ "$str1" = "$str2" ]` |
| `!=` | Not equal to | `[ "$str1" != "$str2" ]` |
| `-z` | String is empty | `[ -z "$str" ]` |
| `-n` | String is not empty | `[ -n "$str" ]` |
| `<` | Less than (ASCII) | `[[ "$str1" < "$str2" ]]` |
| `>` | Greater than (ASCII) | `[[ "$str1" > "$str2" ]]` |

**File Test Operators:**

| Operator | Meaning | Example |
|----------|---------|---------|
| `-e` | File exists | `[ -e file.txt ]` |
| `-f` | Regular file exists | `[ -f file.txt ]` |
| `-d` | Directory exists | `[ -d dir_name ]` |
| `-r` | File is readable | `[ -r file.txt ]` |
| `-w` | File is writable | `[ -w file.txt ]` |
| `-x` | File is executable | `[ -x file.txt ]` |

---

## 🔄 Logical Operators

1. **AND**: `&&` or `-a`
   ```bash
   if [[ $a -gt 10 && $b -lt 20 ]]
   then
       echo "Both conditions are true."
   fi
   ```

2. **OR**: `||` or `-o`
   ```bash
   if [[ $a -gt 10 || $b -lt 20 ]]
   then
       echo "One or both conditions are true."
   fi
   ```

3. **NOT**: `!`
   ```bash
   if ! [[ $a -eq 5 ]]
   then
       echo "Variable 'a' is not equal to 5."
   fi
   ```

4. **XOR**: Implemented with `&&` and `||`
   ```bash
   if [[ $a -eq 1 && $b -ne 1 ]] || [[ $a -ne 1 && $b -eq 1 ]]
   then
       echo "Only one of the conditions is true (XOR)."
   fi
   ```

---

## 🔁 While Loop
Print numbers 1 to 5 using a while loop:
```bash
counter=1
while [ $counter -le 5 ]
do
    echo "Counter: $counter"
    ((counter++))
done
```

Print a countdown from 10 to 1:
```bash
num=10
while [ $num -gt 0 ]
do
    echo "$num..."
    ((num--))
done
echo "Blast off!"
```

Sum numbers from 1 to 10:
```bash
sum=0
i=1
while [ $i -le 10 ]
do
    sum=$((sum + i))
    i=$((i + 1))
done
echo "Sum of numbers from 1 to 10 is: $sum"
```

Infinite loop with break statement:
```bash
count=1
while true
do
    echo "Iteration: $count"
    ((count++))
    
    if [ $count -gt 5 ]
    then
        echo "Breaking the loop!"
        break
    fi
done
echo "Loop finished"
```

Print odd numbers from 1 to 99:
```bash
odd=1
while [ $odd -lt 100 ]
do
    echo $odd
    # Increment by 2 to get next odd number
    odd=$((odd + 2))
done
```

---

## 🔄 For Loop
Loop through a list of names:
```bash
for name in Alice Bob Charlie
do
    echo "Hello, $name"
done
```

C-style for loop:
```bash
for ((i=0; i<3; i++))
do
    echo "Index: $i"
done
```

Range-based for loop (counting from 0 to 10):
```bash
for i in {0..10}
do
    echo "Number: $i"
done
```

---

## 🔍 Combined Example Scripts

### Example 1: Testing Multiple Conditions
```bash
#!/bin/bash

a=15
b=25

# Using AND operator
if [[ $a -gt 10 && $b -le 30 ]]
then
    echo "Condition 1: Both conditions are true."
fi

# Using comparison operator
if [[ $a -ne $b ]]
then
    echo "Condition 2: Variables are not equal."
fi

# Using NOT operator
if ! [[ $a -eq 10 ]]
then
    echo "Condition 3: Variable 'a' is not equal to 10."
fi

# Using OR operator with file test
if [[ -f "config.txt" || -f "settings.txt" ]]
then
    echo "Condition 4: At least one configuration file exists."
fi
```

### Example 2: Triangle Classification
```bash
#!/bin/bash
# Script to classify triangles based on side lengths

# Read three side lengths
read X  # First side
read Y  # Second side
read Z  # Third side

# Check if all sides are equal (equilateral)
if [[ $X -eq $Y && $Y -eq $Z ]]
then
    echo "EQUILATERAL"  # All three sides are equal
# Check if all sides are different (scalene)
elif [[ $X -ne $Y && $Y -ne $Z && $X -ne $Z ]]
then
    echo "SCALENE"  # All three sides are different
# If neither equilateral nor scalene, it must be isosceles
else
    echo "ISOSCELES"  # Exactly two sides are equal
fi
```

### Example 3: Mathematical Calculation with Precision
```bash
#!/bin/bash
# Script to evaluate mathematical expressions with decimal precision
# Takes an expression as input and outputs the result with 3 decimal places

read -r expression  # Read the mathematical expression from user input
printf "%.3f\n" $(echo "$expression" | bc -l)  # Calculate with bc and format to 3 decimal places
```

---
