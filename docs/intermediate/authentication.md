# Authentication

## Introduction

Authentication can be a feat as simple or as complex as you want it to be. In-built authentication can be the easiest (so long as you accept that you store user's passwords, albeit hashed), and there are some systems where this is ideal -- think small single-user applications. Similarly, there are some applications where you'll want to use another authentication system. If you're developing a system for an organisation, it makes sense to try and use what they use - why should I have two different accounts to login to my work computer and my other work tools?

In these contexts, it makes sense to use the same authentication system as the organisation. This is where LDAP comes in.

## LDAP

Putting it simply, LDAP (lightweight directory access protocol) is a protocol that allows us to query directory services. The most common directory service in large organisations is Active Directory (AD), which is what Microsoft uses to manage users, devices, access control, etc. When you log into your work computer, you're (most likely) authenticating against AD. We can harness this to make user experience much simpler for our users, and safer for us as developers (we don't have to store passwords!).

### Pros

- Users use the same user account they use to log in, so one less password to remember
- It's the same account, so password changes are reflected immediately
- You can access other information about the user, such as their email address, etc
- You can view the user's group memberships, which can be used for access control
- The application doesn't need to store passwords (safer + less complexity)

### Cons

- Requires the application to be on the same internal network as the directory server
- Some features may require engagement from the organisation's IT department

## IT engagement

Some desirable features of LDAP might not be allowed by your local IT teams. This can include access to view group memberships, or to view other attributes of the user. From a security perspective, this can be a reasonable measure but you may be allowed a specific user account (service account) that has these permissions.

## SAML

SAML (Security Assertion Markup Language) is a protocol for authentication and authorisation. It's more complex than LDAP, but it can also be more secure. SAML follows an OAuth-style authentication flow where the user is redirected to the identity provider (IdP) to authenticate, and then redirected back to the application with a token. This token can then be used to authenticate the user against the IdP, and to access other information about the user. This also means that multi-factor authentication can be handled by the IdP, which additionally means the application is simpler for not having to handle this. It also means that were an organisation requires MFA, the application doesn't need to be aware of or handle this.

### Pros
- The application server doesn't need to be on the same network as the directory server
- Can be used to authenticate against multiple directory servers
- Follows trust policies around multi-factor authentication
- All authentication complexity is handled by the IdP

### Cons
- Requires more configuration than LDAP
- Can be much more complex than LDAP
- Requires engagement from the organisation's IT department from the get-go

!!! tip "Context is everything"
    Keep it simple. If you don't need to implement an advanced authentication mechanism, don't! Keep it simple now, and add complexity later if you need it. Remember, it's easier to add complexity than it is to remove it. Keeping it simple also means there's less to go wrong!