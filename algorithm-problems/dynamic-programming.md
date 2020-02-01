# Dynamic programming problems

## Count ways to assign unique cap to every person
* Problem
    * There are 100 different types of caps each having a unique id from 1 to 100. Also, there are ‘n’ persons each having a collection of a variable number of caps. They will go to a party where none of them will wear the same type of cap. Count the total number of arrangements or ways such that none of them is wearing the same type of cap.
    * https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/
* Brute-force
    * DFS/ recursion/ backtrack.
    * For each person, iterate through possible hats.
    * For each hat, record it is used, then try next person.
    * End case 1: if the last person can pick a hat, count++.
    * End case 2: if a person has no hat to pick, backtrack.
    * When back tracking, remove the hat from used set.
    * Time complexity: O(prod(hat(1~n))) => O(100^n) => O(2^n), where n is the number of people.
    * Space complexity: O(n) as the depth of search grows with the number of people.
* Bottleneck
    * Stack memory usage is O(n).
* Dynamic programming approach
    * Define state
        * __i__ = a subset of people.
        * __j__ = a subset of hats.
        * __value(i, j)__ = the number of combinations where a subset of people i are wearing a subset of hats j without conflict.
        * Because we need to include all people, but not always all hats. We define hat subset j as all hats from #1 to #j.
        * Because people substes are not ordered, we can use a n-bit bitmask to represent subset i. For example, 01001 represents that subset of 1st and 4th persons have picked hats.
    * State transition
        * Tabluation: value(i, j) = sumof(value(one-person-less-than-i, j - 1)), where the person added to subset can pick hat j.
        * Memorization: value(i, j) = sumof(value(one-person-more-than-i, j + 1)), where the person added to subset can pick hat j.
    * Time complexity: O(2^n) as the dp table is 2^n long and 100 wide, and the algorithm needs to go through at least the length of the table.
    * Memory complexity: O(2^n) as the table is 2^n long.
    * Max stack height: Tabulation = O(1), Memorization = O(100) = O(1).
* Notes
    * In this problem, DP does not seem to improve time complexity, as we still need to go through each combination to count them, which can be O(2^n) if all people have all hats.
    * DP approach puts a limit on the number of people, as bitmask is limited by integer size. DFS approach does not have this limit.
    * DFS approach puts a limit on the stack height. If memory is ample, it is not too bad.
