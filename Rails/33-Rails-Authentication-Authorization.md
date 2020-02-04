# [Rails - Introduction to Authentication and Authorization](https://github.com/saramccombs/introduction-to-authentication-and-authorization)

## Breaking Down the Authentication and Authorization Problem

We can divide the "who can see what" problem into four smaller, but related
problems:

- Who you claim to be (i.e. **Identification**)
- Validation that you _are_ you who you claim to be (i.e. **Authentication**)
  and association of _roles_ based on your identity
- What given _roles_ are allowed to do (i.e. **Access Policy**)
- Mechanisms to enforce the Access Policy (i.e. **Authorization**)

## Examples of Authentication and Authorization Flows

**Identification**, **Authentication**, **Access Policy** and **Authorization**
are security concepts that apply equally to the physical and digital worlds. If
you were to enter your local bank branch, here's how these concepts would
apply.

1. Assert who you are by stating your name and showing an ID
   (**Identification**)
2. Verify your identity claim by verifying you possess a secret that only the
   "real you" would know and which has been established prior to this moment.
   This might be a password, matching signature, [knowledge of bedroom furniture][odyssey],   etc. (**Authentication**)
3. _Interlude_ At this point the bank knows that they are dealing with a
   _verified entity_. From the perspective of their system, all _verified
   entities_ act with respect to _roles_. At point of **Authentication** the
   _verified entity's_ collection of _roles_ is _also_ retrieved.
4. You then proceed to withdraw enough money for another delicious Greenleaf
   juice. At this point the **Access Policy** ("_As an_ `owner` of an account,
   the `owner` is permitted to withdraw money from that account provided that the
   amount to withdraw does not reduce the balance to $0.00 or less") is
   implemented in an activity known as **Authorization**. Since your
   authentication step validated you in the role of `owner`, this transaction
   proceeds (provided you have enough money to cover that delicious, organic
   juice!).
5. You then walk up to the vault and try to go in. Your _roles_ `owner` and
   `customer` have a "NO ACCESS" **Access Policy** as relates to the bank's vault. As
   such, you will _not_ be **Authorized** and cannot enter the vault (and will
   probably earn the new role of `attempted robber`).

Let's apply this thinking to a web login.

When you access your bank account on the web you will:

1. Enter a username. That is an identity claim. (**Identification**)
2. Enter a password. You are providing proof of your identity claim.
   (**Authentication**)
3. You will be granted certain privileges based on your identity. (**Access Policy**)
4. Sprinkled throughout the web application, your bank will have checks
   (**Authorization** events) to enforce the **Access Policy.** You will not be
   allowed to alter your balance and add $1,000,000.

   ## Defining Key Authentication and Authorization Terms

We can define the four security concepts that help us answer the "who can see
what" questions as:

* **Identification**: Obtaining an identity claim from the user. (e.g., my
  email is,  my name is)
* **Authentication**: The process of verifying the identity claim of a user.
* **Access Policy**: A usage policy based on the identities and attributes of
  the resource being accessed and of the user requesting access.
* **Authorization**: Access privileges granted to a user or the act of granting
  those privileges.

P.S. The definitions above are fairly abstract, and they may not always 
directly map to a specific framework or library functionality. Nevertheless, it's 
important to have a general understanding of their meaning.