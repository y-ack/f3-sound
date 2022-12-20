# BANK 1: SEQUENCER (base address 0xC00000)
## interrupt vector (0xC00000)
## sample info table (0xC00134)
each entry is 20 bytes long, 
seems to have information about instrument the sample belongs to, root/note to play at, note adjustment(?)

## sequencer os stuff
0xC058C8: control code string sub offsets
0xC059CC: substituted strings
0xC05C5D: various display strings
0xC0B39C: sequencer code
0xC0C4BA: string control code parser
0xC10D48: general trap handler?
0xC11068: idle
0xC111D0: duart putchar?
0xC11284: ensoniq print
0xC11276: ensoniq putchar
### playback
0xC11DD8: copy note data to ram?
0xC12AFA: copy tempo to ram?
0xC14CB8: measure and beat control?
0xC15A18: get bar count?
0xC158AE: get sequence by id
0xC158CC: get sequence header by id
0xC155E8: set cur seq
0xC18372: does a lot of ESP writes
0xC192EE: more ESP writes

# BANK 2: SEQUENCES (base address 0xC20000)
## section 1: sequence data
bank-relative s32: length
bank-relative s32: negative number (?!?) 
bank-relative s32: *sequence[100]

followed by sequence data
sequences start with length followed by 
up to 11(?) track(?) offsets (relative to seq)

example: seq03 "SELECT_R" hex: https://qcs.shsbs.xyz/c/efokv
recording: https://youtu.be/-OmC2fLUayA?t=67

## section 2: extra sequence information
following the "length" offset leads to a section of additional sequence information. again starts with
 - length (in this case, the following "section" is a 00000000 00000000 entry, the end?)
 - a negative offset(?)
 - a table of up to 100 offsets corresponding to each sequence. this time they're s16.

an entry might look like: (actual structure unknown)
0012
D3C5CCC5C3D4DFD22020202020202020
00180402000000000000000078
0000347F8000000001100015006C
0000507F8000000002110015006C
0000507F8000000002120015006C
0000397FCC00000001130015006C
0000137F8000000001140015006C
0000427F8000000000150015006C
0000107F8000000000160015006C
0000557F8000000003170015006C
00010000000000000005000000000000000A0A000000000000

the second field is the sequence name, but the top bit of each character possibly encodes information for the sequencer display
and then some form of information for each track

landmakr seq content:
| seq00 | Sequence-00 |
| seq01 | Sequence-01 |
| seq02 | Sequence-02 |
| seq03 | SELECT_R    |
| seq04 | BOSS_RI     |
| seq05 | BOSS_RL     |
| seq06 | MAP_R       |
| seq07 | Sequence-07 |
| seq08 | PUSH        |
| seq09 | SOUMEI2     |
| seq10 | Opening     |
| seq11 | Ending      |
| seq12 | HIRYU_I     |
| seq13 | HIRYU_L     |
| seq14 | Sequence-14 |
| seq15 | AIFA        |
| seq16 | SOUMEI_I    |
| seq17 | SOUMEI_L    |
| seq18 | Sequence-18 |
| seq19 | RENKI       |
| seq20 | YOUEN_R     |
| seq21 | ROHKO       |
| seq22 | RINRE_I     |
| seq23 | RINRE_L     |
| seq24 | Sequence-24 |
| seq25 | ROUCHI      |
| seq26 | LAST        |
