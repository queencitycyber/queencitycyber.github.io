As we saw with XSS, SQLi, and Path Traversal vulnerabilities, as very common and ripe place for these to occur is from user-supplied input!

So any place you see things like "**file=/welcome/resources/private/public.txt**", or "**user=charles**", or "**Enter your name:\_\_\_\_\_**", ask yourself:

* What if I request "/welcome/resources/private/bad.txt"? Or what happens if I just browse to "/welcome/resources/private"?
* What if I request "user=; SELECT \* FROM \*"? 
* What if I entered "&lt;script&gt;echo\("Evil Was Here"\); &lt;/script&gt;" when a website asks for my name?



Of course, only test on things you own or have permission to! :\)







