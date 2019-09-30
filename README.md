## inboxcount

this is a simple script to help inform you when you have received a new message in
your gmail-/gsuite-based email accounts.

### setup

create a file containing your account info in `~/.config/inboxcount/accounts.json`,
something like this (see also [application passwords](https://support.google.com/accounts/answer/185833)):
```json
{
    "fake_account@gmail.com": "aiowtuiabwdlkasp",
    "no-reply@business.com": "oqbnaiwlnosdpgwa"
}
```

then set up your system to run checkinbox in the background periodically, e.g. by
adding it to your crontab or creating a plist file and loading it with launchctl.
to include the actual number of new messages in the output, use `checkinbox -c` or
`checkinbox --count` instead.

when new emails are identified, a file will be created at `/tmp/inboxct` - you can 
configure your shell to write the contents of this file to stdout & then delete it
by defining a simple precommand:

bash:
`export PROMPT_COMMAND="[ -e /tmp/inboxct ] && cat /tmp/inboxct && rm /tmp/inboxct"`

zsh:
`precmd () { [ -e /tmp/inboxct ] && cat /tmp/inboxct && rm /tmp/inboxct }`
