# Generating XML DTD File From [TVSchedule.xml](https://github.com/kmjenniferng/xml_dtd/blob/main/TVSchedule.xml) file


The purpose of this project is to generate XML DTD file based on the data inside TVSchedule.xml file

### 1. TVSchedule.xml
In order to construct the XML DTD file, we have to understand the structure of xml file first.

As we see from the following xml file structure, **TVSCHEDULE** is the root with attribute **NAME**. 

Under **TVSCHEDULE**, there are more than one **CHANNEL** as children with attribute **CHAN**.

For each **CHANNEL**, there are **BANNDER** and more than one **DAY**.

For each **DAY**, there are **DATE** and more than one **PROGRAMSLOT**.

For each **PROGRAMSLOT**, there are **TITLE** with two attributes **LANGUAGE** and **RATING**, **TIME** and **DESCRIPTION** where **DESCRIPTION** is optional.

```
<TVSCHEDULE NAME="XXX">
<CHANNEL CHAN="XXX">
<BANNER>XXX</BANNER>
<DAY>
  <DATE>XXX</DATE>
  <PROGRAMSLOT>
    <TITLE LANGUAGE="XXX">XXX</TITLE>
    <TIME>XXX</TIME>
    <DESCRIPTION>XXX</DESCRIPTION>
  </PROGRAMSLOT>
  <PROGRAMSLOT>
    <TITLE RATING="XXX">XXX</TITLE>
    <TIME>XXX</TIME>    
  </PROGRAMSLOT>    
</DAY>
<DAY> ... </DAY>
<DAY> ... </DAY>
</CHANNEL>

<CHANNEL CHAN="XXX"> ... </CHANNEL>
</TVSCHEDULE>
```

### 2. [TVScheduleDTD.dtd](https://github.com/kmjenniferng/xml_dtd/blob/main/TVScheduleDTD.dtd)
Based on the above analysis, we can construct XML DTD file as the following.

```
<!DOCTYPE TVSCHEDULE [

<!ELEMENT TVSCHEDULE (CHANNEL+)>
<!ELEMENT CHANNEL (BANNER, DAY+)>
<!ELEMENT BANNER (#PCDATA)>
<!ELEMENT DAY (DATE, PROGRAMSLOT+)>
<!ELEMENT DATE (#PCDATA)>
<!ELEMENT PROGRAMSLOT (TIME, TITLE, DESCRIPTION?)>
<!ELEMENT TIME (#PCDATA)>
<!ELEMENT TITLE (#PCDATA)>
<!ELEMENT DESCRIPTION (#PCDATA)>

<!ATTLIST TVSCHEDULE NAME CDATA #REQUIRED>
<!ATTLIST CHANNEL CHAN CDATA #REQUIRED>
<!ATTLIST TITLE LANGUAGE CDATA #IMPLIED>
<!ATTLIST TITLE RATING CDATA #IMPLIED>
]>
```
