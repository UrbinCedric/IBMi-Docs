# Introduction to DDS


DDS stands for **Data Description Specification** and it is used to describe a data file format.
Before SQL became a first class citizen on IBMi, DDS was the method you would use to setup physical files (tables) and logical files (views/indexes).
In more modern development, **Data Definition Language** (SQL) is the primary method of setting up tables, views, and indexes.

The fascinating part about DDS is that it isn't just used for describing a database object. DDS can be used to drive printing formats and screen displays.


## Overview of DDS Types
A brief overview of DDS types, each of these will be described in more detail in separate sections.

| Attribute | Name          | Description                                          | Comparison        |
| --------- | ------------- | ---------------------------------------------------- | ----------------- |
| PF        | Physical File | Describe a data format for persisting data           | SQL table         |
| LF        | Logical File  | Describe a record selection from a physical file     | SQL view or index |
| DSPF      | Display File  | Describe a screen display. A frontend for a program. | GUI (Java Swing, Windows Forms) or HTML (kind of) |
| PRTF      | Printer File  | Describe a print layout for a report/document.       | Building a PDF ?  |
| ICFF      | Intersystem Communications Function (ICF) File | Describe data format for I/O with communication devices. | ? |


## Making a DDS Source Member
For a simple example, we will make a physical file with DDS. This method will apply to all DDS types.
For DDS source members, we need a new source physical file. Run the command ```CRTSRCPF```

By convention, the new source physical file will be named **QDDSSRC**.


<figure align="center">
  <img src="./core/dds/_assets/dds-01.png" alt="CRTSRCPF"/>
</figure>
<br>

Next we're going to create a new DDS source member. Run ```WRKMBRPDM BOLIB/QDDSSRC```, **F6 (create)**
<figure align="center">
  <img src="./core/dds/_assets/dds-02.png" alt="DDS Source member"/>
</figure>
<br>

Now we're back in good ole SEU. I will be going more into this in the next sections, so don't worry about doing anything with this now.
<figure align="center">
  <img src="./core/dds/_assets/dds-03.png" alt="SEU"/>
</figure>
<br>


## IBM Documentation
In the next few sections, there will be some links included to various IBM documentation for more detailed explanations.

* DDS Concepts - https://www.ibm.com/support/knowledgecenter/ssw_ibm_i_73/dds/kickoff.htm