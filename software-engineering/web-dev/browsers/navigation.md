---
id: navigation
aliases:
  - Navigation
tags: []
---

# Navigation

Navigation is the first step when loading a web page in a browser.

## DNS Lookup

The first step of navigation is finding out where the page's assets are located. Once the user types in a domain in the URL, the browser requests a DNS lookup at a name server. The resulting IP address is cached for some time for future visits.

DNS lookups usually only need to be performed once per hostname, however if your fonts, images, scripts, etc. are all all have different hostnames then a DNS lookup must be performed for each unique one. This can be problematic for performance, especially on mobile networks.

## TCP Handshake

Now a TCP connection needs to be established via a TCP three-way handshake. This is done so that the browser and server can negotiate the parameters of the network TCP socket connection before transmitting data.

This means that three messages are already sent between the client and server, before the actual request has been made yet.

## TLS Negotiation

After that, a TLS negotiation is used to decide which cypher will be used to encrypt the packets. It also verifies the server and checks that a secure connection is in place before beginning the actual transfer of data. This requires five more roundtrips between the client and server. This adds more time to the page load, but it is worth it since now the data can not be decrypted by a third party.

## Response

After all that, the browser sends an initial HTTP GET request on behalf of the user. Most websites will respond with a HTML file and relevant response headers. Other linked resources in the HTML file like images or scripts are only requested during the HTML parsing phase.
