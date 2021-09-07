---
title: "Is The Lead-Crime Hypothesis Real?"
subtitle:
date: 2021-08-21 00:00:00
update: 
author: Joe Cheung
description:
tags: cryptography finished
wordcount: 2522
---

1. TOC
{:toc}

## Overview

For two decades now, [lead](https://en.wikipedia.org/wiki/Lead%E2%80%93crime_hypothesis) has been very strongly suspected of causing crime. 

![](/images/2021-08-21-Lead-Crime/image10.png)

A [2000 paper](http://www.ricknevin.com/uploads/Nevin_2000_Env_Res_Author_Manuscript.pdf) found that if you add a lag time of 23 years, lead emissions from automobiles explained 90% of the variation in violent crime in the US. A [2007 paper](https://pic.plover.com/Nevin/Nevin2007.pdf) found more or less the same effect in Great Britain, Australia, New Zealand, Finland, France, Italy, and West Germany:

![](/images/2021-08-21-Lead-Crime/image2.png)

Another [2007 paper](http://www3.amherst.edu/~jwreyes/papers/LeadCrimeBEJEAP.pdf) found that the phase-out of lead from gasoline in the US was responsible for a 56% decline in violent crime between 1992 and 2002. A [2011 paper](https://www.un.org/apps/news/story.asp?NewsID=40226&Cr=pollutant&Cr1=#.UZdkooJAsR4) found that the UN-led global effort in de-leading resulted in 58 million fewer crimes.  A [2012 paper](https://www.sciencedirect.com/science/article/pii/S0160412012000566) found that ​​variation in air Pb emissions explained 90% of variation in aggravated assault in six US cities that had good crime and lead data going back to the ’50s.

## More Recent Studies

I have to say I was quite convinced when I first read about it. Kevin Drum [popularised](https://www.motherjones.com/environment/2016/02/lead-exposure-gasoline-crime-increase-children-health/) it in 2013, and (up to [2018](https://www.motherjones.com/kevin-drum/2018/02/an-updated-lead-crime-roundup-for-2018/)) has covered it extensively in two dozen other articles, and highlighted a dozen more papers since 2012 that support the lead-crime hypothesis.

In Charlotte, North Carolina, kids who received intervention reducing blood levels from 15 µg/dl to about 5 µg/dl [grow up](http://ftp.iza.org/dp10872.pdf) to commit fewer violent crimes. In the US, cities with lead pipes had homicide rates [24%](https://scholar.harvard.edu/jfeigenbaum/publications/effects-lead-crime-rates-evidence-fromhistorical-urban-data) higher than cities with iron pipes. In Australia, the variance in air lead explained [30%](http://ehjournal.biomedcentral.com/articles/10.1186/s12940-016-0122-3) of the variance in assault rates with a 21-years time lag at the suburb-level, consistent with the state, and national level. In St. Louis, Missouri, elevated blood lead levels (n=59,645) [strongly correlate](https://www.sciencedirect.com/science/article/pii/S0013935116301037) with crime occurrence (n=90,433) across census tracts. 

![](/images/2021-08-21-Lead-Crime/image5.png)

The statistics have [Andrew Gelman](https://statmodeling.stat.columbia.edu/2016/11/11/29443/)’s approval; the correlation seems real – not just an artifact of a particular regression specification. Though note that they’re all observational so we shouldn’t overinterpret it.

## No Safe Level Of Lead

Lead is a neurotoxin (among [other things](https://www.uptodate.com/contents/childhood-lead-poisoning-clinical-manifestations-and-diagnosis?search=lead%20poisoning&topicRef=2872&source=see_link#H24)) that [crosses](https://doi.apa.org/doiLanding?doi=10.1037%2Fpne0000225) the immature blood-brain barrier to impair fronto-executive functions in children even at low levels, and children absorb more lead per unit body weight than adults ([50%](https://www.who.int/ceh/publications/leadguidance.pdf) vs 10% of a glass of leaded water). 

Blood lead levels (BLL) are measured in micrograms per deciliter (µg/dL), and in the 60s, it wasn’t considered elevated unless they exceeded 60 µg/dL. It’s not until 1991 when the [CDC](https://www.cdc.gov/nceh/lead/data/blood-lead-reference-value.htm) changed the cutoff to 10 µg/dL and in 2012, changed it again to 5 µg/dL based on the 97.5th percentile of the BLL distribution among children aged 1-5. In the US, [550,000](https://www.cdc.gov/nceh/lead/data/Website_StateConfirmedByYear_1997_2014_01112016.htm) children have BPb levels at or above 5 mg/dL, 150,000 of whom have levels of at least 10 mg/dL. Globally, UNICEF estimates that more than [40%](https://www.unicef.org/sites/default/files/2020-07/The-toxic-truth-children%E2%80%99s-exposure-to-lead-pollution-2020.pdf) of children have BPb levels above 5 mg/dL.

This [2020 paper](https://www.gwern.net/docs/iq/2020-gronqvist.pdf) found that a 10% reduction in local moss lead levels corresponds to a 4.7% decrease in blood lead levels in Swedish primary school children (n=800,000 with 30-year followup), and the drop in local air lead levels between 1982 and 1994 can account for as much as 50% of the change in children’s BPb levels. The key thresholds are 5 µg/dL for high school completion and noncognitive skills, and 7 µg/dL for crime. Surprisingly, there wasn’t a clear threshold for high school GPA, and the authors failed to find a significant effect for cognitive skills at age 18 even at higher thresholds.

Perhaps it would be more surprising that extensive lead poisoning _doesn’t_ have any effect on kids. It certainly makes for a compelling [story](https://www.goodreads.com/book/show/30965518-lucifer-curves), but the jump from the neurotoxic effects of lead to crime is complicated by a myriad of factors, so my priors were relatively low coming in.

## Bit Of A Stretch?

Any claim based on correlations between such widely separate variables as lead exposure (the cause) and crime (the effect) are immediately suspect. The causal chain from vitamin C intake to scurvy cure, for example, is just one step. In the lead-crime hypothesis, the causal chain is something like 1) kids were exposed extensively to tetraethyl lead gasoline additive since the 1920s, 2) the neurotoxicity of lead causes kids to be more aggressive and dumber, 3) impaired decision-making and impulse control causes kids to do worse in school, 4) lower education outcomes lowers opportunity cost to commit crime, plus increased impulsivity, causes the now-young-adults to commit more property and violent crimes.

The lead-crime hypothesis only correlates the first and last link in the chain, but it would be more convincing if there were evidence about the intervening links. For instance, presumably most kids exposed to lead were more impulsive while only a minority of the impulsive young adults commit crimes, as the latter effect is time-lagged and necessarily diluted by other factors like policing and incarceration. If that’s true, we should expect to see very strong changes in IQ, school achievement, impulsiveness, aggressiveness, and lack of conscientiousness, all with less time lag.

As Stephen Pinker [noted](https://stevenpinker.com/files/pinker/files/pinker_comments_on_lead_removal_and_declining_crime_0.pdf), it’s the same flaw that torpaedoed _Freakonomic_’s [abortion-crime hypothesis](https://en.wikipedia.org/wiki/Legalized_abortion_and_crime_effect): supposedly legalised abortion led to fewer unwanted babies, which led to fewer maladjusted and violent young men two decades later. Turns out the assumption that states which completely legalised abortion had higher abortion rates than states where abortion was only legal under certain conditions before _[Roe v. Wade](https://en.wikipedia.org/wiki/Roe_v._Wade)_, was simply [untrue](https://ssrn.com/abstract=270126). When you zoomed into the causal chain, it fell apart.

![](/images/2021-08-21-Lead-Crime/image8.png)

_[A generation after gasoline was leaded, crime increased by a factor of four; a generation after lead was banned from gasoline, crime decreased by a factor of four.](https://www.motherjones.com/environment/2016/02/lead-exposure-gasoline-crime-increase-children-health/)_

So do we see the shorter-term effects of lead?[^1] In the US, blood lead levels in children aged 1-5 did decrease [84%](https://pediatrics.aappublications.org/content/123/3/e376) from 1988–1991 to 1999–2004. In Rhode Island, childhood blood lead levels and distance from major roadways [predicted](https://www.nber.org/papers/w23392) school suspensions and juvenile detentions. A [2019 paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6450277/) following up 579 New Zealand children after 30 years found that each 5-μg/dL increase in childhood blood lead level was associated with a 1.34-point (standardised mean of 100) increase in general psychopathology, a 0.10-SD increase in neuroticism, a 0.09-SD decrease in agreeableness, and a 0.14-SD decrease in conscientiousness.

So far the lead-crime hypothesis is holding up pretty well.

## Too Parallel To Be True?

The lead-crime hypothesis assumes the effects of lead exposure are the greatest in childhood, but not every crime-prone, lead-laden young adult starts rummaging and pillaging the moment they hit age 23 – the effects of age on crime is a very gentle bulge spread over the 15-30 age range, not a sharp fall-off. As Stephen Pinker [noted](https://stevenpinker.com/files/pinker/files/pinker_comments_on_lead_removal_and_declining_crime_0.pdf), the time-lagged curve for crime should be an attenuated, smeared version of the curve for lead, not a perfect copy of it. I couldn’t find any paper addressing this issue.

Another angle is that around [5%](https://digitalcommons.newhaven.edu/criminaljustice-facpubs/61/) of the population are responsible for 50% of crime, so the Great American Crime Decline is likely due to falls in this high-crime population, rather than less crimes per individual in that population.

## Biased Data

Researchers can basically pick between National Crime Victimization Survey (NCVS) and the Uniform Crime Reports (UCR) to look at US crime trends. This [2015 paper](https://link.springer.com/content/pdf/10.1007/s10940-015-9277-2.pdf) found NCVS trends in serious violence to be more highly correlated with homicide data than UCR trends, which suggests that the NCVS is a more valid indicator of long-term trends in violence for crimes other than robbery. 

Problem is that most of the studies looking at the lead-crime hypothesis rely on only one data source, and most often that is the UCR. Data from UCR suggest that serious violence was _lower_ in the mid-70s than it was after the crime decline of the 90s, while the NCVS data suggest that serious nonfatal violence was a lot _higher_ throughout the 70s and 80s than it was after the 90s crime decline.

![](/images/2021-08-21-Lead-Crime/image3.png)

This meant that trends in lead exposure were associated only with UCR nonlethal violence rates, and not with NCVS violence rates or homicide rates.

More generally, no agency tracks crimes by the age of the perpetrator – the data just doesn’t exist. Cohort analysis based on murder rates in the 80s is unlikely to have the statistical power to tell us much, and since age data for other crimes and other eras doesn’t exist, we’ll never get anything better.

## Hopelessly Confounded

Is it even possible to have a smoking gun? Causal hypotheses based on epidemiological correlations between widely separated causes and effects have endless confounders – neighborhoods next to smoggy freeways also tend to be poorer, more poorly policed, more poorly schooled, less stable, more dependent on contraband economies, and so on. It’s all too easy to find spurious correlations in this tangle, which is why so many epidemiological studies of the cause and prevention of disease fail to replicate.

More generally, my confidence in the findings from social sciences have tanked pretty hard by the [Replication Crisis](https://en.wikipedia.org/wiki/Replication_crisis) (which I will cover in future posts) – a large fraction, if not [most](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC1182327/), of social science and other fields is simply random noise that cannot be replicated, due to p-hacking, low statistical power, publication bias, and other sources of systematic error.

[Causal graphs](https://en.wikipedia.org/wiki/Bayesian_network#Causal_networks) are also probably denser than you think – the number of indirect connections grows exponentially faster than the number of direct connections, so any given indirect connection is vastly unlikely to be a direct connection, and thus manipulating one variable will not affect the other.  Our intuition formed in simple domains designed to have sparse causal networks just sucks in predicting things as complex as crime.

![](/images/2021-08-21-Lead-Crime/image1.png)

_[I can't even cram half of the nodes of this metabolic network into my head.](https://www.gwern.net/docs/www/biochemical-pathways.com/665fbbacd672c5b3dc16d84cf8fa87211a96c0f5.html#)_ 

My priors were pretty low, safe to say. There doesn’t seem to be much I can do besides repeating ‘correlation ≠ causation’ ad nauseam.

## Publication Bias Strikes Again

Enter the one and only [meta-analysis](https://www.gla.ac.uk/media/Media_774797_smxx.pdf). Higney et al. looked at the effects of lead on crime from 24 studies.

In a [funnel plot](https://en.wikipedia.org/wiki/Funnel_plot), if there is no publication bias, high-[precision](https://en.wikipedia.org/wiki/Precision_(statistics)) studies are plotted near the average, low-precision ones are spread evenly on both sides of the average. Below is the plot for the 24 studies; the clearly missing studies on the left (negative) side indicate possible publication bias:

![](/images/2021-08-21-Lead-Crime/image9.png)

_Negative and significant estimates are 200 times less likely to be published than positive, significant ones._

In a [forest plot](https://en.wikipedia.org/wiki/Forest_plot), the vertical line means no effect. For each study, the further to the right the black square, the bigger the [effect size](https://en.wikipedia.org/wiki/Effect_size) (in this case partial correlation coefficient, or PCC); the wider the horizontal line/whiskers, the larger the [confidence interval](https://en.wikipedia.org/wiki/Confidence_interval) (the more unreliable); the greater the weight/size of the black square, the greater the [power](https://en.wikipedia.org/wiki/Power_of_a_test) (e.g. due to greater [sample size](https://en.wikipedia.org/wiki/Sample_size_determination) and smaller confidence interval) i.e. the weight they have in the meta-analysis. The 24 studies:

![](/images/2021-08-21-Lead-Crime/image7.png)

So the median PCC evaluated at the sample averages for the full sample is 0.11, a [small](https://www.deakin.edu.au/__data/assets/pdf_file/0003/408576/2011_5.pdf) effect size, which is nonetheless over _ten times_ larger than the high-quality sample. Back-of-envelope calculations converting PPC into [elasticities](https://en.wikipedia.org/wiki/Elasticity_(economics)) gave a range of 0.22-0.02 for the full sample and 0.03-0.00 for the high-quality, addressing endogeneity sample. This suggests the fall in blood lead levels may have led to a fall in homicide in the US of between 3-36% with the full sample elasticity, and between 0-5% for the addressing endogeneity sample elasticity.

## Biodeterminism

Overall, the results suggest that the fall in lead levels cannot explain most of the fall in crime observed in many western countries; the upper end of the range of elasticities would imply the lower lead pollution today saves around 6,000 lives a year in the US, while the lower would mean lead has no effect and we must look to other causes entirely.

Like omega-6 fatty acids.

With the advent of industrial food processing, soybean oil, corn oil, cottonseed oil and other industrial creations have replaced milk and meat fat in our diet, while total fat consumption has remained relatively constant. The result is that we're eating a lot more polyunsaturated fat than we were just 30 years ago, most of it [linoleic acid](https://wholehealthsource.blogspot.com/2011/08/seed-oils-and-body-fatness-problematic.html) (omega-6).

![](/images/2021-08-21-Lead-Crime/image4.png)

Now take this [2004 paper](https://pubmed.ncbi.nlm.nih.gov/15736917/) that looked at 12 major seed oils in the food supply for the years 1961 to 2000 in Argentina, Australia, Canada, the United Kingdom, and the United States, and boy does it correlate with homicide rates. [Stephan Guyenet](https://wholehealthsource.blogspot.com/2008/09/vegetable-oil-and-homicide.html) doesn’t think we can draw any solid conclusions from this, but it is worth noting that epidemiological associations don't get much better.

![](/images/2021-08-21-Lead-Crime/image6.png)

_Corn oil may taste so bad it inspires you to violence, but its insidiousness goes beyond the flavor._

Or this [2001 paper](https://www.karger.com/Article/Abstract/59747) that found a linear correlation between the increase in omega-6 fatty acids consumption from seed oils in 38 countries since the 1960s, and the rise in murder rates over the same period. 

Or this famous 2002 double-blinded placebo-controlled, randomised trial of dietary supplements including fish oil vs placebo to 231 prisoners found a [26.3%](https://www.cambridge.org/core/journals/the-british-journal-of-psychiatry/article/influence-of-supplementary-vitamins-minerals-and-essential-fatty-acids-on-the-antisocial-behaviour-of-young-adult-prisoners/04CAABE56D2DE74F69460D035764A498) drop in prison violence (p = .03) using intention to treat and 35% (p = .001) using completers. A 2010 [replication study](https://pubmed.ncbi.nlm.nih.gov/20014286/) on 221 Dutch prisoners found almost exactly the same results. A [2000 paper](https://pubmed.ncbi.nlm.nih.gov/10706231/) of 468 children aged 6-12 found an even more drastic 47% decrease in antisocial behavior.

No really, everything is correlated. When we systematically measure many variables at a large enough scale, even things which seem to have no causal relationship show real correlation with high confidence. If you fail to reject the null hypothesis with p &lt; 0.05, you simply haven’t collected enough data yet.

You can manufacture arbitrarily many spurious results by data mining, and sometimes you find that fish oil makes men kill fewer people. A Comprehensive [review](https://archive.ahrq.gov/downloads/pub/evidence/pdf/o3mental/o3mental.pdf) of the literature on the effects of omega-3 fatty acids on mental health basically dismisses everything done thus far as insufficient to draw meaningful conclusions. Maybe omega-6 studies hold up better but I’m not keeping my hopes up that they’ll [replicate](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8139580/) in the year of our lord 2021.

Like [Scott Alexander](https://slatestarcodex.com/2014/02/18/proposed-biological-explanations-for-historical-trends-in-crime/), I am biased towards biodeterminism – I suspect most social influences matter less than anyone thinks and most biological influences matter more than anyone thinks. So the lead-crime hypothesis sounded pretty appealing to me, and so does the omega-6 story, even if it smells fishy.

All in all I’m glad economists were able to find a cause for crime despite the inability of lead levels to explain most of the variation. Empirically, most efforts to change human behavior in sociology, economics, education fail in RCTs and the mean effect size in meta-analyses typically approaches zero, per the [Metallic Laws](https://www.gwern.net/docs/sociology/1987-rossi.pdf). So [Clair Cameron Patterson](https://en.m.wikipedia.org/wiki/Clair_Cameron_Patterson) is (still) an unsung hero for his seminal anti-lead campaign, which could accidentally be one of the most effective War-on-Crime policies in history.

## Endnotes 

[^1]: We know that the [Flynn effect](https://en.wikipedia.org/wiki/Flynn_effect#Rise_in_IQ) is real – IQ has been rising [2-3](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4152423/) points per decade since the invention of the IQ test. Curiously, I have never seen lead exposure being mentioned as one of the environmental factors, perhaps because the secular rise in IQ is near-constant beginning in the 1940s, which doesn’t track lead exposure even with a time lag.