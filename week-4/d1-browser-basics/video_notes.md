# VIDEO 1 - BROWSER AND BOM LECTURE

Document Object Model (DOM)
- hierarchy of nodes that represent HTML elements rendered on the page
- the API to access the elements inside the document


Browser Object Model (BOM)
- hierarchy of browser objects such as window, navigation, location
- larger representation of everything provided by the browser including the 
current document, location, history, frames, and any other functionality the 
browser may expose to JavaScript


![Browser](./images/browser-diagram.png)


The Browser Diagram:

1. User Interface
   - what users interact with
	 - address bar, back/forward buttons, bookmarks, etc.
	 - everything except page content

2. Browser Engine
	 - manages interactions between UI and rendering engine
	 - communicates user input to rendering engine 

3. Render Engine
	 - displays requested page content
	 - parses HTML and uses CSS to build render tree and display content
	 - constructs DOM (obj rep of document tree)
	 - not all browsers use same rendering engnie
	 	 - this is why things look different
		 - chrome (Blink), safari (Webkit)

4. Networking
	- sends network calls, i.e http requests to server
	- asks for images, docs, etc. that make up page

5. Javascript Interpreter
	 - parses and executes JS code (v8)

6. UI Backend
	 - used for drawing basic widgets like checkboxes, inputs, etc. 

7. Data Storage
	 - persistence of data in browser (i.e cookies, web storage)
	 - small database used to preserve state btwn refreshes
	 - cookies vs web storage
		 - Cookies can be read by the server as well as the client. 
		 - Web storage data can be read only client-side.
		 - more to come




# VIDEO 2 - REQUEST/RESPONSE CYCLE


Overview
- browsing web is series of req and res
- request: searching for info or navigating to page
- response: what we expect to receive from req



![Browser](./images/req-res-cycle.png)


Request / Response Cycle Diagram

1. Client Side (browser)
	 - what user interacts with

2. Internet
	 - series of client req and server responses
	 - more on this to come

3. Server side 
	 - handles req and sends res
	 - more on this later



The role of the browser
- used to make req to server
	- can view req/res in Network Tab of Developer Tools
- parses HTML, CSS, JS
- renders info to user by constructing & rendering DOM tree



# VIDEO 3 - WINDOW OBJECT LECTURE


Window Object
- represents an open window in a browser
- thee global object in the browser
- the root of the DOM
	- contains document property used to reference DOM 


Scripts overview
- browser loads HTML top down 
- if it comes accross script:
	- must wait until script downloads & executes before processing rest of page
	- scripts have longer processing time than html


Script placement issues
1. scripts cant see DOM els below thme so they cant add handlers
2. if bulky script is at top of page, it "blocks the page"
	 - users cant see page content till script runs


Workarounds
1. place script at bottom of page
	 - browser sees script only after full html doc is downloaded
	 - for long html docs, may be noticaeble delay
2. `defer` attribute
	 - tells browser to load script in background
	 - doesnt block html from loading
	 - execute script when DOM is ready (before DOMContentLoaded event)
	 - only for external scripts (with src attrib)
	 - scripts still execute in order
	 - "document order"
3. `async` attributee
	 - script is independent
	 - doesnt block html from loading
	 - async scripts dont wait for eachother
	 	 - small script will run before large even if placed after large
		 - DOMContentLoaded may execute before or after
	 - "load first order"
4. can use both to cover all bases
	 - older browsers may not support `defer` 




# VIDEO 4 - BROWSER COOKIES


Cookies
- small piecese of info websites store on your computer
- stored and managed by web browser
- included with http requests
	- server sends data to browser, sent back on next req
- websites can only look at their own cookies
- must have server running
	- browsers do not store cookies for the file:// url protocol,

What are cookies used for?
- used to store stateful info about user
	- ex: personal info, browser history, form inputs
	- session cookie for user login/validation
- expire at specified time


"good" cookie uses
- store login state (session token)
- store website preferences
- personalized content (cart, items you view)


"bad" cookie uses
- advertising/tracking networks can track youa cross web
- multiple websites might use trackign scripts from same advertising network



Creating Cookies with Javascript
- `document` interface represents web page loaded in browser
- cookies stored in browser
- thus: can use `document` to get/set cookies


```js
const firstCookie = "myDog=Bodhi";
document.cookie = firstCookie;

const secondCookie = "myOtherDog=Lucy";
document.cookie = secondCookie;

document.cookie //=> "myDog=Bodhi; myOtherDog=Lucy"

```


Deleting Cookies
- set cookie's expiration date to date in past
- can manually delete in chrome dev tools

```js

document.cookie = "myDog=; expires = Thu, 01 Jan 1970 00:00:00 GMT";
document.cookie //=> ""

```

managing your cookies
- can clear cookies but you'll be logged out of sites you use