# Bug bounty hunting methodology

Every bug bounty hunter has a different methodology for hunting vulnerabilities, and it varies from person to person. It takes a while for a researcher to develop their own methodology and lots of experimentation as well. Once you get the hang of it, it is a self-driven process.

It could be something like ...

## Scope

The scope is the most important aspect of a bug bounty program because it tells you which assets to test and you don't want to spend time testing out-of-scope domains. The scope also tells you which are the most recent targets and which are the ones that can be tested to speed up your bounty process.
Sometimes a program does not necessarily have the entire infrastructure in its scope and there are just a number of apps or domains that are in the scope of the program. Valid targets are targets that help you quickly test for vulnerabilities in the scope and reduce wasting time.

## High-level testing of discovered targets 

The next thing to do is a quick overview of targets, usually done via automated scanning. This basically tells the researchers whether the targets have been tested before or have they been tested a long time ago. If automated scanning does not reveal vulnerabilities or flaws within a web application or a mobile application, it is likely that the application has been tested by researchers before. Nonetheless, it is still advised to test that application one way or another, as this reveals the application's flaws in detail.

## Reviewing all applications

This is a stage where you review all the applications and select the ones based on your skill set. For instance, Google has a number of applications; some of them are coded in Ruby on Rails, some of them are coded in Python. Doing a brief recon on each application of Google will reveal which application is worth testing based on your skill set and level of experience. The method of reviewing all the applications is mostly information gathering and reconnaissance.

## Fuzzing for errors to expose flaws

Fuzzing is termed as iteration; the fastest way to hack an application is to test all of its input parameters. Fuzzing takes place at the input parameters and is a method of iterating different payloads at different parameters to observe responses. When testing for SQL injection vulnerabilities and cross-site scripting vulnerabilities, fuzzing is the most powerful method to learn about errors and exposure of flaws. It is also used to map an application's backend structure.

## Exploiting vulnerabilities to generate POCs

By fuzzing, vulnerabilities can be identified. In other scenarios, vulnerability identification is just one aspect of it. In bug bounty hunting, vulnerabilities have to be exploited constructively to generate strong proof of concepts so that the report is considered in high regard.
A well explained the proof of concepts will accelerate the review process. In conventional penetration tests, vulnerability exploitation is not that important, but in bug bounty hunting, the stronger the proof of concept, the better the reward.