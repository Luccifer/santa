Intro
=====

USING PYTHON@2!!!!


**secret-santa** can help you manage a list of secret santa participants by
randomly assigning pairings and sending emails. It can avoid pairing 
couples to their significant other, and allows custom email messages to be 
specified.

Pre-Install 
------------

1. Install Brew (MacOS ONLY!!):

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
   
2. Install Python:
```
brew install python2
``` 
3. Install pip:
```    
brew install pip
```
3. Copy this files:
```    
git clone https://github.com/Luccifer/Santa.git
```
Dependencies
------------

pytz, pyyaml

    pip install pytz

    pip install pyyaml

Usage
-----

Copy config.yml.template to config.yml and enter in the connection details 
for your outgoing mail server. Modify the participants and couples lists and 
the email message if you wish.

    cd Santa-master/
    cp config.yml.template config.yml

Here is the example configuration unchanged:

    # Required to connect to your outgoing mail server. Example for using gmail:
    # gmail
    SMTP_SERVER: smtp.gmail.com
    SMTP_PORT: 587
    USERNAME: you@gmail.com
    PASSWORD: "you're-password"

    TIMEZONE: 'US/Pacific'

    PARTICIPANTS:
      - Chad <chad@somewhere.net>
      - Jen <jen@gmail.net>
      - Bill <Bill@somedomain.net>
      - Sharon <Sharon@hi.org>

    # Warning -- if you mess this up you could get an infinite loop
    DONT-PAIR:
      - Chad, Jen    # Chad and Jen are married
      - Chad, Bill   # Chad and Bill are best friends
      - Bill, Sharon

    # From address should be the organizer in case participants have any questions
    FROM: You <you@gmail.net>

    # Both SUBJECT and MESSAGE can include variable substitution for the 
    # "santa" and "santee"
    SUBJECT: Your secret santa recipient is {santee}
    MESSAGE: 
      Dear {santa},

      This year you are {santee}'s Secret Santa!. Ho Ho Ho!

      The maximum spending limit is 50.00


      This message was automagically generated from a computer. 

      Nothing could possibly go wrong...

      http://github.com/underbluewaters/secret-santa

Once configured, call secret-santa:

    python secret_santa.py

Calling secret-santa without arguments will output a test pairing of 
participants.

        Test pairings:

        Chad ---> Bill
        Jen ---> Sharon
        Bill ---> Chad
        Sharon ---> Jen

        To send out emails with new pairings,
        call with the --send argument:

            $ python secret_santa.py --send

If ya wanna send emails through Gmail you should make ONE MORE STEP!!! -> https://github.com/Luccifer/Santa/blob/master/Screenshot%202019-12-21%20at%2018.59.05.png

To send the emails, call using the `--send` argument
      
    python secret_santa.py --send
