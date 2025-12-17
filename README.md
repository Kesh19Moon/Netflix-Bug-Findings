# Teleparty-Bug-Findings
How a Movie Night Turned Into a Security Bug (and a Future Vacation)

It started like many great security stories do…
late at night, zero plans, and the simple goal of watching something with friends 🎬

We installed a popular tele-party — chat on the side, synced play/pause, nicknames, avatars. Smooth experience.
Out of curiosity (occupational hazard), I started poking around the UI.

Then I saw it:
“Set your nickname.”

I thought: What happens if I don’t behave?

So instead of a normal name, I tried something… creative.

Nothing happened at first.
I almost moved on.

Then I paused the video.

💥 Popup. Code execution. On everyone’s screen.

Every time I:

paused or played the video

sent a message

joined or left the session

…the nickname was rendered again — and the injected code executed for all participants.

That’s when it clicked:
this wasn’t a glitch — it was a stored XSS.

Digging Deeper (Because One Bug Is Never Alone)

After confirming the nickname issue, I reviewed other user-controlled inputs.
Classic rule in security: if you find one, look for siblings.

That’s when I noticed the user icon selector.

Icons weren’t uploaded — they were chosen from local extension files.
Looks safe, right?

Except the selected icon name was stored in browser local storage.
And local storage is… very editable.

By modifying that value directly, I could inject attributes into the image tag — leading to another stored XSS, triggered instantly when someone joined the session.

No clicks.
No warnings.
Just JavaScript executing as soon as users appeared.

Why This Mattered

This wasn’t just a “popup bug”:

Malicious overlays could fake login screens

Chat history could be altered

Users could be silently redirected

Phishing could happen without leaving the site

And because sessions could be joined programmatically, exploitation didn’t even require a streaming account.

The Fix & Responsible Disclosure

I reported the issues responsibly.
The developers acknowledged the findings and released a fix that properly escaped all user-controlled fields.

Problem solved. Users protected. Everyone wins 🛡️

Epilogue 🌍

No chaos. No drama. Just clean disclosure.

And yes — thanks to that bug bounty, my upcoming vacation to Morlaix and hiking through the Monts d’Arrée is officially security-funded.
Bug hunting really does take you places 😉

Responsible disclosure for the win — and the trail map is already packed 🥾✨

👀 Bonus Content: Internship Hunt (Now With Real-World XP)

Real talk: I can’t live forever in a digital cave with just a hoodie, coffee, and Burp Suite 😅
I’m also actively looking for an internship to complete my degree — so yes, this mission is both career and graduation-critical.

If your company needs someone who can:

🕵️ Hunt bugs like a caffeinated ninja
🔍 Break things ethically and explain why they broke
🧠 Think like an attacker and write like a professional
⚖️ Handle sensitive cases without doing anything stupid

Then hi 👋 that might be me.

I’m looking for internships (junior-friendly) in:

SOC
Penetration Testing
GRC
IAM
Digital Forensics

🧪 Relevant experience includes:

Bug bounties on real-world platforms

Freelance security & forensic analysis for companies

Digital forensic work with avocats (lawyers) on real cases

Writing clean, defensible forensic reports (the kind that survive meetings and courts 😄)

📍 France / Europe
📅 Internship required for degree completion

📬 DM me on LinkedIn or email me from a real company address
(Please—no fake recruiters, no crypto prophets, no “urgent investment opportunities”)

Let’s make cybersecurity safer, evidence cleaner, and systems slightly less embarrassing 🛡️

💻 Written by Keshor Murugesan
📧 keshorpuresoul@gmail.com

Cybersecurity enthusiast • Bug hunter • Digital forensics practitioner • Aspiring team player
