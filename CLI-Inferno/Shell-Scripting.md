## **📌 Phase 1: Introduction to Bash Scripting**

Bash is a scripting language used to interact with Unix-based operating systems and execute commands. Since May 2019, Windows has supported the Windows Subsystem for Linux (WSL), allowing users to run Bash in a Windows environment. Mastering Bash is essential for working efficiently with these systems. Unlike programming languages, scripting languages do not require compilation before execution.

As penetration testers, we must work with both Windows and Unix-based systems. Understanding these systems, especially for privilege escalation, is crucial. On Unix-based systems, knowing how to use the terminal, filter data, and automate tasks is vital. Large enterprise networks often require handling vast amounts of data, which makes sorting and filtering critical for identifying security gaps quickly.

Scripting enhances efficiency by combining multiple commands and processing individual results. Bash scripting follows a structure similar to programming languages, including:
- Input & Output
- Arguments, Variables & Arrays
- Conditional Execution
- Arithmetic
- Loops
- Comparison Operators
- Functions

### 1️⃣ Executing Bash Scripts
Scripts automate repetitive tasks and process large data sets. Unlike compiled programs, scripts are executed by an interpreter—in this case, Bash. To run a script, specify the interpreter and the script name:

**Examples:**
```bash
bash script.sh <optional arguments>
sh script.sh <optional arguments>
./script.sh <optional arguments>
```

### Example: CIDR.sh Script
This script identifies the network range of a domain, checks for active hosts, and provides relevant details.

Running the script:
```bash
./CIDR.sh inlanefreight.com
```

**Output:**
```
Discovered IP address(es):
165.22.119.202

Additional options available:
1) Identify the corresponding network range of the target domain.
2) Ping discovered hosts.
3) All checks.
*) Exit.

Select your option: 3

NetRange for 165.22.119.202:
NetRange:       165.22.0.0 - 165.22.255.255
CIDR:           165.22.0.0/16

Pinging host(s):
165.22.119.202 is up.

1 out of 1 hosts are up.
```

### 2️⃣ CIDR.sh Code:
```bash
#!/bin/bash

# Check for given arguments
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:\n\t$0 <domain>"
	exit 1
else
	domain=$1
fi

# Function: Identify Network Range
function network_range {
	for ip in $ipaddr
	do
		netrange=$(whois $ip | grep "NetRange\|CIDR" | tee -a CIDR.txt)
		cidr=$(whois $ip | grep "CIDR" | awk '{print $2}')
		cidr_ips=$(prips $cidr)
		echo -e "\nNetRange for $ip:"
		echo -e "$netrange"
	done
}

# Function: Ping Discovered Hosts
function ping_host {
	hosts_up=0
	hosts_total=0
	echo -e "\nPinging host(s):"
	for host in $cidr_ips
	do
		ping -c 2 $host > /dev/null 2>&1
		if [ $? -eq 0 ]
		then
			echo "$host is up."
			((hosts_up++))
		else
			echo "$host is down."
		fi
		((hosts_total++))
	done
	echo -e "\n$hosts_up out of $hosts_total hosts are up."
}

# Identify IP Address of Target Domain
hosts=$(host $domain | grep "has address" | cut -d" " -f4 | tee discovered_hosts.txt)

echo -e "Discovered IP address:\n$hosts\n"
ipaddr=$(host $domain | grep "has address" | cut -d" " -f4 | tr "\n" " ")

# Menu Options
echo -e "Additional options available:"
echo -e "\t1) Identify the corresponding network range of the target domain."
echo -e "\t2) Ping discovered hosts."
echo -e "\t3) All checks."
echo -e "\t*) Exit.\n"

read -p "Select your option: " opt

case $opt in
	"1") network_range ;;
	"2") ping_host ;;
	"3") network_range && ping_host ;;
	"*") exit 0 ;;
esac
```

The script is structured into the following sections:
1. **Check for Given Arguments:**
    - Verifies if a domain is provided; if not, displays usage instructions.
2. **Identify Network Range:**
    - Uses `whois` to retrieve the network range and saves it to `CIDR.txt`.
3. **Ping Discovered Hosts:**    
    - Uses a loop to check which IPs in the network range are active.
4. **Identify IP Addresses:**
    - Extracts the IPv4 addresses of the specified domain.
5. **Menu Options:**
	- Provides different functionality based on user selection.

---

## **📌 Phase 2: Conditional Execution**

Conditional execution allows us to control the flow of a script by specifying different conditions. Without it, we could only execute commands sequentially, limiting flexibility.

By defining conditions, we determine which sections of code should execute based on specific values. When a condition is met, the corresponding code runs while others are skipped. Once that section completes, the script continues executing subsequent commands.

Let's analyze the first part of a Bash script:
```bash
#!/bin/bash

# Check if an argument is provided
if [ $# -eq 0 ]; then
    echo -e "You need to specify the target domain.\n"
    echo -e "Usage:"
    echo -e "\t$0 <domain>"
    exit 1
else
    domain=$1
fi
```

Key Components:
1. **Shebang (`#!/bin/bash`)** - Specifies the script interpreter.
2. **Conditional Execution (`if-else-fi`)** - Controls flow based on conditions.
3. **Echo (`echo`)** - Prints messages to the terminal.
4. **Special Variables (`$#`, `$0`, `$1`)**:
    - `$#` - Number of arguments passed.
    - `$0` - Script name.
    - `$1` - First argument (domain).
5. **Variable (`domain`)** - Stores the input for later use.

### 3️⃣ Understanding Shebang (`#!`)

The **shebang** (`#!`) at the top of a script specifies the interpreter that executes the script. While we typically use Bash (`/bin/bash`), other interpreters like Python or Perl can be specified:
```python
#!/usr/bin/env python
```

```perl
#!/usr/bin/env perl
```

### 4️⃣ Using If-Else for Conditional Execution

Conditional checks are fundamental in scripting. The basic `if` condition follows this logic:
```bash
if [ condition ]; then
    # Code to execute if the condition is met
fi
```

Example:
```bash
#!/bin/bash

value=$1

if [ $value -gt 10 ]; then
    echo "Given argument is greater than 10."
fi
```

Execution:
```bash
$ bash script.sh 5
$ bash script.sh 12
Given argument is greater than 10.
```

### 5️⃣ Extending Conditions with `elif` and `else`

Adding `elif` (else-if) and `else` provides additional condition checks:
```bash
#!/bin/bash

value=$1

if [ $value -gt 10 ]; then
    echo "Given argument is greater than 10."
elif [ $value -lt 10 ]; then
    echo "Given argument is less than 10."
else
    echo "Given argument is not a number."
fi
```

Execution:
```bash
$ bash script.sh 5
Given argument is less than 10.

$ bash script.sh 12
Given argument is greater than 10.

$ bash script.sh Blah-Blah
script.sh: line 5: [: Blah-Blah: integer expression expected
script.sh: line 8: [: Blah-Blah: integer expression expected
Given argument is not a number.
```

### 6️⃣ Handling Multiple Conditions

We can extend our script to check for multiple conditions:
```bash
#!/bin/bash

# Check for the correct number of arguments
if [ $# -eq 0 ]; then
    echo -e "You need to specify the target domain.\n"
    echo -e "Usage:"
    echo -e "\t$0 <domain>"
    exit 1
elif [ $# -eq 1 ]; then
    domain=$1
else
    echo -e "Too many arguments provided."
    exit 1
fi
```

Here, the script:
- Exits if **no** arguments are given.
- Assigns the input to `domain` if **one** argument is provided.
- Exits if **more than one** argument is given.

This structured approach ensures scripts behave predictably based on user input.

---

## **📌 Phase 3: **