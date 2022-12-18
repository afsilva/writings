Artificial Intelligence and Linux (2nd Edition) LG #50 [![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](silva.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](lg_backpage50.html)  

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

Artificial Intelligence and Linux (2nd Edition)
===============================================

#### By [Anderson Silva](/cdn-cgi/l/email-protection#c4a5a2b7ada8b2a584a8ada6a1b6b0bdeaa1a0b1)

> _\[This is a revision of my article that came out in July 1999. The article had a few errors and was missing its conclusion. I have fixed these errors in this revision and added a few references for anyone who is interested in looking deeper into the field of AI. One thing I would like to stress is that this article covers only a very minimal area in AI. -AS\]_

* * *

Artificial Intelligence is a very controversial subject, but the way I will approach it in this article is simple and fast. The way I have been approaching AI is not through the philosophical or biological aspect, but just as a computational subject. When humans want to fly, they don't need to study the birds to learn how to do it, they just get into an airplane. This is my way of approaching AI. We want to solve puzzles and games through a computer without really comparing the way a human accomplishes tasks differently from a computer.

For the first time in the history of my school, there was going to be offered an Artificial Intelligence (AI) class. I was very excited about this class because you hear a lot about AI, but you don't really see a lot of material for it on magazines and online articles.

Probably the greatest example of an AI application is Turing's Test. The test consists in a person being a room with a computer terminal, and this person would start to chat with the computer. At the end the person would have to figure out if he talked to a real person on the other end of the terminal or with a computer program. And if the user confuses the person with the computer then we would have reached AI.

At LU we chose Prolog to be the implementation tool for AI. Our labs at school are Windows NT based and we have only one Linux machine which is designated to students. But I have been a Linux user for almost 2 years, and I wanted to implement all my Prolog assignments in Linux.

I did some research on the web and I found a great Prolog compiler for Linux. Prolog is like Linux in a certain way, there are several flavors that you can pick from. The one I chose was SWI Prolog ( [www.hio.hen.nl/faq/SWI-Prolog.html](http://www.hio.hen.nl/faq/SWI-Prolog.html)). Prolog is a very flexible language. Unlike other languages like C, C++ or Java, Prolog is based on formal mathematical logic, in this case: Predicate Calculus. A Prolog program is normally made of facts with a set of rules. To reach the final solution it has to satisfy this set of rules. Interpreting these rules allows the computer to deduce the solution by itself. In Prolog the facts are normally stored in a separate file called the knowledge base, and rules in another file that is the actual program.

Allow me to show a very basic search algorithm known as the [Depth First Search](gx/silva2/ai_graph.jpg)(click for image).

This program allows you to find a solution path from the START point to some GOAL. The DFS algorithm is pretty simple so implement, since it is a recursive algorithm. What DFS does is go through the child of each node in a sequential manner, therefore even though it is an easy way to implement a search algorithm, it is not time efficient.

**But why search a graph?**

The nodes of a graph correspond to partial problem solution states and the arcs correspond to steps in a problem-solving process. The graph also defines one or more goal conditions, which are solutions to a problem instance. The process of finding a solution path from the start to a goal is called State space search (Luger and Stubblefield 1997).

Through a graph you can find the solutions to several problems that in our minds seems so easy. For example, an entire chess game can be represented in graphs, mathematical problems, virtually anything that involves decision making.  

* * *

The Program below is the representation of the graph above in Prolog. \[[text version](misc/silva2/list1.txt)\]

\=========LIST #1=============

% Name:   Anderson Silva
% Date:   March 10, 1999

% ================================
% A graph that will be used for a
% Depth First Search Algorithm
% Knowledge Base.
% ================================

% linked/2
% A nodes and its children

linked(a, \[b,c,d\]).
linked(b, \[e,f\]).
linked(c, \[g,h\]).
linked(d, \[i,j\]).
linked(e, \[k,l\]).
linked(f, \[l,m\]).
linked(g, \[n\]).
linked(h, \[o,p\]).
linked(i, \[p,q\]).
linked(j, \[r\]).
linked(k, \[s\]).
linked(l, \[t\]).
linked(m, \[\]).
linked(n, \[\]).
linked(o, \[\]).
linked(p, \[u\]).
linked(q, \[\]).
linked(r, \[\]).
linked(s, \[\]).
linked(t, \[\]).
linked(u, \[\]).

% arc/2
% A rule that checks to see if
% there is an arc between two given nodes.

arc(X,Y):- linked(X,L), member(Y,L).

* * *

The algorthim that searches the graph for a specific goal: \[[text version](misc/silva2/list2.txt)\]

\=========# LIST #2=============

% Name:   Anderson Silva
% Date:   March 10, 1999
% ================================
% This is the Depth First Algorithm
% implemented in Prolog that will
% use the graph.pl knowledge base
% ================================

% reverse\_write/1
% Inverts the order of the stack.

reverse\_write(\[\]).
reverse\_write(\[H|T\]):-reverse\_write(T), write(H), nl.

% solve/2
% Gives the path in the reverse
% order since dfs is implemented as
% a stack

solve(INode, Solution):- consult('graph.pl'),
                         query\_goal,
                         dfs(\[\], INode, Solution),
                         reverse\_write(Solution).

% query\_goal/0
% Creates the goal to be reached
% during execution
% We start with abolish, so if solve is ran more
% than once, it will make sure it
% forgets the old goals and only look for the
% new on.

query\_goal :- abolish(goal(Node)),
              write('Goal? \[Followed by a period\]'),
              nl,
              read(Node),
              assert(goal(Node)).


% goal/1
% When the program runs for the first time
% query\_goal needs to abolish at least one goal
% and that is why goal(standard) is used.

goal(standard).

% dfs/3
% The Actual recursive algorithm for the
% Depth First Search

dfs(Path, Node, \[Node|Path\]):- goal(Node).
dfs(Path, Node, Sol):- arc(Node, Node1),
                       \\+ member(Node1, Path),
                       dfs(\[Node|Path\], Node1, Sol).

* * *

With this Prolog program, you will be able to run a Graph Search on your computer. Notice that LIST #1 defines the graph, therefore you can make changes in LIST #1 and make your own graphs, and see if the algorithm will find the node you are looking for.

There are several other search algorithms to solve AI problems, for example: Breadth-First Search, Heuristic Search, Pattern-Directed Search, and others.

As I said, this is one small topic in AI, that I thought it would be useful for some of you that would like to learn more about AI. If you would like some other areas to reasearch, but you do not even know where to start, here are a few topics: Expert Systems, Robots, Knowledge Representation, Fuzzy Logic, Natural Language, Automated Reasoning, and others.

Finally, I would like to leave you with three books that I used in college about AI.

1.  Artificial Intellegence: Structures and Strategies for Complex Problem Solving. Luger, George and Stubblefield, Willian.
2.  Prolog Programming in Depth. Covington, Michael et al.
3.  Are We Unique?. Trefil, James.

* * *

##### Copyright © 2000, Anderson Silva  
Published in Issue 50 of _Linux Gazette_, February 2000

* * *

[![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](silva.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](lg_backpage50.html)
