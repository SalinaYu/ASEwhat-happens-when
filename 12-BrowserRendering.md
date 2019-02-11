### Page Rendering

_Context: Browser has parsed the HTML (DOM tree) and the CSS (CSSOM tree). How are the parsed elements placed within the given frame?_

_OSI Layer(s): 7_

![Webkit Rendering](https://cdn-images-1.medium.com/max/1600/1*WyLhGzIR7BuAhVD4yH20TQ.png)

* Create a 'Frame Tree' or 'Render Tree' by traversing the DOM nodes, and calculating the CSS style values *for each node*.
* Calculate the preferred width of each node in the 'Frame Tree' bottom up by summing the preferred width of the child nodes and the node's horizontal margins, borders, and padding.
* Calculate the actual width of each node top-down by allocating each node's available width to its children.
* Calculate the height of each node bottom-up by applying text wrapping and summing the child node heights and the node's margins, borders, and padding.
* Calculate the coordinates of each node using the information calculated above.
* More complicated steps are taken when elements are ``floated``, positioned ``absolutely`` or ``relatively``, or other complex features are used. See http://dev.w3.org/csswg/css2/ and http://www.w3.org/Style/CSS/current-work for more details.
* Create layers to describe which parts of the page can be animated as a group without being re-rasterized. Each frame/render object is assigned to a layer.
* Textures are allocated for each layer of the page.
* The frame/render objects for each layer are traversed and drawing commands are executed for their respective layer.
* All of the above steps may reuse calculated values from the last time the webpage was rendered, so that incremental changes require less work.
* The page layers are sent to the compositing process where they are combined with layers for other visible content like the browser chrome, iframes and addon panels.
* Final layer positions are computed and the page is rendered via Direct3D/OpenGL/the OS's window server (the details of which we don't really care about).


## Post-rendering and user-induced execution

After rendering has completed, the browser executes JavaScript as a result of some timing mechanism (such as a Google Doodle animation) or user interaction (typing a query into the search box and receiving suggestions). Plugins such as Flash or Java may execute as well, although not at this time on the Google homepage. Scripts can cause additional network requests to be performed, as well as modify the page or its layout, causing another round of page rendering and painting.

_Demonstration Step:_
* Show in developer tools (Network tab) that the search bar JS is making additional queries for every key stroke.

[Back to README.md](./README.md)