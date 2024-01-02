# LOGIN-BRUTE-FORCING

CUPP
Many tools can create a custom password wordlist based on certain information. The tool we will be using is cupp, which is pre-installed in your PwnBox. If we are doing the exercise from our own VM, we can install it with sudo apt install cupp or clone it from the Github repository. Cupp is very easy to use. We run it in interactive mode by specifying the -i argument, and answer the questions, as follows:

[!bash!]$ cupp -i

___________
   cupp.py!                 # Common
      \                     # User
       \   ,__,             # Passwords
        \  (oo)____         # Profiler
           (__)    )\
              ||--|| *      [ Muris Kurgas | j0rgan@remote-exploit.org ]
                            [ Mebus | https://github.com/Mebus/]


[+] Insert the information about the victim to make a dictionary
[+] If you don't know all the info, just hit enter when asked! ;)

> First Name: William
> Surname: Gates
> Nickname: Bill
> Birthdate (DDMMYYYY): 28101955

> Partners) name: Melinda
> Partners) nickname: Ann
> Partners) birthdate (DDMMYYYY): 15081964

> Child's name: Jennifer
> Child's nickname: Jenn
> Child's birthdate (DDMMYYYY): 26041996

> Pet's name: Nila
> Company name: Microsoft

> Do you want to add some key words about the victim? Y/[N]: Phoebe,Rory
> Do you want to add special chars at the end of words? Y/[N]: y
> Do you want to add some random numbers at the end of words? Y/[N]:y
> Leet mode? (i.e. leet = 1337) Y/[N]: y

[+] Now making a dictionary...
[+] Sorting list and removing duplicates...
[+] Saving dictionary to william.txt, counting 43368 words.
[+] Now load your pistolero with william.txt and shoot! Good luck!
And as a result, we get our personalized password wordlist saved as william.txt.

Password Policy
The personalized password wordlist we generated is about 43,000 lines long. Since we saw the password policy when we logged in, we know that the password must meet the following conditions:

8 characters or longer
contains special characters
contains numbers
So, we can remove any passwords that do not meet these conditions from our wordlist. Some tools would convert password policies to Hashcat or John rules, but hydra does not support rules for filtering passwords. So, we will simply use the following commands to do that for us:

sed -ri '/^.{,7}$/d' william.txt            # remove shorter than 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' william.txt # remove no special chars
sed -ri '/[0-9]+/!d' william.txt            # remove no numbers
We see that these commands shortened the wordlist from 43k passwords to around 13k passwords, around 70% shorter.
