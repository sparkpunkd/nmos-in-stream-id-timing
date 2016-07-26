# **[Work in progress]** In-stream Signaling of Identity and Timing information for RTP streams

## Two-byte headers proposal

The repository is a fork of the NMOS RTP streams specification and is a proposal to change the way headers are carried in the streams. Specifically, headers are text strings containing a key and a value, just like for  Although the proposal shares many of the same issues that the one-byte version does - that RTP header extensions are not appropriate for core metadata about the payload - this proposal is as least as pragmatic. If the designers of RTP, RFC4175 and RFC3190 had had the NMOS/JT-NM professional media requirements for timing and identity, they would not have designed the payloads and structures we are sitting on. Either we redefine the base standards ... to use PTP timestamps and UUIDs in RTP headers ... or we use header extensions not quite as intended ... or we use a different protocol? 

This proposal has the following advantages:

* Streams are self-describing to the point they can be decoded. No need for external SDP as the MIME type is carried. Still works with SDP if you want.
* No need to de-reference an external schema to find out the local identifier indexes and not limited by the 4-bit length fields of one-byte headers.
* Grain metadata is carried within the stream, and in a form that will carry over well to other transport mappings in the future.
* No need to define a new RFC - as arguably compatible with RFC 3350 / RFC4175 / RFC3190 / RFC5285 as the current work-in-progress-spec.
* Extendible headers that can be used for use cases taht we haven't thought of yet and/or for vendor/user specific workflows.
* Human readable in network analysers without extension.
* Carried within the same stream - no need to coordinate two separate streams to start processing or reference an external service.

The trade off is longer headers, which some may worry about, but the value of headers is widely accepted and other optimisations, such as HTTP2, are using compression to facilitate more efficient carriage.

This repository contains details of AMWA's Specification for signaling Source and Flow identifiers and Grain timestamps within streams.

The current specification is applicable to RTP streams using any payload format, via the use of RTP header extensions. Mapping of Grain attributes to transport types other than RTP may be specified in later revisions.

## Getting started

Readers are advised to be familiar with the NMOS Technical Overview at (https://github.com/AMWA-TV/nmos) and then read [specifications/IdentityTimingRTP.txt](specifications/IdentityTimingRTP.txt) in this repository.

## Contents
* README.md -- this file
* [specifications/IdentityTimingRTP.txt](specifications/IdentityTimingRTP.txt) -- Specification for carriage of video, audio and time-related data Flows over RTP, including in-stream signalling of identity and timing using RTP header extensions.
* [examples/sdp](examples/sdp) -- Supporting example SDP files
* [examples/pcap](examples/pcap) -- Supporting example Wireshark packet capture files
* [software/wireshark_plugins](software/wireshark_plugins) -- Wireshark plugin supporting parsing of in-stream RTP header extensions
* [LICENSE](LICENSE) -- Licenses for software and text documents
* [NOTICE](NOTICE) -- Disclaimer
