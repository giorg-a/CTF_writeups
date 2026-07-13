PicoCTF — [Challenge Name] — Log Parsing

Category: Forensics/General Skills

Difficulty: Easy

Challenge
Given a server.log file, the flag was scattered across repeated log entries in fragments.

Approach
Started with cat server.log to get a feel for the file's structure and confirm it was plain text with readable timestamps.
Noticed the flag fragments were tagged with FLAGPART, so I piped through grep to isolate just those lines:

   cat server.log | grep FLAGPART


The fragments repeated in a cycle (picoCTF{us3_, y0urlinux_, sk1lls_, cedfa5fb}), so I just reassembled them in the order they first appeared.


Flag:picoCTF{us3_y0urlinux_sk1lls_cedfa5fb}


Takeaway
Good reminder that grep is often the fastest way to cut noise once you know what tag/keyword to filter for — no need for anything fancier when the data's already structured for you.