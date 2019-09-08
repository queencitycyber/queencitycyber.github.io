**Google Cache**

When your goal is to be browsing your target’s website without sending a single packet to their servers, anonymous Googling becomes very helpful.

When you normally perform a Google search, most links will point you directly to the organizations servers, but we don’t want this. If we click on that link, we will be directly interacting with the target. Instead, we want to use a cached version of the page. This is a great way to not just avoid detection and interaction, but also grab content after it has been deleted from the site. So let’s examine this a little more.

In Google, do a search for university of cincinnati”. How many results?

Underneath the blue bolded search result is the domain where the corresponding resource is located. Next to the search result is a green arrow. Click the arrow and select Cached. 

But wait, where is this actual content coming from? We see that Google tells us it’s a cached version of the page, but were do the images and styling come from? Well that’s a good question, because those images are actually coming from the University of Cincinnati. That’s no good – our browser touched UC and we didn't want to!

Lets look back at the cached image from before. Did you notice we were defaulted to the Full version of the page, when there are options for Text-only version as well as viewing the source of the page?



This is what we want. By forcing Google to only display the text version of the target page, we are positive we are only loading content from Google, not our target. We are now free to browse the page and our target would never know.

Not convinced? Let’s exmaine the two URL’s from the Full and Text verions.

Full: `http://webcache.googleusercontent.com/search?q=cache:MiO5INR0R6sJ:www.uc.edu/+&amp;cd=1&amp;hl=en&amp;ct=clnk&amp;gl=us`

Text: `http://webcache.googleusercontent.com/search?q=cache:MiO5INR0R6sJ:www.uc.edu/&amp;hl=en&amp;gl=us&amp;strip=1`

The bold section is all that determines whether or not you send a packet to the target or not. By adding** &strip=1** to the end of your search query, you will only touch Google, and never your target.

