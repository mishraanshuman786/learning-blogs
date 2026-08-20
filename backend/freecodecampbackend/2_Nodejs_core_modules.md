<!-- Nodejs Core Modules -->

# What Is the fs Module and How Does It Work?
Node.js lets you do this with the fs or file system module.

The Node fs module provides you with methods for working with files and folders, including opening and closing, reading and writing, and deleting operations.

The fs module is a Node.js standard module, so it's available to use as long as you have Node.js installed in your environment. To use the module, you import it this way:
```
const fs = require("fs");
```
The flexibility the fs module offers is that it allows you to use its methods both synchronously and asynchronously. The fs module methods are asynchronous by default, but for every method, there's a synchronous form:
```
fs.writeFile() // Asynchronous file writing
fs.writeFileSync() // Synchronous file writing

fs.readFile() // Asynchronous file reading
fs.readFileSync() // Synchronous file reading

fs.open() // Opens a file
fs.openAsBlob() // Opens as blob
fs.openSync() // Synchronous open
fs.opendir() // Opens directory
fs.opendirSync() // Synchronous directory open
```

### It doesn't end there. Depending on your needs, you can use the methods in three ways:

- with callbacks, for example `fs.writeFile()` (asynchronous)
- with promises if you prefer the `async/await` syntax, for example `fs.promises.writeFile()`
- synchronously, for example, `fs.writeFileSync()`

Here's the basic syntax for the asynchronous usage of the methods:
```
fs.writeFile("filePath", "content", "utf8", (err) => {
  if (err) {
    throw err;
  }
  console.log("File written to!");
});
```

For the promises version, you can import that from fs/promises or chain promises to your fs import. Here's the syntax:
```
async function promisesExample() {
  try {
    await fs.promises.writeFile("filePath", "content", "utf8");
    console.log("File written to!");
  } catch (err) {
    console.error("Error:", err);
  }
}

promisesExample();
```

And here's the synchronous version:
```
try {
  fs.writeFileSync("filePath", "content", "utf8");
  console.log("File written to!");
} catch (err) {
  console.error("Error:", err);
}
```

Note that using any of the methods synchronously is blocking. In other words, your program will stop running and wait until the operation is finished before moving on to the next line of code.

For quick scripts, small projects, or one-off tasks, synchronous methods are probably fine. But in real world applications, blocking I/O (input/output) becomes a problem because it can freeze other parts of your app while Node waits for the file system to finish its operations. That slows things down and hurts performance and user experience.

That's why asynchronous methods exist. They let the rest of your program continue running while Node handles file operations in the background. Traditionally, this used callbacks, but those can get messy fast as your app grows.

Promises and async/await solve that problem. They are still non-blocking, but the code reads like normal synchronous code and is much easier to maintain.

For this reason, the promises-based approach is generally preferred today.

### writeFile() method
The `writeFile()` method lets you write to an existing file. If the file doesn't exist, it creates it in the current directory, then writes the specified content to it.

Here's how to use the `writeFile()` method:
```
const fs = require("fs/promises");

async function writeToFile() {
  try {
    await fs.writeFile(
      "article.md",
      "## Node `fs` Module: The Complete Guide",
      "utf8",
    );
    console.log("File written to!");
  } catch (err) {
    console.error("Error writing to file:", err);
  }
}

writeToFile(); // File written to!

```

Here's the content of the article.md file after that:
```
## Node `fs` Module: The Complete Guide
```
### appendFile() method
The appendFile() method lets you add to the content of an existing file. Here's how to use it:
```
const fs = require("fs/promises");

async function appendToFile() {
  try {
    await fs.appendFile(
      "article.md",
      "\nIn this article, you will learn all there is to know about the Node fs module...",
      "utf8",
    );
    console.log("File appended to!");
  } catch (err) {
    console.log("Error appending to file:", err);
  }
}

appendToFile(); // File appended to!
```
### readFile() method
The readFile() method lets you see what the content of a file is:
```
const fs = require("fs/promises");

async function readFileContent() {
  try {
    const fileContent = await fs.readFile("article.md", "utf8");
    console.log("File content:", fileContent);
  } catch (err) {
    console.error("Error reading file:", err);
  }
}

readFileContent();

/*
File content: ## Node `fs` Module: The Complete Guide

In this article, you will learn all there is to know about the Node fs module...
*/
```

If you don't specify the utf8 character encoding, you will get the content of the file as a buffer:
```
async function readFileContent() {
  try {
    const fileContent = await fs.readFile("article.md");
    console.log("File content:", fileContent);
  } catch (err) {
    console.error("Error reading file:", err);
  }
}

readFileContent();

/*
File content: <Buffer 23 23 20 4e 6f 64 65 20 60 66 73 60 20 4c 69 62 72 61 72 79 3a 20
 54 68 65 20 43 6f 6d 70 6c 65 74 65 20 47 75 69 64 65 0a 0a 49 6e 20 74 68 69 73 20 ... 
72 more bytes>
*/
```

In the next lesson, you will learn how to handle a buffer like this with the Node.js Buffer module.

### unlink() method
Lastly, the unlink() method lets you delete a file:
```
const fs = require("fs/promises");

async function deleteFile() {
  try {
    await fs.unlink("article.ts");
    console.log("File deleted successfully!");
  } catch (err) {
    console.error("Error deleting file:", err);
  }
}

deleteFile();
```
If the file does not exist, you get an error message similar to this:
```
Error deleting file: Error: ENOENT: no such file or directory, unlink 'article.ts'
```
If it exists, the file is deleted, and you get the success message you set.


# What Is the Buffer Module and How Does It Work?


JavaScript was originally created to run in web browsers, where its main role was to make web pages interactive. Because of this, early JavaScript focused primarily on handling text in forms and manipulating the Document Object Model (DOM).

However, not all data on the web is text. Files, images, and videos are binary data, which require different handling mechanisms. In browsers, these types of data are typically processed by specialized components of the browser rather than by JavaScript itself.

Modern browsers use rendering engines and JavaScript engines to manage these tasks — for example, Blink (with V8) in Chrome, WebKit (with JavaScriptCore) in Safari, and Gecko (with SpiderMonkey) in Firefox.

Node.js does not run in the browser, so it needed its own way to handle binary data, especially when handling file input and output (I/O) and TCP streams, where data comes in chunks. That's where the Buffer module comes in.

The Node.js Buffer module lets you work with binary data like files, images, or network streams directly. With it, you can store and manipulate binaries directly in memory.

Just like the fs module, Buffer is one of the core Node.js modules, so you don't need to install it separately before using it.

To use it, import the module first by destructuring:
```
const { Buffer } = require("buffer");
```

Then call Buffer with the methods it provides. For example, Buffer.from() lets you create a buffer from a string, array, or other raw data.

```
// Create a buffer from a string
const myStrBuffer = Buffer.from("freeCodeCamp");
console.log(myStrBuffer); // <Buffer 66 72 65 65 43 6f 64 65 43 61 6d 70>

// Create a buffer from an array of numbers
const myNumBuffer = Buffer.from([
  70, 82, 69, 69, 67, 79, 68, 69, 67, 65, 77, 80,
]);

console.log(myNumBuffer); // <Buffer 46 52 45 45 43 4f 44 45 43 41 4d 50>
```

console.log(myNumBuffer); // <Buffer 46 52 45 45 43 4f 44 45 43 41 4d 50>
While it is possible to use some methods from the Buffer module without importing it first, other methods aren't available unless you explicitly import Buffer. So it's recommended that you always import Buffer whenever you use it in your projects.

You can access individual buffer elements just like an array:
```
console.log(myNumBuffer[0]); // 70
console.log(myStrBuffer[0]); // 102
```
You can also use the toString() method on the buffers to see what they really look like:
```
console.log(myStrBuffer.toString()); // freeCodeCamp
console.log(myNumBuffer.toString()); // FREECODECAMP
```
`Buffer.alloc()` lets you create a new buffer of a given size (number of bytes).Every byte inside it is automatically filled with 0:
```
const someBuffer=Buffer.alloc(10);
console.log(someBuffer);    // <Buffer 00 00 00 00 00 00 00 00 00 00>
```

You can  see that the Buffer is initialized with zeroes, based on the size passed into the `alloc()` method.

You can go ahead and use the `Buffer.write()` method to write to this buffer:
```
someBuffer.write('Hello fCC');

console.log(someBuffer);  // <Buffer 48 65 6c 6c 6f 20 66 43 43 00>
console.log(someBuffer.toString());   // Hello fCC
```

If you write more data than the buffer can hold, it will be truncated:

```
someBuffer.write("Hello freeCodeCamp");

console.log(someBuffer); // <Buffer 48 65 6c 6c 6f 20 66 72 65 65>
console.log(someBuffer.toString()); // Hello free
```

Finally, you can use Buffer.byteLength() to show the number of bytes needed to store a string in a certain encoding:
```
console.log(Buffer.byteLength("Hello freeCodeCamp")); // 18
```

Other `Buffer`` methods include:

`Buffer.isBuffer()`: checks if a given object is a buffer     
`Buffer.compare()`: compares two buffers and returns their sort order     
`Buffer.concat()`: joins multiple buffers together into one

# What Is the Crypto Module and How Does It Work?
Crypto is another core module that's built into Node.js. It includes tools for things like hashing, encryption, decryption, and creating digital signatures, all of which are used to protect sensitive information and keep your app secure.

`crypto` gives you low-level building blocks, not plug-and-play security. Writing your own encryption or authentication code can be unsafe if you're not careful. In most cases, it's best to use well-tested libraries like `bcrypt` for password hashing or `jsonwebtoken` (JWT) for handling logins and tokens.

That said, it's still useful to understand how some of the methods in the crypto module work.

To use these methods, you need to import the crypto module:
```
const crypto = require("crypto");
```

Some methods are used for data tranformations purposes, such as the one for hashing and encrypting data, and some others are for key and security management, such as the ones for generating random values and creating secrets.

## Methods for Hashing and encrypting data:
- `createHash()` is usefull for hashing passwords and fingerprinting files. To use it , you pass in your algorithm.
- use the `update()` method to feed in the data
- and finally use `digest()` with an encoding to get the hash value.

```
const crypto = require("crypto");

const hashedPassword = crypto
  .createHash("sha256")
  .update("myStrongPassword")
  .digest("hex");

console.log("createHash result:", hashedPassword);
// createHash result: f92c9cfa0ead1bcec05ca75888a4074ba994ad237e5e2a8c7cc6a620378c061d
```

createHmac() does almost the same thing as createHash(), but it takes things to the next level by accepting a secret key, so only someone with that key can verify the hash. It is ideal for authentication and verifying data integrity:

```
const crypto = require("crypto");

const hashedMessage = crypto
  .createHmac("sha256", "secretkey")
  .update("important-secret-message")
  .digest("hex");

console.log("createHmac result:", hashedMessage);
// createHmac result: da48d6f026b6036286b1fb872c63264130d5cc4271f3a213bb6ddca5a023e77e
```

The `createCipheriv()` and `createDecipheriv()` methods encrypt and decrypt data. They both take in an algorithm, a key, and an `iv`, which is a block of random or unique data used at the start of the encryption process:
```
createCipheriv(algorithm, key, iv);
createDecipheriv(algorithm, key, iv);
```

To decrypt the data, the key must be the same, otherwise, the decryption will fail, and you'll either get an error or unreadable gibberish instead of the original message.

Here are the two in action:
```
const crypto = require("crypto");

// A key must match the algorithm length. Here AES-256 is 32 bytes
const key = Buffer.from("12345678901234567890123456789012");

// A fixed IV, 16 bytes for AES
const iv = Buffer.from("1234567890123456");

const cipher = crypto.createCipheriv("aes-256-cbc", key, iv);

let encrypted = cipher.update("Hello campers!", "utf8", "hex");
encrypted += cipher.final("hex");

console.log("Encrypted data:", encrypted);
// Encrypted data: 4ee93aa398ab44e3540e4a67ca96bc8c

// Decrypt the "Hello campers!" message
const decipher = crypto.createDecipheriv("aes-256-cbc", key, iv);
let decrypted = decipher.update(encrypted, "hex", "utf8");
decrypted += decipher.final("utf8");

console.log("Decrypted data:", decrypted);
// Decrypted data: Hello campers!
```

### Another crypto method for data transformation is sign() and verify(). 

`sign()` creates a digital signature from some data using a private key. This signature proves that the data came from the holder of the private key and has not been tampered with.

`verify()` then checks that signature, and it fails if the data or signature does not match.

### Now, let's look at the crypto methods for generating random values and creating secrets.

`randomBytes()` takes in a `size` and generates cryptographically secured tokens. That makes it good for generating UUIDs (universally unique IDs). In addition, it's a good replacement for `Math.random()`, which is not secure for tokens and keys.

```
console.log("Random Bytes:", crypto.randomBytes(16));
// Random Bytes: <Buffer 01 88 aa 1e 2c 38 48 39 26 e1 6b a9 d8 c5 ed 49>
```
The output is a buffer by default. As you learned in the lesson on the Buffer module, you can convert that Buffer to a string with the `toString()` method:
```
console.log("Random Bytes:", crypto.randomBytes(16).toString("hex"));
// Random Bytes: a6154ef5a296fa176ad0f332bd94d712
```
The `'hex'` argument in `toString('hex')` here tells Node to encode the binary data from the Buffer as a hexadecimal string.

The `randomInt()` method takes in a `min` and `max` values and generates a secure random integer between them. It is useful for OTPs and random selection.
```
console.log("Random Int:", crypto.randomInt(0, 100)); // 89
```

Again, the upgrade over `Math.random()` and `Math.floor()` is that the method uses cryptographically secure randomness under the hood, so attackers can't predict the resulting random number.

Another method is `createSecretKey()`. It takes a buffer and generates a raw byte wrapped into a `KeyObject`:
```
const crypto = require("crypto");

const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret); // SecretKeyObject [KeyObject] { [Symbol(kKeyType)]: 'secret' }
```

You can then use the `export` method to send out that `KeyObject`:
```
const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret.export());
// <Buffer 53 06 a1 c7 75 69 8b 38 8b a4 b2 f7 1b bc b8
// ae e2 d1 bf 67 af 1a 6a 0a 6e a0 29 62 bb 52 52 32>
```
And finally, use `toString()` on the buffer to see the string representation of it:
```
const secret = crypto.createSecretKey(crypto.randomBytes(32));
console.log(secret.export().toString('hex'));
// 32dfe5917668580160986f1623bf8152913329c71163be9c3404a110cd78efd6
```

In addition to these, there are:

- `createPublicKey()` and `createPrivateKey()` that lets you work with keys generated elsewhere
- `createDiffieHellman()` for two parties to generate a shared secret without sending the secret directly
- `Certificate()` for working with the one used in HTTPS, so you can parse, export, and verify certificate contents

# What Is the os Module and How Does It Work?

The OS module is another standard module that comes built into Node.js.

It lets you interact with the current operating system Node is running on so you can access vital information like the OS type, CPU details, available memory, total memory, network interfaces, and more.

To use the OS module, you import it this way:
```
const os = require("os");
```

## Some usefull methods are:

### platform()
The `platform()` method retrieves the operating system Node is currently running on:
```
const os = require("os");
console.log(os.platform()); // darwin
```

It can be useful for implementing cross-platform scripting:
```
if (os.platform() === 'win32') {
 // Windows specific code
} else {
 // Non-Windows specific code
}
```

### arch()
The `arch()` method shows a string representing the CPU architecture Node.js was compiled for:
```
const os = require("os");
console.log(os.arch()); // arm64
```
This can be useful if you want users to download the correct binaries and dependencies for a given architecture.

Other possible values are `'x64'`, `'arm'`, `'arm64'`, `'ia32'`, `'mips'`, `'ppc'`, and others.

### type()
`type()` gets the official OS name, so you can programmatically identify operating systems:
```
const os = require("os");
console.log(os.type()); // Darwin (the core OS for macOS, iOS, and other Apple products)
```
### release()
`release()` shows the system's OS kernel version, the core part of the operating system that manages system resources and communication between hardware and software components. This method can be useful for tracking compatibility between OS kernel versions and server requirements.

It returns this as a string like '20.6.0':
```
const os = require("os");
console.log(os.release()); // 25.0.0
```

### version()
`version()` returns the specific operating system version with more details than the `release()` method:
```
const os = require("os");
console.log(os.version());
// Darwin Kernel Version 25.0.0: Wed Sep 17 21:41:39 PDT 2025;
// root:xnu-12377.1.9~141/RELEASE_ARM64_T8103
```

### cpus()
`cpus()` returns an array of objects with details about each logical CPU core. This can help monitor CPU load:
```
const os = require("os");
console.log(os.cpus());

/*
[
 {
   model: 'Apple M1',
   speed: 2400,
   times: { user: 2184260, nice: 0, sys: 1767340, idle: 8344200, irq: 0 }
 },
 {
   model: 'Apple M1',
   speed: 2400,
   times: { user: 2049430, nice: 0, sys: 1641050, idle: 8612980, irq: 0 }
 },
 {
   model: 'Apple M1',
   speed: 2400,
   times: { user: 1162300, nice: 0, sys: 1193390, idle: 9986140, irq: 0 }
 },
 ...
]
*/
```
### uptime()
`uptime()` shows the time since the system was booted up. It can help determine how long servers have been running:
```
const os = require("os");
console.log(os.uptime()); // 23047
```

### totalmem() and freemem()
`totalmem()` and `freemem()` show the total amount of system memory in bytes and free system memory in bytes, respectively:
```
const os = require("os");
console.log(os.totalmem()); // 8589934592 (8 GB)
console.log(os.freemem()); // 93585408 (87 MB)
```

### userInfo()
`userInfo()` returns an object containing information about the current system user:
```
const os = require("os");
console.log(os.userInfo());

/*
[Object: null prototype] {
 uid: 502,
 gid: 20,
 username: 'user',
 homedir: '/Users/user',
 shell: '/bin/zsh'
}
*/
```
### networkInterfaces()
`networkInterfaces()` returns an object containing only network interfaces that have been assigned a network address.
```
console.log(os.networkInterfaces());

/*
{
  lo0: [
    {
      address: '127.0.0.1',
      netmask: '255.0.0.0',
      family: 'IPv4',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '127.0.0.1/8'
    },
    {
      address: '::1',
      netmask: 'ffff:ffff:ffff:ffff:ffff:ffff:ffff:ffff',
      family: 'IPv6',
      mac: '00:00:00:00:00:00',
      internal: true,
      cidr: '::1/128',
      scopeid: 0
    }
  ],
  en0: [
    {
      address: '192.168.1.10',
      netmask: '255.255.255.0',
      family: 'IPv4',
      mac: 'aa:bb:cc:dd:ee:ff',
      internal: false,
      cidr: '192.168.1.10/24'
    },
    {
      address: 'fe80::abcd:1234:5678:9abc',
      netmask: 'ffff:ffff:ffff:ffff::',
      family: 'IPv6',
      mac: 'aa:bb:cc:dd:ee:ff',
      internal: false,
      cidr: 'fe80::abcd:1234:5678:9abc/64',
      scopeid: 2
    }
  ],
  // ...more network interfaces
};
*/
```

