---
id: 1988
title: The Mendel 3d printer Z axis working (kinda of)!
date: 2011-12-01 15:37:13
author: 4
---
## error
Failed to parse. Text: "```json
{"en": "Updates for everyone. First, thanks Alex for the continued dedication on the printer. He identified a few problems we can fix and improve on. 2 major issues:\n\n1. Z axis is stuck; it moves a little bit but then stops.  Not sure if it's a mechanical issue (something jamming) or an electrical problem. Alex will try adjusting belt tension to see if that helps. Another possibility is that one of the screw rods and bearings might be misaligned, causing the jam. I recall being able to move it up and down by hand pulling on the belt. If that continues to work, maybe the problem is the motor isn't strong enough. Luckily, I've been experimenting with motors and have one that's 3x more powerful. I'll mount that one if nothing else works.\n\n2. Filament feeds into the first hole but can't get into the second hole of the heating chamber.  Alex can push the idler bearing block back and feed the filament into the first hole and then between the brass gear and idler bearing. But then the filament is pushed slightly to the side and can't find the second hole. The likely problem is the brass gear is too large. Two solutions: reduce the gear size (either by buying a smaller one or by filing down the current one) or help the filament into the second hole using small ramps or funnels around the second hole. I'll try the ramps/funnels first. If that doesn't work, then we'll look for a smaller gear.\n\nAlex followed up with good news:\n\nThe Z axis works now after loosening the belt. The bearings might be too tight now, but it's easy to adjust.  We need to fix the broken part, though it's not essential but improves precision. I wasn't able to disassemble the extruder part to try hand-feeding and see if it extrudes, but Ricky just said he received the new parts, so we should be able to replace the whole thing on Saturday... hopefully!  ", "zh": null}
```
". Error: SyntaxError: Unexpected token '`', "```json
{""... is not valid JSON

Troubleshooting URL: https://js.langchain.com/docs/troubleshooting/errors/OUTPUT_PARSING_FAILURE/


## code
 <!\[CDATA\[\[:en\]

Mike, after chatting online with Alex over Skype, updated the group with this:

> Updates for everyone. First, thanks Alex for the continued dedication on the printer. He identified a few problem we can fix and improve on. 2 major issues:
> 
> 1\. Z axis is stuck, moves a little bit but then stops. Not sure if it's a mechanical issue where something is jamming or possibly electrical. Alex will try loosening and tightening the belt tension to see if that helps. Other potential issue is one of the screw rods and bearing seem to be canted, which may be the cause of the jam. I recall being able to make it move up and down by pulling on the belt by hand. If that continues to work, maybe the problem is the motor isn't strong enough. Lucky me, I've been playing with motors and have one that's 3x more powerful. Will mount that one if nothing else seems to work.
> 
> 2\. Filament feeds into the first hole but can't find the second hole into the heating chamber. Seems Alex can push the idler bearing block back and feed the filament into the first hole and then between the brass gear and idler bearing. But then the filament is pushed to the side slightly and can't find the second hole itself. Likely problem is the brass gear I used is too large. 2 solutions, reduce the gear size or help the filament into the second hole. Reduce gear size by either buying a smaller one or file down the one we have. Help the filament into the second hole can be done with a small ramps or funnels around the second hole. I'll give the ramp/funnel method a try first. If that doesn't work, then we'll go gear hunting.

Alex followed up a bit later with exciting news:

> Z axes works after untightening the belt. Bearings may be too tight now but is easy to adjust and we need to fix up the broken part. The part is not a essential but helps to have precision on the axis. I wasn't able to unassemble the extruder part to try hand feeding and see if extrudes but Ricky just told me that he received the new parts so Saturday we will be able to change the whole thing... hopefully ;P

\[:\]\]\]> \[:\]
