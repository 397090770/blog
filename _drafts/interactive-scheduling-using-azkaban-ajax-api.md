---
layout: post
title: "Interactive Scheduling using Azkaban - Part 2 : Understanding scheduling for the interactive big data workloads"
date : 2016-04-03
categories: scala azkaban
---
Every big data application needs some kind of scheduling to run daily jobs. So over the years having a good stable scheduling systems for hadoop, spark jobs has become more common place. The different workloads in big data needs different requirements from  the scheduler. So in this blog post I will be discussing about different scheduling requirements for batch, streaming and interactive usecases and how azkaban supports interactive use case better than other options out there.

This is second post in series of blogs where I will be discussing about using Azkaban scheduler to interactive scheduling. You can access all other posts from the series here.

## Scheduling needs of different big data workloads

In big data, primarily we have the following three kinds of work loads

* ### Batch
Set of jobs which needs to be executed on timely manner. In this scenario, a workflow system allow user to define the script ones with all the dependencies of a flow and allow it to be scheduled. To add/modify the jobs user will normally changes the script and runs the updated ones. The examples for these kind of systems are Ozzie, airflow etc

* ### Streaming
Continuous stream of data is processed to produce results. Normally streaming doesnot need any kind of scheduling as stream processor like spark streaming itself takes care of it.

The above two scenarios are one of most supported and common place in big data world from quite sometime. So all the scheduling system, including azkaban, supports them well. But there is a new workload emerging these days which needs special attention.

## Interactive big data workload

As spark became popular, it has made interactive programming one of the important part of big data workloads. In interactive settings, a user will be analyzing the data adhoc  and once he/she is happy with the steps then they want to schedule them to run in timely manner.

The notebook systems like Zeppelin,Jupiter have made interactive programming highly popular. Initially used for the data science use cases, they are also used for data engineering use cases.

So as interactive workloads becoming common place, supporting ability to scheduling jobs interactively becoming more and more important. But doing this with existing systems is not easy.

## Challenges of scheduling Interactive Scheduling

Unlike batch workloads, interactive workloads are not static. They evolve as user adds/removes the code. Normally user may want to add / remove scheduling on the fly rather than modifying the script. So the non azkaban frameworks cannot be used for following reasons

* ### No/Limited REST API support

Most of the scheduling systems like oozie have very limited support for programmatic access. Often they rely upon the traditional scripting world, where you need to configure jobs using script and submit them. It works great for batch, but cannot be used for interactive applications as they need an good programmatic API to schedule jobs.

* ### Lack of good UI

Most of the scheduling system have very limited UI's. Most of them limit themselves to show work flow graphs. Also many of them doesn't allow users to extend the user interfaces which results in building the custom ones themselves.

In batch, normally user interface is not that important. But in interactive it plays a huge role. Ability to monitor the jobs in a small time frame is important as it results in good user feed back.

* ### Support for different executors

Many scheduling systems limit themselves for Hadoop or Spark. But in interactive application one often likes to run different kind of processing on same system. So ability to run different workloads becomes extremely important.

So from above points it's clear that the most of the existing scheduler systems are geared towards the batch processing scenarios. So using them in a interactive application is hard.

## Azkaban for batch workload

Though my blog posts are focusing on using azkaban for interactive workloads, azkaban fares well in the batch also. Even most of it's documentation is dedicated to do batch scheduling using it's web UI rather than for interactive workloads. But with it's hidden gem of REST API, it's well suited for the interactive applications too.

So in this blogpost, we have looked at the different requirements of big data workloads for a scheduling system. In the next blogpost, we are going to discuss how azkaban solves these issues and is good candidate scheduler framework interactive workloads. 






