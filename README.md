# DSN parser

## Installation

Follow the [instructions](https://docs.halon.io/manual/comp_install.html#installation) in our manual to add our package repository and then run the below command.

### Ubuntu

```
apt-get install halon-extras-dsn
```

### RHEL

```
yum install halon-extras-dsn
```

## Exported functions

These functions needs to be [imported](https://docs.halon.io/hsl/structures.html#import) from the `extras://dsn` module path.

### dsn_parse($mail, $options)

Parse a rfc3464 (message/delivery-status) or rfc6533 (message/global-delivery-status) compliant MIME part into a associative array containing the per-message fields and per-recipient fields (all lowercased).

**Params**

- mail `MailMessage` - The mail message
- options `array` - options array

**Returns**:
* An `array` with keys `message`, `recipients` and optionally `original_message` and `original_headers`
* `none` on errors

The following options are available in the **options** array.

- original_message `boolean` - Include the original mail message in the output (if it exists), the default is `false`
- original_headers `boolean` - Include the original mail message headers in the output (if they exist), the default is `false`

```
{
  "message": {
    "reporting-mta": "dns; mail.example.org",
    "received-from-mta": "smtp; mx1.example.com (1.2.3.4)",
    "original-envelope-id": "f03cf414-5fa5-11e9-9074-d9e886935329",
    "arrival-date": "Mon, 15 Apr 2019 19:42:44 +0200"
  },
  "recipients": [
    {
      "final-recipient": "rfc822; user@example.org",
      "action": "failed",
      "status": "5.7.1",
      "remote-mta": "dns; imap.example.org",
      "diagnostic-code": "smtp; 550 5.7.1 An error message"
    }
  ]
}
```
