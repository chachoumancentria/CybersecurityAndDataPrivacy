# PortSwigger

Labs completed (20 total):
1. SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
2. SQL injection vulnerability allowing login bypass
3. SQL injection attack, querying the database type and version on Oracle
4. Unprotected admin functionality
5. Unprotected admin functionality with unpredictable URL
6. User role controlled by request parameter
7. User role can be modified in user profile
8. User ID controlled by request parameter 
9. User ID controlled by request parameter, with unpredictable user IDs 
10. User ID controlled by request parameter with data leakage in redirect 
11. User ID controlled by request parameter with password disclosure
12. Insecure direct object references
13. Username enumeration via different responses
14. 2FA simple bypass
15. Password reset broken logic
16. Information disclosure in error messages
17. Information disclosure on debug page
18. Source code disclosure via backup files
19. Authentication bypass via information disclosure
20. Information disclosure in version control history


# The booking system project
## Phase1
During this task we were a bit confused at what we were supposed to do. It wasn't hard, it's just that we were using new tools, and we needed to understand them before actuallyy working. However, once we understood how to use ZAP and Burp, finding vulnerabilites was very easy. We missed a few of them, but were able to find plenty, and we had to choose which ones would be in the report.

For the second part, since we already had figured out plenty of vulnerabilities, we basically had nothing to do. We just added the vulnerabilities we found in the first part that couldn't make it into our initial report.

## Phase2
During this Phase, we had to use hashcat. Once again, this was a new tool. We were easily capable of finding four passwords by using the most simple dictionnary attack. However, what was interesting, was when we tried a combinator attack. This takes a lot more time (took 7 hours of compute), however, it is much more powerfull. We learned that even regular consumer hardware has the capability of cracking unsecure passwords, and that more specialized equipment can crack any unsecure password.

## Phase3
During this Phase, it was very tedious to go through each possible interaction, within every single context. These context could be logged in/not logged in, ressource existed/not existed, accessed through URL/UI, and many more.

## Phase4
We had some trouble with a few things. It was mainly the wording of the things to check. We would sometimes disagree on what we should check for a specific field, but in the end, we managed to work it out.

# Logbook
Online classes: 24h
Netacad course introduction: 12h
Booking project: 28h
PortSwigger labs: 16h

Total: 80h
[Link to the logbook](https://github.com/chachoumancentria/CybersecurityAndDataPrivacy/blob/main/logbook.md)
