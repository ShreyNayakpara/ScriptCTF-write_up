**Write Up: Renderer(Web)**

Obviously the flag.txt file contains the fake flag and is of no use. 

Begin by inspecting the html based web page provided and try uploading  something to see if anything changes or not. Also inspect the site to check if anything is hidden inside the html comments or not. However this will unfortunately not result in any solutions for this problem.   
Since the implementation is flawed by carefully exploring the application, we can read **sensitive files** that should not be accessible directly.

A) **Discover vulnerability in the /render/\<filename\> :**

The endpoint **/render/\<filename\>** is vulnerable because it allows us to directly fetch files inside **/static/uploads**.  
Normally, this feature should be restricted to user uploads only, but we can exploit it to read other files stored on the server as long as they are within /static/uploads.

B) **Preparing the secret file :** 

By visiting **/developer**, we notice that the server sets a cookie. The developer page likely checks for a valid cookie to show sensitive information.

But here’s the twist:

* If no cookie exists, the **secret\_cookie.txt** file is empty.  
* If we set **any random cookie value**, the application writes it into **/static/uploads/secrets/secret\_cookie.txt.**

So, to make sure secret\_cookie.txt is not empty, we:

1. Go to **/developer**.  
2. Manually set the cookie in our browser (any random value, e.g., **shrey123**).

Now, the server saves this cookie value in **secret\_cookie.txt.** 

So now we have the actual valid cookie required to access the  protected /developer page. 

C) **Using the valid cookie to get the Flag:**

Finally, we revisit the **/developer** page, but this time we replace our browser cookie with the secret cookie value we retrieved from the text file.

With the correct cookie set, the page authenticates us successfully and displays the flag.

**The Flag – scriptCTF{my\_c00k135\_4r3\_n0t\_s4f3\!}**
