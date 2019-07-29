# Vulgar REST

## Purpose & Scope

Vulgar REST specifies how to create REST-ful APIs.

As any REST intro will tell you, REST is not a specification. Rather, it is a collection of concepts and loose standards. Vulgar REST, on the other hand, is a specification that tells you how to do much of the stuff REST doesn't answer and over which developers endlessly argue (and change their minds).

## Requests

### URL Construction

* All URIs *must* end in a trailing slash. Our reasoning is explained in [On Trailing Slashes](./background/On-trailing-slashes.md).
* Services *may* redirect otherwise valid requests without a trailing slash to valid URI with at trailing slash.
* Services *should not* internally forward requests without a trailing slash.
