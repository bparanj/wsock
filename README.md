# wsock
Simple Websocket Client and Websocket Server https://rubyplus.com/articles/4451-WebSocket-Basics-Hello-World

Let's create a index.html file. This is a simple html template that has jQuery library. It is blank. Let' add a form that has
a text field and a submit button. If we reload this page, we see the text field and the button. We can provide a value and 
click on the button. Nothing happens. We can go to the console and make sure there is no error. When the form is submitted, we
will call the sendMessage javascript function and return false to prevent submission of the form to the server. When the send
button is clicked, we will call the sendMesage javascript function. 

The javascript within this script section will be the Websocket client. The variable ws is initialized to an instance of
WebSocket that will connect to the localhost on port 8080. We can implement the function for the onopen event. We will log
'Connected to server' in the console. We can now implement the sendMessage javascript function. We can call the send method on
web socket object. The value entered in the text field is retrieved using jQuery and passed in as the argument to the send 
method. 

Let's reload the browser. If we inspect this page, we see 'Connection refused' error message. I have already installed node
on my machine. We need to install the web socket server. You can see that this installed bunch of stuff inside the
node_modules. 

Let's develop the Websocket server that will use the ws package we just installed. We need to require the ws package we 
installed. We can create a WebSocket server running on port 8080 and initialize the wss constant. When a client connects,
we can respond to it by handling the on connection event. The function connection will take the ws variable as the input.
We will print client connected to the standard terminal where the server is running. When we receive a message from the client
we will handle the incoming message in this function. We will print the message that was sent by the client. 

Let's start the websocket server. Let's reload the page. We can now enter some text and send it to the server. We get an error
because of wrong method name. We need to restart the server to pickup the changes. Let's send a hello message to the server. 
We now see the client conntected and the message sent by the client on the server log.

This is a very simple Websocket demo. I hope this was useful to introduce the basics of how the websocket client and server
work.
