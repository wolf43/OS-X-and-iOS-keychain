# Keychain


### Introduction
Keychains are a secure storage containers provided by Apple for OS X and iOS. They are the recommended way of storing sensitive information like passwords, private keys, certificates and other information an application or user wants to protect.  
Keychain services are built on top of CDSA(Common Data Security Architecture). The keychain API also provides some funcitonality to interact with native CCSM structures. Most developers can get everything done just by using keychain API.  


### Differences between iOS and OSX keychain
* iOS only has one keychain : OSX has one keychain per account by default and user/applications can add more
* Apps in iOS can only access its own items in keychain : Users in OSX allow access to keychain items to apps
* Keychain only exists in one(unlocked state) in iOS : There are 2 states in OSX, locked and unlocked


### Using keychain  
There are 3 main ways to access keychain API on OSX:  
* Command line utility named security - We will go over basic keychain operations using this utility
* Through swift and objective c methods(from security framework) listed here <https://developer.apple.com/library/mac/documentation/Security/Reference/keychainservices/index.html#//apple_ref/doc/uid/TP30000898-CH1g-SW5>  
* Keychain Acess app - This is a nice UI that lets you see the keychain and entries in the keychain  
Next we will go over a few basic keychain operations

#### Listing available options
security h or just security

#### Listing keychains
security list-keychains

#### Adding a keychain
security add-keychain  
This will not show up if you run security list-keychains, you have to add it to search  
This stackoverflow answer can help <http://stackoverflow.com/questions/20391911/os-x-keychain-not-visible-to-keychain-access-app-in-mavericks> or you can open key chain access, click file->add keychain, select keychain_you_created.keychain(it will be in the same location as the login keychain - your_user/Library/Keychains)  

#### Adding entry to keychain
security add-generic-password [-a account] [-s service] [-w password] [options...] [-A|-T appPath] [keychain_to_add]

#### Retriving entry from keychain
security find-generic-password password_to_find keychain_to_search

#### Removing entry from keychain
security delete-generic-password password_to_find keychain_to_search

#### Deleting keychain
security delete keychain keychain_to_delete

### Additional reading material  
Keychain services programming guide - <https://developer.apple.com/library/mac/documentation/Security/Conceptual/keychainServConcepts/01introduction/introduction.html#//apple_ref/doc/uid/TP30000897-CH203-TP1>  
Keychain concepts - <https://developer.apple.com/library/mac/documentation/Security/Conceptual/keychainServConcepts/02concepts/concepts.html#//apple_ref/doc/uid/TP30000897-CH204-TP9>  
OSX keychain services tasks - <https://developer.apple.com/library/mac/documentation/Security/Conceptual/keychainServConcepts/03tasks/tasks.html#//apple_ref/doc/uid/TP30000897-CH205-BCIHAAGG>  
iOS keychain services tasks - <https://developer.apple.com/library/mac/documentation/Security/Conceptual/keychainServConcepts/iPhoneTasks/iPhoneTasks.html#//apple_ref/doc/uid/TP30000897-CH208-SW1>  
CDSA definition - <https://www.techopedia.com/definition/10244/common-data-security-architecture-cdsa>  
CDSA reference - <http://www.opengroup.org/security/cdsa.htm>  
SANS doc on CDSA - <https://www.giac.org/paper/gsec/578/common-data-security-architecture/101346>  
