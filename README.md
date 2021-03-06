# Cinegy TS Analyzer Tool

Use this tool to view inbound network, RTP and TS packet details. Use newly introduced powers to view into the service description tables, and even decode a teletext stream!

New with V3 - now built with Net Core 3, using single-file-exe features with an integrated runtime, making deployment dependencies incredibly low! This also means that operation on Linux and MacOS are possible (although should be considered beta - it is not particularly tested).

Linux builds, for Intel/AMD 64-bit, and for Arm64, are now created by the AppVeyor build (tested on Ubuntu 16.04 / 18.04 and on RPi4 with 18.04 Arm64).

## How easy is it?

Well, we've added everything you need into a single EXE again, which holds the Net Core 3.1 runtime - so if you have the basics installed on a machine, you should be pretty much good to go. We gave it all a nice Apache license, so you can tinker and throw the tool wherever you need to on the planet.

Just run the EXE from inside a command-prompt, and you will be offered a basic interactive mode to get cracking checking out your stream.

From v1.3, you can check out a .TS file and scan through it - just drag / drop the .TS file onto the EXE!

You can print live Teletext decoding, and you can use the tool to generate input logs for 'big data' analysis (which is very cool).

## Command line arguments:

Double click, or just run without (or with incorrect) arguments, and you'll see this:

```
TsAnalyzer 3.0.198
Cinegy GmbH

ERROR(S):
  No verb selected.

  stream     Stream from the network.

  read       Read from a file.

  help       Display more information on a specific command.

  version    Display version information.

```

The help details for the 'stream' verb look like this:

```
c:\> tsanalyzer.exe  help stream      
                                                         
TsAnalyzer 3.0.198
Cinegy GmbH

  -m, --multicastaddress             Input multicast address to read from - if left blank, assumes unicast.

  -p, --port                         Required. Input UDP network port to read from.

  -a, --adapter                      IP address of the adapter to listen for multicasts (if not set, tries first binding adapter).

  -n, --nortpheaders                 (Default: false) Optional instruction to skip the expected 12 byte RTP headers (meaning plain MPEGTS inside UDP is expected

  -q, --quiet                        (Default: false) Don't print anything to the console

  -s, --skipdecodetransportstream    (Default: false) Optional instruction to skip decoding further TS and DVB data and metadata

  -c, --teletextdecode               (Default: false) Optional instruction to decode DVB teletext subtitles / captions from default program

  --programnumber                    Pick a specific program / service to inspect (otherwise picks default).

  -d, --descriptortags               (Default: ) Comma separated tag values added to all log entries for instance and machine identification

  -v, --verboselogging               Creates event logs for all discontinuities and skips.

  -t, --telemetry                    (Default: false) Enable telemetry to Cinegy Telemetry Server

  -o, --organization                 Tag all telemetry with this organization (needed to indentify and access telemetry from Cinegy Analytics portal

  --help                             Display this help screen.

  --version                          Display version information.


```

So - what does this look like when you point it at a complex live stream? Here is a shot from a UK DVB-T2 stream:

```
Network Details - rtp://@239.5.2.1:6670         Running: 00:00:22
---------------------------------------------------------------------
Total Packets Rcvd: 103514      Buffer Usage: 0.00%/(Peak: 0.27%)
Total Data (MB): 131            Packets per sec:4757
Period Max Packet Jitter (ms): 6
Bitrates (Mbps): 48.19/43.54/102.32/0.26 (Current/Avg/Peak/Low)

RTP Details - SSRC: 0
---------------------------------------------------------------------
Seq Num: 59290  Timestamp: 3987292082   Min Lost Pkts: 0
PCR Value: 08:52:49.2610044

PID Details - Unique PIDs: 62, (10 shown by packet count)
---------------------------------------------------------------------
TS PID: 8191    Packet Count: 279916            CC Error Count: 0
TS PID: 5700    Packet Count: 88463             CC Error Count: 0
TS PID: 5500    Packet Count: 87038             CC Error Count: 0
TS PID: 5600    Packet Count: 84393             CC Error Count: 0
TS PID: 5400    Packet Count: 43627             CC Error Count: 0
TS PID: 5300    Packet Count: 42413             CC Error Count: 0
TS PID: 2322    Packet Count: 21701             CC Error Count: 0
TS PID: 3847    Packet Count: 10128             CC Error Count: 0
TS PID: 2321    Packet Count: 7234              CC Error Count: 0
TS PID: 192     Packet Count: 5370              CC Error Count: 0

Service Information - Service Count: 10, (5 shown)
---------------------------------------------------------------------
Service 6912: BBC Two Wal HD (BSkyB) - H.264/AVC HD digital television service
Service 6940: BBC Two HD (BSkyB) - H.264/AVC HD digital television service
Service 6941: BBC One HD (BSkyB) - H.264/AVC HD digital television service
Service 6943: BBC One NI HD (BSkyB) - H.264/AVC HD digital television service
Service 6945: 6945 (BSkyB) - H.264/AVC HD digital television service

Elements - Selected Program: BBC Two Wal HD (ID:6912) (first 5 shown)
---------------------------------------------------------------------
PID: 5700 (H.264 video)
PID: 5703 (Teletext)
PID: 5704 (DVB Subtitles)
PID: 5701 (AC-3 / Dolby Digital)
PID: 2322 (MPEG-2 tabled data)

Teletext 888 (eng) - decoding Service ID 6912, PID: 5703, PTS: 2877230998
---------------------------------------------------------------------
Packets (Period/Total): 375/1608, Total Pages: 10, Total Clears: 9

20 -      If you're happy for us
22 - to deal with his master about...
```

Just to make your life easier, we auto-build this using AppVeyor - here is how we are doing right now: 

[![Build status](https://ci.appveyor.com/api/projects/status/08dqscip26lr0g1o/branch/master?svg=true)](https://ci.appveyor.com/project/cinegy/tsanalyser/branch/master)

You can check out the latest compiled binary from the master or pre-master code here:

[AppVeyor TSAnalyzer Project Builder](https://ci.appveyor.com/project/cinegy/tsanalyser/build/artifacts)

