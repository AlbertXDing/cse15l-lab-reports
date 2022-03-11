# Lab 5

I croned the two repositories on `ieng6`, then I run the shell script `script.sh` and piped the results to files. I found tests with different results using the `diff` command :

`diff CSE15L-RoseateSpoonbill/tests.txt markdown-parse/results.txt `

![Image](Differences.png)

**Difference 1:**

The first difference I picked is on line 230 for `tests.txt` and `results.txt`. This shows that a difference was on test file `201.md`.

![Image](Location.png)

This test file has the following content:

```
[foo]: <bar>(baz)
[foo]
```

My implemenation prints `[]` while the provided MarkDownParse implemenation prints `[baz]`. I believe my implementation is correct. The provided MarkDownParse does not check if the parenthesis following brackets is directly after the brackets. The following code:

```
String potentialLink = markdown.substring(openParen + 1, closeParen).trim();
```

needs to add a check like this:

```
String potentialLink;
if(openParen - nextCloseBracket == 1) {
    potentialLink = markdown.substring(openParen + 1, closeParen).trim();
}
```

**Difference 2:**

The second difference is on Line 270 for `tests.txt` and `results.txt`, corresponding to a difference in test file `22.md` which has the following content:

`[foo](/bar\* "ti\*tle")`

My implemenation prints `[/bar\* "ti\*tle"]` while the provided MarkDownParse implemenation prints `[]`. I believe both implemenations have bugs. It should print `[/bar\*]`. My implemenation needs to check for the title attribute of the link, which is in the format of `[link](url "title")`. It needs to add a code block to check the space and the double quotes, like this:

```
int ii = markdown.substring(openParen + 1, closeParen).indexOf(" ");
if( ii != -1 && && markdown.charAt(closeParen-1) == '"' && markdown.charAt(openParen + 2 + ii) == '"'){
    toReturn.add(markdown.substring(openParen + 1, openParen + 1 + ii));
}
```

The provided MarkDownParse implemenation needs to check the space in the parenthesis correct to include the title just like above. So the following code block:

```
if(potentialLink.indexOf(" ") == -1 && potentialLink.indexOf("\n") == -1) {
    toReturn.add(potentialLink);
    currentIndex = closeParen + 1;
}
```
needs to be replaced by this block:

```
if(potentialLink.indexOf("\n") == -1) {
    int ii = potentialLink.indexOf(" ");
    System.out.println(markdown.charAt(closeParen-1));
    System.out.println(markdown.charAt(openParen + 2 + ii));
    if( ii != -1 && markdown.charAt(closeParen-1) == '"' && markdown.charAt(openParen + 2 + ii) == '"'){
        toReturn.add(markdown.substring(openParen + 1, openParen + 1 + ii).trim());
    }
    else
        toReturn.add(potentialLink);
    currentIndex = closeParen + 1;
}