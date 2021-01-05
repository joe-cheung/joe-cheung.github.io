---
title:  "Charity Is Still Not About Helping"
subtitle:
date:   2020-12-16 00:00:00
update:
author: Joe Cheung
description:
tags: philosophy sociology charity
wordcount: 628
---

*[This is sort of an appendix to my [post](https://subcriticalappraisal.com/2020/Did-DeepMind-solve-the-protein-folding-problem/) about DeepMind protein structure prediction. Epistemic status: not too sure, just doing the back-of-the-envelope with more up-to-date numbers.]*

1. TOC
{:toc}

This is an update of Gwern's [cost-benefit analysis](https://www.gwern.net/Charity-is-not-about-helping) of Folding@home (FAH) which made the case that distributed computing is harmful as scientific [lemon](https://www.wikiwand.com/en/The_Market_for_Lemons) projects running at high resource cost.

## Charitable Supercomputer

FAH [<span class="underline">boasts</span>](https://archive.vn/20200412111010/https://stats.foldingathome.org/os) of being the world's first [exaFLOP](https://en.wikipedia.org/wiki/Exascale_computing?oldformat=true) (10<sup>18</sup> [FLOPS](https://en.wikipedia.org/wiki/FLOPS?oldformat=true)) computer system when it achieved a processing speed of 1.22 exaFLOPS by late March 2020 and reached 2.43 exaFLOPS by April 12, 2020. As it is powered by volunteers running its clients on their CPUs and GPUs (and until 2012 their PS3s too), heightened interest during the COVID-19 pandemic has allowed it to be faster than the top 500 supercomputers combined.

![](/images/2020-12-17-Did-DeepMind-solve-the-protein-folding-problem/image40.png)
*[<span class="underline">The exascale barrier is a quintillion (1,000,000,000,000,000,000) operations per second</span>](https://twitter.com/foldingathome/status/1249778379634675712?s=20)

## Sins of Commission

How much electricity does FAH consume? When it hit 1.01 exaFLOPS, an [<span class="underline">estimated</span>](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7337393/) ~280,000 GPUs and 4.8 million CPU cores were participating. According to FAH, although power supplies on most computers are rated at 400 watts, a Pentium-type computer uses about 100 watts on average (if the monitor is off), so let’s assume each CPU and GPU draw 100 watts, not factoring in heat production, normal system load, nor dynamic frequency scaling. That gives 508,000,000 watts, and a power efficiency of 1.99 GFLOP (10<sup>9</sup> FLOP)/watt, putting it at 145th on the [<span class="underline">November Green500 List</span>](https://www.top500.org/lists/green500/list/2020/11/?page=2).

How much air pollution does FAH produce? Assuming 1.01 exaFLOPS is sustained for a whole year, it consumes 4.45 terawatt-hours per year. That means a [<span class="underline">greenhouse gas emission</span>](https://www.epa.gov/energy/greenhouse-gas-equivalencies-calculator) of 3,150,000 metric tons, as much as that from 680,000 cars. If we’re being generous and pretend that all the electricity is produced in the US, and take into account Gwern’s estimation of 7.7 deaths per year for a US power mix, it means 34 deaths per year due to air pollution from powering FAH.

## Sins of Omission

How much does all that electricity cost? As of September 2020, the average US rate for 1 kilowatt-hour is $0.1355, so the electricity bill of FAH is $602,975,000 per year. Take the [<span class="underline">Against Malaria Foundation</span>](https://www.givewell.org/charities/amf#Cost_per_death_averted) for example, GiveWell [<span class="underline">estimates</span>](https://80000hours.org/2017/05/most-people-report-believing-its-incredibly-cheap-to-save-lives-in-the-developing-world/) that $2,300 can save a child’s life in the developing world. The opportunity cost of FAH is 262,163 [<span class="underline">dead children</span>](https://www.gwern.net/docs/philo/2011-yvain-deadchild.html) per year.

## Benefits

Has FAH actually accomplish [anything](https://old.reddit.com/r/askscience/comments/r93i6/has_foldinghome_really_accomplished_anything/)? They boast of [<span class="underline">233</span>](https://arstechnica.com/science/2020/04/how-the-pandemic-revived-a-distributed-computing-project-and-made-history/) [<span class="underline">papers</span>](https://foldingathome.org/papers-results/) produced in the 20 years since the start of the project, but their own [<span class="underline">summary</span>](https://foldingathome.org/faqs/press/what-have-you-done-so-far/summarize-key-papers-resulted-fah/) doesn't give the impression that they were too impressed, but who am I to [judge](https://www.quora.com/What-do-biologists-think-of-gwerns-criticism-of-Folding-Home). Folding@home, per its namesake, initially set out to simulate protein folding, but it [<span class="underline">seems</span>](https://www.reddit.com/r/askscience/comments/r93i6/has_foldinghome_really_accomplished_anything/c43yxd4/) that they are more about dynamics of the folding mechanism, than predicting anything. They have never competed in [CASP](https://subcriticalappraisal.com/2020/Did-DeepMind-solve-the-protein-folding-problem/#casp).

## Charity Is Still Not About Helping

Gwern,

> "It is sad and pitiable that we spend so many billions on things like dog food and cosmetics rather than saving lives; but isn’t it even sadder that we can avoid that error, and try to do good, and still fail? The only thing sadder, I think, would be if we could know of our failure and go on supporting FAH. If charity truly was not about helping."