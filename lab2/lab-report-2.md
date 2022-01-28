# Debugging Lab Report

**Checking For Brackets**

![Image](change1.png)

Symptom:

![Image](bug1symptom.png)

[Test File](https://github.com/AlbertXDing/CSE15L-RoseateSpoonbill/blob/main/test-file2.md)

We found that MarkdownParse did not work if a file did not have brackets. This was because `closeParen` would always be -1 and `currentIndex` would therefore never be greater than `markdown.length()`. This was fixed by checking to make sure the file had brackets in it.




**Making Sure Parenthesis Come Right After Brackets**

![Image](change2.png)

Symptom:

![Image](bug2symptom.png)

[Test File](https://github.com/AlbertXDing/CSE15L-RoseateSpoonbill/blob/main/test-file6.md)

MarkdownParse was recording links that did not immediately follow brackets. This was fixed by checking if the opening parenthesis immediately followed closing brackets.

Symptom:

![Image](bug2symptom.png)

**Checking For Images**

![Image](change2.png)

Symptom:
![Image](bug3symptom.png)

[Test File](https://github.com/AlbertXDing/CSE15L-RoseateSpoonbill/blob/main/test-file4.md)


MarkdownParse could not distinguish between links and images. This was fixed by checking for `!` before brackets, and skipping the parenthesis right after. 

