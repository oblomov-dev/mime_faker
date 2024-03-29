# MIME Faker
No MIME Repository exists in ABAP Cloud. This solution helps to store files on the ABAP Stack and serves an "ABAP Standard" and "ABAP for Cloud" compatible solution. Of course this is not a real MIME Repository!

#### Approaches
1. Store files as comments in an ABAP method <br>
2. Store files in a custom table <br>
3. ...? <br>


## Approach I
Use the interface:
```abap
INTERFACE z2ui5_if_mime_container
  PUBLIC.

  TYPES:
    BEGIN OF ty_s_metadata,
      name   TYPE string,
      format TYPE string,
      descr  TYPE string,
    END OF ty_s_metadata.

  METHODS get_metadata
    RETURNING
      VALUE(result) TYPE ty_s_metadata.

  "! Dummy Container, filled with file data as comments, don't use this!
  METHODS container.

ENDINTERFACE.
```
And store your file as a comment in the method "container":
```abap
  METHOD z2ui5_if_mime_container~container.
*{
*    "glossary": {
*        "title": "example glossary",
*        "GlossDiv": {
*            "title": "S",
*            "GlossList": {
*                "GlossEntry": {
*                    "ID": "SGML",
*                    "SortAs": "SGML",
*                    "GlossTerm": "Standard Generalized Markup Language",
*                    "Acronym": "SGML",
*                    "Abbrev": "ISO 8879:1986",
*                    "GlossDef": {
*                        "para": "A meta-markup language, used to create markup languages such as DocBook.",
*                        "GlossSeeAlso": ["GML", "XML"]
*                    },
*                    "GlossSee": "markup"
*                }
*            }
*        }
*    }
*}
 ENDMETHOD.
```
Read your file as it is done in the sample app: <br>
<img width="1200" alt="image" src="https://github.com/oblomov-dev/a2UI5_cloud_mime_fake/assets/102328295/cdd2a42a-a40a-4c01-b3de-64f1299c2f40">
### Demo
![mime_faker](https://github.com/oblomov-dev/a2UI5_cloud_mime_fake/assets/102328295/2a30f523-9c2b-46be-89d1-516836ba7e2b)

## Approach II
Store Files in a z-table. No tranportation as a development object possible.
