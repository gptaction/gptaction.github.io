---
layout: post
title: Base64 encoding in Cloudflare Worker
date: 2023-12-03
categories: programming
tags: ["JavaScript", "Cloudflare", "Encoding"]
---

When working with Cloudflare Workers, a common task is to encode data in base64 format. Unlike Node.js environments where the Buffer class is available, Cloudflare Workers require a different approach since Buffer is not present.

### Using `btoa` for Base64 Encoding

The `btoa` function, which stands for binary-to-ASCII, is a standard JavaScript function available in most JavaScript environments, including Cloudflare Workers. It encodes a string in base64 format. Here's how you can use it:

```javascript
function encodeBase64(str) {
    return btoa(unescape(encodeURIComponent(str)));
}

const data = "Hello, world!";
const encodedData = encodeBase64(data);
console.log(encodedData); // Outputs base64 encoded string
```

In this code snippet, `encodeURIComponent` is used to encode the string as a URI component, and `unescape` is used to get a Unicode string. This prepares the string for encoding in base64 format with `btoa`.

### Handling Large Strings

When encoding large strings, the approach needs to be slightly different to avoid the 'Maximum call stack size exceeded' error. This error typically occurs in JavaScript when a function calls itself too many times (recursion) or when using the spread syntax (`...`) on a large array. To handle large strings safely, use the `reduce` method combined with `String.fromCharCode` to convert the encoded data to a string:

```javascript
function encodeBase64(str) {
  const encoder = new TextEncoder();
  const encoded = encoder.encode(str);
  
  const binaryString = encoded.reduce((acc, byte) => {
    return acc + String.fromCharCode(byte);
  }, '');

  return btoa(binaryString);
}
```

This method efficiently handles larger strings without exceeding the call stack size, making it a more robust solution for base64 encoding in Cloudflare Workers.