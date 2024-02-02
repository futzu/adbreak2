# adbreak2
adbreak2 Generates SCTE-35 Cues for Sidecar files.
```js
a@fu:~$ ./adbreak2 -h
usage: adbreak2 [-h] [-d DURATION] [-e EVENT_ID] [-i] [-o] [-p PTS]
                [-s SIDECAR] [-v]

options:
  -h, --help            show this help message and exit
  -d DURATION, --duration DURATION
                        set duration of ad break. [ default: 60.0 ]
  -e EVENT_ID, --event-id EVENT_ID
                        set event id for ad break. [ default: 1 ]
  -i, --cue-in-only     only make a cue-in SCTE-35 cue [ default: False ]
  -o, --cue-out-only    only make a cue-out SCTE-35 cue [ default: False ]
  -p PTS, --pts PTS     set start pts for ad break. Not setting pts will
                        generate a Splice Immediate CUE-OUT. [ default: 0.0 ]
  -s SIDECAR, --sidecar SIDECAR
                        Sidecar file of SCTE-35 (pts,cue) pairs. [ default:
                        sidecar.txt ]
  -v, --version         Show version



```

## Install 
1. `git clone https://github.com/futzu/adbreak2`
2. `python3 -mpip install threefive`
3.  `cd adbreak2`
4.  `install adbrerak2 /usr/local/bin`

## Use

* Running `adbreak2` with no args will generate a Splice Insert Cue, with `Splice Immediate` and `Out of Network` set. A CUE_OUT.
* The Cue data is displayed, and the base64 SCTE-35 string is written to sidecar.txt.
```json
a@fu:~$ adbreak2
{
    "info_section": {
        "table_id": "0xfc",
        "section_syntax_indicator": false,
        "private": false,
        "sap_type": "0x03",
        "sap_details": "No Sap Type",
        "section_length": 32,
        "protocol_version": 0,
        "encrypted_packet": false,
        "encryption_algorithm": 0,
        "pts_adjustment_ticks": 0,
        "pts_adjustment": 0.0,
        "cw_index": "0x00",
        "tier": "0x0fff",
        "splice_command_length": 15,
        "splice_command_type": 5,
        "descriptor_loop_length": 0,
        "crc": "0xc38e9258"
    },
    "command": {
        "command_length": 15,
        "command_type": 5,
        "name": "Splice Insert",
        "break_auto_return": true,
        "break_duration": 60.0,
        "break_duration_ticks": 5400000,
        "splice_event_id": 1,
        "splice_event_cancel_indicator": false,
        "out_of_network_indicator": true,
        "program_splice_flag": true,
        "duration_flag": true,
        "splice_immediate_flag": true,
        "event_id_compliance_flag": true,
        "unique_program_id": 1,
        "avail_num": 0,
        "avail_expected": 0
    },
    "descriptors": []
}
```
```lua
a@fu:~$ cat sidecar.txt

0.0,/DAgAAAAAAAAAP/wDwUAAAABf//+AFJlwAABAAAAAMOOklg=
```
