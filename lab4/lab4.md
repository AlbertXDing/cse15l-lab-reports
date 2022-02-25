# Lab Four

[My repository](https://github.com/AlbertXDing/CSE15L-RoseateSpoonbill)

[Repository I'm reviewing](https://github.com/AlbertXDing/markdown-parse) 

**What the snippets should preduce**

Snippet 1:

[`google.com, google.com, ucsd.edu]

Snippet 2:

[a.com(()), example.com]

Snippet 3:

[]

**Tests**

![Image](tests.png)

**Test Outputs**

My tests:

![Image](mytests.png)

The bug in snippit 1 can be fixed by making sure any brackets are not counted within backticks. This can be done by recording the index of the backticks, and an if statement within a loop that negates brackets between those indexes.

The bug in snippit 2 can be fixed by searching for the last `)` in the line. Markdownparse also needs to identify `/{`.

Snippit 3 worked as expected.

The tests I am reviewing:

![Image](review.png)