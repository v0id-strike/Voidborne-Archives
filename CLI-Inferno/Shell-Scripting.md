## **📌 Phase 1: Introduction to Bash Scripting**

### 1️⃣ **Introduction / Definition**  
> Bash is a Unix shell and command language used for automating tasks, system administration, and penetration testing. Unlike compiled languages, Bash scripts are interpreted, making them flexible for quick execution. Key features include:  
> - **No compilation needed**  
> - **Direct system command integration**  
> - **Essential for privilege escalation and data filtering in security tasks**  

### 2️⃣ **Syntax Block**  
#### Basic Script Structure:  
```bash
#!/bin/bash  
# Comments start with '#'  

# Variables  
variable="value"  

# Functions  
function_name() {  
    commands  
}  

# Conditional Execution  
if [ condition ]; then  
    commands  
fi  

# Loops  
for item in list; do  
    commands  
done  

# User Input  
read -p "Prompt: " variable  
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `#!/bin/bash` → **Shebang** declares the interpreter.  
- ✅ `variable="value"` → **Variables** store data (no spaces around `=`).  
- ✅ `if [ condition ]; then` → **Conditionals** use square brackets for tests.  
- ✅ `for item in list; do` → **Loops** iterate over lists/arrays.  
- ✅ `read -p "Prompt: " var` → **User input** stored in `var`.  

### 4️⃣ **Why / When to Use**  
| Scenario                | Bash | Python/C |     |
| ----------------------- | ---- | -------- | --- |
| Quick system automation | ✅    | ❌        |     |
| Parsing command output  | ✅    | ⚠️       |     |
| Complex data structures | ❌    | ✅        |     |

> **Best for**:  
> - Combining Unix commands (`grep`, `awk`, `whois`).  
> - Rapid prototyping for pentesting (e.g., host discovery).  

### 5️⃣ **Examples**  
#### Example 1: Basic Script  
```bash
#!/bin/bash  
echo "Hello, $USER!"  
```  

#### Example 2: IP-finder.sh 
```bash
#!/bin/bash  
domain=$1  
ip=$(host $domain | grep "has address" | cut -d" " -f4)  
echo "Discovered IP: $ip"  
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Pattern Matching**:  
```bash
case $opt in  
    [Yy]*) echo "Yes" ;;  
	[Nn]*) echo "No" ;;  
esac  
```  
- **Command Substitution**:  
```bash
cidr=$(whois $ip | grep "CIDR")  
```  

### 7️⃣ **Tips & Common Mistakes**  
- ❌ **Spaces in variables**: `var = "value"` (wrong) vs. `var="value"` (correct).  
- ✅ **Debugging**: Use `set -x` to trace execution.  
- ❌ **Forgotten `;;`** in `case` statements causes syntax errors.  

### 8️⃣ **Summary**  
> Bash scripting is ideal for automating system tasks, especially in security (host discovery, log analysis). It combines simplicity with powerful command-line integration.  

### 🔖 Bonus  
- **Use `#!/usr/bin/env bash`** for portability.  
- **Colorize output**:  
  ```bash
  echo -e "\e[31mError\e[0m"  # Red text  
  ```  


---

## **📌 Phase 2: Conditional Execution**

### 1️⃣ **Introduction / Definition**  
> Conditional execution allows scripts to make decisions based on specified conditions. Without it, scripts would run sequentially without flexibility. Key structures:  
> - `if-then-fi` → Basic condition check.  
> - `elif` → Additional conditions.  
> - `else` → Default action if no conditions match.  

### 2️⃣ **Syntax Block**  
#### Basic Structure:  
```bash
if [ condition ]; then  
    # Code if true  
elif [ condition ]; then  
    # Code if elif-true  
else  
    # Default code  
fi  
```

#### Example: Argument Check  
```bash
if [ $# -eq 0 ]; then  
    echo "Error: No arguments provided."  
    exit 1  
fi  
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `if [ condition ]` → Starts conditional block. **Spaces around `[ ]` are mandatory**.  
- ✅ `-eq`, `-lt`, `-gt` → Comparison operators (`=`, `<`, `>`).  
- ✅ `$#` → Number of arguments passed.  
- ✅ `exit 1` → Terminates script with error code.  

### 4️⃣ **Why / When to Use**  
| Scenario                  | Use Case                |     |
| ------------------------- | ----------------------- | --- |
| Validate user input       | `if [ $# -eq 0 ]`       |     |
| Handle different outcomes | `if-elif-else` ladder   |     |
| Error handling            | `exit` on failed checks |     |

> **Key Benefit**: Prevents script failures due to invalid inputs.  

### 5️⃣ **Examples**  
#### Example 1: Numeric Comparison  
```bash
value=$1  
if [ $value -gt 10 ]; then  
    echo "Value > 10"  
elif [ $value -lt 10 ]; then  
    echo "Value < 10"  
else  
    echo "Value = 10"  
fi  
```

#### Example 2: File Existence Check  
```bash
if [ -f "file.txt" ]; then  
    echo "File exists."  
else  
    echo "File not found."  
fi  
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Combining Conditions**:  
```bash
if [ $age -gt 18 ] && [ "$country" = "US" ]; then  
	echo "Eligible."  
fi  
```  
- **Regex Matching**:  
```bash
if [[ "$input" =~ ^[A-Za-z]+$ ]]; then  
    echo "Alphabetic input."  
fi  
```  

### 7️⃣ **Tips & Common Mistakes**  
- ❌ **Missing Spaces**: `if[$#-eq0]` → Syntax error.  
- ✅ **Quote Variables**: `if [ "$var" = "value" ]` → Prevents word splitting.  
- ❌ **Using `=` for numbers**: Use `-eq` instead of `==`.  

### 8️⃣ **Summary**  
> Conditionals (`if-elif-else`) are essential for validating inputs, handling errors, and creating dynamic scripts. Always test edge cases!  

### 🔖 Bonus  
- **Use `[[ ]]` instead of `[ ]`** for advanced features (regex, logical operators).  
- **Colorize Errors**:  
```bash
echo -e "\e[31mError: No arguments.\e[0m"  
```    

---

## **📌 Phase 3: Variables, Arguments and Array**

### 1️⃣ **Introduction / Definition**  
> Bash provides automatic handling of command-line arguments through special variables (`$0-$9`, `$#`, `$@`). Variables store data as strings by default, while arrays allow storing multiple values. These features enable dynamic script behavior based on user input.

### 2️⃣ **Syntax Block**  
#### Command-Line Arguments:
```bash
$0          # Script name
$1-$9       # 1st to 9th arguments
${10}       # Arguments beyond 9 (braces required)
```

#### Variable Assignment:
```bash
var="value"   # Correct (no spaces)
var = "value" # Incorrect (causes error)
```

#### Array Declaration:
```bash
arr=("val1" "val2" "val3")  # Zero-based indexing
echo ${arr[1]}              # Access second element
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `$0` → Always contains the script name.  
- ✅ `$1`, `$2`... → Positional arguments (up to `$9`). Use `${10}` for higher numbers.  
- ✅ `var="value"` → Spaces around `=` break assignment.  
- ✅ `arr=(...)` → Arrays require parentheses and quoted elements with spaces.  

### 4️⃣ **Why / When to Use**  
| Scenario                | Tools                 |
| ----------------------- | --------------------- |
| Handling user input     | `$1`, `$2`, `$@`      |
| Storing multiple values | Arrays (`arr=(...)`)  |
| Checking input validity | `$#` (argument count) |
| Debugging scripts       | `$?` (exit status)    |

> **Key Benefit**: Enables flexible, user-driven script execution.

### 5️⃣ **Examples**  
#### Example 1: Basic Argument Handling
```bash
#!/bin/bash
echo "Script: $0"
echo "First arg: $1"
echo "All args: $@"
```

#### Example 2: Array Usage
```bash
domains=("www.example.com" "ftp.example.com")
echo "First domain: ${domains[0]}"
echo "All domains: ${domains[@]}"
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Shift Arguments**:  
  ```bash
  shift   # Discards $1, shifts remaining args left ($2 becomes $1)
  ```
- **Default Values**:  
  ```bash
  name=${1:-"Guest"}  # Uses "Guest" if $1 is empty
  ```
- **Associative Arrays (Bash 4+)**:  
  ```bash
  declare -A colors=(["red"]="#FF0000" ["green"]="#00FF00")
  echo ${colors["red"]}
  ```

### 7️⃣ **Tips & Common Mistakes**  
- ❌ **Unquoted variables**: `rm $file` fails if `$file` contains spaces. Use `rm "$file"`.  
- ✅ **Check argument count**:  
  ```bash
  if [ $# -lt 2 ]; then echo "Need 2 args"; exit 1; fi
  ```
- ❌ **Forgotten braces**: `$10` is interpreted as `$1` followed by `0`. Use `${10}`.  

### 8️⃣ **Summary**  
> Bash's special variables (`$0-$9`, `$#`, `$@`) and arrays provide robust input handling. Variables are string-based by default, while arrays simplify multi-value storage. Always validate inputs!

### 🔖 Bonus  
- **List all arguments**:  
  ```bash
  for arg in "$@"; do echo "$arg"; done
  ```
- **Slice arrays**:  
  ```bash
  echo ${arr[@]:1:3}  # Elements 1 to 3
  ```

---

## **📌 Phase 4: Comparison Operators

### 1️⃣ **Introduction / Definition**  
> Comparison operators in Bash allow scripts to make decisions by evaluating conditions. They are categorized into:  
> - **String operators** (text comparisons)  
> - **Integer operators** (numeric comparisons)  
> - **File operators** (filesystem checks)  
> - **Logical operators** (combining conditions)  

### 2️⃣ **Syntax Block**  
#### String Comparison:  
```bash
[ "$var" == "value" ]   # Equality
[[ "$var" > "A" ]]      # ASCII comparison (requires [[ ]])
```

#### Integer Comparison:  
```bash
[ $num -lt 10 ]   # Less than
```

#### File Checks:  
```bash
[ -f "file.txt" ]  # Is a regular file
```

#### Logical Operators:  
```bash
[ "$var" ] && [ -f "$var" ]  # AND
[[ -z "$var" || ! -d "$dir" ]]  # OR/NOT
```

### 3️⃣ **Explanation of Syntax**  
- ✅ **Quotes matter**: `"$var"` prevents errors with spaces/empty values.  
- ✅ `[[ ]]` vs `[ ]`:  
  - `[[ ]]` supports `&&/||` and advanced string comparisons (`<`, `>`).  
  - `[ ]` is POSIX-compliant but more limited.  
- ✅ **File operators**: `-e`, `-f`, `-d` check existence/types.  

### 4️⃣ **Why / When to Use**  
| Scenario               | Operator Type          | Example                            |
| ---------------------- | ---------------------- | ---------------------------------- |
| Validating user input  | String (`==`, `!=`)    | `[ "$1" == "admin" ]`              |
| Numeric range checks   | Integer (`-lt`, `-gt`) | `[ $age -ge 18 ]`                  |
| File permission checks | File (`-r`, `-w`)      | `[ -w "/etc/passwd" ]`             |
| Complex conditions     | Logical (`&&`/`\|\|`)  | `[ -f "$file" ] && [ -s "$file" ]` |

### 5️⃣ **Examples**  
#### Example 1: String Comparison  
```bash
if [ "$USER" != "root" ]; then
    echo "Error: Run as root!"
    exit 1
fi
```

#### Example 2: File Check  
```bash
if [[ -f "$logfile" && -s "$logfile" ]]; then
    echo "Logfile exists and is not empty."
fi
```

#### Example 3: Numeric Range  
```bash
if [ $count -gt 0 ] && [ $count -le 100 ]; then
    echo "Valid count (1-100)."
fi
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Pattern Matching**:  
  ```bash
  if [[ "$file" == *.txt ]]; then
      echo "Text file detected."
  fi
  ```  
- **Combining Checks**:  
  ```bash
  [ -d "$dir" ] || mkdir -p "$dir"  # Create dir if missing
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ❌ **Unquoted Variables**: `[ $var == "value" ]` fails if `$var` is empty. Use `[ "$var" == "value" ]`.  
- ✅ **Use `[[ ]]` for Strings**: Safer and supports regex (`=~`).  
- ❌ **Mixing Operators**: `-eq` for numbers, `==` for strings.  

### 8️⃣ **Summary**  
> Comparison operators are essential for:  
> - Validating inputs (strings/numbers).  
> - Checking files/permissions.  
> - Building complex logic with `&&/||`.  
> Always quote variables and prefer `[[ ]]` for strings!  

---

### 🔖 Bonus  
- **Regex Matching**:  
  ```bash
  if [[ "$email" =~ ^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$ ]]; then
      echo "Valid email."
  fi
  ```  
- **Exit Code Check**:  
  ```bash
  if grep -q "error" logfile; then
      echo "Errors found!"
  fi
  ```  

---

## **📌 Phase 5: Arithmetic Operators**  

Bash provides **seven** arithmetic operators to perform mathematical operations and modify integer values.  

### **1️⃣ Arithmetic Operators**  

| Operator     | Description         |
| ------------ | ------------------- |
| `+`          | Addition            |
| `-`          | Subtraction         |
| `*`          | Multiplication      |
| `/`          | Division            |
| `%`          | Modulus (remainder) |
| `variable++` | Increment by 1      |
| `variable--` | Decrement by 1      |

### **2️⃣ Arithmetic Operations in Bash**  

You can use `$((expression))` to perform arithmetic calculations.  

**Example:**  

```bash
#!/bin/bash

increase=1
decrease=1

echo "Addition: 10 + 10 = $((10 + 10))"
echo "Subtraction: 10 - 10 = $((10 - 10))"
echo "Multiplication: 10 * 10 = $((10 * 10))"
echo "Division: 10 / 10 = $((10 / 10))"
echo "Modulus: 10 % 4 = $((10 % 4))"

((increase++))
echo "Increment Variable: $increase"

((decrease--))
echo "Decrement Variable: $decrease"
```

📌 **Output:**  

```bash
Addition: 10 + 10 = 20
Subtraction: 10 - 10 = 0
Multiplication: 10 * 10 = 100
Division: 10 / 10 = 1
Modulus: 10 % 4 = 2
Increment Variable: 2
Decrement Variable: 0
```

### **3️⃣ Determining Variable Length**  

To find the length of a string variable, use `${#variable}`.  

**Example:**  

```bash
#!/bin/bash

htb="HackTheBox"

echo "Length of string: ${#htb}"
```

📌 **Output:**  

```bash
10
```

### **4️⃣ Arithmetic in a Loop (CIDR Ping Example)**  

Increment (`++`) and decrement (`--`) operators are useful in loops, such as when checking active hosts within a CIDR range.  

**Example:**  

```bash
<SNIP>
echo -e "\nPinging host(s):"
for host in $cidr_ips; do
    stat=1
    while [ $stat -eq 1 ]; do
        ping -c 2 $host > /dev/null 2>&1
        if [ $? -eq 0 ]; then
            echo "$host is up."
            ((stat--))
            ((hosts_up++))
            ((hosts_total++))
        else
            echo "$host is down."
            ((stat--))
            ((hosts_total++))
        fi
    done
done
<SNIP>
```

📌 **Explanation:**  
- `((stat--))` ensures the loop eventually exits.  
- `((hosts_up++))` increments the count of online hosts.  
- `((hosts_total++))` keeps track of the total hosts scanned.  

---

## **📌 Phase 6: Arithmetic Operators**

### 1️⃣ **Introduction / Definition**  
> Bash provides integer-based arithmetic operations through `$(( ))` and `(( ))` syntax. Key capabilities:  
> - Basic calculations (`+`, `-`, `*`, `/`, `%`)  
> - Auto-increment/decrement (`++`, `--`)  
> - String length checks (`${#var}`)  
> - Essential for loop control and network operations (e.g., host scanning)  

### 2️⃣ **Syntax Block**  
#### Basic Arithmetic:
```bash
echo "$((5 + 3))"     # → 8
echo "$((5 / 2))"     # → 2 (integer division)
```

#### Increment/Decrement:
```bash
((counter++))         # Post-increment
((--total))           # Pre-decrement
```

#### String Length:
```bash
str="Hello"
echo "${#str}"        # → 5
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `$(( ))` → Expands to calculation result (use in `echo`, assignments).  
- ✅ `(( ))` → Performs arithmetic *without* output (ideal for loops/conditionals).  
- ✅ `${#var}` → Returns character count (spaces included).  
- ❌ **No native floats**: Use `bc` or `awk` for decimals.  

### 4️⃣ **Why / When to Use**  
| Scenario                  | Operator            | Example                  |
| ------------------------- | ------------------- | ------------------------ |
| Loop counters             | `++`/`--`           | `for ((i=0; i<10; i++))` |
| Network host calculations | `%` (modulus)       | `$((ip % 256))`          |
| Input validation          | `${#var}`           | `[ ${#pass} -ge 8 ]`     |
| CIDR range iteration      | Combined arithmetic | `((hosts_total++))`      |

### 5️⃣ **Examples**  
#### Example 1: Basic Calculator  
```bash
#!/bin/bash
read -p "Enter two numbers: " a b
echo "Sum: $((a + b))"
echo "Product: $((a * b))"
```

#### Example 2: Password Strength Check  
```bash
password="P@ssw0rd"
if [ ${#password} -lt 8 ]; then
    echo "Weak: Password too short!"
fi
```

#### Example 3: CIDR Host Scanner (Snippet)  
```bash
for ip in $cidr_ips; do
    ping -c 1 $ip >/dev/null && ((alive++))
    ((total++))
done
echo "$alive/$total hosts responded."
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Bitwise Operations**:  
  ```bash
  echo "$((5 & 3))"   # AND → 1
  echo "$((16#FF))"   # Hex to decimal → 255
  ```  
- **Floating-Point Workaround**:  
  ```bash
  echo "scale=2; 10/3" | bc  # → 3.33
  ```  
- **Random Numbers**:  
  ```bash
  echo $((RANDOM % 100))  # Random 0-99
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ❌ **Spaces in assignments**: `sum = $((a+b))` fails (use `sum=$((a+b))`).  
- ✅ **Force exit on error**:  
  ```bash
  ((count > 0)) || exit 1  # Exit if count ≤ 0
  ```  
- ❌ **Unquoted strings in `[ ]`**: Use `[[ "${var}" == value ]]` for safety.  

### 8️⃣ **Summary**  
> Bash arithmetic enables:  
> - **Efficient loop control** (counters, exit conditions).  
> - **Network operations** (host scanning, IP calculations).  
> - **Input validation** (length checks, numeric ranges).  
> Combine with loops and conditionals for powerful automation!  

---

### 🔖 Bonus: Pro Tips  
- **Ternary-like operations**:  
  ```bash
  (( result = condition ? 1 : 0 ))  # Sets result=1 if condition is true
  ```  
- **Quick math in terminal**:  
  ```bash
  $ echo $(( (10 + 5) * 2 ))  # → 30
  ```  

---

## **📌 Phase 7: Input and Output Control 

### 1️⃣ **Introduction / Definition**  
> Bash provides powerful tools for:  
> - **Interactive input** (`read`) to guide script execution  
> - **Output control** via redirection (`>`, `>>`, `2>`) and `tee`  
> - **Clean flow control** with `case` statements  
> Essential for building user-friendly scripts and logging results.

### 2️⃣ **Syntax Block**  
#### User Input:
```bash
read -p "Prompt: " variable  # Stores input in $variable
```

#### Output Redirection:
```bash
command > file.txt      # Overwrite file
command >> file.txt     # Append to file
command 2> errors.log  # Redirect errors
command &> output.log  # Redirect all output
```

#### Tee for Dual Output:
```bash
command | tee file.txt      # Display+overwrite
command | tee -a file.txt  # Display+append
```

#### Case Statement:
```bash
case $var in
    "1") command1 ;;
    "2") command2 ;;
    *) default_command ;;
esac
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `read -p` → Prompts user and stores input (e.g., menu selections).  
- ✅ `tee` → Splits output to both terminal and file (`-a` appends).  
- ✅ `case` → Cleaner alternative to nested `if` for multiple conditions.  
- ❌ **Unquoted variables** in `read`: May cause word splitting issues.  

### 4️⃣ **Why / When to Use**  
| Scenario               | Tool               | Example                |                 |
| ---------------------- | ------------------ | ---------------------- | --------------- |
| Interactive menus      | `read` + `case`    | CIDR.sh options        |                 |
| Logging command output | `tee`              | `whois $ip             | tee -a log.txt` |
| Error handling         | `2>`               | `cmd 2> errors.log`    |                 |
| Progress visibility    | `tee` without `-a` | Real-time scan updates |                 |

### 5️⃣ **Examples**  
#### Example 1: Interactive Menu
```bash
read -p "Choose (1-Scan, 2-Ping): " opt
case $opt in
    1) nmap -sV $target ;;
    2) ping -c 4 $target ;;
    *) echo "Invalid option" ;;
esac
```

#### Example 2: Logging with Tee
```bash
nmap -sS 192.168.1.0/24 | tee scan_results.txt
```

#### Example 3: Error Handling
```bash
curl https://example.com &> curl.log || echo "Failed!"
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Silent Mode**:  
  ```bash
  read -s -p "Password: " pass  # Hides input
  ```  
- **Timeout for Input**:  
  ```bash
  read -t 10 -p "Quick! Answer (10s): " response
  ```  
- **Multi-output Logging**:  
  ```bash
  cmd | tee >(grep "ERROR" > errors.log) > output.log
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ✅ **Always initialize variables**:  
  ```bash
  declare -i hosts_up=0  # Integer for counters
  ```  
- ❌ **Overwriting logs**: Use `>>` or `tee -a` for critical data.  
- ✅ **Validate input**:  
  ```bash
  [[ "$opt" =~ ^[1-3]$ ]] || exit 1
  ```  

### 8️⃣ **Summary**  
> Key takeaways:  
> - Use `read` + `case` for interactive menus.  
> - `tee` is ideal for real-time monitoring + logging.  
> - Redirect errors (`2>`) to separate debug files.  
> - Always test input validation edge cases.  

### 🔖 Bonus: Pro Tips  
- **Colorize menu prompts**:  
  ```bash
  echo -e "\e[32m1) Scan\e[0m"  # Green text
  ```  
- **Audit trails**:  
  ```bash
  echo "$(date): User chose $opt" >> audit.log
  ```  

---

## **📌 Phase 8: Flow Control and Loops

### 1️⃣ **Introduction / Definition**  
> Flow control structures determine how Bash scripts execute commands based on conditions and repetitions. They enable:  
> - **Decision-making** (`if`, `case`)  
> - **Repetitive execution** (`for`, `while`, `until`)  
> - **Output management** (`tee`, redirection)  

### 2️⃣ **Syntax Block**  
#### Branches:
```bash
# If-Else
if [ "$var" -eq 1 ]; then  
    commands  
elif [ "$var" -eq 2 ]; then  
    commands  
else  
    commands  
fi  

# Case
case $var in  
    "a") commands ;;  
    "b") commands ;;  
    *) default_commands ;;  
esac  
```

#### Loops:
```bash
# For
for item in {1..5}; do  
    commands  
done  

# While
while [ $counter -le 5 ]; do  
    commands  
    ((counter++))  
done  

# Until
until [ $counter -gt 5 ]; do  
    commands  
    ((counter++))  
done  
```

#### Output Control:
```bash
command | tee file.txt          # Display + save  
command >> file.txt 2>&1        # Append stdout/stderr  
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `if [ ]` → Spaces inside `[ ]` are mandatory. Use `-eq` for numbers, `==` for strings.  
- ✅ `case` → Cleaner than nested `if` for multiple matches. Terminate patterns with `;;`.  
- ✅ `for` → Iterates over lists (`{1..5}`, `*.txt`, `${array[@]}`).  
- ✅ `while`/`until` → Update loop variables to prevent infinite loops.  
- ❌ **Unquoted variables** → May cause word splitting in `[ ]` tests.  

### 4️⃣ **Why / When to Use**  
| Scenario                 | Structure         | Example                    |                 |
| ------------------------ | ----------------- | -------------------------- | --------------- |
| Menu-driven scripts      | `case`            | CIDR.sh options            |                 |
| Iterating files/IPs      | `for`             | `for ip in $(prips $cidr)` |                 |
| Error-tolerant execution | `while` + `break` | Retry failed commands      |                 |
| Real-time logging        | `tee`             | `scan                      | tee -a log.txt` |

### 5️⃣ **Examples**  
#### Example 1: Network Scanner
```bash
for ip in $(prips 192.168.1.0/24); do  
    ping -c 1 $ip >/dev/null && echo "$ip: LIVE" | tee -a live_hosts.txt  
done  
```

#### Example 2: User Menu
```bash
case $choice in  
    1) nmap -sV $target ;;  
    2) ping -c 4 $target ;;  
    3) exit 0 ;;  
    *) echo "Invalid option" && exit 1 ;;  
esac  
```

#### Example 3: Conditional File Processing
```bash
while read -r file; do  
    if [ -f "$file" ]; then  
        wc -l "$file"  
    else  
        echo "Missing: $file" >> errors.log  
    fi  
done < file_list.txt  
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Loop Control**:  
  ```bash
  for i in {1..100}; do  
      [ $i -eq 50 ] && break    # Exit loop early  
      [ $i -lt 10 ] && continue # Skip iterations  
  done  
  ```  
- **Background Processing**:  
  ```bash
  while read ip; do  
      ping $ip &  # Run pings in parallel  
  done < ips.txt  
  ```  
- **Named Pipes for Tee**:  
  ```bash
  mkfifo pipe  
  command | tee pipe > output.log &  
  grep "ERROR" pipe > errors.log  
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ✅ **Quote variables**: `[ "$file" = "test" ]` (safe with spaces).  
- ❌ **Infinite loops**: Always update loop variables (`((i++))`).  
- ✅ **Use `[[ ]]` for regex**: `[[ "$str" =~ ^[0-9]+$ ]]`.  
- ❌ **Overwriting files**: Prefer `>>` or `tee -a` for logs.  

### 8️⃣ **Summary**  
> Key takeaways:  
> - `if`/`case` handle decisions, loops automate repetition.  
> - `tee` splits output for real-time monitoring + logging.  
> - Always validate inputs and exit conditions to prevent hangs.  

### 🔖 Bonus: Pro Tips  
- **Parallel Execution**:  
  ```bash
  for ip in ${ips[@]}; do  
      (ping -c 1 $ip | tee -a ping.log) &  
  done  
  wait  # Wait for all background jobs  
  ```  
- **Colorized Output**:  
  ```bash
  echo -e "\e[31mFAIL\e[0m"  # Red text  
  ```  

---

## **📌 Phase 9: Case Statements**

### 1️⃣ **Introduction / Definition**  
> Case statements (switch-case) provide cleaner pattern matching than `if-elif-else` chains when:  
> - Comparing **exact values** (not ranges/conditions)  
> - Handling **multiple fixed options** (e.g., menus)  
> - Matching **patterns** (wildcards, regex-like syntax)  

Key differences from `if-else`:  
✅ Cleaner syntax for exact matches  
❌ Cannot evaluate boolean expressions (`-gt`, `-lt`)  

### 2️⃣ **Syntax Block**  
#### Basic Structure:
```bash
case $variable in
    pattern1)
        commands
        ;;
    pattern2|pattern3)
        commands
        ;;
    *)
        default_commands
        ;;
esac
```

#### CIDR.sh Example:
```bash
case $opt in
    "1") network_range ;;
    "2") ping_host ;;
    "3") network_range && ping_host ;;
    "*") exit 0 ;;
esac
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `case $var in` → Starts comparison against `$var`  
- ✅ `pattern)` → Matches exact value or wildcard:  
  - `"1"` → Literal `1`  
  - `"*"` → Catch-all (default case)  
  - `[Yy]*)` → Matches "Yes", "yes", etc.  
- ✅ `;;` → Terminates each block (like `break` in C)  
- ✅ `esac` → Ends the `case` statement  

### 4️⃣ **Why / When to Use**  
| Scenario                  | `case` vs `if`        | Example                 |
| ------------------------- | --------------------- | ----------------------- |
| Menu-driven scripts       | ✅ Cleaner with `case` | CIDR.sh options         |
| Exact value matching      | ✅ More readable       | `"yes"`/`"no"` input    |
| Pattern/wildcard matching | ✅ Built-in support    | `[Yy]*` for "Yes"/"yes" |
| Numeric ranges            | ❌ Use `if`            | `[ $num -gt 10 ]`       |

### 5️⃣ **Examples**  
#### Example 1: Simple Menu
```bash
read -p "Action (start|stop|restart): " cmd
case $cmd in
    "start") systemctl start nginx ;;
    "stop") systemctl stop nginx ;;
    "restart") systemctl restart nginx ;;
    *) echo "Invalid option" && exit 1 ;;
esac
```

#### Example 2: Wildcard Matching
```bash
read -p "Confirm (Y/n): " answer
case $answer in
    [Yy]*) echo "Proceeding..." ;;
    [Nn]*) echo "Aborted." && exit 0 ;;
    *) echo "Invalid input" ;;
esac
```

#### Example 3: Multi-Pattern Matching
```bash
case $file_ext in
    "jpg"|"png"|"gif") echo "Image file" ;;
    "txt"|"md") echo "Text file" ;;
    "sh") echo "Script file" ;;
esac
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Regex-Like Patterns**:  
  ```bash
  case $host in
      web*) echo "Web server" ;;       # Starts with "web"
      *db) echo "Database server" ;;   # Ends with "db"
  esac
  ```  
- **Fall-Through (Bash 4+)**:  
  ```bash
  ;&  # Continues to next block (no ;;)
  ```  
- **Exit Codes**:  
  ```bash
  case $(curl -s example.com) in
      *"200 OK"*) exit 0 ;;
      *) exit 1 ;;
  esac
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ✅ **Quote patterns**: `"pattern"` to prevent globbing.  
- ❌ **Missing `;;`**: Causes fall-through (may be unintended).  
- ✅ **Use `*` last**: Default case should be the final pattern.  
- ❌ **Over-nesting**: Avoid complex logic; use functions instead.  

### 8️⃣ **Summary**  
> Case statements excel at:  
> - **Menu systems** (cleaner than `if-elif`)  
> - **Exact/pattern matching** (wildcards, `|` for OR)  
> - **Default fallbacks** (`*` case)  
> Not suitable for numeric ranges/boolean logic.  

### 🔖 Bonus: Pro Tips  
- **Colorized Menus**:  
  ```bash
  echo -e "1) \e[32mScan\e[0m\n2) \e[31mExit\e[0m"  
  ```  
- **Audit Logging**:  
  ```bash
  case $opt in
      "1") echo "$(date): Scan chosen" >> audit.log ;;
  esac
  ```

---
## **📌 Phase 10: Functions**

### 1️⃣ **Introduction / Definition**  
> Functions in Bash allow:  
> - **Code reuse** (avoid repetition)  
> - **Better organization** (modular structure)  
> - **Localized variables** (with `local` keyword)  
> - **Parameter passing** (`$1`, `$2` within function)  
> - **Return values** (exit codes or stdout capture)  

### 2️⃣ **Syntax Block**  
#### Function Definition:
```bash
# Method 1 (explicit)
function name {
    commands
}

# Method 2 (concise)
name() {
    commands
}
```

#### Function Call:
```bash
name          # Without arguments
name "arg1"   # With arguments
```

#### Return Values:
```bash
return 0      # Success (0-255)
echo "value"  # Output capture
```

### 3️⃣ **Explanation of Syntax**  
- ✅ **`function` keyword**: Optional but improves readability.  
- ✅ **Parameters**: Accessed via `$1`, `$2` (scoped to function).  
- ✅ **`local` variables**: Restrict scope: `local var="value"`.  
- ❌ **Global by default**: Undeclared variables affect entire script.  

### 4️⃣ **Why / When to Use**  
| Scenario            | Function Benefit                 | Example                      |
| ------------------- | -------------------------------- | ---------------------------- |
| Repeating code      | Single definition, multiple uses | `network_range()` in CIDR.sh |
| Complex logic       | Isolate and debug separately     | Input validation             |
| Script organization | Break into logical units         | `main()` with sub-functions  |

### 5️⃣**Examples**  
#### Example 1: Basic Function
```bash
function greet {
    echo "Hello, $1!"
}
greet "Alice"  # → "Hello, Alice!"
```

#### Example 2: Return Status
```bash
function is_file {
    [ -f "$1" ] && return 0 || return 1
}
is_file "test.txt"
echo "Exists? $?"  # 0=yes, 1=no
```

#### Example 3: Output Capture
```bash
function get_ips {
    host $1 | grep "has address" | cut -d" " -f4
}
live_ips=$(get_ips "example.com")
```

### 6️⃣ **Advanced Usage / Tricks**  
- **Dynamic Variables**:  
  ```bash
  function set_var {
      local "$1"="$2"  # Safe assignment
  }
  set_var "color" "red"
  ```  
- **Array Arguments**:  
  ```bash
  function process_files {
      for file in "$@"; do
          wc -l "$file"
      done
  }
  process_files *.txt
  ```  
- **Trap Errors**:  
  ```bash
  function safe_rm {
      [ -e "$1" ] || { echo "Missing file"; return 1; }
      rm "$1"
  }
  ```

### 7️⃣ **Tips & Common Mistakes**  
- ✅ **Always `local`**: Prevent side effects: `local counter=0`.  
- ❌ **Overusing globals**: Makes debugging harder.  
- ✅ **Document functions**:  
  ```bash
  # Usage: greet <name>
  # Returns: Greeting string
  function greet { ... }
  ```  
- ❌ **Ignoring returns**: Check `$?` or capture output.  

### 8️⃣ **Summary**  
> Key takeaways:  
> - Use functions for **reusable code blocks**.  
> - **`local` variables** prevent unintended global changes.  
> - Return via **exit codes** (`0`=success) or **stdout capture**.  
> - **Document** purpose/usage for maintainability.  

---

### 🔖 Bonus: Pro Tips  
- **Debugging**:  
  ```bash
  function debug {
      echo "DEBUG: $*" >&2  # Print to stderr
  }
  debug "Variable x=$x"
  ```  
- **Colorized Output**:  
  ```bash
  function warn {
      echo -e "\e[33mWARN: $*\e[0m" >&2
  }
  warn "Low disk space"
  ```  

---

## **📌 Phase 11: Debugging** 

### 1️⃣ **Introduction / Definition**  
> Debugging in Bash involves identifying and resolving:  
> - **Syntax errors** (missing quotes, brackets)  
> - **Logical errors** (incorrect flow/calculations)  
> - **Runtime issues** (permissions, missing files)  
> Primary tools: `-x` (xtrace) and `-v` (verbose) flags  

### 2️⃣ **Syntax Block**  
#### Debugging Commands:
```bash
bash -x script.sh      # Step-by-step execution
bash -v script.sh      # Shows raw script + output
bash -xv script.sh     # Combined verbose tracing
```

#### In-Script Debugging:
```bash
#!/bin/bash
set -x   # Enable debugging from this point
code_block
set +x   # Disable debugging
```

### 3️⃣ **Explanation of Syntax**  
- ✅ `-x` → **Prints commands** with expanded variables/arguments (prefixed with `+`).  
- ✅ `-v` → **Displays raw script** lines before execution.  
- ✅ `set -x/+x` → **Toggle debugging** within script sections.  
- ❌ **No breakpoints**: Unlike IDE debuggers, Bash lacks pause/inspect.  

### 4️⃣ **Why / When to Use**  
| Scenario                   | Tool           | Example                           |
| -------------------------- | -------------- | --------------------------------- |
| Tracing variable values    | `-x`           | See expanded `$domain` in CIDR.sh |
| Verifying control flow     | `-x`           | Confirm `if-else` branch taken    |
| Checking script parsing    | `-v`           | Detect unexpanded variables early |
| Isolating problematic code | `set -x` block | Debug just one function           |

### 5️⃣ **Examples**  
#### Example 1: Basic Debugging
```bash
$ bash -x CIDR.sh inlanefreight.com
+ '[' 1 -eq 0 ']'
+ domain=inlanefreight.com
+ echo -e 'Discovered IP address:\n165.22.119.202'
Discovered IP address:
165.22.119.202
```

#### Example 2: Focused Debugging
```bash
#!/bin/bash
# ... normal code ...

set -x  # Start debug
network_range  # Function to debug
set +x  # End debug

# ... rest of script ...
```

#### Example 3: Verbose Mode
```bash
$ bash -v script.sh
#!/bin/bash
# Check args
if [ $# -eq 0 ]
then
    echo "Error: No args"
fi
...shows raw code before execution...
```

### 6️⃣ **Advanced Usage / Tricks**  
- **PS4 Customization**:  
  ```bash
  export PS4='+ ${BASH_SOURCE}:${LINENO}: '  # Show file/line numbers
  bash -x script.sh
  ```  
- **Log to File**:  
  ```bash
  bash -x script.sh 2> debug.log
  ```  
- **Error Tracing**:  
  ```bash
  trap 'echo "Error on line $LINENO"' ERR
  ```  

### 7️⃣ **Tips & Common Mistakes**  
- ✅ **Start small**: Debug one function/block at a time.  
- ❌ **Over-tracing**: Avoid `-xv` on large scripts (use selectively).  
- ✅ **Clean output**: Redirect noise (`2>/dev/null`) when needed.  
- ❌ **Ignoring exit codes**: Always check `$?` after critical commands.  

### 8️⃣ **Summary**  
> Effective debugging requires:  
> - **Systematic tracing** (`-x` for execution flow).  
> - **Context awareness** (`-v` for pre-execution checks).  
> - **Precision** (`set -x` blocks to isolate issues).  
> Combine with `echo` statements for complex logic.  

### 🔖 Bonus: Pro Tips  
- **Colorized Debugging**:  
  ```bash
  export PS4='\e[33m+ ${BASH_SOURCE}:${LINENO}:\e[0m '  # Yellow trace
  ```  
- **Function Timing**:  
  ```bash
  set -x; start=$SECONDS; network_range; echo "Took $((SECONDS-start))s"; set +x
  ```  
