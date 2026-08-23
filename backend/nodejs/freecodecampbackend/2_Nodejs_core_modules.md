<!-- Nodejs Core Modules -->

# fs Module:
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

# Crypto Module
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

# os Module

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

# Path Module

The Node.js path module lets you work with files and directory paths. It provides several useful methods for handling and transforming directories, including joining, normalizing, and resolving the directories across different platforms and operating systems.

To use the path module, you can import it like this:
```
const path = require("path");
```

First, you should be aware of the Node.js global variables `__filename` and `__dirname`, AKA "common JS" variables. You don't need the `path` module to access them, which is why they are called global variables.

`__filename` is the absolute path of the current file and `__dirname` is the absolute path of the directory containing the current file.

For example, I have a `script.js` file I'm currently working with. Here's what the two methods return:
```
console.log(__filename);
// /Users/user/Desktop/fCC/script-code/node/node-path/script.js

console.log(__dirname);
// /Users/user/Desktop/fCC/script-code/node/node-path
```
You should also be aware of relative and absolute paths.

A relative path points to a file or folder based on your current working directory. For example, `./assets/src/text-files`.

An absolute path, on the other hand, gives the complete address of a file or folder from the root of your system, such as `/Users/johndoe/projects/app/assets/src/text-files`.

The `basename()` method shows the last part of the file, that is, the filename:
```
console.log(path.basename(__filename)); // script.js
```
`dirname()` returns the directory name of a path:
```
console.log(path.dirname(__dirname)); // node-path
```
`extname()` returns the extension of the current file:
```
console.log(path.extname(__filename)); // .js
```
You can also specify a different file to return the extension of:
```
console.log(path.extname('text-files/text1.txt')); // .txt
```

The `join()` method takes all the path segments you pass in and joins them into one clean, normalized path. 

This could be useful if you want to merge related files in different folders so you can work with them together:
```
const joinedPath = path.join("src", "assets", "text-files");
console.log(joinedPath); // src/assets/text-files
```
Windows uses backslashes to separate directories, so the result will be `src\assets\text-files`.

In addition, the `join()` method automatically fixes wrong slashes and removes extra ones:
```
const wrongPath = path.join("/src//", "assets", "text-files");
console.log(wrongPath); // /src/assets/text-files
```

The `resolve()` method turns a sequence of path segments into an absolute path. It starts from your current working directory and results in a full path that points to the exact location on the device:
```
const absolutePath = path.resolve("assets", "src", "text-files");
console.log(absolutePath);
// /Users/user/Desktop/fCC/script-code/node/node-path/assets/src/text-files
```

The difference between `join()` and `resolve()` is that `join()` creates a relative path, while `resolve()` returns an absolute path.

Lastly, there are the `parse()` and `format()` methods.

`parse()` takes a directory or file and returns an object that contains the breakdown of its parts, such as the system root, its directory, extension, and the filename:
```
const parsedFile = path.parse(__filename);

console.log(parsedFile);
/*
{
 root: '/',
 dir: '/Users/user/Desktop/fCC/script-code/node/node-path',
 base: 'script.js',
 ext: '.js',
 name: 'script'
}
*/
```

`format()`, on the other hand, builds a path from an object containing directory, name, and extension:

```
const formattedDirectory = path.format({
  dir: "/users/johndoe/docs",
  name: "file",
  ext: ".txt",
});

console.log(formattedDirectory); // /users/johndoe/docs/file.txt
```

# Process Module


`process` is one of the most important Node.js core modules. It gives you access to information about the current Node.js process, and lets you control it while your app is running.

When you execute a command like `node script.js` in the terminal, Node.js starts a process, which is a running instance of the Node program that executes the `script.js` file. This process has its own memory, environment, and execution context. 

The current process is exposed globally through the `process` module, so you don't even need to import it. As long as you have Node.js installed, then you can call it anywhere.

The `process` module exposes properties and methods for you to get certain information about the current execution context.

## process.env
`process.env` gets you information about the current environment Node is running on. This always returns a giant object with many parameters, so here's how you can access some of the most important information directly:

```
// Gets all environment variables available to the current Node.js process
console.log(process.env);

// Gets the current Node.js environment mode (like 'development' or 'production')
console.log(process.env.NODE_ENV); // development

// Gets the path of the shell program running the Node.js process
console.log(process.env.SHELL); // /bin/bash

// Gets the system PATH variable where executables are searched for
console.log(process.env.PATH); // /usr/local/bin:/usr/bin:/bin

// Gets the present working directory from where the process was started
console.log(process.env.PWD); // /Users/johndoe/projects/myapp

// Gets the username of the user running the current process
console.log(process.env.USER); // johndoe
```

`process.argv` lets you read command-line arguments:
```
console.log(process.argv);
/*
script.js --watch
Hello world
[
  '/Users/user/.nvm/versions/node/v22.17.0/bin/node',
  '/Users/user/Desktop/fCC/script-code/node/node-process/script.js',
  '--watch'
]
*/
```

The `cwd()` method shows the current working directory:
```
console.log(process.cwd());
```

### Process events
Process events are a core feature of Node.js that let your app respond to key moments in its lifecycle, like when it's about to exit, encounters an error, or receives a system signal.

The `exit` event, for example, runs right before the Node.js process finishes:
```
process.on("exit", (code) => {
  console.log(`Process exiting with code: ${code}`);
});

// Process exiting with code: 0
```

The `uncaughtException` event is triggered when an error is not caught in your code, which can help you prevent crashes:
```
process.on("uncaughtException", (err) => {
  console.error("Uncaught error:", err.message);
});
```
Lastly, the `warning` event is triggered when Node.js emits a process warning:
```
process.on("warning", (warning) => {
  console.warn("Warning name:", warning.name);
  console.warn("Warning message:", warning.message);
});
```

You can then use the `emitWarning()` method to trigger a custom warning:
```
// Example warning with the emitWarning() method
process.emitWarning('This is a custom warning message', 'CustomWarning');

/*
  Warning name: CustomWarning
  Warning message: This is a custom warning message
*/
```

# Stream Module
Strem module helps you handle data efficiently, especially when the data is too large to load all at once, like reading a big text file or downloading a large video.

Instead of waiting to read or write all the data before doing anything, streams process chunks of data as they arrive, similar to how you can start watching a Youtube video before video finishes loading.

There are four main types of streams in Node.js: readable, writable, duplex, and transform.

- Readable streams let you read data in chunks (for example, reading a large file).
- Writable streams lets you write data in chunks (for example, saving a file).
- Duplex streams can both read and write data.
- Transform streams are a special kind of duplex stream that can change or process the data as it flows through.

You can import the stream classes you need by destructuring them from the stream module:
```
const {Readable, Writable, Transform }=require("stream");
```

Most of the time, you don't need to create the custom stream classes yourself. For everyday file operations, built-in methods like `fs.createReadStream()` and `fs.createWriteStream()` are usually all you need.

These two methods take the path of the file to read or write. This means you also need the `fs` and the `path` modules to implement the streaming on many occassions.

Here;s how you can read data from a file, say an `input.txt` file:

```
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");

// Readable stream
const readInputFileStream = fs.createReadStream(inputFilePath);
console.log(readInputFileStream);
```
This will not do anything yet, as you need to use the events from the stream to read the data. For example, you can listen to the `data` event this way:

```
readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
}); // Received 622 bytes of data
```

You can also log the chunk of data to the console:
```
readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  console.log("Received data:", chunk);
});

/*
Received 622 bytes of data
Received data: <Buffer 4c 6f 72 65 6d 20 69 70 73 75 6d 
20 64 6f 6c 6f 72 20 73 69 74 20 61 6d 65 74 20 63 6f 6e
73 65 63 74 65 74 75 72 20 61 64 69 70 69 73 69 63 69 6e 67 ... 572 more bytes>
*/
```

Since it returns a buffer, you can call the toString() method to convert it into readable text:

```
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");

// Readable stream
const readInputFileStream = fs.createReadStream(inputFilePath);

readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  console.log("Received data:", chunk.toString());
});
/*
Received 622 bytes of data
Received data: Lorem ipsum dolor sit amet consectetur adipisicing elit. Ducimus sint facilis
aliquid. Odio voluptatibus veniam saepe consectetur alias modi non fuga in,
tempore explicabo numquam maiores quod inventore quibusdam! Nam cumque repellat
facere voluptatem nulla aliquam atque ratione numquam ea aperiam porro ducimus
animi tempora laboriosam, labore quae voluptatum? Nam, hic quas dolore
repudiandae placeat eius! Voluptate reiciendis totam hic expedita tenetur. Nisi
ipsa ad facere optio sint debitis. Magni nostrum sit ipsa saepe suscipit facilis
eaque doloribus assumenda, minima fuga tempore, porro, debitis rem harum in
*/
```

To implement a writable stream, particularly when you're reading from one file and writing to another, you need to create the read stream first, followed by the write stream:

```
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");
const outputFilePath = path.join(__dirname, "output.txt");

// Create the read stream first
const readInputFileStream = fs.createReadStream(inputFilePath);

// Create the write stream
const writeOutputFileStream = fs.createWriteStream(outputFilePath);
```

Next, use the .pipe() method to connect the readable stream to the writable stream. This lets Node.js automatically read data from the source and write it to the destination, chunk by chunk:

```
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");
const outputFilePath = path.join(__dirname, "output.txt");

// Create the read stream first
const readInputFileStream = fs.createReadStream(inputFilePath);

// Create the write stream
const writeOutputFileStream = fs.createWriteStream(outputFilePath);

// Pipe the read stream to the write stream
readInputFileStream.pipe(writeOutputFileStream);
```

Then you can listen for the finish and error events on the writable stream to know when the streaming is complete or if something goes wrong:

```
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");
const outputFilePath = path.join(__dirname, "output.txt");

// Create the read stream first
const readInputFileStream = fs.createReadStream(inputFilePath);

// Create the write stream
const writeOutputFileStream = fs.createWriteStream(outputFilePath);

readInputFileStream.pipe(writeOutputFileStream);

writeOutputFileStream.on("finish", () => {
  console.log("All data has been written to the file");
});

writeOutputFileStream.on("error", (err) => {
  console.error("Error writing to file:", err);
});
```

The `finish` event tells you that the stream is complete and there is no more data to write, while the error event helps you catch problems that might happen during writing, like permissions issues or missing directories.