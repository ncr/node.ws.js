# Minimal WebSockets for node.js

* Interface is almost the same as tcp.createServer(...)
* Flash policy file requests are handled (hardcoded, permissive), see http://github.com/gimite/web-socket-js

## Example

<pre><code>
  var sys = require("sys"),
    ws = require("./ws");
  
  ws.createServer(function (websocket) {

    websocket.addListener("connect", function (resource) { 
      // emitted after handshake

      sys.debug("connect: " + resource);
      setTimeout(websocket.close, 10 * 1000); // server closes connection after 10s, will also get "close" event

    }).addListener("data", function (data) { 
      // handle incoming data

      sys.debug(data);

      // send data to client
      websocket.write("Thanks!"); 

    }).addListener("close", function () { 

      // emitted when server or client closes connection
      sys.debug("close");

    });
  }).listen(8080);
</code></pre>

### Author

Jacek Becela
