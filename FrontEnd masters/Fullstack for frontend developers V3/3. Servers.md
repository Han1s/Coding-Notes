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
		- not secure
		- used for validation of files (here is the file, here is md5, compare on your end)
	- SHA1
		- more rigurous
	- SHA256
		- golden standard
		- used by bitcoin
	- openssl is a cryprography toolkit program
- **SALT**
	- random number that is unique to the process

### SSh
- public key & private key
- you connect with you private key and put public key to a server
- if only you hold the private key only you can read the message
- you can add the private key to the keychain so you don't have to specify it every time you ssh to a server
