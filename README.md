# Assignment 4. Patient Zero

Student ID: 251187
Name: Ilya D.
Group: SE-2511

This file is the report. Fill it in as you go. How to start: `START_HERE.md`. The task: `docs/Assignment4.pdf`.

## Program output

The 9 lines your program prints on your data (`java -cp out Main`):

    Mutations: 74
    Shared core: 1221
    Marker hits: 4
    First hit: 9489
    Border length: 4
    Shared words: 664
    Tests needed: 38
    Cheapest testing: 183
    Longest chain: 25

My outbreak report (a screenshot of `output/outbreak.html`):

![outbreak](output/outbreak.png)

## Questions

Answer in your own words, two or three sentences each.

Mission 1. What does the cell d[i][j] of your table mean, and how is it computed from other cells?

It's the minimum changes to turn the first i letters of A into the first j of B. It takes the minimum of inserting, deleting, or replacing.

Mission 2. How is the longest common subsequence different from the longest common substring? My Shared core is bigger than the number of letters that are the same at the same place: why?

Substrings' subsequences only need the same relative order. Shared core is larger because insertions/deletions shift the string without breaking the relative order of the core letters.

Mission 3. What does the prefix function tell you, and why does the pointer in the text never go back in KMP? What is the Border length of my marker and what does it mean?

It tracks the longest prefix/suffix. KMP uses this to slide the pattern forward without moving the text pointer backward. Border length is the last value which shows how many end letters exactly match the start letters.

Mission 4. Why must you compare the letters after the hashes are equal? What happens to the cost of Rabin-Karp if many windows have the same hash?

Because different words can produce the same hash. If many hashes match, the algorithm must do a letter-by-letter check, increasing the cost from O(1) to O(n).

Mission 5. What are the two states of a person in your DP, and how do you get the answer for a person from its children? Why does a greedy "test the person with most links first" not always give the cheapest answer?

A person is either tested or not tested. A tested parent chooses the cheapest valid option for each child, while an untested parent must take the tested cost of every child. Greedy fails because testing the most linked person might cost more than testing multiple cheap leaf nodes.

## AI use

Gemini - code review, general assistance.

## Timing (Mission 7)

Milliseconds, average of 3 runs, from `java -cp out Bench`.

| test | size | time                            |
|---|---|---------------------------------|
| naive search | 20 000 / 40 000 / 80 000 | 50ms / 91.7ms / 191.4ms         |
| KMP | 20 000 / 40 000 / 80 000 | 2.8ms / 1.1ms / 0.4ms           |
| edit distance | 500 / 1000 / 2000 / 4000 | 5.7ms / 6.6ms / 19.9ms / 65.4ms |

What do the numbers say about how the time grows? When you double the size, by how much does each time grow? Two or three sentences.

Naive search time doubles when the text size doubles which corresponds to linear growth. KMP is highly efficient, so its execution time remains near zero and varies only slightly. Edit distance time quadruples each time the size doubles, matching its $O(n^2)$ complexity.

## Complexity

n is the length of the text (or of a strain), m the length of the pattern, k the length of the window, v the number of people. Fill in every algorithm you wrote.

| algorithm | time | space | assumptions                                                                                              |
|---|-|-|----------------------------------------------------------------------------------------------------------|
| Edit distance |O(n × m)|O(n × m)| n and m are the lengths of the two strains; entire matrix is kept in memory.                             |
| LCS |O(n × m)|O(n × m)| n and m are the lengths of the two strains; entire matrix is kept in memory.                             |
| Prefix function and KMP |O(n + m)|O(m)| m is pattern length, n is text length. Space is O(m) to store the prefix array.                          |
| Rabin-Karp (shared words) |O(n + m)|O(m)| Assumes hash collisions are rare so letter-by-letter comparisons are infrequent.                         |
| Tree DP |O(v)|O(v)| The graph is a valid tree with no cycles, exactly v-1 edges. Space covers DP arrays and tree structures. |

## Before you submit

- The four files in `data` and the screenshot `output/outbreak.png` are in the repository.
- `java tools/Check.java` shows all examples right.
- This README is filled in, the program output and the section AI use included.
- The work is pushed to main (at least one commit per mission) and the repository is public.
- The link is attached in Moodle.
