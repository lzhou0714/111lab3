# Hash Hash Hash

This code implements a concurrent hash table in two different ways, 
the first way prioritizing correctness and the second also to improve 
performance.

## Building

Using the given code and the pthread libray, I added in mutexes to make my code thread safe

## Running

Show an example run of your (completed) program on using the `-t` and `-s` flags
of a run where the base hash table completes in between 1-2 seconds.

## First Implementation

I created a single mutex for the entire hash table under struct hash_table_v1 
and initialized it in hash_table_v1_create(). To ensure correctness I locked the 
entirety of the hash_table_v1_add_entry function so that no other thread may attempt
to access or modify the hashtable while the current thread is adding the entry.
This includes the initiation of variables at the beginning as many depends on
accessing the head of the current bucket, which will change when we insert at the head.
I also added an unlock under the if statement in the case that the value
already exists.

### Performance

gets better with more threads because it


bash-5.2$ ./hash-table-tester -t 16 -s 25000
Generation: 72,508 usec
Hash table base: 1,275,708 usec
  - 0 missing
Hash table v1: 1,602,784 usec
  - 0 missing

./hash-table-tester -t 8 -s 50000
Generation: 73,646 usec
Hash table base: 1,075,112 usec
  - 0 missing
Hash table v1: 1,486,182 usec
  - 0 missing

./hash-table-tester -t 4 -s 100000
Generation: 70,484 usec
Hash table base: 1,049,858 usec
  - 0 missing
Hash table v1: 2,013,679 usec
  - 0 missing

./hash-table-tester -t 2 -s 200000
Generation: 72,008 usec
Hash table base: 1,273,805 usec
  - 0 missing
Hash table v1: 1,825,333 usec
  - 0 missing




Run the tester such that the base hash table completes in 1-2 seconds.
Report the relative speedup (or slow down) with a low number of threads and a
high number of threads. Note that the amount of work (`-t` times `-s`) should
remain constant. Explain any differences between the two.

## Second Implementation

Describe your second implementation strategy here (the one with a multiple
mutexes). Argue why your strategy is correct.

### Performance

Run the tester such that the base hash table completes in 1-2 seconds.
Report the relative speedup with number of threads equal to the number of
physical cores on your machine (at least 4). Note again that the amount of work
(`-t` times `-s`) should remain constant. Report the speedup relative to the
base hash table implementation. Explain the difference between this
implementation and your first, which respect why you get a performance increase.

## Cleaning up

Explain briefly how to clean up all binary files.
