# 929. Unique Email Addresses

https://leetcode.com/problems/unique-email-addresses/

Every email consists of a local name and a domain name, separated by the @ sign.

For example, in `alice@leetcode.com`, `alice` is the local name, and `leetcode.com` is the domain name.

Besides lowercase letters, these emails may contain '.'s or '+'s.

If you add periods ('.') between some characters in the **local name** part of an email address, mail sent there will be forwarded to the same address without dots in the local name. For example, "alice.z@leetcode.com" and "alicez@leetcode.com" forward to the same email address. (Note that this rule does not apply for domain names.)

If you add a plus ('+') in the **local name**, everything after the first plus sign will be **ignored**. This allows certain emails to be filtered, for example `m.y+name@email.com` will be forwarded to `my@email.com`. (Again, this rule does not apply for domain names.)

It is possible to use both of these rules at the same time.

Given a list of `emails`, we send one email to each address in the list. How many different addresses actually receive mails?

**Example 1**

```
Input: ["test.email+alex@leetcode.com","test.e.mail+bob.cathy@leetcode.com","testemail+david@lee.tcode.com"]
Output: 2
Explanation: "testemail@leetcode.com" and "testemail@lee.tcode.com" actually receive mails
```

**Note:**

- `1 <= emails[i].length <= 100`
- `( 1 <= emails.length <= 100`
- Each `emails[i]` contains exactly one '@' character.
- All local and domain names are non-empty.
- Local names do not start with a '+' character.

## My Solution

```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        unique_emails = []
        for email in emails:
            at_index = email.index('@')
            local_name = email[:at_index].replace('.', '')
            if '+' in email:
                plus_index = local_name.index('+')
                unique_emails.append(local_name[:plus_index] + email[at_index:])
                continue
            unique_emails.append(local_name + email[at_index:])

    return len(set(unique_emails))
```

## Faster Solution

```python
class Solution:
    def numUniqueEmails(self, emails: List[str]) -> int:
        result = []

        for email in emails:
            aux = email.split("@")
            contact = aux[0]
            email = aux[1]
            result.append(contact.replace(".","").split("+")[0] + "@" + email)

        return len(set(result))
```

## Challenge

Try to do it with Regular Expresion operations:

https://docs.python.org/2/library/re.html
