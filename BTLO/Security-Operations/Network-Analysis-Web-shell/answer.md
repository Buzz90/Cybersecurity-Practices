# Network Analysis - Web Shell

*The SOC received an alert in their SIEM for ‘Local to Local Port Scanning’ where an internal private IP began scanning another internal system. Can you investigate and determine if this activity is malicious or not? You have been provided a PCAP, investigate using any tools you wish.*

Here I'm using Wireshark for my main tool.

# Questions

## 1. What is the IP responsible for conducting the port scan activity?

The question asks about port scan activity, which fortinet describes as:

> *"A port scan is a common technique hackers use to discover open doors or weak points in a network."*

The way hackers does this is by sending message to multiple ports and they will get response from those ports that either the ports is being used or if there are any potential weakness that could be exploited.

For detecting this, I can directly go to communication