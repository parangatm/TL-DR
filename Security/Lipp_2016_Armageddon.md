## ARMageddon: cache attacks on mobile devices

### Publication:
Moritz Lipp, Daniel Gruss, Raphael Spreitzer, Clémentine Maurice, and Stefan Mangard. 2016. ARMageddon: cache attacks on mobile devices. In Proceedings of the 25th USENIX Conference on Security Symposium (SEC'16). USENIX Association, USA, 549–564.

## Summary: 

Cache attacks on x86 processors have been studied extensively,  but not much studies have been performed on ARM processors. This paper bridges this gap by exploring cache attacks on mobile devices, which are mainly powered by ARM processors.

### Attack Model
**Flush and Reload Attacks**
- attacker flushes shared cache line
- victim loads data into the line during access (or encryption in the specific workload)
- attacker uses timing side channel to determine accessed line

**Prime and Probe Attacks**
- attacker prefills entire data line of cache
- victim access cache during eviction
- timing side channel used for determination of access pattern

### Issues in ARM
ARM processors are inherently difficult to attack due to the system design choices.

1. **Non-Inclusive Cache**
	- Last level cache is L2, instead of L3 in x86
	- LLC is shared but all cores but is non-inclusive
	- data evicted from L1 might still be in L2

2. **No shared Cache**
	- No shared cache between CPUs in modern ARM devices 

3. **No Flush instruction**
	- x86 has unprivileged flush instruction
	- ARM has no flush instruction available to use

4. **Cache Eviction**
	- Pseudo-random replacement in ARM
	- Eviction process adds noise to the data
	
5. **Timing and Clocks**
	- x86: **rdtsc** allows unprivileged cycle count access
	- ARM: needs access to privileged cycle counter

### Attack Scenarios

**Issue 1**: Non-Inclusive Caches
- Caches are data non-inclusive, but instruction inclusive
- Load enough instructions that ends up evicting data from both levels anyways
- Using a remote cache

**Issue 2**: No Flush Instruction
Fill cache with "congruent" addresses so that cache mapping patterns can be predicted and leveraged to flush out desired address.

**Issue 3**: Timing Information
- Unprivileged syscall to get performance information
- POSIX function get difference of time stamps
- Dedicated thread timer

### Example: Android
- Map mobile events to user inputs in Android through covert channels
- Still gives away certain level of information

| Action | Information |
|--------|-------------|
| Key    | Alphabet    |
| Long Press | Enter   |
| Swipe  | Space       |
| Tap    | Backspace   |

- Potentially give a sense of length of passwords, input messages - not much granularity, but still certain insights