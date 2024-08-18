# Sepur

> Version 0.0.0-alpha

In Sepur, there are two concepts: type system and formats.

The sepur type system defines what kinds of types that are possible to be 
represented in a sepur file.

Serialization is performed by converting application data into the sepur type
system then represented in bytes by following the sepur format. And vice versa
for deserialization.

## Type System

TODO

## Format

The following section will describe the format of sepur.

### Notation

Inspired from MessagePack.

```
one byte:
+--------+
|        |
+--------+

a variable number of bytes:
+========+
|        |
+========+
```

### Structure

The sepur format is separated into two sections: Content and Index, each will
be referred to "The content section" and "The index section", respectively.

The content section should contain a single object that we call as a "cell".
The main cell that is contained in the content section will be referred to as
"the root cell".

There are two different cells: nested cells and primitive cells.

Nested cells are cells that contain other cells, such as an Array or an Object.

Primitive cells are cells that contain primitive data, such as a String, Number,
or a Boolean.

A cell is defined by its type and its value. The type of the cell is determined
by the first byte in the cell. The value of the cell is determined by the bytes
after the first byte, limited by the length of the type.

The first 4 bytes in the sepur format will always be fixed to be the ASCII of
`spur`.

The next bytes will be the content section, until it reaches the index section
header, which is `0x00 0x00 0x00 0x00`, which will then be followed by the
content of the index.
