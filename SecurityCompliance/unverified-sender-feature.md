--
title:
ms.author: tracyp
author: msfttracyp
--

# Identify suspicious messages in Outlook.com and Outlook on the web

To prevent phishing messages from reaching your mailbox, Outlook.com and Outlook on the web verify that the sender is who they say they are and mark suspicious messages as junk email.

> [!IMPORTANT]
> When a message is marked as a phishing scam, Outlook.com and Outlook on the web display a warning at the top of the page, but any links in the message can still be opened.

## How can I identify a suspicious message in my inbox?

Outlook.com and Outlook on the web show indicators when the sender of a message either can't be identified or their identity is different from what you see in the From address.

### You see a '?' in the sender image

When Outlook.com and Outlook on the web can't verify the identity of the sender using email authentication techniques, they display a '?' in the sender photo.

![Message did not pass verification](media/message-did-not-pass-verification.jpg)

Not every message that fails to authenticate is malicious. However, you should be careful about interacting with messages that don't authenticate if you don't recognize the sender. Or, if you recognize a sender that normally doesn't have a '?' in the sender image, but you suddenly start seeing it, that could be a sign the sender is being spoofed.

### The sender's address is different than what appears in the From address

Frequently, the email address you see in a message is different than what you see in the From address. Sometimes phishers try to trick you into thinking that the sender is someone other than who they really are.

When Outlook.com and Outlook on the web detect a difference between the sender's actual address and the address on the From address, they show the actual sender using the via tag, which will be underlined.

![unverified sender alt text](media/unverified-sender-feature1.png)

In this example, the sending domain `suspicious.com` is authenticated, but the sender put `unknown@contoso.com` in the From address.

Not every message with a via tag is suspicious. However, if you don't recognize a message with a via tag, you should be cautious about interacting with it.

In Outlook.com and the new Outlook on the web, you can hover your cursor over a sender's name or address in the message list to see their email address, without needing to open the message.

