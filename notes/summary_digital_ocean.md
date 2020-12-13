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

## Data Information Trees

LDAP organizes the various entries in Data Information Trees. These are similar
to a directory structure on a file system, where except for the root directory,
all entries have one parent and 0-n children.

The _full path_ of an entry is represented by the distinguished name (dn), and
for the previous example, the distinguished name is:

```ldif
dn: sn=Reitsma,ou=People,dc=ing,dc=com
```

Defining new attributes in LDAP is quite cumbersome. An example definition
of the _name_ attribute is:

```text
attributetype (2.5.4.41 NAME 'name' DESC 'RFC4519: Common supertype of name attributes'
               EQUALITY caseIgnoreMatch
               SUBSTR caseIgnoreSubStringMatch
               SYNTAX 1.3.6.1.4.1.1466.114.121.1.15{32768})
```

Most useful attributes are already part of most LDAP implementations.

## Attributes, Object Classes and Schemas

Multiple attributes can be collected in an `objectClass`. For example, the
`objectClass: person` has the following attributes:

- cn: Common name, required attribute
- sn: Surname, required attribute
- description
- seeAlso: reference to related entries
- telephoneNumber
- userPassword

There are two types of objectClasses:

- Structural: Entries must have exactly one of these objectClasses
- Auxiliary: 0-n extra objectClasses

The objectClasses and attribtues can be combined in schemas. These are just a
combination of all the definitions of objectClasses and attributes, and can
be shared with an LDAP server to define all required objectClasses and
attributes.

## Adding Entries

Entries are usually added as a child of an already existing entry. The top
level is usually a label that can be of any objectClass, and make sense for
the type of data stored in the tree. Three examples are:

1. Domain components: `dn=mreitsma,dn=com` for the domain `mreitsma.com`
1. Location: `l=Almere,c=Netherlands` for the location Almere in the country
   Netherlands
1. Organizational Units: `ou=CoreBank,o=ING` for the organizational unit
   CoreBank in the organization ING

The organizationalUnit obeject classes are mainly used in organizations to
group together entries. Common examples are `ou=People`, `ou=groups` or
`ou=inventory`.

## Searching and Navigating Entries

LDAP is optimized for lateral searched, which means that shallow trees
(minimal depth) are better.

Entries are referred to by the attributes within an entry. Withing an entry,
all child entries must be uniquely defined by a (combination of) attrubutes.
This is called the relative distinguished name (RDN). All RDN's up to the
root are called the distinguished name (dn), which must be specified when
introducing entries. The file system analogue of the RDN and dn are the
full path (dn) and files/directories withing a directory (RDN).

The distinguished name, unlike file system paths and internet domains, read
right to left instead of left to right.

## Inheritance

An objectClass can inherit, using the term SUP in the definition, followed by
the parent. Other terms used in definitions are AUXILIARY or STRUCTURAL.

Attributes can also implement from other attributes, and be more specific. The
new attribute then inherits all methods and properties of the parent.

## Protocols

There are three common LDAP protocols:

- `ldap://`: The normal LDAP protocol
- `ldaps://`: LDAP over TLS/SSL
- `ldapi://`: An IPC version of LDAP, using local sockets.


[digital-ocean-tutorial]: https://www.digitalocean.com/community/tutorials/understanding-the-ldap-protocol-data-hierarchy-and-entry-components
[LDIF]: https://en.wikipedia.org/wiki/LDAP_Data_Interchange_Format
[RFC2849]: https://tools.ietf.org/html/rfc2849
[RFC4511]: https://tools.ietf.org/html/rfc4511
