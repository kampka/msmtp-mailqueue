# msmtp-mailqueue
sendmail msmtp drop-in that enqueues mail and sends them at a later time using msmtp and a scheduler (eg. cron, systemd-timer).
Can be useful if
* the machine sending mail is not always connected to the internet, eg. laptops
* you want reliable mail transfer but don't want to run a heavy smtp service like postfix
* don't want to run an mta as root

## Configuration
The scripts are configured using environment variables

* `MSMTP_CONFIG` The path to the msmtp config file to use. See `msmtp(1)` for details.
* `MAILQUEUE_DIR` The directory where your mail queue is stored. Defaults to `$HOME/.msmtp-mailqueue`
* `MAILQUEUE_FLUSH_TIMEOUT` Timeout for sending mail. Defaults to 120 seconds.
* `GPG_ENCRYPT_KEYS` Comma separated list of gpg public keys to use for encrypting your mail. Useful if you don't want to send system mail (eg. failed cron or logs) as plain text as those can often contain sensetive information.

## Installation

Install `src/msmtpq` as your systems `sendmail`, usually `/usr/bin/sendmail`

Add a cron job, systemd-timer or equivalent to run `src/msmtpq-flush`
