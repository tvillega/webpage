+++
title = "Procmail Rules"
date = "2023-08-21"
draft = true
[taxonomies]
tags = ["linux","mail"]
+++

## Backstory

I always focus on my department when I talk about my designated server credentials and mail system. However, truth be told, the faculty itself already gives us those. They are just not friendly. Not at all.

On my first year of university I was given a single item: a username under the domain [ing.uchile.cl](https://ingenieria.uchile.cl) - this one redirects to the main page of my faculty. It gave me access to the mail system, the printing system and the computer center.

Later on I realized I was one of the few who used it, the university was transitioning onto the new domain name [ug.uchile.cl](https://ug.uchile.cl) - which redirects to nowhere - that its linked to a Google Workspace account. Everyone I asked about the institutional account talked to me about that one. Since the internal services of the university only ask for the username, it took me a while to catch up.

> On a bright side, my out-of-date knowledge helped a good friend of mind to retrive some important emails from our university - that's above our faculty's authority. Since the credential system got fractured, he was having a hard time trying to figure out how to get access to those emails.

The advantage of the Google Workspace account it's that we can use a gmail-like front-end on a web browser to access our mail. The disadvantage is that everything is clumsy you are not using the web browser.

I use [K-9 Mail](https://f-droid.org/packages/com.fsck.k9/) on my Android device and setting up Google has been a strange move every time. You have to choose between activating 2FA to lift the restriction above IMAP or to use OAuth 2.0 to get an access token. Microsoft has only asked me my credentials and the folders are there waiting for me to open them.

## Client mail filtering

I used to use [Samsung Email](https://play.google.com/store/apps/details?id=com.samsung.android.email.provider) since it was fist released. Google pushed too hard its ecosystem and I got annoyed about the useless features and the heavy interface just to read a plain mail. That's when I learnt about OAuth 2.0 for the first time and Samsung made it painless.

Since back in the day IMAP wasn't locked behind 2FA I didn't have to link my entire phone to my personal gmail account. I follow the concept of different email addresses for different bussiness so I don't get shady pharmaceutical advice next to my plane checkouts and bank transfers.

There is this one little feature that I got addicted to: **spam filter**. Everytime I got an unwanted email, I could just mark it as such and I would never see another message from that mail address.

This was specially useful for my [ing.uchile.cl](htttps://ingenieria.uchile.cl) mail address, because since the dawn of time our university subscribes us to every possible mailing list in the existence. There's no opt-out, and if such button exists it doesn't work. I find really handy to check the updates from my courses on the mail, but getting from five to ten extra mails with no important information whatsoever got me fed up really fast.

Everyday I checked faculty mail, if something wasn't about my courses I just sent it to spam. It wasn't easy to do, since I had to learn the purpose of each mailing list. I got some false possitives over time and missed some important information from what were actual *announcement lists* that had actual information like scolarships and payment reports.

There was a downside to all this magic filtering. It was *client-side*. It means that whenever I uninstalled the app I would have lost all my filters. No export feature was available. I got on many cicles of adding/removing my faculty mail address so at the end of the day I learnt what was important and what not.

## Server side filtering

I eventually moved onto K-9 Mail because Samsung Mail's interface was getting too heavy for such a simple task. When it comes to mail clients, every feature it's appreciated. However, when it comes to my phone, I rather have a *potato* for an app than a *Mona Lisa*.
