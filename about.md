# About `tillitis.se/tillitis-witness-1`

This document describes configuration and operational aspects of
[Tillitis](https://tillitis.se)'s transparency-log witness
`tillitis.se/tillitis-witness-1`.

## Changes to this document

The complete git history is available at:

- [https://github.com/tillitis/tillitis.se-tillitis-witness-1](https://github.com/tillitis/tillitis.se-tillitis-witness-1)

Non-trivial changes are announced on the mailing list at:

- [https://lists.tillitis.se/mailman3/postorius/lists/sigsum-ops.lists.tillitis.se/](https://lists.tillitis.se/mailman3/postorius/lists/sigsum-ops.lists.tillitis.se/)

## Funding

[Tillitis][] is funded by Amagicom AB.

Any changes in funding that would *eventually* affect operation of
`tillitis.se/tillitis-witness-1` will be [announced][] at least three
years in advance.

[Tillitis]: https://tillitis.se/
[announced]: #changes-to-this-document

## Interoperability

`tillitis.se/tillitis-witness-1` implements version 1 of the following
specifications:

- [https://c2sp.org/tlog-cosignature](https://c2sp.org/tlog-cosignature)
- [https://c2sp.org/tlog-witness](https://c2sp.org/tlog-witness)

The witness uses bastion service to be reachable. The specification
for bastion:

- [https://c2sp.org/https-bastion](https://c2sp.org/https-bastion)

## Availability

Any plans to discontinue `tillitis.se/tillitis-witness-1` or the
version 1 specifications that it complies with will be [announced][]
at least one year in advance.

Operational issues are tended to during regular working hours.  This
means weekdays between 08:00 and 17:00 CET/CEST, unless during [public
holidays in Sweden][].

Planned maintenance is [announced][] at least 24h in advance.  Short
disturbances like server reboots, service restarts, and similar are
typically not announced in advance.

Other noteworthy events are [announced][] as soon as possible.

How to report operational issues:

- [https://github.com/tillitis/tillitis.se-tillitis-witness-1/issues](https://github.com/tillitis/tillitis.se-tillitis-witness-1/issues)

Where to find information about past operational issues:

- [timeline](./timeline.md)

[public holidays in Sweden]: https://en.wikipedia.org/wiki/Public_holidays_in_Sweden

## Operations

- **Hardware:** Raspberry Pi 5 with a PoE HAT.
  - 8 GiB RAM
  - 128 GiB SD
- **System software:** Based on Debian 13 (Trixie).
  - Automatic updates are enabled, checking once per day.
  - System is rebooting automatically into new kernel.
  - System time is synchronized with gbg1.ntp.se, gbg2.ntp.se, sth1.ntp.se, sth2.ntp.se, mmo1.ntp.se, mmo2.ntp.se, using systemd.
- **Witness software:** [litewitness](https://github.com/FiloSottile/torchwood/tree/main/cmd/litewitness).
  - Versions are bumped manually after review.
- **Key management:** Signing key is kept in a TKey.
  - [Tkey](https://www.tillitis.se) with [tkey-ssh-agent](https://github.com/tillitis/tkey-ssh-agent).
  - FIXME: [](https://git.glasklar.is/glasklar/trust/audit-log)
- **Physical access:** Employees at [Tillitis][] (Sweden).
- **Remote access:** Employees at [Tillitis][].
  - `ssh-ed25519` keys only, no passwords.
- **Service redundancy:** Little.
  - Power and internet connectivity outages will render the service unavailable.
    - UPS for shorter interruptions (tens of minutes).
  - Hardware failures will render the service unavailable.
- **Key backup:** Yes.
  - FIXME: [https://github.com/tillitis/.github/blob/key-mgmnt/sigsum/key-mgmnt/docs/sigsum-key-management.md](https://github.com/tillitis/.github/blob/key-mgmnt/sigsum/key-mgmnt/docs/sigsum-key-management.md)
- **Availability monitoring:** Physical buzzer if signing does not function.

## How to request witnessing of a log

Send an email to the non-public inbox:

- `witness-registry (at) tillitis (dot) se`

Specify:

- The log's [verification key][]
  - The key name should be a [schema-less URL][]
  - The key name should be the same as the log's [origin line][]
- Some "proof" that you're authorized to use the verification-key name
  - E.g., serve the verification key under a page for the same domain
  - Self-authenticated key-names are exempted from this (e.g., Sigsum logs)
- How often the log is expected to submit `add-checkpoint` requests
- Which bastion host the witness can receive those requests through
- Contact information to someone responsible for the log's operations

Expect a response within three working days.

[verification key]: https://pkg.go.dev/golang.org/x/mod/sumdb/note#hdr-Verifying_Notes
[schema-less URL]: https://github.com/C2SP/C2SP/blob/main/signed-note.md#signatures
[origin line]: https://github.com/C2SP/C2SP/blob/main/tlog-checkpoint.md#note-text

## Configuration

For log operators and trust policies:

- **Verification key:**
`tillitis.se/tillitis-witness-1+9246694a+BAdr6MnufqYJFvDfNgjJRddzAILss3dJ2tLJ7TOf6ncM`

The above key is in vkey format. You may find [sigsum-key][] helpful for
conversions between this and other verification-key formats.

[sigsum-key]: https://git.glasklar.is/sigsum/core/sigsum-go/-/tree/main/cmd/sigsum-key
