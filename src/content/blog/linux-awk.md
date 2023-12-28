---
title: Linux AWK
description: My notes on Linux AWK command.
pubDatetime: 2023-12-28T17:26:07+05:30
postSlug: linux-awk
featured: false
draft: false
tags:
  - Linux
---

![tp.web.random_picture](https://images.unsplash.com/photo-1683009427500-71296178737f?crop=entropy&cs=tinysrgb&fit=crop&fm=jpg&h=300&ixid=MnwxfDB8MXxyYW5kb218MHx8dHJlZSxsYW5kc2NhcGUsd2F0ZXIsbW91bnRhaW58fHx8fHwxNzAyMjYzOTE3&ixlib=rb-4.0.3&q=80&utm_campaign=api-credit&utm_medium=referral&utm_source=unsplash_source&w=900)

My notes on Linux AWK command.

## Table of contents

## Introduction

AWK is a utility that enables programmers to write tiny programs in the form of statements for pattern searching and processing.

It is a handy tool to extract a particular line / range of lines, get count of some text occurrences from a file / log file.

**AWK requires the data to be delimited or formatted `csv`, `tsv` files.**

Let's say, we want to extract the 2<sup>nd</sup> line from the following sample log file. We can do that using `head` command.

```shell
head -n 2 app.log
```

This will output the first 2 lines.

```
03/22 08:53:22 TRACE  :.....rsvp_event: received event from RAW-IP on interface 9.67.116.98
03/22 08:53:22 TRACE  :......rsvp_explode_packet: v=1,flg=0,type=2,cksm=54875,ttl=255,rsv=0,len=84
```

Easy, right? But what if we just want date & time column values from the file? That's where `AWK` shines. It lets you extract information by rows and columns.

## AWK Commands

```shell
# AWK logic is written inside ''.
awk '' app.log
```

### Print File

```shell
# Prints entire `app.log` file
awk '{print}' app.log
```

### Print Columns

```shell
# Prints 1st col
awk '{print $1}' app.log

# Prints 1st, 2nd, 3rd, and 5th col
awk '{print $1,$2,$3,$5}' app.log
```

### Filter Columns

Supply your filter query inside double-slashes `//` followed by your `awk` operation.

```shell
# Filter INFO level logs and dump it inside `only_info.log` file.
awk '/INFO/ {print $1,$2,$3,$5}' app.log > only_info.log
```

```only_info.log
03/22 08:53:22 INFO obj
03/22 08:53:22 INFO state
03/22 08:53:22 INFO Ioctl
03/22 08:53:22 INFO state
03/22 08:53:38 INFO Ioctl
03/22 08:53:38 INFO state
03/22 08:53:52 INFO obj
03/22 08:53:52 INFO state
03/22 08:53:53 INFO Ioctl
03/22 08:53:53 INFO state
03/22 08:54:09 INFO Ioctl
03/22 08:54:09 INFO state
03/22 08:54:22 INFO obj
03/22 08:54:22 INFO state
03/22 08:54:24 INFO Ioctl
03/22 08:54:24 INFO state
```

### Occurrences

Let's say we want to find number of occurrences of the `INFO` logs.

```shell
awk '/INFO/ {count++} END {print "Total occurrences: ", count}' app.log

# Output
# Total occurrences: 16
```

Here, `END` keyword marks the end of the first query that is total count of `INFO` keyword.

**Worth noting, the `count` is a variable not an `awk` keyword. You can use any other variable name there.** The following command will produce same result.

```shell
awk '/INFO/ {i++} END {print "Total occurrences: ", i}' app.log

# Output
# Total occurrences: 16
```

### Query by timestamp

Let's find logs generated between `08:53:00` and `08:53:40`. Since, the `timestamp` column is 2<sup>nd</sup> in the `app.log` file we have queried on column 2 (`$2`).

```shell
awk '$2 >= "08:53:00" && $2 <= "08:53:40" {print $2,$3,$4}' app.log
```

```
08:53:22 TRACE :.....rsvp_event:
08:53:22 TRACE :......rsvp_explode_packet:
08:53:22 TRACE :.......rsvp_parse_objects:
08:53:22 INFO :.......rsvp_parse_objects:
08:53:22 TRACE :......rsvp_event_mapSession:
08:53:22 INFO :.......rsvp_flow_stateMachine:
08:53:22 TRACE :........flow_timer_stop:
08:53:22 TRACE :........flow_timer_start:
08:53:22 TRACE :.......rsvp_flow_stateMachine:
08:53:22 EVENT :..mailslot_sitter:
08:53:22 TRACE :.....event_timerT1_expire:
08:53:22 INFO :......router_forward_getOI:
08:53:22 TRACE :......router_forward_getOI:
08:53:22 TRACE :......router_forward_getOI:
08:53:22 TRACE :......router_forward_getOI:
08:53:22 TRACE :......router_forward_getOI:
08:53:22 INFO :......rsvp_flow_stateMachine:
08:53:22 TRACE :.......rsvp_action_nHop:
08:53:22 TRACE :.......flow_timer_start:
08:53:22 TRACE :......rsvp_flow_stateMachine:
08:53:22 TRACE :.......mailslot_send:
08:53:38 EVENT :..mailslot_sitter:
08:53:38 TRACE :.....event_timerT1_expire:
08:53:38 INFO :......router_forward_getOI:
08:53:38 TRACE :......router_forward_getOI:
08:53:38 TRACE :......router_forward_getOI:
08:53:38 TRACE :......router_forward_getOI:
08:53:38 TRACE :......router_forward_getOI:
08:53:38 INFO :......rsvp_flow_stateMachine:
08:53:38 TRACE :.......rsvp_action_nHop:
08:53:38 TRACE :.......flow_timer_start:
08:53:38 TRACE :......rsvp_flow_stateMachine:
08:53:38 TRACE :.......mailslot_send:
```

### Extract row range

Let's find logs from 2<sup>nd</sup> to 4<sup>th</sup> lines.

```shell
awk 'NR >=2 && NR <= 4 {print}' app.log
```

```
03/22 08:53:22 TRACE  :......rsvp_explode_packet: v=1,flg=0,type=2,cksm=54875,ttl=255,rsv=0,len=84
03/22 08:53:22 TRACE  :.......rsvp_parse_objects: STYLE is WF
03/22 08:53:22 INFO   :.......rsvp_parse_objects: obj RSVP_HOP hop=9.67.116.99, lih=0
```

## Sample Log File

Source: [IBM Sample Log File](https://www.ibm.com/docs/en/zos/2.4.0?topic=problems-example-log-file)

```plaintext-ibm
03/22 08:53:22 TRACE  :.....rsvp_event: received event from RAW-IP on interface 9.67.116.98
03/22 08:53:22 TRACE  :......rsvp_explode_packet: v=1,flg=0,type=2,cksm=54875,ttl=255,rsv=0,len=84
03/22 08:53:22 TRACE  :.......rsvp_parse_objects: STYLE is WF
03/22 08:53:22 INFO   :.......rsvp_parse_objects: obj RSVP_HOP hop=9.67.116.99, lih=0
03/22 08:53:22 TRACE  :......rsvp_event_mapSession: Session=9.67.116.99:1047:6 exists
03/22 08:53:22 INFO   :.......rsvp_flow_stateMachine: state RESVED, event RESV
03/22 08:53:22 TRACE  :........flow_timer_stop: Stop T4
03/22 08:53:22 TRACE  :........flow_timer_start: Start T4
03/22 08:53:22 TRACE  :.......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:53:22 EVENT  :..mailslot_sitter: process received signal SIGALRM
03/22 08:53:22 TRACE  :.....event_timerT1_expire: T1 expired
03/22 08:53:22 INFO   :......router_forward_getOI: Ioctl to query route entry successful
03/22 08:53:22 TRACE  :......router_forward_getOI:         source address:   9.67.116.98
03/22 08:53:22 TRACE  :......router_forward_getOI:         out inf:   9.67.116.98
03/22 08:53:22 TRACE  :......router_forward_getOI:         gateway:   0.0.0.0
03/22 08:53:22 TRACE  :......router_forward_getOI:         route handle:   7f5251c8
03/22 08:53:22 INFO   :......rsvp_flow_stateMachine: state RESVED, event T1OUT
03/22 08:53:22 TRACE  :.......rsvp_action_nHop: constructing a PATH
03/22 08:53:22 TRACE  :.......flow_timer_start: started T1
03/22 08:53:22 TRACE  :......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:53:22 TRACE  :.......mailslot_send: sending to (9.67.116.99:0)
03/22 08:53:38 EVENT  :..mailslot_sitter: process received signal SIGALRM
03/22 08:53:38 TRACE  :.....event_timerT1_expire: T1 expired
03/22 08:53:38 INFO   :......router_forward_getOI: Ioctl to query route entry successful
03/22 08:53:38 TRACE  :......router_forward_getOI:         source address:   9.67.116.98
03/22 08:53:38 TRACE  :......router_forward_getOI:         out inf:   9.67.116.98
03/22 08:53:38 TRACE  :......router_forward_getOI:         gateway:   0.0.0.0
03/22 08:53:38 TRACE  :......router_forward_getOI:         route handle:   7f5251c8
03/22 08:53:38 INFO   :......rsvp_flow_stateMachine: state RESVED, event T1OUT
03/22 08:53:38 TRACE  :.......rsvp_action_nHop: constructing a PATH
03/22 08:53:38 TRACE  :.......flow_timer_start: started T1
03/22 08:53:38 TRACE  :......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:53:38 TRACE  :.......mailslot_send: sending to (9.67.116.99:0)
03/22 08:53:52 TRACE  :.....rsvp_event: received event from RAW-IP on interface 9.67.116.98
03/22 08:53:52 TRACE  :......rsvp_explode_packet: v=1,flg=0,type=2,cksm=54875,ttl=255,rsv=0,len=84
03/22 08:53:52 TRACE  :.......rsvp_parse_objects: STYLE is WF
03/22 08:53:52 INFO   :.......rsvp_parse_objects: obj RSVP_HOP hop=9.67.116.99, lih=0
03/22 08:53:52 TRACE  :......rsvp_event_mapSession: Session=9.67.116.99:1047:6 exists
03/22 08:53:52 INFO   :.......rsvp_flow_stateMachine: state RESVED, event RESV
03/22 08:53:52 TRACE  :........flow_timer_stop: Stop T4
03/22 08:53:52 TRACE  :........flow_timer_start: Start T4
03/22 08:53:52 TRACE  :.......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:53:53 EVENT  :..mailslot_sitter: process received signal SIGALRM
03/22 08:53:53 TRACE  :.....event_timerT1_expire: T1 expired
03/22 08:53:53 INFO   :......router_forward_getOI: Ioctl to query route entry successful
03/22 08:53:53 TRACE  :......router_forward_getOI:         source address:   9.67.116.98
03/22 08:53:53 TRACE  :......router_forward_getOI:         out inf:   9.67.116.98
03/22 08:53:53 TRACE  :......router_forward_getOI:         gateway:   0.0.0.0
03/22 08:53:53 TRACE  :......router_forward_getOI:         route handle:   7f5251c8
03/22 08:53:53 INFO   :......rsvp_flow_stateMachine: state RESVED, event T1OUT
03/22 08:53:53 TRACE  :.......rsvp_action_nHop: constructing a PATH
03/22 08:53:53 TRACE  :.......flow_timer_start: started T1
03/22 08:53:53 TRACE  :......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:53:53 TRACE  :.......mailslot_send: sending to (9.67.116.99:0)
03/22 08:54:09 EVENT  :..mailslot_sitter: process received signal SIGALRM
03/22 08:54:09 TRACE  :.....event_timerT1_expire: T1 expired
03/22 08:54:09 INFO   :......router_forward_getOI: Ioctl to query route entry successful
03/22 08:54:09 TRACE  :......router_forward_getOI:         source address:   9.67.116.98
03/22 08:54:09 TRACE  :......router_forward_getOI:         out inf:   9.67.116.98
03/22 08:54:09 TRACE  :......router_forward_getOI:         gateway:   0.0.0.0
03/22 08:54:09 TRACE  :......router_forward_getOI:         route handle:   7f5251c8
03/22 08:54:09 INFO   :......rsvp_flow_stateMachine: state RESVED, event T1OUT
03/22 08:54:09 TRACE  :.......rsvp_action_nHop: constructing a PATH
03/22 08:54:09 TRACE  :.......flow_timer_start: started T1
03/22 08:54:09 TRACE  :......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:54:09 TRACE  :.......mailslot_send: sending to (9.67.116.99:0)
03/22 08:54:22 TRACE  :.....rsvp_event: received event from RAW-IP on interface 9.67.116.98
03/22 08:54:22 TRACE  :......rsvp_explode_packet: v=1,flg=0,type=2,cksm=54875,ttl=255,rsv=0,len=84
03/22 08:54:22 TRACE  :.......rsvp_parse_objects: STYLE is WF
03/22 08:54:22 INFO   :.......rsvp_parse_objects: obj RSVP_HOP hop=9.67.116.99, lih=0
03/22 08:54:22 TRACE  :......rsvp_event_mapSession: Session=9.67.116.99:1047:6 exists
03/22 08:54:22 INFO   :.......rsvp_flow_stateMachine: state RESVED, event RESV
03/22 08:54:22 TRACE  :........flow_timer_stop: Stop T4
03/22 08:54:22 TRACE  :........flow_timer_start: Start T4
03/22 08:54:22 TRACE  :.......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:54:24 EVENT  :..mailslot_sitter: process received signal SIGALRM
03/22 08:54:24 TRACE  :.....event_timerT1_expire: T1 expired
03/22 08:54:24 INFO   :......router_forward_getOI: Ioctl to query route entry successful
03/22 08:54:24 TRACE  :......router_forward_getOI:         source address:   9.67.116.98
03/22 08:54:24 TRACE  :......router_forward_getOI:         out inf:   9.67.116.98
03/22 08:54:24 TRACE  :......router_forward_getOI:         gateway:   0.0.0.0
03/22 08:54:24 TRACE  :......router_forward_getOI:         route handle:   7f5251c8
03/22 08:54:24 INFO   :......rsvp_flow_stateMachine: state RESVED, event T1OUT
03/22 08:54:24 TRACE  :.......rsvp_action_nHop: constructing a PATH
03/22 08:54:24 TRACE  :.......flow_timer_start: started T1
03/22 08:54:24 TRACE  :......rsvp_flow_stateMachine: reentering state RESVED
03/22 08:54:24 TRACE  :.......mailslot_send: sending to (9.67.116.99:0)
03/22 08:54:35 TRACE  :......rsvp_event_mapSession: Session=9.6
```

## References

- [Linux AWK vs SED vs GREP - YouTube Tutorial in Hindi by Train With Shubham](https://youtu.be/SJTJVb5w45E)
