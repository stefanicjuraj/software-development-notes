# Code Obfuscation

In software development, obfuscation is a techniques for deliberately hardening the code (source or machine code) to resist any kind of code analysis ([static code analysis](static-code-analysis), [binary code analysis](binary-code-analysis), or [dynamic code analysis](dynamic-code-analysis)).

While the process may modify actual method instructions or data, it does not alter the output of the program.

Obfuscations techniques could be divided into two categories:

- **Data Obfuscation** - Distorts data in order to hide information. Masks the original data by replacing it with a new content.
- **Control Flow Obfuscation** - Produces spaghetti logic that can be very difficult for an attacker or reverse engineer to analyze. Modifies the program so that it yields the same result when run, but is impossible to decompile into a well-structured source code and/or is more difficult to understand. Branching, conditional, and iterative constructs that produce same result are being generated to replace the original coding, yielding non-deterministic semantic results when decompilation is attempted.

![[control-flow-obfuscation.png]]

![[control-flow-obfuscation-1.png]]

**Secure Sensitive Data in Non-Production Environments** - Many companies mask their production data for research, analysis, testing and development purposes. Production data often contain sensitive information and when being accessed by testers, developers, analysts, external consultants and offshore teams who do not have the necessary clearances can leave
organizations vulnerable to attacks, data leaks and non-compliance with regulations, such as, GDPR, HIPAA, PCI, FISMA etc.

**Malware** - Malware developers use this technique for many years to avoid the analysis of both antivirus detection engines and reverse engineers.

**Protection of Intellectual Property** - Skype, Apple’s iMessage, and the Dropbox client protect their communication protocol formats with obfuscation and cryptography.

**Deter Non-Expert Hackers** - Determined expert hackers will succeed anyways, but it will at least slow them down. Reduce the number of successful hacks. Limit the effectiveness of the hacks.

**Code Minimizer** - Reducing the size of the file containing the source code.

**Recreational Challenge**

Many companies mask their production data for research, analysis, testing and development purposes.

![[data-masking.png]]

Also referred to as data anonymization, data masking, data privacy, data scrambling.

**Constant Unfolding** performs the opposite operation of a technique known as constant folding (compiler optimization technique). A constant value that is used in the program is replaced by some computation that produces the same value.

**Substitution** is another authentic looking value is used to substitute the existing value. For example, in data which contains student records, the name can be randomly substituted from a supplied or customized look up file.

**Shuffling** is similar to substitution but the substitution set is being derived from the same data that is being obfuscated.

**Number and date variance** applies a random numeric variance to data fields while still preserving the data distribution and preventing traceability back to a known data value.

**Encryption** - the encrypted application requires the decryption key to be applied to view the original data/classes.

## Obfuscation Drawbacks

- Harder to maintain.
- Can affect performance either by introducing bad constructs or not allowing JVM or compilers to be able to optimize the code.
- May break your code in case certain APIs are being used (e.g. Reflection - ability of a program to examine, inspect and modify its own structure and behavior during runtime).
- May create false positive in anti-virus software.

## Obfuscation Tools

A variety of tools exist to perform or assist you with code obfuscation, starting from experimental research tools created by academics, up to commercial products written by professionals, and open-source software.

There also exist de-obfuscation tools that attempt to reverse the process done by an obfuscator.
