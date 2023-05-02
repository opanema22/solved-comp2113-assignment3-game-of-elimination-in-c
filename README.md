Download Link: https://assignmentchef.com/product/solved-comp2113-assignment3-game-of-elimination-in-c
<br>
<strong>Problem 1: Game of Elimination in C++</strong>

Consider a prize to be awarded to a winner among n &gt; 0 contestants by a game of elimination. The n contestants first line up in a line, and are assigned the numbers 1 to n one by one.

The host of the game then decides on an integer k &gt; 1, and starting from contestant 1, the host counts k contestants down the line and eliminates the k-th contestants from the circle. He then continues to count for another k contestants, and eliminates the k-th contestants from the line. When he counts to the end of line, he will continue counting from the beginning of the line. This process repeats until there is only one contestant remains who will be the winner of the prize.

For example, if n = 7 and k = 3,The initial line: 1234567, count to 3 and contestant 3 is eliminatedLine now becomes: 124567, continue counting from 4 and contestant 6 is eliminatedLine now becomes: 12457, continue counting from 7 and contestant 2 is eliminatedLine now becomes 1457, continue counting from 4 and contestant 7 is eliminatedLine now becomes 145, continue counting from 1 and contestant 5 is eliminatedLine now becomes 14, continue counting from 1 and contestant 1 is eliminatedWinner is contestant 4

Write a <strong>C++ program</strong> which implements a circular linked list (see Module 8 Guidance Notes p.92) to determine which contestant will win the prize.

<strong>Program input.</strong> Two input numbers n and k (n &gt; 0 and k &gt; 1).

<strong>Program output.</strong> The winner of the game.

<strong>Requirement:</strong> You will need to implement the circular linked list on your own, i.e., you may NOT use any STL containers or external linked list libraries.

<strong>Idea:</strong>

<ul>

 <li>Use the program build_list_forward.cpp of Module 8 as a basis for your work. The program essentially has built a linked list; to turn it into a circular linked list, you just need to point the next pointer of the last node to the head of the list.</li>

 <li>You will need to build a circular linked list containing the numbers 1 to n</li>

 <li>You will then need to traverse through the linked list and remove a node once you have traversed for k nodes.</li>

 <li>After removing a node, you should check if there remains only one node in the list. If yes, the winner is identified.</li>

 <li>Remember to free all memories used by the linked list before the program terminates.</li>

</ul>

<strong>Hint:</strong>

<ul>

 <li>Study carefully build_list_forward.cpp and build_list_sorted.cpp of Module 8. They should contain the main building blocks for you to finish this task.</li>

 <li>It is expected that you will only need to write no more than 20-30 lines of additional code, after reusing the appropriate codes in build_list_forward.cpp and build_list_sorted.cpp. Of course, it is OK if you write more than that.</li>

</ul>

<strong>Sample Test Cases</strong>

User inputs are shown in blue.

1_1:

7 3

4

1_2:

5 2

3

1_3:

1 6

1

1_4:

2 5

2

1_5:

100 5

47

1_6:

1000 8

185

1_7:

1200 23

473

1_8:

100000 9

42610

<strong>Problem 2: STL – Log Analyzer</strong>

You are provided with a template program 2.cpp. Complete the program and the program will read and process a web log data file from user input (cin). The program will then print out the 5 most popular pages, and the 5 most active users and the corresponding pages they have visited.

The log file consists of records of three types, each record occupies exactly one line. Here is the format of these three types of record:

<strong>Page record</strong>: PAGE &lt;page id&gt; &lt;page url&gt;<strong>User record</strong>: USER &lt;user id&gt;<strong>Visiting record</strong>: VISIT &lt;page id&gt;

A <strong>page</strong> record represents a page on the web server. A <strong>user</strong> record represents a user that accesses the system. A <strong>visiting</strong> record represents a visit by the user indicated by the most recent user record. Here is a sample data file:

PAGE 1288 /library

PAGE 1282 /home

USER 20686

VISIT 1288

VISIT 1282

USER 20687

VISIT 1288

In this case, we have 2 pages (/library and /home) on the server. Two users have accessed the server, one (#20686) visiting 2 pages (/library and /home) and the other (#20687) visiting 1 page (/library).

You can assume the followings regarding the data file:

<ul>

 <li>The data file always consists of the three types of records only</li>

 <li>The page ids are unique across all PAGE records</li>

 <li>The user ids are unique across all USER records</li>

 <li>The page ids are unique across all VISIT records of a user</li>

 <li>VISIT records will only appear after the first USER record</li>

 <li>The page id in a VISIT record appears only after its corresponding PAGE record</li>

 <li>There will be at least 5 users and 5 pages</li>

</ul>

The followings have been implemented for you:

<ul>

 <li>A Page structure, each Page object consists of the id, path and a counter to count the number times it is being visited</li>

</ul>

struct Page {

int id;

string path;

int counter;

Page(int id, string path) {

this-&gt;id = id;

this-&gt;path = path;

counter = 0;

};

};

<ul>

 <li>A STL vector for organizing the Page objects</li>

</ul>

vector&lt;Page&gt; pages;

<ul>

 <li>A User structure, each User object consists of the id and the pages the user visited</li>

</ul>

struct User {

int id;

vector&lt;string&gt; visits;

User(int id) {

this-&gt;id = id;

};

void add_visit(int page_id) {

…

};

int size() const {

return visits.size();

};

void print_visits() {

…

}

};

<ul>

 <li>A STL vector for organizing the User objects</li>

</ul>

vector&lt;User&gt; users;

<ul>

 <li>A function to overload &lt; operator for the comparison of 2 pages based on their ids</li>

</ul>

bool operator&lt;(const Page &amp; a, const Page &amp; b) {

return (a.id &lt; b.id);

};

You are required to complete the missing functions in the template program to make it work.<em>Note</em>: The functions Page() and User() in the structs Page and User above are called <strong>struct constructors</strong>. Refer to Module 10 “C Programming (Part 3)” for the discussion on the struct constructor functions. It works the same in C++.

<strong>Sample Test Cases</strong>

You are provided with 4 sample test cases. We will use the first test case and detail the test run below.

Assume we have input2_1.txt in the current directory. If we run the program like this (assuming that we are working on Linux):

$ g++ -pedantic-errors -std=c++11 2.cpp -o 2

$ ./2 &lt; input2_1.txt

The program will print:

*** 5 most popular pages ***

36:/msdownload

32:/ie

17:/products

17:/search

13:/sitebuilder

*** 5 most active users ***

23:10068

– /activeplatform

– /activex

– /automap

– /frontpage

– /gallery

– /ie

– /intdev

– /isapi

– /java

– /msdownload

– /musicproducer

– /office

– /promo

– /sbnmember

– /search

– /sitebuilder

– /spain

– /vbasic

<em>…</em>

<em>[snipped]</em>

<em>…</em>

11:10019

– /athome

– /clipgallerylive

– /games

– /isapi

– /kb

– /logostore

– /msdownload

– /msoffice

– /ntserver

– /products

– /search

<strong>Note:</strong>

<ul>

 <li>If two pages are equally popular, the pages are ordered lexicographically.</li>

 <li>If two users visit the same number of pages, the users are ordered by their id ascendingly.</li>

 <li>The list of pages a user visit must be printed in ascending order.</li>

 <li>You can choose not to use the provided template program and implement in your own way. However, your program must contain the provided Page and User structures and use STL vectors for storage.</li>

 <li>Once again, you MUST use STL vectors in your program. Your program will be checked and your score will be 0 if we find that you use traditional arrays to store pages and users in your implementation.</li>

</ul>