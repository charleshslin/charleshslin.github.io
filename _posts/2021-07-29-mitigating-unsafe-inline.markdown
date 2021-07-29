---
layout: single
title:  "Mitigating unsafe inline scripts in Content Security Policy"
date:   2021-07-29 15:32:31 -0400
categories: jekyll update
---

<br>
When setting the Content Security Policy (CSP) of a site, unsafe-inline should not be allowed. Allowing unsafe-inline opens up XSS attack vectors significantly, since it effectively allows malicious actors to inject scripts if those attack vectors exist. The best solution is to move inline scripts into its own files and ensure the Content Security Policy is set to be as strict as possible.

**What mitigations are available if unsafe-inline must be used?**

<u>CSP Hash</u>

If you have a `<script></script>` block, simply compute the SHA-256 hash of the text between the script tags, and add it to your `script-src` CSP directive, prepended by the hash you used and a hyphen (example below).

CSP supports sha256, sha384, and sha512.

`script-src 'sha512-XhWVDVHe6n6DxQlEQ9VwT3nllTd1Cwo9KHMRPe/0amwPqTK5Bc1TqZLPUvISGjVAj5uZJ4IbwVqiHpzY1ffjpg==';`

{% highlight javascript %}
<script>alert(“hi”);</script>
{% endhighlight %}

<br>
<u>CSP Nonce</u>

A nonce is a cryptographically secure token that needs to be added to every inline script and generated for each HTTP request. A random value generator should be used, and characters must be limited to those found in a base64 encoded string with at least 128 bits of entropy. It would then work as shown below (this would be for a single HTTP request).

`script-src 'nonce-1684fa296e4a70a58053a902413ce95272707228a1e2eab98bef1dcde2f6b240cdae35d143f199bbede1d5fb91eae14f3b5c4ab4cc774fe9708846d6795b0d03';`

{% highlight javascript %}
<script nonce="1684fa296e4a70a58053a902413ce95272707228a1e2eab98bef1dcde2f6b240cdae35d143f199bbede1d5fb91eae14f3b5c4ab4cc774fe9708846d6795b0d03">alert(“hi”);</script>
{% endhighlight %}

<br>
<u>CSP strict-dynamic</u>

The `‘strict-dynamic’` directive allows scripts to be executed on the page, as long as it was loaded by a trusted script. Note that strict-dynamic is not currently supported (as of July 2021) in Safari or Internet Explorer.

