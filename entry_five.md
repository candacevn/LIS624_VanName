# Entry Five
This entry will cover installing Apache2 and creating a web page using the program.

## Getting the page up and running
- Check that the VM's packages are up-to-date (see Entry Two for a step-by-step guide).
- Use ``` apt search package_name ``` to identify a package from a list of results (in this case, Apache2).
- Use ``` apt show package_name ``` to view the details of a specific package.
- Check the pakage's status using ``` systemctl status package_name ``` (in our case, we want to see Apache 2 **Enabled** and **Active**).

## Browsing
- The web server will display a default page, letting me know the server is working and accpeting http traffic.
- Text-based browsing (which is done in the VM) can be achieved using ``` w3m ``` which can be installed similarly to Apache.
- To connect ``` w3m ``` to the web server, we use the command ``` w3m 127.0.0.1 ``` or ``` w3m localhost ```. Both of these serve as **loopback IP addresses** , pointing our network traffic back at itself.
- Web-based browsing can be achieved by clicking the External IP linked to the VM in Google Cloud Console.

## The Web Page
- The web server essentially hosts files stored in the **document root** to be displayed as pages when requested by users (the rewuest occurs when we attempt to connect to the server via browsing).
- The **document root** is ``` /var/www/html/ ``` and should already contain the file for the default page, ``` index.html ```.
- Any file can be created in the document root using a text editor like ``` tilde ```, but the files should be saved as .html.
- Other files stored at the root can be accessed via web-browsing using ``` http://public_ip_address/file_name.html ```.
- It is important to browse the page in order to ensure all changes have been saved.

## Reflections
* I learned about **document roots** and **loopback ip addresses**, which are important to understand for document storage and browsing connections.
* I learned how to download new packages to the VM, which means I have the ability to add packages to future projects.
* I don't feel like I struggled with this assignment because the instructions were pretty clear and I have gotten more comfortable with using the VM.

## HTML and CSS
This and following sections will include some of my research and notes concerning how to code using HTML and CSS. Dr. Burns gave me the link to his [Semantic Web Development](https://cseanburns.github.io/semantic_web_development/p1-introduction-to-semantic-web-development.html) class's textbook, which I have used to make some of the following notes
## HTML: The Framework
* HTML is a markup language that provides structure to our document, like headers, paragraphs, images, and more.
* Here are references for HTML Elements: [Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements)
					 [W3C](https://www.w3.org/TR/2012/WD-html-markup-20121025/elements-by-function.html)
* HTML5 or semantic HTML meets issues related to accessibility, usability, and inclusion, in comparision to earlier HTML codes and other programming/scripting languages like JavaScript.

## CSS: A nice coat of paint
* CSS is used to style the document, concerned more with presentation rather than content like HTML. CSS is technically out of scope for this class, but I find it personally interesting.
* There are a few ways to apply CSS to a webpage: external, internal, and in-line.
	1. External CSS uses a stylesheet saved in the project's directory to dictate the style of all the website's web pages.
	2. Internal CSS uses the ``` <style> ``` tag in the ``` <head> ``` section of the web document. This applies the style to just the page the ``` <style> ``` tag was created in.
	3. Inline uses the ``` <style> ``` attribute to change individual elements in the web document.
* When I have more free time, I will update this entry with more notes.