# Hello World Websocket Client and Websocket Server using Node

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

## Screencast Outline

1. Basic template:

```javascript
const WebSocket = require('ws');

const ws = new WebSocket('ws://www.host.com/path');

ws.on('open', function open() {
  ws.send('something');
});

ws.on('message', function incoming(data) {
  console.log(data);
});


var WebSocketServer = require('ws').Server,
    wss = new WebSocketServer({port: 8080});

wss.on('connection', function(ws) {
    console.log('client connected');
    ws.on('message', function(message) {
        console.log('received: %s', message);
    });
});
```


2

```javascript
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
  ws.on('message', function incoming(message) {
    console.log('received: %s', message);
  });

  ws.send('something');
});


wss.on('connection', function(ws) {
    console.log('client connected');
    ws.on('message', function(message) {
        console.log('received: %s', message);
    });
});
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>WebSocket Hello World</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script>

    </script>
</head>
<body lang="en">

  <form id="echo_form" >
    <input class="form-control" type="text" name="message" id="message" placeholder="Type text to echo in here" value="" autofocus/>

    <button type="button" id="send" class="btn btn-primary">Send</button>
  </form>

</body>
</html>
```

3

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>WebSocket Hello World</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script>

    </script>
</head>
<body lang="en">

  <form id="echo_form" onsubmit="sendMessage(); return false;">
    <input class="form-control" type="text" name="message" id="message" placeholder="Type text to echo in here" value="" autofocus/>

    <button type="button" id="send" class="btn btn-primary" onclick="sendMessage();">Send</button>
  </form>

</body>
</html>
```

4.

```html
<!DOCTYPE html>
<html lang="en">
<head>
<title>WebSocket Hello World</title>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script>
        var ws = new WebSocket("ws://localhost:8080");
        ws.onopen = function(e) {
          console.log('Connected to server');
        }

        function sendMessage() {
            ws.send($('#message').val());
        }
    </script>
</head>
<body lang="en">

  <form id="echo_form" onsubmit="sendMessage(); return false;">
    <input class="form-control" type="text" name="message" id="message" placeholder="Type text to echo in here" value="" autofocus/>

    <button type="button" id="send" class="btn btn-primary" onclick="sendMessage();">Send</button>
  </form>

</body>
</html>
```

5.

server.js

https://rubyplus.com/articles/4451-WebSocket-Basics-Hello-World

# Streaming Data from Server using Websocket in Node

In the Websockets basics episode, we saw how to send data from the client to the server. In this episode, we will see how to send data from the server to the client. 

Let's create index.html file. This is a simple html template. We will use jQuery to display the random numbers we get from the server on the browser. The page does not display anything. We can check the console to make sure there are no error messages. Let's add a div with id randomNumbs. 

We require the Websocket library ws we installed in the earlier episode. We establish connection to the server. When the connection is opened, we can log 'Connected to server' message in the console. 

We are now ready to receive messages from the server in the onmessage handler. We can log the data we get from the server in the console. When we receive a data from the server, we append the number to the div with id randomNums. Whenever the data is received from the server, the onmessage javascript function is fired.

Let's create server.js file for the Websocket server that will listen on port 8080. We first require the websocket library. We can create a new WebSocket server that listens on port 8080. When a client connects to the server, we can handle it in the connection function that takes an argument. We can handle any incoming message from the client in the incoming message function. We will just log the message we received from the client in the console. 

We can define our own function that takes the ws parameter as the argument. This function generates a random number and sends it to the client by calling the send on the client object ws. The setInterval function is used to stream random number at one second at a time to the client so that we can see the numbers emerging one by one in the browser. This function calls our custom function, sendRandomNumbers repeatedly once every second. 

Let's comment out the streaming part. We can start the server. Let's reload the page. We don't see anything in the console. Let's uncomment the streaming code and reload the browser. We need to restart the server. If we reload the browser, we now see the random numbers from the server. We can check the logs for the messages we log on the console. We see the 'Connected to server' on the onopen event. 

When a connection is establised by the client, we can log it here. We can restart the server. If we reload this page, we see the 'Connected to server' message in the console. We don't need to receive any message from the client for this streaming example. You can modify this program to take a stock symbol from the client and stream the stock price of a particular stock to the browser. This requires combining this example with the example shown in the previous episode.

Let's clear the log and reload the browser. You can see the console log message that we added to the server in the terminal. Let's stop the server. If we click on the onopen event handler, we go to the corresponding line in the code. Similarly, the onmessage goes to the onmessage event handler. 

In a real app like tennis score board, there will be an unknown amount of delay in getting the latest score. The score board on the browser will be updated whenever the point is won. I used the Server example found in the ws library github home page as a starting point for this demo.


The server will send a random number once every second. 
