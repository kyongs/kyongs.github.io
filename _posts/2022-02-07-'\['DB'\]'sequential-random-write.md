---
title: "[DB] Sequential Write vs. Random Write"
updated: 2022-01-23 23"23
---

### Differences between sequential vs. random write

<p>
When people talk about sequential vs random writes to a file, they're generally drawing a distinction between writing without intermediate seeks ("sequential"), vs. a pattern of seek-write-seek-write-seek-write, etc. ("random").<br/>

The distinction is very important in traditional disk-based systems, where each disk seek will take around 10ms. Sequentially writing data to that same disk takes about 30ms per MB. So if you sequentially write 100MB of data to a disk, it will take around 3 seconds. But if you do 100 random writes of 1MB each, that will take a total of 4 seconds (3 seconds for the actual writing, and 10ms\*100 == 1 second for all the seeking).<br/>

</p>
[COPY FROM 🔍](https://stackoverflow.com/questions/2100584/difference-between-sequential-write-and-random-write#:~:text=(%22random%22).,will%20take%20around%203%20seconds.)
