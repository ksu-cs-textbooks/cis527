---
title: "Users & Groups"
weight: 20
pre: "4. "
---

{{< youtube OJgNrBxwJbs >}}

#### Resources

* [Slides]({{< relref "/1-secure-workstations/04-users-groups-slides.md" >}})

#### Video Script

Working with user accounts and groups is one of the key tasks within system administration. Before we get to working directly within a system, here is some background information about users and groups to help you understand why they are so important.

Early computers did not have any concept of user accounts. If you had physical access to a machine and knew how to use it, you could. As computers became more powerful, the concept of time-sharing became increasingly important. While one user was reviewing outputs or rewriting code, another user could use the computer to run a program. To keep track of each person's usage, user accounts were introduced.

With user accounts, each person could be assigned different permissions, allowing some users to have full access while protecting the system from other users who may not have as much knowledge or experience. In addition, user accounts aid in the process of auditing, useful when you need to determine which user performed a malicious action. Finally, user accounts can help protect your systems from unauthorized use. A strong user account and permissions setup is one of the first lines of defense in any cybersecurity scenario.

One of the major concepts in user accounts is authentication and authorization. Authentication is the process of confirming a user's identity by a computer, usually through the use of a password or some other authentication factor. We'll discuss those more deeply on the next slide.

Once a user is authenticated, the user account can then be given authorization to access resources on the computer system. One important caveat to keep in mind: authentication does not imply authorization. Put simply, just because a computer system is able to recognize your user account does not mean you'll automatically be given access to that system.

Let's focus a bit more on authentication. Typically authentication is performed by a computer system confirming the presence of one or more authentication factors from the user. There are three traditional types of authentication factors:

* Ownership - something the user has, such as keys, keycards, tokens, phones, etc. These are typically something physical, but could also be the ownership of a particular email account or phone number.
* Knowledge - something the user knows, such as a password, pass phrase, PIN, or other item. Most computer systems rely solely on knowledge factors for authentication.
* Inherence - something the user is. This includes things such as fingerprints, retina scans, DNA, or other factors about the user which would be very difficult to change or duplicate.

Many modern computer systems, particularly ones used online or in highly secure areas, may use multiple factors of authentication, typically referred to as "two-factor" or "multi-factor" authentication. Some examples are using a debit card, where the card is the ownership factor and the PIN is the knowledge factor, or logging on to an online game, where the password is the knowledge factor and the phone number or email address used for verification is the ownership factor.

Once the user is authenticated, the system has several methods for determining if the user is authorized to access system resources. Typically, the system has some sort of security policy, access control list, or file security in place to determine what resources a user can access. We'll discuss these in more detail as we work with each type of system.

One important concept in user accounts is the use of a user identifier for each account. Internally, the operating system refers to the user account by that identifier instead of the username. This allows the user to change usernames in the future, and for users to reuse usernames from old accounts without inheriting that user's authorization. User identifiers should never be reused. On Linux, this is referred to as the user identifier or UID, while Windows uses the term security identifier or SID.

Beyond the identifier, most operating systems store a few other bits of information about the user account. Namely, the username, password, location of the user's home directory, and any groups the user should be a member of.

Speaking of groups, they are simply a list of user accounts. Their usefulness comes in the fact that you can assign system permissions to a group of users instead of each user individually. That way, as users come and go on a system, they can simply be assigned to the correct groups in order to access resources. Of course, users can be a member of multiple groups, and each group has a unique identifier as well.

Finally, let's review some best practices for working with user accounts on a system. First and foremost, each user of the system should have a unique account. Do not allow users to share accounts, as that will make auditing and working with users who leave that much more difficult.

In addition, enforce strong password policies, and require your users to change their passwords regularly. The recommendation varies, but I've found that changing the password every few months is a good practice.

When you are assigning user permissions, follow the principle of least privilege. Only give users access to the smallest number of resources they need to complete their task. Most users do not need to be full administrators, and don't need access to all of the files on the system. It is much better to be a little overprotective at first than to allow information to be lost due to a user having unnecessary access.

Also, it is very important to create and maintain logs for when users access a system or use administrator privileges. Most computer systems can be configured to create these logs with minimal effort, so it is well worth your time to do so.

As users leave your organization, it is also very important to quickly disable their access. There are many stories online of users leaving a company, only to access the systems after they left to either steal resources or destroy data. By having a policy to disable old user accounts as soon as possible, you'll be able to minimize that risk.

Finally, as a system administrator, it is very important to get into the practice of not using an administrator account as your normal user account on the system. In most cases, you yourself won't need administrator access very often, so by using a normal account, you'll protect your entire organization in the off chance that your account is compromised.

That is all the background information regarding users and groups for this module. Hopefully it will be useful as you work on the first lab in this class.
