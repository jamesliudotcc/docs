# Saving Money on AWS

These are just some easy wins that you can take advantage of. They are cumulative to using savings plans and reserved instance. You should do these things and then reserve the instances. Or you should do these things ahead of your reserved instances expiring, to take advantage the next cycle.

Also, there are more savings that come from rearchitecting to take advantage of the AWS. But that is very case-by-case specific.

## Storage should be in the lowest tier of S3 you can reasonably use

S3 has a feature called automtic tiering. It figures out the usage pattern of your files and puts some of them onto infrequent access tiers. Automatic tiering has an optional feature that puts objects into deep archive (also called Glacier), but you may not want a naive heuristic to put your objects there. Infrequent Access is fine, though. So just enable that.

You should figure out what can go to Deep Archive though. The cost for Deep Archive is so low that it is effectively free, probably because it is tape under the hood. Database backups that are older than the most recent backup? If you have to keep them, put them in Deep Archive.

## Store things in S3 instead of EBS

S3 is much cheaper than any form of EBS or EFS. The storage in RDS Aurora is fundamentally S3, whereas RDS without Aurora is EBS. If you have append-only data that is rarely accessed, put it in S3 and bring it back when you need it.

## Find and destroy your unuused EBS volumes

Self explanatory. AWS has an incentive to keep those around, not just to charge extra money. The volumes contain your data, so you should take active steps to throw it away.

## Measure!

S3 has a feature that allows you to see access patterns for your objects. It takes some S3 storage to keep the logs, so it is not free. But you will almost certainly save more money once you know what you can downtier than if you keep everything in the most expensive tier.

## Use the right CPU/memory balance

Once you know how much CPU and memory you are using, you can change how much RAM per CPU by selecting a different EC2 type. There is even some flexibility in their managed offerings. The standard is M, C has half the RAM per CPU, R has double, X has four times or more.

## Use the right generation/chip

In general, newer generations have better performance for less money. The only exception are the 7 series, which are even with or sligthly worse than the 6 series.

## Consider using Graviton

Ok, not necessarily for the code that you've written. If you recently started supporting M1 macs for your developers, you kind of know how much of a pain this is (maybe it just works, in which case, go for it). But for sure, recent versions of popular databases (and database-like-things like Redis, Rabbit, Kafka) will just work.
