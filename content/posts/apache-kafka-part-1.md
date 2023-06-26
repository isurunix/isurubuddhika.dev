---
title: "Apache Kafka Series : Introduction to Apache Kafka"
date: 2023-02-20T01:07:47+05:30
draft: false
series: 
- Apache kafka
tags: 
- Apache Kafka
- Event Streaming
- Distrubuted Computing
- Programming
categories:
- Programming
showShareButtons: true
showBreadcrumbs: true
---

I recently had the chance to start working with Apache Kafka as a part of a new module I'm working on at my workplace.
So this is just me noting down my thoughts about my experience with Kafka as a series of articles. 

## What is Apache Kafka?

**Apache Kafka** is a popular distributed event processing or event streaming platform. Kafka contains three main capabilities under the hood, 
which we can use for our event streaming workloads.
These capabilities are,
1. Ability to **publish** (write) and **subscribe** (read) to event streams.
2. Ability to **store** event streams reliably and durably for a configured amount of time.
3. Ability to **process** events as they occur or retrospectively.

Apart from that, what led to Kafka's popularity was it's highly-scalable, elastic, and fault-tolerant nature.

If you read up to this point, you would probably have the question of what the hell is Event Streaming in your head unless you have heard about it before.
So let's have a quick look into that before going any further.

## What is Event Streaming?

To put it simply, think of a system continuously generating data. Each of these data points is considered an event, 
and when we capture those events as a continuous stream of events, it's called an event stream.  

Capturing and storing these event streams durably for later retrieval; manipulating, processing, 
and reacting to the event streams in real-time as well as retrospectively; 
and routing the event streams to different destination technologies as required is known as event streaming.

## Why Apache Kafka or Event Streaming/Processing

So now we know what is Apache Kafka and what is Event Streaming/Processing is. Let's now try to digest why do we need such things.
We are all aware that purpose of most applications we develop is to recive some data, process them according given set of rules and provide
a response or not. So let's see how does Kafka fits into this.

As of today most of the applications we use rely on REST APIs for communication. REST provide us a way to talk to these applications over HTTP
and it happens mostly in 3 steps. First a request is made and then the application processes that request. Then a response is sent back to the party
which made the request and then they act upon the received response. This scenario works for most of the situations out there. 

But think of an scenario where an application is producing 100s of events in a minute and we need these events to be processed by another application, or of
a scenario where multiple applications are doing different actions based on a data received from another application.
One key thing common to both scenarios is that data processing is not immediate and the system which ever is sending the data does not expect an
immediate response from the downstream systems. So a usual REST based communication between systems won't work for such scenarios since REST is
all about synchronous request and response. And in first scenario it would be a pain to scale the application with growing number of events.
So it's clear that for cases like this we need a new way of doing thigs.
This is where Kafka or in general event streaming and processing comes in. Kafka provides us a reliable location to write our data (events) and means for
other applications to read and process these data asynchronously without having tight coupling between them.

So now we have an general idea about what is Kafka and why we need it. Let's dive into more details about Kafka with the next article from this sereis.
See you next time. 

