
This section defines the actors and transactions in this implementation guide.

Figure 1.1-1 below shows the actors directly
involved in the SANER
Profile and the relevant transactions between them.



![Figure 3-1: SANER Actor Diagram](ActorsAndTransactions.svg "Figure 3-1: SANER Actor Diagram")

**Figure 3-1: SANER Actor Diagram**

Table 3-1 lists the transactions for each actor directly involved in the SANER Implementation Guide. To claim compliance with this guide, an actor shall
support all required transactions (labeled "R") and may support the
optional transactions (labeled "O").


<table border="1" borderspacing="0" style='border: 1px solid black; border-collapse: collapse'>
<caption>
<b>
Table 3-1: SANER Implementation Guide - Actors and Transactions
</b>
</caption>
<thead>
<tr class="odd" style='background: gray;'>
<th>Actors</th>
<th>Transactions</th>
<th>Optionality</th>
</tr>
</thead>
<tbody>
                
<tr>
                        
<td rowspan="2">
<a href="#measure-source">Measure Source</a>
</td>
                        
<td>
<a href='transaction-1.html'>
                        Query Measure [PULL-TX]</a>
</td>
<td align='center'>
                        C

                                <sup> 1</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-2.html'>
                        Produce Measure [PUSH-TX]</a>
</td>
<td align='center'>
                        C

                                <sup> 2</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td rowspan="3">
<a href="#measure-consumer">Measure Consumer</a>
</td>
                        
<td>
<a href='transaction-3.html'>
                        Communicate Results [REPORT-TX]</a>
</td>
<td align='center'>
                        R
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-1.html'>
                        Query Measure [PULL-TX]</a>
</td>
<td align='center'>
                        C

                                <sup> 3</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-2.html'>
                        Produce Measure [PUSH-TX]</a>
</td>
<td align='center'>
                        C

                                <sup> 4</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td rowspan="5">
<a href="#measure-intermediary">Measure Intermediary</a>
</td>
                        
<td>
<a href='transaction-1.html'>
                        Query Measure [PULL-TX]</a><br/><i>As Measure Source</i>
</td>
<td align='center'>
                        C

                                <sup> 1</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-2.html'>
                        Produce Measure [PUSH-TX]</a><br/><i>As Measure Source</i>
</td>
<td align='center'>
                        C

                                <sup> 2</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-3.html'>
                        Communicate Results [REPORT-TX]</a><br/><i>As Measure Consumer</i>
</td>
<td align='center'>
                        R
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-1.html'>
                        Query Measure [PULL-TX]</a><br/><i>As Measure Consumer</i>
</td>
<td align='center'>
                        C

                                <sup> 3</sup>
                            
</td>
</tr>
                    
<tr>
                        
<td>
<a href='transaction-2.html'>
                        Produce Measure [PUSH-TX]</a><br/><i>As Measure Consumer</i>
</td>
<td align='center'>
                        C

                                <sup> 4</sup>
                            
</td>
</tr>
                    
</tbody>
</table>
        
        
**Notes:**

1. This transaction is required when the Measure Source implements the [Pull Option](#pull-option).

2. This transaction is required when the Measure Source implements the [Push Option](#push-option).

3. This transaction is required when the Measure Consumer implements the [Pull Option](#pull-option).

4. This transaction is required when the Measure Consumer implements the [Push Option](#push-option).

### Actors
The actors in this profile are described in more detail in the sections below.

#### Measure Source

The Measure Source Actor reports results for a single facility, collection of facilities or aggregated data for a region.



In a single facility, or organization, the Measure Source Actor will compile data directly from the facility
or organization source systems.

A Measure Source may also exist in an Aggregator, Intermediary or Bridging role.  In this guide we will use
the term Intermediary to describe these roles.

A Measure Source provides the FHIR data that is used by a Measure Consumer.



##### Measure Source Requirements
1. 1. 

#### Measure Consumer

The Measure Consumer provides access to aggregated or fine-grained
data gathered from one or more Measure Sources.
        



The Measure Consumer provides the ability to report on data from one or more Measure Sources.

In the case of a single facility or organization the Measure Consumer is reporting the data at aggregated
or varying levels of granularity using data extracted from a Measure Source.
        


##### Measure Consumer Requirements
1. 1. 

#### Measure Intermediary

The Measure Intermediary is a grouping of a Measure Source with a Measure Consumer.


This actor represents the composition of a [Measure Source](actors_and_transactions.html#measure-source) with a [Measure Source](actors_and_transactions.html#measure-source).

The Measure Intermediary role can aggregate data from multiple Measure Sources.  Data from Measure Sources may
be pulled in by the Intermediary, pushed to the Intermediary by the Measure Source, or may be pushed from a
Measure Source via a dump.

Using the Dump option with a Measure Intermediary provides a Push or Pull mechanism to transfer
non-FHIR data or FHIR bulk data.  The Measure Intermediary can then convert the dump data into FHIR data that can be
served up to Measure Consumers in a format that is compliant with the requirements of a Measure Source.

The Measure Intermediary may also provide the capabilities of a Measure Consumer to enable data to be
reported at an aggregated level.

The Measure Intermediary role may aggregate data from other Measure Intermediaries.  Since the Intermediary
is exposing a Measure Source capability this method allows data to be aggregated in a hierarchy such as:

    - Supporting multiple data inputs within a single facility to create a complete measure from multiple partial reports,
    - Enabling aggregation of data for Groups of hospitals in a health system, a hospital service area, or referral region,
    - Aggregating to county or state levels for local and regional Public Health agencies
    - Communicating aggregated data to National / Federal Agencies such as CDC or FEMA.


#### Bridging between Incompatible Options
In networking parlance, a Bridge is a system that connects between different protocols.  The different options in this Implementation Guide
can create incompatibilities, but these can be bridged by an Intermediary.

For example, a Measure Intermediary that implements the Dump and Pull Options in the Measure Consumer, that groups with a Measure Source
implementing the Push and API Options can bridge bridge between a Measure Source implementing the Dump and Push options to enable
communication with a Measure Consumer implementing the API and Push options.

![Bridge](Bridge.svg)

#### Measure Repository
A Measure Respository is simply a FHIR Server.  A FHIR Server that supports CRUD operations on MeasureReport and Measure effectively implements both the Measure Consumer with the API and Push Options
and the Measure Source actor implementing the Pull and API Options.

![FHIR Server](FHIRServer.svg)


        



### Actor Options

Options that may be selected for each actor in this guide, are listed in Table 3.2-1 below. Dependencies
between options when applicable are specified in notes.

<table border="1" style="border: 1px solid black; border-collapse: collapse">
    <caption><b>Table 3.2-1 Actor Options</b></caption>
    <thead>
        <tr style="background: gray;" class="odd">
            <td>Actor</td>
            <td>Option Name</td>
        </tr>
    </thead>
    <tbody>
        
                <tr>
                
                    <td rowspan='4'>Measure Source</td>
                
                <td><a href="#storage-option">Storage Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#api-option">API Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#push-option">Push Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#pull-option">Pull Option</a></td>
                </tr>
            
                <tr>
                
                    <td rowspan='4'>Measure Consumer</td>
                
                <td><a href="#storage-option">Storage Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#api-option">API Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#push-option">Push Option</a></td>
                </tr>
            
                <tr>
                
                <td><a href="#pull-option">Pull Option</a></td>
                </tr>
            
                <tr><td>Measure Intermediary</td>
                <td><i>No Options Defined</i></td></tr>
            
    </tbody>
</table>

        
The options in this guide are describe in more detail the sections below.

#### Storage Option

An actor implementing the Storage Option supports the ability to exchange FHIR Resources through
various means of simple data transfer, rather than directly through a FHIR API call. This include mechanisms such
as SFTP, S3 Blob Storage, Azure Blob Storage, a Message Queue, https: File Download, File System dumps, or Direct Messages with a
data payload. Supported formats include JSON, XML and NDJSON.
        

This option applies to the actors as described below.

##### Measure Source

A [Measure Source](actors_and_transactions.html#measure-source) actor implementing the Storage Option uses external storage to communicate data.


##### Measure Consumer

A [Measure Consumer](actors_and_transactions.html#measure-consumer) actor implementing the Storage Option uses external storage to communicate data.


#### API Option

An actor implementing the API Option supports the
ability to exchange FHIR Resources using [FHIR RESTful APIs](http://hl7.org/fhir/R4/http.html).

This option applies to the actors as described below.

##### Measure Source

An [Measure Source](actors_and_transactions.html#measure-source) actor implementing the API option uses FHIR RESTful APIs to communicate data.


##### Measure Consumer

An [Measure Consumer](actors_and_transactions.html#measure-consumer) actor implementing the API option uses FHIR RESTful APIs to communicate data.


#### Push Option

An actor implementing the Push Option supports the periodic push of resources
describing the current status of health delivery resources to a centralized collection point.
	    




This option applies to the actors as described below.

##### Measure Source

A Measure Source implementing the Push Option periodically sends updates to a
[Measure Consumer](actors_and_transactions.html#measure-consumer) using the [Produce Measure](actors_and_transactions.html#produce-measure) transaction.


##### Measure Consumer

An Measure Consumer implementing the Push Option periodically recieves updates from the
[Measure Source](actors_and_transactions.html#measure-source) using the [Produce Measure](actors_and_transactions.html#produce-measure) transaction.


#### Pull Option

An actor implementing the Pull Option supports the periodic pull resources
describing the current status of selected health delivery resources.




This option applies to the actors as described below.

##### Measure Source

A Measure Source implementing the Pull Option is periodically queried by an
[Measure Consumer](actors_and_transactions.html#measure-consumer) using the [Query Measure](actors_and_transactions.html#query-measure) transaction to enable collection of the current status.



##### Measure Consumer

An Measure Consumer implementing the Pull Option periodically queries a
[Measure Source](actors_and_transactions.html#measure-source) using the [Query Measure](actors_and_transactions.html#query-measure) transaction to enable collection of the current status.
            


### Transaction Descriptions
The transactions in this profile are summarized in the sections below.

#### Query Measure

The Query Measure transaction allows a Measure Consumer to
periodically query about the availability of a resource from an Measure Source.


For more details see the detailed [transaction description](transaction-1.html)

#### Produce Measure

The Produce Measure transaction allows an Measure Source to
periodically report on availability of resources to a Measure Consumer.


For more details see the detailed [transaction description](transaction-2.html)

#### Communicate Results

The Communicate Results transaction allows users (e.g., Public Health Officials) to view current resource availability,
or other systems to access resource availability data.


For more details see the detailed [transaction description](transaction-3.html)
