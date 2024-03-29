Him: Hmmm. I don’t see an SSL cert. Why would one go to HTTPS instead of HTTP? That’s just a way to see the certificates?

Me: HTTPS is a way to validate that the website you’re talking to is who they claim to be (and that it hasn’t been tampered with in transit). It’s really HTTP-Secure in that your web browser has to validate the information coming from the server as \*actually coming from Google\*. The way it does it using cryptographic certificates, signed by a globally trusted third party authority that says, “This website is who they claim to be.” It works through the transitive property – I trust the CA (Certificate Authority), the CA trusts Google, therefore, I trust Google.

At the core this means that anything you do online, \*\_ANYTHING\_\* can be tampered with and/or modified by the company at will – and you’d never know the difference.

Further reading: <http://en.wikipedia.org/wiki/HTTP_Secure>
