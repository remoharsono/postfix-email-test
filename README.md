# POSTFIX Email Testing

Very few application stacks on which I have worked take the time to do
full round-trip E2E testing on their email delivery. What I mean by that
is we rigorously test the generated email content, but it can be quite
difficult to send the email to an inbox and then retrieve/test the
**delivered** content of that email, including transport headers and
any additional encoding.

This project is one way to set up an ephemeral email delivery system to
receive inbound messages and relay the final transport content back
into the test script.

## Overall Logical Flow

```sequence
Test->Test: start server
Test->POSTFIX: send email
Note right of POSTFIX: Email contains x-message-id\nand x-message-callback headers
POSTFIX->POSTFIX: process email transport
POSTFIX->Test: send raw message back
Test->Test: run any assertions
Note over Test: done
```

