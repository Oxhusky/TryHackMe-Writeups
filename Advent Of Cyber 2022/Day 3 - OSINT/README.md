![1](https://user-images.githubusercontent.com/84150540/207571665-22c4404c-628f-433a-b2a0-001b56fb398d.png)

# The Story Nothing escapes detective McRed
As the elves are trying to recover the compromised ```santagift.shop``` website, elf Recon McRed is trying to figure out how it was compromised in the first place. Can you help him in gathering open-source information against the website? 

## Learning Objectives
- What is OSINT, and what techniques can extract useful information against a website or target?
- Using dorks to find specific information on the Google search engine
- Extracting hidden directories through the Robots.txt file
- Domain owner information through WHOIS lookup
- Searching data from hacked databases
- Acquiring sensitive information from publicly available GitHub repositories

## What is OSINT?
OSINT is gathering and analysing publicly available data for intelligence purposes, which includes information collected from the internet, mass media, specialist journals and research, photos, and geospatial information. The information can be accessed via the open internet (indexed by search engines), closed forums (not indexed by search engines) and even the deep and dark web. People tend to leave much information on the internet that is publicly available and later on results in impersonation, identity theft etc.

## OSINT Techniques
  ### Google Dorks
Google Dorking involves using specialist search terms and advanced search operators to find results that are not usually displayed using regular search terms.
You can use them to search specific file types, cached versions of a particular site, websites containing specific text etc. Bad actors widely use it to locate website configuration files and loopholes left due to bad coding practices.

  ### WHOIS Lookup
WHOIS database stores public domain information such as registrant (domain owner), administrative, billing and technical contacts in a centralised database. The database is publicly available for people to search against any domain and enables acquiring Personal Identifiable Information (PII) against a company, like an email address, mobile number etc., of technical contact. Bad actors can, later on, use the information for profiling, spear phishing campaigns (targeting selected individuals) etc. Nowadays, registrars offer Domain Privacy options that allow users to keep their WHOIS information private from the general public and only accessible to certain entities like designated registrars.

  ### Breached Database Search
Major social media and tech giants have suffered data breaches in the past.  As a result, the leaked data is publicly available and, most of the time contains PII like usernames, email addresses, mobile numbers and even passwords. Users may use the same password across all the websites; that enables bad actors to re-use the same password against a user on a different platform for a complete account takeover. Many web services offer to check if your email address or phone number is in a leaked database; [HaveIBeenPwned](https://haveibeenpwned.com/) is one of the free services.

### Searching GitHub Repos
GitHub is a renowned platform that allows developers to host their code through version control. A developer can create multiple repositories and set the privacy setting as well. A common flaw by developers is that the privacy of the repository is set as public, which means anyone can access it. These repositories contain complete source code and, most of the time, include passwords, access tokens, etc.

# Tasks

  ### Task 1: What is the name of the Registrar for the domain santagift.shop?
  We can do this in two ways:
  1. We can browse to [Whois](https://who.is) and in the search bar we write ```santagift.shop``` and under resigrtrat info we find ``` NAMECHEAP INC ``` 
  2. Whois also come preinstalled on Kali Linux we can run the same search with the command: ```whois santagift.shop```

  ### Task 2: Find the website's source code (repository) on [github.com](https://github.com/) and open the file containing sensitive credentials. Can you find the flag?
  1. Go to github.com in the browser
  2. On the top-left in the search bar search for ```santagift.shop```
  3. We see a repository with the name "muhammadthm/SantaGiftShop"
  4. The README.md tells us the credentials for the database are in the **config.php** file
  5. On the second line we can find the flag.

  ### Task 3: What is the name of the file containing passwords?
  **config.php**

  ### Task 4: What is the name of the QA server associated with the website?
  On line 34 in the **config.php** file we can see the the QA server's hostname ```qa.santagift.shop```

  ### Task 5: What is the DB_PASSWORD that is being reused between the QA and PROD environments?
  Again lets look at the **config.php** file on line 31 and 55 we can see the DB_PASSWORD 
