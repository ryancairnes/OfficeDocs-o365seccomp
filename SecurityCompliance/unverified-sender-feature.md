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

![Get started with OneDrive](media/get-started-with-onedrive-message.png)

How do you know if you're using the new Outlook on the web? See the following examples:

![Outlook vs Office 365](media/outlook-vs-outlook365.png)

## Frequently asked questions

### What criteria does Outlook.com and Outlook on the web use to add the '?' and the 'via' properties?

For the '?' in the sender image:  Outlook.com requires that the message pass either SPF or DKIM authentication. For more details, see [Set up SPF in Office 365 to help prevent spoofing](set-up-spf-in-office-365-to-help-prevent-spoofing.md) and [Use DKIM to validate outbound email sent from your custom domain in Office 365](use-dkim-to-validate-outbound-email.md).

For the via tag: If the domain in the From address is different from the domain in the DKIM signature or the SMTP MAIL FROM, Outlook.com displays the domain in one of those two fields (preferring the DKIM signature).

### Can I override these properties with IP Allows, Exchange Transport Rule Allows, or safe senders?

You can't override these properties.

### How do I remove these properties?

For the '?' in the sender image: As a sender, you should authenticate your message with either SPF or DKIM.

For the via tag: As a sender, you should ensure that either the domain in the DKIM signature or the SMTP MAIL FROM is the same as, or is a subdomain of, the domain in the From address.

### Does Outlook.com and Outlook on the web show this for every message that doesn’t pass authentication?

Not necessarily. Outlook.com and Outlook on the web may have other properties within the message to authenticate the sender.

## Related topics

[Help protect your Outlook.com email account](https://support.office.com/article/a4f20fc5-4307-4ece-8231-6d4d4bd8a9ba)

[Deal with abuse, phishing, or spoofing in Outlook.com](https://support.office.com/article/0d882ea5-eedc-4bed-aebc-079ffa1105a3)

[Filter junk email and spam in Outlook on the web](https://support.office.com/article/db786e79-54e2-40cc-904f-d89d57b7f41d)
