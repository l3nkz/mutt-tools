# Mutt Tools

A collection of useful tools which I use in conjunction with my Mutt setup.

## mutt_profile

Since I use multiple Mutt instances for my different mail accounts, I created
a script which manages the configuration file hell for me. In addition to the
different accounts, I also start mutt in different modes. So for example for
normal reading or composing of mails. Accordingly, I have a relatively complex
directory structure to configure my Mutt, which looks as follows:

    mutt
     |-> config
     |-> profiles
     |    |->     profile1
     |    |->     profile2
     |-> accounts
     |    |->     account1
     |    |        |-> general
     |    |        |-> mailboxes
     |    |->     account2
     |    |        |-> general
     |    |        |-> mailboxes
     |    |        |-> maillinglists
     |-> common
     |    |->     general
     |    |->     colors
     |    |->     keybindings
     |-> foldertypes
          |->     default
          |->     normal
          |->     mailinglists

The files in the profile directory contain the mode depending settings and load
additional files from the common directory. The files in the account
directories contain the corresponding settings for the account such as mail
address, signature, and headers. The config file in the base directory sets up the
directories and then loads the mode and account settings. In the foldertypes directory
one can define various settings for special types of folders (e.g. mailinglists) which
can then be loaded via folder-hooks.

The `mutt_profile` script adapts the main configuration file and then starts
Mutt with the correct settings.


## mutt_compose

I use this script to create additional terminal windows running their own mutt instance
to be able to write my mails in a different terminal than where I read my mails. The
script uses `mutt_profile` to spawn a new Mutt instance in the compose mode.


## mutt_view

This script is a small starter script which can be used to execute viewers for attachments
detached from the actual Mutt instance. The script will copy the file and then run the viewer
program in the background so that Mutt can be used as if nothing happened.


## mutt_send

This script will act as a proxy between Mutt in the compose profile and the actual sendmail
binary. The purpose of this script is to handle various auxiliary tasks such as marking a mail
as replied-to, logging and other similar things.


## mutt_addresses

This script is intended to work as an address book for mutt. It can query the notmuch mail
indexing tool to retrieve mail addresses with the given search string. Hence, this script can
be used as a drop-in replacement for mutt's 'query\_command' setting and thus replace tools
such as abook.


## mailboxsplit

I wrote this script to be able to extract all mailboxes belonging to one account from the
mailboxes file created by offlineimap. The script extracts the mailboxes and performs some
simple renaming so that Mutt properly understands them.


## mailboxwatcher

This script continuously monitors the mailboxes file generated by offlineimap and adapts the
account mailboxes files accordingly so that they are always up to date.


## mailmanage

`mailmanage` is a script which can automatically remove mails from a maildir which are older
than a specified number of days. I use this script to keep my maildirs which contain mails from
mailing lists small so that Mutt can open them as fast as possible.

The script uses [mmanage](https://github.com/l3nkz/mail-tools "mail-tools"), a python tool designed
to perform archiving or cleaning operations on maildirs.
