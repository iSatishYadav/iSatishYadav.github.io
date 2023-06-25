Developers spend much more time reading the code than writing it. So, after optimizing code for time and space complexity — optimize it for reading complexity. There’s even a term for that — Cyclomatic Complexity.

After having written more than 1 million lines of code and having read much more awful lot, here are the top 5 things I wish I knew sooner to write more readable code.

1. Your code will be read more times than you think.
A common misconception among upcoming and new developers is — Software Development is about writing the O(n) complexity code of binary tree inversion. And I hate to break it to you — it’s not.

A lot of time it’s about, adding a new feature or fixing a bug in an existing code base with its own coding conventions, naming conventions, design, and architecture. So reading and understanding the existing code becomes one of the most important parts of the job.

> Great developers spend a lot of time reading other people’s code.

2. Readable code > Smart Code
In almost all programming languages and frameworks, there are numerous ways of doing the same thing. The smarter and one-liner way may feel good to write at the moment, but often it’s not good for the next reader — which can be YOU six months down the line.

So,

> If there is a little more verbose but more readable way to do it — do it and your future self will thank you later.

3. Document the “why” instead of “what”.
Usually, I’m against documentation. Because

> The code is literally the instructions written to build something.

The only parts that need documentation are the “why”. Why we’ve written this piece of code this way?

If you don't understand the "what"? Maybe you shouldn't be the one changing it.

4. Describe everything your function/method does in the name.
> There are only 2 difficult things in Computer Science — Cache Invalidation and Naming

Just by reading the name of the function, its intent should be clear.

“But then large functions would have way big names” — that’s the point. Your function should do only 1 or a few things and do it properly.

> Refactor the function/method if it’s job can’t be described in the name.

5. “Deadline” is a silly excuse for writing bad code.
“There’s no time to write good code” is not a good enough excuse for writing bad code.

> Checking for the readability of your code is like flushing the toilet — it’s part of the ceremony. You do it no matter how late you are for anything else.

So next time you write code, think about your future self, what would you answer to that person? Don’t bring the shame to yourself. Write readable code.

Happy Coding!
