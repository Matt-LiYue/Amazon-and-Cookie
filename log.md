##The Quest to Replace Passwords: A Framework for Comparative Evaluation of Web Authentication Schemes∗

This paper summarizes different types of authentication schemes and evaluate them in 3 dimensions -- Usability, deployability, and security. In each of the dimensions the authors propose finer-grained factors to consider.
* Usability
	* Memorywise-effortless: password is not memorywise-effortless
	* Scalable for users: no, more passwords confuse users
	* Nothing to carry: yes
	* Physically-effortless: no, need typing
	* Easy-to-learn: yes
	* Efficient to use: yes, several seconds to type
	* Infrequent errors: yes
	* Easy-recovery-from-loss: yes
* Deployability
	* Accessible: yes
	* Negligible-cost-per-user: yes
	* Server-Compatible: yes
	* Browser-compatible: yes
	* Mature: yes
	* Non-Proprietary: yes
* Security
	* Resilient-to-Physical-Observations: no
	* Resilient-to-Targeted-Impersonation: partially
	* Resilient-to-Throttled-Guessing: no
	* Resilient-to-Unthrottled-Guessing: no
	* Resilient-to-Internal-Observation: no (key-logging)
	* Resilient-to-Leaks-from-Other-Verifiers: no
	* Resilient-to-Phishing:no
	* Resilient-to-Theft:  yes(no hardware required)
	* No-Trusted-Third-Party: yes
	* Requiring-Explicit-Consent: yes
	* Unlinkable: yes


There are many other authentication schemes that can be evaluated using this framework. However, I will focus on introducing other authentication schemes.

###Encrypted password managers: Mozilla Firefox
Firefox offers a password manager that can be managed using a single master password -- Once the master password is input, other passwords will be automatically filled. The passwords are encrypted and stored locally, which can also be synchronized to the cloud.

###Proxy-based: URRSA <font color='red'>(One-time password access to any server without changing the server 2008 ISC)</font>
URRSA schemes place men-in-the-middle between a client and a server. It generatess multiple one-time passwords under encryption for each of the password and distributes them to the user. It does not store user passwords, instead it stores encryption keys.

URRSA works as follows

1. A user registeres his/her passwords in URRSA server, the server will send back a set of encrytped versions of passwords using different keys to the user's cellphone. 
2. Every time the user needs to authenticate to a certain website, it visits URRSA website and input the URL of target system, the username, and (next unused) encrypted passowrds.
3. The server pulls the (unused) encrypting keys and decrypt the ciphertext password and redirect the real password to the system.
4. if all encrypted passwords (OTP) are used, the user can regenerate a new set of keys and ciphertext in URRSA.

Benefits:
* Defend malware-affected clients (because all passwords can only be used for one time and the ciphertext is stored in the user's cellphone).
* Do not require any modification on the target system.
* Do not store passwords in the server side.

###Federated Single Sign-On: OpenID ()

Federated SSO allows websites to authenticate a user by redirecting them to a trusted identity server which attests the users' identity (such as Facebook).

### Graphical passwords: Persuasive Cued Clickpoints (PCCP)
<font color='red'>persuasive cued click-points design implementation and evaluation </font>

PCCP is a cued-recall scheme. Users first click an image and a subsequent image, which is determined on the point clicked on the last image, will be prompted. Correctly clicking the points in 5 consecutive images will authenticate successfully.

When creating the password, a portal which consists part of all images is shown as the first image to flatten the password distribution. While when authenticating, the portal is absent.

There are also many other works on graphical passwords. For example, requiring users to draw a secret graph. Graphical passwords are mainly used to defend guessing attacks.

### Cognitive Authentication: GrIDsure
Challenge-Response schemes attempt to address the re- play attack on passwords by having the user deliver proof that he knows the secret without divulging the secret itself. The server could require the user to input a hash of a password plus a random-generated phrase. Then the user does not need to type in the real passwords in their mind. 

GrIDsure is one scheme of this kind. When registering, it presents a (E.g. 5*5) squre grid for users to select a cell for each character of the passwords. There are 25^4 permutations for a 4-character passwords. Then when the user tries to log in, the system will fill the cells with numbers (or chars). The user inputs corresponding numbers to authenticate.

Such schemes can be used to defend key-log malwares. 

### Paper tokens: OTPW <font color='red'>(OTPW – A one-time password login package, 1998)</font>
Using paper to store long secrets is the cheapest form of a physical login token. OTPW is a later refinement. the server stores a larger set of independent hash values, consisting of about 4 kB per user. The user carries the hash pre-images, printed as 8-character values such as "weqriojd". The authentication requires both a prefix passwords and a randomly-queried pre-images, which are carried by the user on a piece of paper.

###Hardware tokens: RSA SecurID
Hardware tokens store secrets in a dedicated tamper- resistant module carried by the user; the RSA SecurID [34] family of tokens is the long-established market leader. Each instance of the device holds a secret “seed” known to the back-end.

A cryptographically strong transform generates a new 6- digit code from this secret every 60 seconds. The current code is shown on the device’s display. On enrollment, the user connects to the administrative back-end through a web interface, where he selects a PIN and where the pairing between username and token is confirmed. From then on, for authenticating, instead of username and password the user shall type username and “passcode” (concatenation of a static 4-digit PIN and the dynamic 6-digit code).

###Mobile-Phone-based: Sound-proof <font color='red'>Sound-Proof: Usable Two-Factor Authentication Based on Ambient Sound" 2014 USENIX Security</font>
Mobile-phone-based authentication is just another kind of token-based authentication. Mobile phone has many sensors nowadays, which can be used to authenticate the users. For example, the ambient noise. 

###Biometrics: Fingerprint,facial,gesture recognition
pass


##Password and the Evolution of Imperfect Authentication

__Password role changing__

1960s, password was first introduced in MIT for protecting resources -> plaintext password leaks

1970s, MULTICS store passwords in hashed form, in 1979 salt was introduced

1990s, pubilc-key cryptography was designed to replace passwords but failed due to burdon on managing certificates and private keys. Plaintext in HTML form exchanges for token becomes dominant.

Hardware tokens as a second factor -- low deployment.

Use smartphones as a second factor of authentication.



__Measuring password strength__

Shanon Entropy -> NIST Entropy -> Guesswork-> partial guesswork

__Improving password strength__

Forcing users to use longer and more type-complex passwords may not increase the password strength than expected. (<font color='red'>Testing metrics for password creation policies by attacking large sets of revealed passwords. ACM CCS, 2010.</font>)

Sites facing greater competition are less prone to use such complex policy <font color='red'>(Where Do Security Policies Come From? ACM SSOUPS, 2010.)</font>

Another way is to nudge users to choose better passwords by feedback (password meters). Aggressive meters can make guessing passwords more difficult (<font color='red'>How Does Your Password Measure Up? The Effect of Strength Meters on Password Creation. USENIX Security, 2012.</font>). However, if users are not prompted to consider their passwords, the impact of such meters is negligible <font color='red'>(Does My Password Go Up to Eleven?: The Impact of Password Meters on Password Selection. ACM CHI, 2013.)</font>. An exmpirical data from Yahoo prove adding a password meter did improve password security, but marginally <font color='red'>(The science of guessing: analyzing an anonymized corpus of 70 million passwords.IEEE Symposium on Security and Privacy, 2012.)</font>

__dependence when choosing multiple passwords__

Password is reused. The median number of accounts a user has is 25 while unique passwords are only 6 (<font color='red'> A large-scale study of web password habits. 16th International Conference on the World Wide Web (WWW), 2007.</font>). Even a user does not re-use passwords, an attacker can guess small variations, which at least double the chances to crack the passwords.(<font color = 'red'>The Tangled Web of Password Reuse.NDSS, 2014.</font>). Similarly, forcing users to update their passwords makes users choose produce regular password sequences.(<font color = 'red'> The Security of Modern Password Expiration: An Algorithmic Framework and Empirical Analysis. ACM CCS, 2010.</font>)

__Offline and Online Attacks__
Besides guessing, there are many other ways for online attackers, such as phingshing, eavesdropping, and subverting automated password reset process. __Mandating strong passwords do not stop these attacks__

Offline attacks happen in a very narrow sets of circumstances. Empirical estimates sugest that over 40% sites store passwords unhashed (<font color = 'red'> The password thicket: technical and market failures in human authentication on the web. Workshop on the Economics of Information Security (WEIS), June 2010.</font>). Recent password leaks revealed many of them are plaintext (Rockyou and Tianya), hashed but unsalted (Linkedin), improperly hashed (gawker), or reversibly encrypted (Adobe). Finally, offline attacks may be interrupted by forcing the users to change their passwords after a breach. However, few websites dare to do so.

There are many online guessing countermeasures. The most commonly used method is to require a CAPTCHA after each failed attempt(58% of 28 sites examined). Others include set a attempt limit (from 3 to 25), password reset after 5 attempts, or impose timeout. (<font color = 'red'>The password thicket: technical and market failures in human authentication on the web. Workshop on the Economics of Information Security (WEIS), June 2010.</font>). Choosing a password to withstand an online attack is much easier. It makes little sense to focus on the risk of offline attacks.

####Password seems over-constrained

__Password replacement__

Passwords offer compelling economic advantages over alternatives.

* lowest start-up and incremental costs per user
* deployability (backwards compatibility, interoperability, no marginal costs).
* 'password replacement' is under-specified (no universally agreed set of concrete requirements covering diverse environments, technology platforms, cultures and applications) so no single solution is expected to address all requirements.

	* Pssword manager (Or graphical password) are challenging to configure across all user agents (cellphone or commandline).
	* Biometric schemes have significant deployment hurdles, and are also poorly suited to unsupervised environment of web authentication (fraudsters can replay digital representations os fingerprint and iris patterns)
	* Using hardware tokens or mobile phones to generate one-time access codes is much more secure, but ubiquitous adoption remains elusive due to usability issues and cose.
	* Federated Authentication (Single Sign-on) protocols can significantly reduce several problems. However, it introduces privacy issues (Facebook collects much information from single sign on data)
	* Inertia becomes a substantial hurdle
* besides, improving security despite any decline in usability may mean losing users.
* Requiring server or client software modifications is often a show-stopper
A better choice is to prioritize competing reequirements depending on organizational priorities and usage scenarios.

__Advice to users__

Now users are facing unrealistic and even mutually incompatible advices: use a different password for each account; change them often; use a mix of letter, number, punctuations; Make it at least 8 characters long; avoid personal information; avoid write them down, etc. 

However, user's willingness to comply with annoying security requirements is a finite exhaustible resource that should be managed carefully. (<font color = 'red'>The Compliance Budget: Managing Security Behaviour in Organisations. NSPW, 2008.</font>)

Actually choosing extremely strong passwords is of far more limited benefit. Advices for users may be to select a password that cannot easily be guessed by acquitance and can withstand a reasonable amount of online attacks. Over half of users are already above this bar.(<font color = 'red'>The science of guessing: analyzing an anonymized corpus of 70 million passwords. IEEE Symposium on Security and Privacy, 2012.</font>)

Another important advice is to encourge users not to reuse passwords in important sites. 

Writing passwords down or using password manager introduce a single point of failure. However, now they may be no more vulnerable than webmail accounts due to automated email password reset.

__Imperfect Authentication__

A multidimensional feature

Besides passwords, websites start to use multiple features to classify users including the user’s IP address; geolocation; browser information, including cookies; the time of the login; how the password is typed; and what resources are being requested, etc. Such classification does not require any user effort. (<font color = 'red'> Implicit authentication for mobile devices. USENIX Conference on Hot Topics in Security (HotSec), 2009.</font>)Mobile devices introduce many new signals from sensors that measure user interaction(<font color = 'red'>Touch me once and I know it’s you!: Implicit authentication based on touch screen patterns. ACM CHI, 2012.</font>) Although none of the features is unforgeable, such as geo-location (<font color = 'red'> Internet geolocation: Evasion and counterevasion. ACM Computer Surveys, 42(1), 2009.</font>), by combining 120 such signals Google reported a 99.7% reduction in 2013 in the rate of accounts compromised by spammers. (<font color = 'red'>. An update on our war against account hijackers. Google Security Team Blog, Feb 2013</font>)


##Surpass: System-initiated user-replaceable passwords

This paper measures how much security and usability does a system-generated password maintains is the password is user-replaceable.

On a dataset consisting of over 5,000 users, the authors allow interviewees to replace 0-4 characters in a 8-character length passwords generated by the system. They show 3-4 character replacements outperform over 10% purely random-generated passwords in memorability while maintain similar security (less cracked passowrds). They also show that user-chosen passwords do not show statistical superiority in memorability than their schemes.

__Highlight:__
* They use Atkinson-Shiffrin dual memory model, which introduces the concept of short-term memory and long-term memory and elaborate their relations. (<font color = 'red'>A proposed system and its control processes. volume 2 of Psychology of Learning and Motivation, pages 89 – 195. Academic Press, 1968)</font>. So they test short-term memory immediately (after training the user to remember it) and long-term memory after 2 days.
* Measurement metrics: 
	* Fisher's exact test
	* Mann–Whitney U test
	* False discovery rate





