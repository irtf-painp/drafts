---

stand_alone: yes
pi:
  rfcedstyle: yes
  toc: yes
  tocindent: yes
  tocdepth: 4
  sortrefs: yes
  symrefs: yes
  strict: yes
  comments: yes
  inline: yes
  text-list-symbols: o-*+
  compact: yes
  subcompact: no

title: Traffic Matrices File Format
abbrev: Traffic Matrices
docname: draft-ietf-kepner-traffic-matrices-latest
category: info

ipr: trust200902
area: "Internet Area (INT)"
workgroup: "Individual"

stream: IETF
keyword: Internet-Draft
consensus: true

venue:
  group: "Network Working Group"
  type: "Working Group"
  mail: "painp@mit.edu"
  arch: "https://mailman.mit.edu/pipermail/painp/"
  github: "irtf-painp/drafts"
  latest: "https://github.com/irtf-painp/drafts/blob/main/draft-kepner-traffic-matrices.md"

author:
  -
    ins: J. Kepner
    name: Jeremy Kepner
    organization: MIT
    email: kepner@ll.mit.edu
  -
    ins: M. Satterfield
    name: Martin Satterfield
    organization: U. Alabama
    email: kepner@ll.mit.edu


informative:
  Houle2024:
    author:
    - ins: M. Houle
    - ins: M. Jones
    - ins: D. Wallmeyer
    - ins: R. Brodeur
    - ins: J. Burr
    - ins: H. Jananthan
    - ins: S. Merrell
    - ins: P. Michaleas
    - ins: A. Perez
    - ins: A. Prout
    - ins: J. Kepner
    date: September 2024
    target: https://arxiv.org/abs/2409.12297
    title: Hypersparse traffic matrices from Suricata network flows using GraphBLAS



normative:
  NIST:
    author:
    - ins: Katerina Megas
    - ins: Barbara Cuthill
    - ins: Marissa Dotter
    - ins: Michael Garris
    - ins: Ishika Khemani
    - ins: Bronwyn Patrick
    - ins: Noah Schiro
    - ins: Julie Nethery Snyder
    - ins: Mohammad Zarei
    date: December 2025
    target: https://nvlpubs.nist.gov/nistpubs/ir/2025/NIST.IR.8596.iprd.pdf
    title: Cybersecurity Framework Profile for Artificial Intelligence (NIST IR 8596 iprd)


--- abstract

This document proposes a standard format for traffic matrices for data corresponding to the layers of the Internet architecture. Traffic matrices are highly adaptable and sources/destinations can be any combination of physical, logical, persona, and/or AI agent endpoints.


--- middle

# Introduction

{: #introduction-doc}

Modern networks generate traffic at a scale and speed that make large-scale long-duration packet-level capture and analysis challenging. While network flow data reduces overall data volume, analyzing large numbers of flows across extended time periods and across an entire network remains computationally expensive. As a result, security teams often struggle to identify subtle but important behaviors, such as distributed scanning, slow data exfiltration, and gradual deviations from normal traffic patterns.


In all domains protection requires observing the domain and analyzing the observations. Effective cyber domain observation and analysis must be done with the highest regard for privacy. In the broader networking community anonymized source-to-destination traffic matrices with standard data sharing agreements have emerged as one approach to meeting many of these requirements. Traffic matrices are highly adaptable and sources/destinations can be any combination of physical, logical, persona, and/or AI agent endpoints. 

With increasing numbers of Artificial Intelligence (AI) systems and AI-based agents coming online, there is an increased usage of AI technology for cyberattacks against many enterprise organizations. As such, there is an urgent need to utilize AI technology also for cyber-defense against these new forms of cyberattacks [NIST].

A core component to the new cyber-defense AI profile is the speed at which network-related data can be made available to AI cyber-defense systems within an enterprise. A standard format for traffic matrices produces by network devices (e.g., routers), network elements (e.g. VPNs) and higher-layer functions of the enterprise (e.g., AI Agents) enables the enterprise AI systems dedicated to cyber-defense to process the data in the traffic matrices at a higher speed and efficiency.  




# Terminology

{: #terminology-sect}

The following are some terminology used in the current document:

- PCAP: (definition here).

- Traffic matrix: (definition here).



# Background

{: #background-sect}

Rapid analysis of network traffic there requires condensed representations that retain the necessary information but also allow for anonymization when needed.


## Data from Network and Transport Layers

{: #network-transport-data}

Analysis on data from the Network Layer typically utilizes IP addresses as explicit endpoint identifiers to determine source and destination hosts within network communications, with packet counts serving as a common quantitative metric for characterizing communication patterns and network activity.
This IP-based approach can be expended by incorporating information on the Transport Layer, demonstrating that the combination of IP addresses and port numbers provides a more detailed representation of communication endpoints by identifying both the host and the associated application-level service.
Across both layers, packet count was used as the measurement parameter for analyzing network behavior. Thus, a useful approach is to define source and destination endpoints using IP address pairs at the Network Layer and IP address–port number combinations at the Transport Layer. Packet counts can be extracted from PCAP [PCAP] files to quantify communication activity.


## Data from the Application Layer

{: #application-data}

Analytics on data at the application layer typically focus on HTTP-related data because of its ease of identification within PCAP files. For this layer, the source is defined as the device initiating the request, while the destination is represented by the corresponding web address or DNS-resolved endpoint. The counting parameter is defined as the complete transaction between the client device and the server, providing a measure of Application Layer communication activity.


## Data from the AI Layer

{: #AI-layer-data}

With the emergence of Agent-to-Agent interactions protocols (e.g. Model Context Protocol (MCP)), a new layer of data has emerged at (or above) the Application Layer. We refer to this new level as the AI Layer, which includes interactions data (prompts and responses) from Human-AI interactions as well as Agent-to-Agent interactions.



# Matrix Generator Architecture

{: #matrix-generator-sect}

Here is the text. (The figure is a placeholder, and will be replaced).


~~~
      +------------+
      | Exporter’s |  +----------+              +---------------------+
      |    Bank    |  | Exporter |              |       Exporter      |
      +------------+  +----------+              +---------------------+
            | |            |                       | |              |
       3    | |    5       |    4           1      | |      2       |   4
    Approve | | Request    | Upload       Book     | |   Create     | Accept
      L/C   | | Payment    |   B/L     Consignment | | Consignment  |  B/L
            | |            |                       | |              |
            V V            V                       V V              V
    +-------------------------------+     +-------------------------------+
    |     Trade Finance Network     |     |    Trade Logistics Network    |
    +-------------------------------+     +-------------------------------+
            ˄              ˄                           ˄     ˄
       2    |              |    1               5      |     |    3
    Propose |              | Request        Dispatch   |     | Upload
      L/C   |              |   L/C         Consignment |     |   B/L
            |              |                           |     |
      +------------+  +----------+                 +-------------+
      | Importer’s |  | Importer |                 |   Carrier   |
      |    Bank    |  +----------+                 +-------------+
      +------------+
                   (a)                                   (b)
~~~
{: #matrix-gen-figure}



# Security Considerations

{: #security-consider}



# IANA Considerations

{: #iana-consider}

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}


We thank the following for contributions: (list here).


