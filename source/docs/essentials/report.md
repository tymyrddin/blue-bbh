# Writing a report

Report formats are not universal, and it may vary from platform to platform, person to person, and case to case. Below are sections that can be included for reporting.

## Descriptive title

The first part of a great vulnerability report is always a descriptive title. Try for a title that sums up the issue in one sentence. It is to allow developers and security team to immediately get an idea of what the vulnerability is, where it occurred, and its potential severity.

----

* _Client-side prototype pollution via flawed sanitization in xyz_
* _Union-based SQL injection in xyz portal_
* _Hostile subdomain takeover in admin.xyz.com_
* _Account takeover using password reset token_
* _Host validation bypass via connection state attack_

----

## Description or summary

The second part of the report is a description or summary. It must be precise, clear, and to the point. People want to have direct engagement with any text, so they do not have to read much and can pick out the salient points easily. The description should not be something generic; it should be environmental and scenario-specific.

----

_The https://example.com/change_password endpoint takes two POST body parameters: `user_id` and `new_password`. A `POST` request to this endpoint would change the password of user `user_id` to `new_password`. This endpoint is not validating the `user_id` parameter, and as a result, any user can change anyone else’s password by manipulating the `user_id` parameter._

----

## Proof of Concept

Without the proof of concept replication steps, there is no way that a developer or security team can recreate the scenario, so it is important to list down the steps exactly which can be used to replicate the vulnerability. 

Some requested report formats will ask for "Clear Steps to Reproduce" AND "PoC". In this case the PoC can be a video, screenshots, photos documenting an exploit, or a code file (for example, an HTML file with a CSRF payload embedded).

When writing "Clear Steps to Reproduce", always treat developer, security team members, or customer as a newbie when writing the proof of concept. This is not unwarranted "talking down". List down all the steps in a detailed and hierarchical manner. Having simple, easy-to-follow, step-by-step instructions will help those triaging the issue to confirm its validity at the earliest opportunity.

----

### Example PoC: Manipulating the WebSocket handshake

1. Click "Live chat" and send a chat message.
2. In Burp Proxy, go to the WebSockets history tab, and observe that the chat message has been sent via a WebSocket message.
3. Right-click on the message and select "Send to Repeater".
4. Edit and resend the message containing a basic XSS payload, such as:

```text
<img src=1 onerror='alert(1)'>
```

5. Observe that the attack has been blocked, and that your WebSocket connection has been terminated. 
6. Click "Reconnect", and observe that the connection attempt fails because your IP address has been banned.
7. Add the following header to the handshake request to spoof your IP address:

```text
X-Forwarded-For: 1.1.1.1
```

8. Click "Connect" to successfully reconnect the WebSocket. 
9. Send a WebSocket message containing an obfuscated XSS payload, such as:

```text
<img src=1 oNeRrOr=alert`1`> 
```

----

## Severity assessment

The report should also include an honest assessment of the bug’s severity to help developers or security team in their prioritisation which vulnerabilities to fix first. 

This depends on the scoring system the client or customer is using. For example, Bugcrowd’s rating system takes into account the [type of vulnerability and the affected functionality](https://bugcrowd.com/vulnerability-rating-taxonomy/), and HackerOne provides a severity calculator based on the [CVSS scale](https://docs.hackerone.com/hackers/severity.html).

List the severity in a single line, or if an impact statement is used, a single sentence.

----

_Severity of the issue: High_

----

## Exploitability

Illustrate a plausible scenario in which the vulnerability could be exploited. 

----

_To exploit this vulnerability, an attacker would have to create an exploit from a well-known template; then would need to convince the administrator into visiting the page with the exploit by social engineering techniques, potentially giving the attacker access to the administrator's account and all associated privileges and resources._

----

## Impact

Show developers or the security team how likely it is that this vulnerability can pose a significant threat and describe its possible impact. This can help them escalate this to higher levels if needs be. 

This is not the same as a severity assessment. A severity assessment describes the severity of the consequences of an attacker exploiting the vulnerability, whereas an impact statement explains what those consequences would actually look like.

----

_The attacker could disable account notifications, enable 2FA to lock them out, and transfer their data to an arbitrary address._

----

## Remediation

It is also important to suggest fixes and patches for a vulnerability found. Demonstrate there are solutions for the flaws. This statement should never be about generically sanitizing the inputs. It should provide them with references and probable methods to reach the solution. Sometimes, the development team doesn't know how to warrant a fix to a vulnerability, and giving them a great statement of a suggested fix, it will be highly appreciated.

----

_The application should validate the user’s `user_id` parameter within the change password request to ensure that the user is authorised to make account modifications. Unauthorised requests should be rejected and logged by the application._

----

## Validate

Always validate the report. Go through your report one last time to make sure that there are no technical errors, or anything that might prevent the security team from understanding it. Follow your own Steps to Reproduce or PoC to ensure that they contain enough details. Examine all the files and code to make sure they work. 

## Resources

* [Intigrity: How to write a good report](https://blog.intigriti.com/hackademy/how-to-write-a-good-report/)
* [HackerOne: Submitting Reports](https://docs.hackerone.com/hackers/submitting-reports.html#related-pages)
* [BugCrowd: Reporting a Bug](https://docs.bugcrowd.com/researchers/reporting-managing-submissions/reporting-a-bug/#creating-a-vulnerability-report)

