# Summary of Digital Ocean's LDAP Tutorial

This is a summary of the digital ocean's [tutorial][digital-ocean-tutorial] on
LDAP.

## LDAP

The Lightweight Directory Access Protocol (LDAP) is an open protocol for a
directory service. Everybody is able to implement this, and the latest version
of the  protocol is described in [RFC4511].

LDAP is a communication protocol, and determines how data in a directory
service is presented to users.

## Attributes

Main elements in LDAP are called attributes. Attributes are basically
key-value pairs. The keys in these key-value pairs are pre-defined, and should
be know by the LDAP server.

Setting the values of attributes is done by `: `, and refering an attributes
just uses a `=`. The following example sets the value `dn`, and refers to the
attributes `sn`, `ou` and `dc`:

```text
dn: sn=Reitsma,ou=People,dc=ing,dc=com
```

## Entries

In LDAP, attributes describe a particular _thing_, the _thing_ itself is called
and entry, and is a collection of attributes. When comparing to a relational
database, the entries are records, and attributes are the columns.

An example of an entry in the LDAP Data Interchange Format [LDIF], described by
[RFC2849]:

```ldif
dn: sn=Reitsma,ou=People,dc=ing,dc=com
objectClass: person
sn: Reitsma
cn: Mischa Reitsma
```


[digital-ocean-tutorial]: https://www.digitalocean.com/community/tutorials/understanding-the-ldap-protocol-data-hierarchy-and-entry-components
[LDIF]: https://en.wikipedia.org/wiki/LDAP_Data_Interchange_Format
[RFC2849]: https://tools.ietf.org/html/rfc2849
[RFC4511]: https://tools.ietf.org/html/rfc4511
