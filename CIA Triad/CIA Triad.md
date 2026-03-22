# CIA Triad - the security mindset
what is CIA?
CIA stands for:
> confidentiality
> integrity
> availability
but this is not just a definition.

it is a security thinking framework.

whenever you see a system, website, server or data your brain should automatically ask:
is it protected?
is it correct?
is it accessible when needed?

that is the CIA mindset.

1) confidentiality
meaning:
data should only be accessed by authorized people.

mindset question:
> who is allowed to see this?
> what happens if an attacker reads it?

example:
- passwords
- personal data
- bank details
- company secrets

how it is protected:
- encryption
- strong passwords
- access control
- permissions
- MFA

if broken:
- data leak
- data breach
- privacy violation

2) integrity
meaning:
data should not be modified or tampered with.

mindset question:
> has this data been changed?
> can someone alter it without permission?

examples:
- bank transaction amount
- exam results
- logs in soc
- software code

how it is protected:
- hashing
- digital signatures
- file permissions
- checksums
- logging

if broken:
- wrong data
- fraud 
- fake logs
- malware injected

3) Availability
meaning:
systems and data should be accessible when needed.

mindset question:
> can users access this right now?
> what if the server crashes?

examples:
- website uptime
- atm machine working
- email server running
- company network

how it is protected:
- backups
- redundancy
- laod balancing
- DDos protection
- monitoring

if broken:
- website down
- business loss
- service disruption

CIA IS A MINDSET
CIA triad is not just theory.

it is a way of thinking.

whenever you analyze something (as SOC or pentester), ask:
- did attacker steal data? -> confidentiality issue
- did attacker modify data? -> integrity issue
- did attacker crash system? -> availabilty issue

Real world thinkingj example
if a hacker breaks into a company:
- if he steals customer data -> C
- if he changes salary records -> I
- if he shuts down website -> A


