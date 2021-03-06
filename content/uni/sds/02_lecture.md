+++
title = "Security of Distributed Software - Lecture 02"
author = ["eo shiru"]
date = 2019-04-09
lastmod = 2019-04-27T09:49:29+02:00
tags = ["uni", "security-ds"]
draft = false
+++

We can achieve the security goals mentioned in the previours lecture by:

-   information encryption
-   implementation of authentication
-   establishment of security activities
-   monitoring of the system or the network in terms of attacks
-   continous reduction of weak spots
-   etc

{{< figure src="/knowledge-database/images/security-procedures.png" >}}

In the data transfer model (2 users communicating) we can distinguish for example two types of attackers:

-   passive attacker
    -   can only listen, not manipulate
    -   confidentiality threat
-   active attacker
    -   can listen, change, delete, duplicate
    -   threat for confidentiality, integrity and authenticity

The difference between authenticity and liability lays in the focus between internal and external relationships. Here's an example: Authenticity means that Bob is sure the data comes from Alice (internal) - Liability means that Bob can prove this to third parties (external).

Here are some types of threats:
Interception of transmitted data

-   Modification of transmitted data
    -   Change
    -   Delete
    -   Insert
    -   Reorder data blocks
-   Masquerade
    -   Faking a false identity
    -   Sending messages with a false source address
-   Unauthorized access to systems
    -   Keyword „Hacking”
-   Sabotage (Denial of Service)
    -   Causing an overload situation (including hardware)
    -   “Destroying” protocol instances by illegal packets

And here are _some_ attack techniques:
Tapping cables or radio links

-   Interposing (man-in-the-middle attack)
-   Replaying of intercepted messages (replay attack) (e.g. replay of login messages for the purpose of unauthorized access)
-   Selective changing / swapping of bits or bit strings (without being able to decrypt the message)
-   Break-in by taking advantage of errors (buffer overflows)
-   Break-in by means of active components (trojans, worms, backdoors)
-   Breaking cryptographic algorithms
-   Social Engineering (e.g. through direct contact and social web)

And some countermeasures:

-   Don‘t use self-made algorithms, use only proven algorithms that are considered safe!
-   Use safe methods and replace old algorithms
-   Behaviour (Pattern) analysis
-   Use Social Web the right way
-   Know your enemy
-   limit the attack surface
-   limit identity properties
-   distribute attack surface
-   apply encryption everywhere

Security should be considered in an integrated way. This means:

-   consideration of all assets
-   based on risk assesment
-   use adequate security approaches and services (often a mix of different techniques)

All in all it is almost impossible to achieve 100% security. Therefore one has to clearly define what has to be protected and how high the according security requirements should be.


## Excourse: GDPR {#excourse-gdpr}

**What is a data subject?**

-   any person whose personal data is being collected, held or processed

**What are the data subject's rights?**

-   Individuals/Citizen (data subjects) have the right to:
    -   information about the processing of your personal data
    -   obtain access to the personal data held about you
    -   ask for incorrect, inaccurate or incomplete personal data to be corrected
    -   request that personal data be erased when it’s no longer needed or if processing it is unlawful
    -   object to the processing of your personal data for marketing purposes or on grounds relating to your particular situation
    -   request the restriction of the processing of your personal data in specific cases
    -   receive your personal data in a machine-readable format and send it to another controller (‘data portability’)
    -   request that decisions based on automated processing concerning you or significantly affecting you and based on your personal data are made by natural persons, not only by computers; You also have the right in this case to express your point of view and to contest the decision

**What is personal data and what not?**<br />
&rarr; Personal data is any information that relates to an identified or identifiable living individual. Different pieces of information, which collected together can lead to the identification of a particular person, also constitute personal data.<br />
Personal data that has been de-identified, encrypted or pseudonymised but can be used to re-identify a person remains personal data and falls within the scope of the law.<br />
Personal data that has been rendered anonymous in such a way that the individual is not or no longer identifiable is no longer considered personal data. For data to be truly anonymised, the anonymisation must be irreversible.<br />
Examples of personal data:

-   name and surname, home adress, email adress
-   identification card number
-   location data
-   IP adress
-   cookie ID

Examples of data not considered personal data:

-   a company registration number
-   an email adress such as info@company.com
-   anonymised data

**What is a data controller?**<br />
The controller or data controller is simply the organization (a legal person, agency, public authority, etc.) or the natural person which, alone or depending on the organization and personal data processing activity, in collaboration with others defines what needs to happen with the personal data (and also collects personal data) and obviously is key in personal data protection.
Formal definition (Article 4):<br />
_‘controller’ means the natural or legal person, public authority, agency or other body which, alone or jointly with others, determines the purposes and means of the processing of personal data; where the purposes and means of such processing are determined by Union or Member State law, the controller or the specific criteria for its nomination may be provided for by Union or Member State law_

**What is a data processor?**<br />
The processor or data processor is a person or organization who deals with personal data as instructed by a controller for specific purposes and services offered to the controller that involve personal data processing (remembering that processing can be really many things under the GDPR). The formal definition of the processor as you can read it in the GDPR Articles (GDPR Article 4):<br />
_Processor means a natural or legal person, public authority, agency or other body which processes personal data on behalf of the controller._ The main difference to data controllers is that the GDPR has a really different stance with regards to data processors whereby they have duties and responsibilities that are directly applicable and can be directly enforced and GDPR compliance is a shared obligation as you will discover.
