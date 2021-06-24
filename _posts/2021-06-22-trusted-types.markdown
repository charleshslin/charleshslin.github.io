---
layout: single
title:  "Preventing DOM XSS Using Trusted Types"
date:   2021-06-22 15:32:31 -0400
categories: jekyll update
---

<br>
Trusted Types were introduced by the Google Chrome team in February 2019 as a method of combating DOM XSS.

Although the `trusted-types` and `require-trusted-types-for` Content-Security-Policy directives currently (as of June 2021) have limited browser support (Chrome and Edge support it but Firefox, Safari, and Internet Explorer do not), using Trusted Types is a form of secure coding that can significantly reduce the risk of DOM XSS, which is arguably the most challenging form of XSS to detect since the attack is conducted on the client-side.

DOM XSS is difficult to prevent, especially for large, complex applications, due to the difficulty of easily determining the origin of injection sink inputs.

**What are injection sinks?**

Injection sinks are risky and powerful Web APIs that are highly targeted by attackers due to its exploitability when accepting user-provided input. Common examples include (but are not limited to, since there are over 60 total):

{% highlight javascript %}
<script src>
<script>
innerHTML
outerHTML
insertAdjacentHTML
<iframe> srcdoc
document.write
document.writeln
DOMParser.parseFromString
<embed src>
<object data>
<object codebase>
eval
setTimeout
setInterval
new Function()
{% endhighlight %}

[OWASP’s DOM based XSS Prevention Cheat Sheet][owasp-cheat-sheet] highlights the importance of proper encoding of untrusted data ahead of placing it in injection sinks. Emphasis is also placed on steering developers away from using more dangerous injection sinks (for example, using document.createTextNode instead of innerHTML), which should be the primary mitigation technique.

**How do you use Trusted Types?**

In order to enforce Trusted Types, you need to set the [Content Security Policy][csp]. For example, 

{% highlight javascript %}
Content-Security-Policy: require-trusted-types-for 'script'
{% endhighlight %}

Before you enforce Trusted Types via Content Security Policy, you should ensure your application does not produce violations (you can also set a report-only CSP header). If your application produces violations, you have 2 main options for removing them:
* Remove the offending code
* Create Trusted Type objects (using a library or your own code)

**How to remove offending code**

Rewrite the code without using dangerous injection sinks. Perhaps the code is no longer needed or there is a more secure approach to writing the code.

For example, instead of:

{% highlight javascript %}
var anElement = document.getElementById("exampleId");
anElement.innerHTML = exampleVar;
{% endhighlight %}

Do:

{% highlight javascript %}
var anElement = document.getElementById("exampleId");
anElement.textContent = exampleVar;
{% endhighlight %}

Or if you use the eval() function, rewrite the code so that eval is no longer needed.

**Creating Trusted Type objects using DOMPurify**

[DOMPurify][dompurify] is an open-source library for removing XSS payloads from strings and returning sanitized strings for safe usage. In addition, when Trusted Types is supported and RETURN_TRUSTED_TYPE is set to true, it will return a TrustedHTML object so that a violation is not generated.

In order to use DOMPurify, simply import the library and run DOMPurify.sanitize() on the HTML that needs to be sanitized.

**Creating your own Trusted Type objects**

If using a library for sanitizing strings and creating Trusted Types does not work for you, you can create your own Trusted Types. For example:

{% highlight javascript %}
// Note this is just an example for high-level understanding, not best practice policy and sanitizing implementation
const myPolicy = trustedTypes.createPolicy('myPolicyName', {
    createHTML: input => input.replace(/\</g, '&lt;')
  });
myDiv.innerHTML = sanitizingPolicy.createHTML(untrustedValue);
{% endhighlight %}

<br>
**Conclusion**

Although Trusted Types are only supported by limited browsers, writing code using Trusted Types is a new best practice and will significantly reduce the risk of DOM XSS.

[owasp-cheat-sheet]: https://cheatsheetseries.owasp.org/cheatsheets/DOM_based_XSS_Prevention_Cheat_Sheet.html
[csp]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/trusted-types
[dompurify]: https://github.com/cure53/DOMPurify