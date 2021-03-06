# What is SeetiTel?
In developing nations, ready access to secure internet isn't always available, and whistleblowers may not posess the technical expertise necessary to secure a transmission line or obscure their identity.

Many in the Western world see SMS and voice interaction as last-generation, largely being replaced by native mobile and web applications. However, the developing world is using SMS and telephone based systems in unprecedented numbers, and SeetiTel leverages that. SeetiTel is a telephone and SMS based whistleblowing and leak-releasing system that allows for the use of payphones, anonymous "burner" cell phones, and other anonymous telephonic devices to publish their leaks or whistles, safely and anonymously.

*Seeti* is the Hindi word for "whistle," the name is meant to represent the telephonically enabled leaking/whistleblowing activity, as well as the SeetiTel servers as a "citadel" of security.

# Mechanics

SMS Whistle
  * Immediate release
  * Optionally encrypted
  * Encryption will return a leak ID and a key, the key being a 128 digit
  * Whistles can be looked up by ID, or clicked from the Recent Leaks area

Image Whistle
  * Immediate release
  * Whistles can be looked up by ID, or clicked from the Recent Leaks area

Voice Whistle
  * ID is verbally returned over the phone

The application will be built on node.js and express, with an Apache Cassandra database for data storage to allow for distributed resilience to possible takedown attempts.

# Interfaces

SeetiTel will have a backend API. Frontend access will be through a responsive web interface, possibly utilizing ReactJS, android application, and iOS application, as well as possible browser extensions. Actual leaks will be made through the Twilio API.
