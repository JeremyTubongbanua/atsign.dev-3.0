---
layout: single

title: 'Public and Private Keys' # The title (ON THE PAGE)
lead: | # The lead below the title (ON THE PAGE)
  Providing access to information


description: | # SEO Description of the page (Shows in google and atsign.dev search)
    Definition of public and private keys

draft: false # Change this to "true" to hide the page
toc: true # Change this to "true" to show the table of contents
weight: 205 # For single pages, lower is first.
---

## Definition
A private key is used in asymmetric key cryptography. Asymmetric key cryptography is based on applying mathematical functions to numbers to achieve personal secrecy. It uses two keys, one being the private key. If you think of decryption as locking and unlocking padlocks with keys, then the padlock that is locked with a public key can only be unlocked with its corresponding private key.

On the other hand, public keys are distributed to the trusted masses. This is done through a public-key distribution channel. This channel should provide authentication and integrity. Someone should not send their public key to the community pretending to have a different public key. Everyone should have their own private and public keys. For example, Bob only needs one private key to receive all correspondence in the community, but Alice needs *n* public keys to communicate with *n* entities in the community, one public key for each entity. In other words, Alice needs a ring of public keys.

## How it works at Atsign

A key in the @protocol can be formed by using any alphanumeric and special characters (UTF-8) excluding "@", ":" and a white space (" "). A key in a secondary can be any of the following 5 types:

1. Public Key

    - A public key is a key which can be looked up by any @sign holder.

    - A public key should be part of the *scan* verb result.

    - Format of the public key should be **public**:\<identifier>:**<@sign>**

    **Example:**    

    ```public:location@alice```

    > The owner of the secondary should be allowed to update or delete the value of a public key.


2. Self Key
        
    - A Self key is a key which cannot be looked up any @sign holder other than the one created it.
    
    - A Self key should not be returned in a *scan* verb result.
    
    - Format of the Self key should be **privatekey**:\<identifier>:**<@sign>**

    **Example:**    

    ```privatekey:pk1@alice```

    > The owner of the secondary should be allowed to update or delete the value of a private key.


3. Shared key
    - A shared key can only be looked up by an @sign holder with whom the data has been shared.
    - A shared key should be part of the *scan* verb result only for the person who created it and the specific person it has been shared with.
    - Format of the key shared with someone else should be   
    **cached**:**<Shared with @sign>**:\<identifier>:**<Created by @sign>**

    **Example:**    

    ```@bob:phone@alice```
    
    > Note: Above Key should be part of scan verb result for only @alice and @bob 

    > The owner of the secondary should be allowed to update or delete the value of a user key.
 

4. Private Key

    - Private keys start with an underscore(_) and are not displayed in scan results. Private keys can only be looked up by the owner of the secondary


5. Cached Key

    - A cached key is a key that was originally created by another @sign owner but is now cached on the Secondary Server of another person's @sign as they were given permission to cache it. 
    
    - A cached key should be listed in the *scan* verb result for the @sign owner who cached it.

    - Format of the key shared with someone else should be   
    **cached**:**<Shared with @sign>**:\<identifier>:**<Created by @sign>**

    **Example:**    

    ```cached:@bob:phone@alice```

    > The person who has cached the key should not be allowed to update the cached key.

    > An @sign owner who has created and shared the key should be allowed to update a cached key, and if the "autoNotify" config parameters is set to true, the updated value should be notified (please refer to the `notify` verb) and the cached key updated with the new value.

    > If the person who originally shared the keys set the CCD (Cascade delete) to true, the cached key will be deleted when the original key is deleted.   

{{< image class="bg-white" src="E2EE.png" type="page"  >}}


## Related Resources

{{< card/breadcrumb href="/docs/reference/encryption/" first="Encryption" >}}

{{< card/breadcrumb href="/docs/reference/privacy/" first="Privacy" >}}

{{< card/breadcrumb href="/docs/reference/cram/" first="CRAM" >}}

{{< card/breadcrumb href="/docs/reference/pkam/" first="PKAM" >}}