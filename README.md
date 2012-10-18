## Usage - Client

```javascript
    var SSDP = require('ssdp').SSDP;
    var client = new SSDP;
    
    client.on('notify', function () {
		console.log('Got a notification.');
	});
	
	client.on('response', function inResponse(msg, rinfo) {
		console.log('Got a response to an m-search.');
	});
	
	ssdp.search('urn:schemas-upnp-org:service:ContentDirectory:1');
	
	// Or maybe if you want to scour for everything
	
	ssdp.search('ssdp:all');
	
	// This should get you at least started.
```

## Usage - Server

```javascript
	var SSDP = require('ssdp').SSDP;
	
	var server = new SSDP;
	server.addUSN('upnp:rootdevice');
	server.addUSN('urn:schemas-upnp-org:device:MediaServer:1');
	server.addUSN('urn:schemas-upnp-org:service:ContentDirectory:1');
	server.addUSN('urn:schemas-upnp-org:service:ConnectionManager:1');
	
	server.on('advertise-alive', function (heads) {
		// Expire old devices from your cache.
		// Register advertising device somewhere (as designated in http headers heads)
	}
	
	server.on('advertise-bye', function (heads) {
		// Remove specified device from cache.
	}
	
	// This should get your local ip to pass off to the server.
	require('dns').lookup(require('os').hostname(), function (err, add) {
		server.server(add);
	};
```

## Author

Initial commit of this module is a clone of https://bitbucket.org/Xedecimal/node-ssdp, commit 0c6cd0a (2012-03-21).

Forked with author's permission.

# License

(The MIT License)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

