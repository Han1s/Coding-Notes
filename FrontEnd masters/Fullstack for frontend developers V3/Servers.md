## basic node server
```js
const http = require("http");
const fs = require("fs");
const PORT = 3000;

const server = http.createServer((req, res) => {
	res.writeHead(200, { "content-type": "text/html" })
	fs.createReadStream("index.html").pipe(res);
});

server.listen(PORT);
console.log(`Server started on port ${PORT}`);
```

- **virtualization**: dividing server resources into virtual computers
- **virtual machine**: digital version of a physical computer
- **VPS**: virtual private server

## Buying a VPS
- www.digitalocean.con
- for server chose a LTS version. Use the most stable version.

## Operating system
- everythin in UNIX is either a file or operating system

### Security and hashing 
- hashing
	- MD5 most common
		- very predictable and not very long
	- SHA1
	- SHA256
	- openssl is a cryprography toolkit program