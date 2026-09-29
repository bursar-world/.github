# Security policy

Bursar contracts hold real funds on Robinhood Chain mainnet (chain 4663). If you find a way to
move, freeze or misdirect those funds, or to make any part of Bursar act outside the limits a
principal set, please tell us privately before anyone else.

This policy covers every repository in the bursar-world organization that does not publish its
own. The [bursar repository's policy](https://github.com/bursar-world/bursar/blob/main/SECURITY.md)
lists the contract addresses in scope and takes precedence for that code.

## Audit status

No Bursar contract or service has had an external audit. Limits on mainnet are kept low so that a
defect costs little: a provider with no history can be paid at most 25 USDG per job, rising with
its record to at most 125 USDG per job.

## How to report

Do not open a public issue, discussion or pull request about a vulnerability. Use one of these:

- Email **[security@bursar.world](mailto:security@bursar.world)**.
- Open a private report through **Security → Report a vulnerability** on the affected repository.

If funds are at risk now, start the email subject with `URGENT`. Contracts can be paused and
agents revoked quickly, and an early report is what makes that possible.

Please include the affected contract address, package, service or page; what an attacker gains and
what it costs them; steps to reproduce, ideally a Foundry test or a script against a fork of chain
4663; any transaction hashes involved; and how you would like to be credited. Never send private
keys, and never move funds you do not own to prove a point.

## What happens next

- We acknowledge every report within 3 business days.
- We confirm whether we can reproduce it, share our severity assessment, and keep you updated
  while we work on a fix.
- We agree a disclosure date with you. By default we publish an advisory once the fix is live and
  no later than 90 days after your report.
- We credit you in the advisory unless you ask us not to.

There is no bug bounty programme yet. This page will say so when there is one.

## Good faith

We will not pursue legal action against anyone who reports in good faith, stays within this
policy, avoids harm to users and their funds, and gives us reasonable time to fix the issue before
talking about it publicly.
