---
title: "AGI: Scale Is All You Need"
subtitle:
date: 2022-06-05 00:00:00
update: 
author: Joe Cheung
description:
tags: AI finished
wordcount: 5329
---

The deep learning revolution started with [AlexNet](https://en.wikipedia.org/wiki/AlexNet) in 2012. Since then, more and more money is being poured into training larger and larger models:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image19.png)

_[Most of the increase in compute has been companies willing to pay more rather than algorithmic or hardware progress.](https://www.economist.com/technology-quarterly/2020/06/11/the-cost-of-training-machines-is-becoming-a-problem)_

1. TOC
{:toc}

## GPT-3 And The Blessings of Scale

In May 2020, OpenAI announced [GPT-3](https://www.gwern.net/docs/www/arxiv.org/90cd91e98db4f7b0b1cd57da7c3713dbe34c2146.pdf#openai), an unsupervised deep learning [transformer](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model))-based language model trained on Internet text for the single purpose of predicting the next word in a sentence. It’s the 117x larger 175B-parameter successor to [GPT-2](https://openai.com/blog/better-language-models/), which itself [surprised everyone](https://slatestarcodex.com/2019/02/19/gpt-2-as-step-toward-general-intelligence/) with its ability to learn question answering, reading comprehension, summarisation, and translation, all from the raw text using no task-specific training data. [Image GPT](https://openai.com/blog/image-gpt/), the same exact model trained on pixel sequences instead of text, could generate coherent image completions and samples. GPT-3 [astounded everyone](https://www.lesswrong.com/posts/6Hee7w2paEzHsD6mn/collection-of-gpt-3-results) — instead of running into diminishing or negative returns, the vast increase in size didn’t merely translate into quantitative improvements in language tasks but also qualitatively distinct improvements that implies meta-learning (attention mechanism as “[fast weights](https://www.gwern.net/docs/www/arxiv.org/5f3ef8ce619f3af4f40dc1e235b3492d3c2685e3.pdf#deepmind)” that “learnt to learn”), such as:

* [Basic arithmetics](https://openai.com/blog/grade-school-math/)
* [Creative fiction](https://www.gwern.net/GPT-3) (poetry, puns, literary parodies, storytelling) e.g. fine-tuned version powered [AI Dungeon](https://play.aidungeon.io/main/home) capable of generating [cohesive space operas](https://kajsotala.fi/2020/07/gpt-3-space-opera/) with almost no editing 
* [Automatic code generation](https://twitter.com/sharifshameem/status/1282676454690451457) from natural language descriptions e.g. [building a functional React app](https://twitter.com/sharifshameem/status/1284095222939451393)
* Almost passing a coding [phone screen](https://twitter.com/lacker/status/1279136788326432771) to land a software engineering job

GPT-3 is the first AI system that has obvious, immediate, transformative economic value:

* [OpenAI API](https://openai.com/api/): GPT-3-as-a-service (from January 2022 onwards the safer, more helpful, more aligned 1.3B-parameter [InstructGPT](https://openai.com/blog/instruction-following/) [capable](https://www.lesswrong.com/posts/dypAjfRCe4nyasGSs/new-gpt3-impressive-capabilities-instructgpt3-1-2) of brainstorming, summarising main claims, and analogizing) that powers [hundreds of applications](https://gptcrush.com/resources/?sort=upvotes-desc)
* [Codex](https://openai.com/blog/openai-codex/) (GPT-3 trained on GitHub code) powers their programming autocompletion tool [GitHub Copilot](https://copilot.github.com/)

GPT-3 demonstrates the _blessings of scale_: for deep learning, hard problems are easier to solve than easy problems — everything gets better as models get larger (in contrast to the usual outcome in research, where small things are hard and large things impossible). The [Bitter Lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html) goes:

> The biggest lesson that can be read from 70 years of AI research is that general methods that leverage computation are ultimately the most effective, and by a large margin. The ultimate reason for this is Moore's law, or rather its generalization of continued exponentially falling cost per unit of computation. 

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image8.png)

The scaling laws of deep learning, highly consistent over more than 6 orders of magnitude, is driven by neural networks (NNs) functioning as ensembles of many sub-networks that average out to an [Occam’s razor,](https://en.wikipedia.org/wiki/Occam%27s_razor#Objective_razor) which for small data and models, learn superficial or memorised parts of the data, but can be forced into true learning with hard and rich enough problems. As [⁠meta-learners learn amortised Bayesian inference](https://www.gwern.net/Backstop#deep-bayes)⁠, they build in informative [priors](https://en.wikipedia.org/wiki/Prior_probability) when trained over many tasks, and become dramatically more sample-efficient and better at generalisation.

Once the compute is ready, the paradigm will appear:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image11.png)

_[Each paradigm having a certain amount of compute you can “feed” it before it stops scaling with compute effectively.](https://astralcodexten.substack.com/p/biological-anchors-a-trick-that-might?s=r)_

As Gwern [writes](https://www.gwern.net/Scaling-hypothesis), GPT-3 is terrifying because it is a tiny model compared to what's possible, trained in the dumbest way possible on a single impoverished modality on tiny data, sampled in a dumb way⁠⁠⁠, its benchmark performance sabotaged by bad prompts and data encoding problems, and yet the first version already manifests crazy runtime meta-learning — and the scaling curves _still_ are not bending!

Per OpenAI’s [Kaplan et al. 2020](https://arxiv.org/abs/2001.08361), the leaps we have seen over the past few years are not even halfway there in terms of absolute likelihood loss:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image17.png)

_[GPT-3 represents ~10^3 — plenty of room for further loss decreases](https://www.gwern.net/docs/www/arxiv.org/20d126b9c3baf640f8d1d5dff3e253faac2e8242.pdf#openai)._ 

If we see such striking gains in halving the validation loss from GPT-2 to GPT-3 but with so far left to go, what is left to emerge as we halve again?

## Pretraining And The Scaling Hypothesis

The [pretraining thesis](https://www.gwern.net/Scaling-hypothesis#blessings-of-scale:~:text=Cambria%20%26%20White%C2%A02014) goes:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image7.png)

Humans are the [cyanobacteria](https://en.wikipedia.org/wiki/Great_Oxidation_Event) of AI: we emit large amounts of structured data in which logic, causality, object permanence, history are encoded. A model like GPT-3 trains on such data in which “intelligence” is implicit, and learns from the crudest level:

1. Some letters are more frequent than others (alphanumeric gibberish): 8-5 bit error per character
2. Words and punctuations exist (still gibberish): 4-3 bit error per character
3. Words “cluster” (bag of words): &lt;3 bit error per character
4. Sentences exist (starts making sense): 2 bit error per character (every additional 0.1 bit decrease starts to come more costly[^1])


5. Grammar exists e.g. keeping pronouns consistent (multiple sentences make sense): 1-2 bit bit error per character
6. Subtleties e.g. solving repetition loops (paragraphs make sense) &lt;0.02 bit error per character

Language model performance can be measured by how many bits it takes to convey a character i.e. bits per character (BPC): GPT-2 had a [cross-entropy ](https://en.wikipedia.org/wiki/Cross_entropy#Cross-entropy_loss_function_and_logistic_regression)WebText validation loss of ~3.3 BPC; GPT-3 halved that loss to ~1.73 BPC. For a hypothetical GPT-4, if the scaling curve continues for another 3 orders or so of compute (100–1000x) before hitting harder diminishing returns⁠, the cross-entropy loss will drop to ~1.24 BPC.

It still won’t be near the natural language performance of humans who (in [ASCII](https://en.wikipedia.org/wiki/ASCII)) use a byte to express a full [7 bits](https://www.gwern.net/Differences#efficient-natural-languages) of information i.e. Shannon’s [7-gram character entropy](https://thegradient.pub/understanding-evaluation-metrics-for-language-models/) (0.7 BPC).

What is in that missing >0.4? _Everything!_ While random babbling sufficed at the start, nothing short of true understanding will suffice for ideal prediction. _The last bits are deepest._ Analogous to humans: we all perform everyday actions like buttoning our shirts well given enough practice and feedback, but we differ when we run into the long tail of choices that are:

1. Novel
2. Rare
3. Short in execution but unfold over a lifetime
4. Without any feedback (e.g. after our death)

One only has to make a single bad decision to fall into _ruin_. A small absolute average improvement in decision quality can be far more important than its quantity indicates, hence why the last bits are the hardest and deepest.

If GPT-3 gained so much meta-learning and world knowledge by dropping its absolute loss 50% when starting from GPT-2’s level, what capabilities would another 30% improvement over GPT-3 gain? If we trained a model which reached that loss of 0.7 i.e. predict text indistinguishable from a human, how could we say that it doesn’t truly understand everything[^2]?

Thus, the [scaling hypothesis](https://www.gwern.net/Scaling-hypothesis#scaling-hypothesis): the blessings of scale as the secret of [artificial general intelligence](https://en.wikipedia.org/wiki/Artificial_general_intelligence) (AGI) — intelligence is “just” simple NNs applied to diverse experiences at a (currently) unreachable [scale](https://www.lesswrong.com/posts/xwBuoE9p8GE7RAuhd/brain-efficiency-much-more-than-you-wanted-to-know); as increasing computational resources permit running such algorithms at the necessary scale, NNs will get ever more intelligent.

## Slowly At First, Then All At Once

Even in 2015, the scaling hypothesis seemed highly dubious — you needed something to scale, after all, and it was all too easy to imagine flaws in existing systems would never go away, and progress would sigmoid any month now. Like the genomics revolution where a few far-sighted seers extrapolated that the necessary _n_ for GWASes would increase exponentially and deliver powerful polygenic scores soon (which I [wrote about](https://subcriticalappraisal.com/2021/Practical-Ethics-Of-Preimplantation-Polygenic-Screening/)), while sober experts wrung their hands over “missing heritability” and the miraculous complexity of biology to scoff about how such _n_ requirements proved GWAS was a failed paradigm, the future arrived at first slowly and then quickly.

For a while after GPT-3 was published, we were [possibly](https://www.lesswrong.com/posts/3nDR23ksSQJ98WNDm/developmental-stages-of-gpts) [in](https://www.lesswrong.com/posts/N6vZEnCn6A95Xn39p/are-we-in-an-ai-overhang) [hardware overhang](https://aiimpacts.org/hardware-overhang/) where large quantities of compute can be diverted to running powerful AI systems as soon as the software is developed (so as one powerful AI system exists, probably a large number of them do). Google Brain was entirely too practical and short-term; DeepMind believes that AGI will require effectively replicating the human brain module by module; OpenAI, lacking anything like DeepMind’s Google cashflow or its enormous headcount is making a startup-like bet that they know an important truth that is a [Thielian secret](https://blakemasters.tumblr.com/post/22866240816/peter-thiels-cs183-startup-class-11-notes): the Scaling Hypothesis is true.

In August 2021, Stanford’s entire AI department released a 200-page 100-author [neural scaling laws manifesto](https://arxiv.org/abs/2108.07258) announcing their pivot to position themselves as the number one at academic ML scaling research. Only recently do we see Google AI, Google Brain, and DeepMind treat GPT-3 as scaling’s Sputnik moment:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image12.png)

_[Google's 540 billion parameter PaLM is the right-most, up-most dot](https://ourworldindata.org/grapher/ai-training-computation?time=2017-08-04..2022-07-01)_. 

In just the past two months, we saw bigger and bigger models like DeepMind’s 80B-parameter [Flamingo](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/tackling-multiple-tasks-with-a-single-visual-language-model/flamingo.pdf) ([paper](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/tackling-multiple-tasks-with-a-single-visual-language-model/flamingo.pdf)), Robotics at Google and Everyday Robots (also Alphabet-owned)’s [SayCan](https://say-can.github.io/) ([paper](https://arxiv.org/abs/2204.01691)), and Robotics at Google’s [Socratic Models](https://socraticmodels.github.io/) ([paper](https://arxiv.org/abs/2204.00598)). Below I highlight the most blockbusting five.

#### Google AI’s 540B-parameter PaLM 

([Blog](https://ai.googleblog.com/2022/04/pathways-language-model-palm-scaling-to.html), [paper](https://storage.googleapis.com/pathways-language-model/PaLM-paper.pdf))

Continues the Kaplan scaling, sees discontinuous improvements from model scale (see [comparison](https://www.lesswrong.com/posts/EHbJ69JDs4suovpLw/testing-palm-prompts-on-gpt3) with GPT-3). The surprise is perhaps how poor the communication between Google and DeepMind is, as you will see.

#### DeepMind’s 70B-parameter Chinchilla

([Blog](https://www.deepmind.com/publications/an-empirical-analysis-of-compute-optimal-large-language-model-training), [paper](https://arxiv.org/abs/2203.15556))

Outperforms the much larger 175B-parameter GPT-3 and DeepMind's own 280B-parameter [Gopher](https://www.deepmind.com/blog/language-modelling-at-scale-gopher-ethical-considerations-and-retrieval), demonstrating that essentially everyone has been training LLMs with a deeply suboptimal use of compute.

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image10.png)

_Model size is (almost) everything._

DeepMind chose 9 quantities of compute (10<sup>18</sup>-10<sup>21</sup> FLOPs) and trained many different-sized models at each quantity:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image1.png)

_The best models are at the minima._

Connecting the minima at each curve gives you a new scaling law: for every increase in compute, data and model sizes should increase by the _same amount_. DeepMind verified the new training law by training the 70B-parameter Chinchilla using the same compute used for their own 280B-parameter Gopher i.e. Chinchilla trained with 1.4 trillion tokens compared to Gopher’s 300 billion tokens. Indeed, Chinchilla outperforms Gopher by 7.6% on average:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image6.png)

This implies that we shouldn’t see models larger than the 540B-parameter PaLM trained on 780B tokens for a while — it doesn’t make sense until we have 60x as much compute as was used for Gopher/Chinchilla (which is why it is surprising DeepMind let Google piss away millions of dollars in TPU time).

#### OpenAI’s 3.5B-parameter DALL·E 2

([Blog](https://openai.com/dall-e-2/), [paper](https://arxiv.org/abs/2204.06125))

Successor to the 12B-parameter [DALL·E](https://openai.com/blog/dall-e/) (an implementation of GPT-3 trained on text-image pairs from the Internet). Improvements mainly due to [algorithmic innovation](https://twitter.com/gdb/status/1528838813182730243?s=20&t=IZmLF-OeFLUjzFp8kXN6cw) (not scaling). The examples are stunning:

* [Kermit in style of different movies/TV shows](https://twitter.com/HvnsLstAngel/status/1531506455714492416)
* [Physical artwork](https://twitter.com/GuyP/status/1532774011595374595) 
* [Playing with DALL·E 2](https://www.lesswrong.com/posts/r99tazGiLgzqFX7ka/playing-with-dall-e-2)
* [What DALL-E 2 can and cannot do](https://www.lesswrong.com/posts/uKp6tBFStnsvrot5t/what-dall-e-2-can-and-cannot-do)

DALL·E 2 struggles with anime, realistic faces, text in images, multiple subjects arranged in complex ways, and editing. How many of these will be solved by throwing more compute and training data at them? The scaling curves still haven’t bent, and no one has tried diffusion models’ [scaling law](https://arxiv.org/abs/2102.09672#openai) on better hyperparameterised models like Chinchilla yet.

The text in image problem[^3] is probably due to an obscure technical detail that also plagued GPT-3 performances in rhyming, alliteration, punning, anagrams or permutations, acrostic poems, and arithmetic: the models do not see characters but ~51k word or sub-word-chunks called [byte-pair encodings](https://www.gwern.net/GPT-3#bpes) (BPEs). To breakthrough, the models just need to memorise enough of the [encrypted number/word representations](https://nostalgebraist.tumblr.com/post/620663843893493761/bpe-blues) using tricks like rewriting numbers to individual digits or BPE-dropout to expose all possible tokenizations, or better yet, character-level representations.

#### Google Brain’s ​Imagen

([Blog](https://imagen.research.google/), [paper](https://arxiv.org/abs/2205.11487)) 

Outcompetes DALL·E 2 on text-to-image [COCO](https://paperswithcode.com/sota/text-to-image-generation-on-coco) benchmark despite being smaller than DALL·E 2. The main change appears to be reducing the CLIP reliance in favour of a much larger and more powerful text encoder before doing the image diffusion stuff. They make a point of noting superiority on "compositionality, cardinality, spatial relations, long-form text, rare words, and challenging prompts." The samples also show text rendering fine inside the images. The results are stunning:

* [Imagen vs Dall·E 2](https://twitter.com/joeyliaw/status/1528856081476116480)
* [More comparisons](https://twitter.com/ak92501/status/1528860003733364737?s=20&t=dxW7EcPJJqXESxJhdAbIfg) 

What does this mean for artists? Most AI art criticism comes from a place of not realising that (almost) everyone’s favourite artists are actually curators and not manufacturers. Artists will become more like today’s art directors: people with amazing visual imagination and taste, the ability to see new things, and to help orchestrate it into existence. The net result may be a far more visual culture[^4]. (See also Oxford’s report on [AI and the Arts](https://www.oii.ox.ac.uk/wp-content/uploads/2022/03/040222-AI-and-the-Arts_FINAL.pdf))

In the US, only art created by humans, [not AI][smith], can be copyrighted.

[smith]: https://www.smithsonianmag.com/smart-news/us-copyright-office-rules-ai-art-cant-be-copyrighted-180979808/#:~:text=The%20U.S.%20Copyright%20Office%20(USCO,ruling%2C%20which%20found%20his%20A.I.

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image13.png)

When DALL·E 2 can do this to any artwork, what does it mean for copyright? 

#### DeepMind’s 1.2B-parameter Gato

([Blog](https://www.deepmind.com/publications/a-generalist-agent), [paper](https://arxiv.org/pdf/2205.06175.pdf))

Trained for a myriad of tasks like image captioning, engaging in dialogue, stacking blocks with a real robot arm, and playing Atari games, the tiny (1.2B parameters) Gato performs 450 out of 604 taks at over 50% expert score: 

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image4.png)

Scaling just works: just train a 1.2B-paramater Transformer on half a thousand different tasks and the scaling curve looks exactly like you'd expect:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image3.png)

Multi-task learning is indeed just another blessing of scale: as DeepMind notes, it used to be that learning multiple Atari games in parallel was really hard; people thought very hard and ran lots of experiments to try to create things like [Popart](https://arxiv.org/abs/1809.04474#deepmind) less than 4 years ago where it was a triumph that, due to careful engineering, a single checkpoint could play just the ALE-57 games with mediocre performance.

If one had any doubts, DeepMind is now fully scale-pilled.

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image9.png)

We live in a timeline in which the final breakthrough that precipitates AGI could plausibly be literally some one-sentence platitude about general problem-solving — [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916), Kojima et al. 2022: simply adding “Let’s think step by step” before each answer increases GPT-3 accuracy on MultiArith from 17.7% to state-of-the-art (SOTA) 78.7% and GSM8K from 10.4% to SOTA 40.7%.

## Technological Unemployment Is Already Here

[Technological unemployment](https://en.wikipedia.org/wiki/Technological_unemployment#:~:text=A%20contemporary%20example%20of%20technological,unemployment%20has%20long%20been%20controversial.) is a very complex issue. Normal people [worry](https://slatestarcodex.com/2018/02/19/technological-unemployment-much-more-than-you-wanted-to-know/) about technological unemployment.  Economists like [Bryan Caplan](https://www.econlib.org/technological-unemployment-a-self-test/), [Robin Hanson](https://www.overcomingbias.com/2009/10/take-both-econ-tech-seriously.html), [Tyler Cowen](https://marginalrevolution.com/marginalrevolution/2009/10/noah-stoffman-asks-me-two-questions.html), and [Arnold Kling](https://www.econlib.org/archives/2009/10/the_singularity.html) keep telling them to relax, but LLMs since GPT-3 should make them rethink. From [AlphaZero](https://www.deepmind.com/blog/alphazero-shedding-new-light-on-chess-shogi-and-go), we can see that there is no chance any useful man+machine combination will work together for more than a few years, as humans soon will be only a liability. Humans need not apply.

This time is different: before, the machines began handling brute force tasks and replacing things that offered only brute force and not intelligence like horses or watermills. It’s clear that the machines are now slowly absorbing intelligence — the final province of humans. Machines switched from being complements to being substitutes in some [sectors](https://www.theatlantic.com/magazine/archive/2012/01/making-it-in-america/308844/?single_page=true) a while ago. Humans need not apply.

During the various panics and busts in the past centuries, there were huge disemployment effects as companies were forced to automate, but the people were able to switch sectors or find new jobs. The trucking industry alone employs [3%](https://en.wikipedia.org/wiki/Trucking_industry_in_the_United_States#Economic_impact) of the entire American population, and how many of those employees are skilled operations research PhDs who can easily find employment elsewhere in logistics? Imagine a kid with an IQ of 70, his Ricardian comparative advantage doesn’t guarantee there’s anything worth hiring him for (even laundry has gotten [harder](http://online.wsj.com/article/SB10001424052702304410504575560552064806106.html)). Humans need not apply.

We live in a world where in some cases we would not hire someone at any price. One video of an employee spitting in customer's food can go viral and do more damage to a chain's sales than that employee would earn for the chain in a hundred years. One person in an [o-ring process](https://en.wikipedia.org/wiki/O-ring_theory_of_economic_development) can do an incredible amount of damage if they are only slightly subpar; to continue the NASA analogy, one loose bolt can cost [$135 million](https://en.wikipedia.org/wiki/NOAA-19#Damage_during_manufacture), one young inexperienced technician can cost [$200 million](http://www.russianspaceweb.com/proton_glonass49.html#culprit). We just have to calculate the expected-value of reducing the number of such incidents by even 0.01%. Humans need not apply.

## Frankfurtian Bullshit In A Post-GPT-3 World

As Sarah Constantin [writes](https://srconstantin.wordpress.com/2019/02/25/humans-who-are-not-concentrating-are-not-general-intelligences/), humans who are not concentrating are not general intelligences. Unless you make an effort to read carefully, you probably cannot detect any mistakes in GPT-3’s [nonfiction](https://www.gwern.net/GPT-3-nonfiction) upon skimming — OpenAI has achieved the ability to pass the [Turing test](https://en.wikipedia.org/wiki/Turing_test) against humans on autopilot.

As Robin Hanson [notes](https://www.overcomingbias.com/2017/03/better-babblers.html), and I don’t think he’s exaggerating, that a lot of human speech is just babbling — simply linking words and sentences statistically likely to come after the next, not unlike GPT-3. The median student learns a set of low order correlations, but if you ask an exam question probing a deep structure answer, most students give the wrong answer. These low order correlations also seem sufficient to capture most polite conversation talk (e.g. the weather is nice, how is your mother’s illness, and damn that other political party), inspirational TED talks, and when podcast guests pontificate on topics they really don’t understand (e.g. quantum mechanics, consciousness, postmodernism, or the need always for more regulation everywhere).

What unites the GPT-3 and its cousins is an unflagging enthusiasm to render whatever’s been requested, no matter how absurd or overwrought — they are fundamentally [Frankfurtian bullshitters](http://www2.csudh.edu/ccauthen/576f12/frankfurt__harry_-_on_bullshit.pdf):

> The liar cares about the truth and attempts to hide it; the bullshitter doesn’t care if what they say is true or false, but cares only whether the listener is persuaded.

As Venkatesh Rao [notes](https://twitter.com/vgr/status/1533881461979418625?s=20&t=QJE0HEBPPpj13kUH2SQ2Pw), bullshit in this epistemological sense is not a moral failure, but an incomplete cognition mode. It corresponds to the upstream part of what Daniel Dennett called the "[multiple drafts](https://en.wikipedia.org/wiki/Multiple_drafts_model#:~:text=Daniel%20Dennett's%20multiple%20drafts,Consciousness%20Explained%2C%20published%20in%201991.)" view of consciousness. First you confabulate, then you discriminate — you free-associate to produce output that has a cosmetic coherence, and then close the truth loop somehow in a downstream discrimination step before actual output. Basically, bullshitters output indiscriminately.

All presentations of AI art include the text prompt — the viewer’s pleasure is not in the image, but in the spectacle of the computer’s interpretation. Hence AI art is a genre unto itself, and the bullshit has not found its footing as “mere” art. As Robin Sloan [notes](https://www.robinsloan.com/lab/notes-on-a-genre/):

> That’s the paradox of AI art: it leverages access to the spigot of infinity to produce a sense of scarce invention. In an overstuffed audiovisual landscape, it’s the “AI” and not the “art” that provides a reason to look at this and not that, listen to this and not that.

Just as AI art has no artistic merit until OpenAI solves “taste”, [effortful thinking](https://srconstantin.wordpress.com/2017/10/10/distinctions-in-types-of-thought/) is still out of reach until OpenAI fully embodies complete cognition (the generation + discrimination production pipeline with a truth loop) in GPT-n.

Constantin again: 

> The mental motion of “I didn’t really parse that paragraph, but sure, whatever, I’ll take the author’s word for it” is, in my introspective experience, absolutely identical to “I didn’t really parse that paragraph because it was bot-generated and didn’t make any sense so I couldn’t possibly have parsed it”, except that in the first case, I assume that the error lies with me rather than the text.  This is not a safe assumption in a post-GPT2 world. Instead of “default to humility” (assume that when you don’t understand a passage, the passage is true and you’re just missing something) the ideal mental action in a world full of bots is “default to null” (if you don’t understand a passage, assume you’re in the same epistemic state as if you’d never read it at all.)

## The Singularity Is Nigh

In _[The Precipice](https://www.goodreads.com/en/book/show/50485582-the-precipice)_, the definitive book on existential risks, Toby Ord ranks unaligned artificial intelligence as _the_ greatest risk to humanity’s potential in the next century. 

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image2.png)

Ord explains the high number for such a speculative risk:

> A common approach to estimating the chance of an unprecedented event with earth-shaking consequences is to take a sceptical stance: to start with an extremely small probability and only raise it from there when a large amount of hard evidence is presented. But I disagree. Instead, I think that the right method is to start with a probability that reflects our overall impressions, then adjust this in light of the scientific evidence. When there is a lot of evidence, these approaches converge. But when there isn’t, the starting point can matter.

> In the case of artificial intelligence, everyone agrees the evidence and arguments are far from watertight, but the question is where does this leave us? Very roughly, my approach is to start with the overall view of the expert community that there is something like a 1 in 2 chance that AI agents capable of outperforming humans in almost every task will be developed in the coming century. And conditional on that happening, we shouldn’t be shocked if these agents that outperform us across the board were to inherit our future.

Read Gwern’s (fictional) [It Looks Like You're Trying To Take Over The World](https://www.gwern.net/fiction/Clippy) to imagine a [hard takeoff](https://en.wikipedia.org/wiki/Technological_singularity#Hard_vs._soft_takeoff) scenario using solely known sorts of NN and ⁠scaling effects. Then read [AGI Ruin: A List of Lethalities](https://www.lesswrong.com/posts/uMQ3cqWDPHhjtiesc/agi-ruin-a-list-of-lethalities) in which Eliezer Yudkowsky, for the first time publicly, explains what he spent the last several years doing (and he is pessimistic).

Richard Ngo on [AGI safety from first principles](https://www.alignmentforum.org/s/mzgtmmTKKn5MuCzFJ/p/8xRSjC76HasLnMGSf):

1. We’ll build AIs which are much more intelligent than humans; that is, much better than humans at using generalisable cognitive skills to understand the world.
2. Those AGIs will be autonomous agents which pursue long-term, large-scale goals, because goal-directedness is reinforced in many training environments, and because those goals will sometimes generalise to be larger in scope.
3. Those goals will by default be misaligned with what we want, because our desires are complex and nuanced, and our existing tools for shaping the goals of AIs are inadequate.
4. The development of autonomous misaligned AGIs would lead to them gaining control of humanity’s future, via their superhuman intelligence, technology and coordination - depending on the speed of AI development, the transparency of AI systems, how constrained they are during deployment, and how well humans can cooperate politically and economically. 

What are some concrete problems in AI safety? Fom [Amodei et al. 2016](https://arxiv.org/abs/1606.06565), take a robot that cleans up messes in an office using common cleaning tools as an example:

1. Avoiding negative side effects (e.g. ensure robot doesn’t knock over vase to clean faster without manually specifying everything it shouldn’t disturb)
2. Avoiding reward hacking (e.g. ensure robot doesn’t disable its vision so it won’t find any mess while rewarding it for a mess-free environment)
3. Scalable oversight (e.g. ensure robot doesn’t throw away phone but does candy wrapper without having to ask the humans every time)
4. Safe exploration (e.g. ensure robot doesn’t put a wet mop in an electrical outlet while allowing it to experiment with mopping strategies)
5. Robustness to distributional shift (e.g. ensure robot learns that its cleaning strategies for an office might be dangerous on a factory workfloor)

The explainable ML community and AI safety is nowadays an eminently empirical field centred around understanding the kinds of models, like transformers, that seem promising, and trying to devise new ways to train them that lead to desired behaviours, for example [trying to get language models to output benign completions to a given prompt](https://www.alignmentforum.org/posts/k7oxdbNaGATZbtEg3/redwood-research-s-current-project). There's more tool building, more concrete tractable problems and less theorising about arbitrarily general intelligent systems.

#### AI timeline

[Is AI Progress Impossible To Predict?](https://www.lesswrong.com/posts/G993PFTwqqdQv4eTg/is-ai-progress-impossible-to-predict) AI has improved on a task recently gives us exactly _zero_ predictive power for how much the next model will improve on the same task. Moore’s Law giveth, [Platt’s Law](https://archive.nytimes.com/www.nytimes.com/library/cyber/surf/1120surf-vinge.html) taketh away: any AI forecast will forecast strong AI to be 30 years out:

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image5.png)

_[Platt’s Law in blue, OLS regression line in orange; the median forecast is 25 years out.](https://www.lesswrong.com/posts/nNqXfnjiezYukiMJi/reply-to-eliezer-on-biological-anchors?commentId=zJ8EGJ3cHdeyjQZvc)_

Nevertheless, the average 50% prediction clusters around 2040-60. Holden Karnofsky predicts more than a 10% chance of [PASTA](https://www.cold-takes.com/transformative-ai-timelines-part-1-of-4-what-kind-of-ai/) (Process for Automating Scientific and Technological Advancement) transformative AI (see also [burden of proof](https://www.cold-takes.com/forecasting-transformative-ai-whats-the-burden-of-proof/) and [where the arguments and “experts” stand](https://www.cold-takes.com/where-ai-forecasting-stands-today/)) : >10% probability by 2036; a 50% by 2060; and a 66% by 2100.

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image16.png)

_[Bio Anchors assumes transformative AI would be 10x the size of the human brain; GPT-3 is only 0.1% as big.](https://www.cold-takes.com/forecasting-transformative-ai-the-biological-anchors-method-in-a-nutshell/)_

* OpenPhil’s [Report on Semi-informative Priors](https://www.openphilanthropy.org/blog/report-semi-informative-priors) predicts: 8% by 2036; 13% by 2060; 20% by 2100
* [Grace et al. 2018](https://arxiv.org/pdf/1705.08807.pdf) surveyed 352 AI researchers at the 2015 NIPS and ICML (_the_ premier) conferences: 20% probability by 2036; 50% by 2060; 70% by 2100.
* [Richard Sutton](https://twitter.com/ethanCaballero/status/1529907226630049808?s=20&t=KEGemFAm5lJFM7paiVw7mQ) of _[The Bitter Lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html)_ fame predicts 50% probability of Human-Level AI by 2040.
* Ajeya Cotra’s [Report on Biological Anchors](https://drive.google.com/drive/u/1/folders/15ArhEPZSTYU8f012bs6ehPS6-xmhtBPP) (summaries by [Scott Alexander](https://astralcodexten.substack.com/p/biological-anchors-a-trick-that-might?s=r), [Holden Karnofsky](https://www.cold-takes.com/forecasting-transformative-ai-the-biological-anchors-method-in-a-nutshell/), [Rohin Shah](https://www.lesswrong.com/posts/KrJfoZzpSDpnrv9va/draft-report-on-ai-timelines?commentId=7d4q79ntst6ryaxWD))” predicting arrival of [transformative AI](https://www.openphilanthropy.org/blog/some-background-our-views-regarding-advanced-artificial-intelligence#Sec1): >10% probability by 2036; 50% chance by 2055; 80% chance by 2100

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image15.png)

 _FLOPs alone turn the wheel of history._

[Metaculus](https://www.metaculus.com/questions/5121/date-of-general-ai/): 

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image14.png)

Cotra’s report reminds [Scott Alexander](https://astralcodexten.substack.com/p/biological-anchors-a-trick-that-might?s=r) of an old joke:

> An astronomy professor says that the sun will explode in five billion years, and sees a student visibly freaking out. She asks the student what’s so scary about the sun exploding in five billion years. The student sighs with relief: “Oh, thank God! I thought you’d said five _million_ years!”

> You can imagine the opposite joke: A professor says the sun will explode in five minutes, sees a student visibly freaking out, and repeats her claim. The student, visibly relieved: “Oh, thank God! I thought you’d said five _seconds_.”

In all the AGI timeline predictions, the professor is saying the sun will explode in five minutes instead of five seconds. Compared to the alternative, it’s good news. But if it makes you feel complacent, then the joke’s on you.

## Conclusion

As [Kaplan](https://twitter.com/russelljkaplan/status/1513128007434530818?s=20&t=wUFpVKKFqOCtX3t8BwdevA) notes, all products for creators will have embedded intelligence from LLMs (Copilot in VSCode,  DALL·E 2 in Photoshop, GPT-3 in Google Docs); these companies will need to roll their own LLMs or pay a tax to OpenAI/DeepMind/Google.

If you actually believe in AI risk, you should vote with your feet and [work on AI safety](https://forum.effectivealtruism.org/posts/7WXPkpqKGKewAymJf/how-to-pursue-a-career-in-technical-ai-alignment). If you don’t, you should still pivot your career to work on AI as every successful tech company will use their data moats to build some variant of AGI. 

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image20.png)

_[All tech problems are ultimately AGI-complete.](https://evjang.com/2022/04/25/rome.html)_

It is up to _you_ to immanentize the eschaton.

## Additional Readings

ML Intro

* Jay Alammar: [A Visual and Interactive Guide to the Basics of Neural Networks](https://jalammar.github.io/visual-interactive-guide-basics-neural-networks/)
* [Machine Learning for Everyone](https://vas3k.com/blog/machine_learning/)
* Google AI: [education](https://ai.google/education/)
* [A Neural Network in 11 lines of Python part 1](https://iamtrask.github.io/2015/07/12/basic-python-network/), [part 2](https://iamtrask.github.io/2015/07/27/python-network-part2/)
* [Beginner's Guide to Understanding CNN](https://adeshpande3.github.io/adeshpande3.github.io/A-Beginner%27s-Guide-To-Understanding-Convolutional-Neural-Networks/)
* Jason Mayes: [Machine Learning 101 (deck)](https://docs.google.com/presentation/d/1kSuQyW5DTnkVaZEjGYCkfOxvzCqGEFzWBy4e9Uedd9k/preview?imm_mid=0f9b7e&cmp=em-data-na-na-newsltr_20171213&slide=id.g168a3288f7_0_58)

ML Books

* Michael Nielsen: [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/chap1.html)
* Ian Goodfellow: [Deep Learning Book](https://www.deeplearningbook.org/)
* [Maths Basics for Computer Science and Machine Learning](http://www.cis.upenn.edu/~jean/math-basics.pdf)
* [Grokking Deep Learning](https://www.manning.com/books/grokking-deep-learning?a_aid=grokkingdl&a_bid=32715258)
* [Introduction to Machine Learning Interviews](https://huyenchip.com/ml-interviews-book/)
* [Top Machine Learning Books recommended by experts (2022 Edition)](https://mentorcruise.com/books/ml/)

ML Courses

* Andrew Ng: [Stanford ML Syllabus](http://cs229.stanford.edu/syllabus.html), [Coursera](https://www.coursera.org/learn/machine-learning), [Python assignments](https://github.com/dibgerge/ml-coursera-python-assignments)
* deeplearning.ai: [Deep Learning](https://www.coursera.org/specializations/deep-learning#howItWorks)
* Stanford: [CS231n Convolutional Neural Networks for Visual Recognition](https://cs231n.github.io/)
* Stanford: [CS229 Problem Set Solutions](https://github.com/zhixuan-lin/cs229-ps-2018)
* MIT: [6.S191: Introduction to Deep Learning](https://www.youtube.com/playlist?list=PLtBw6njQRU-rwp5__7C0oIVt26ZgjG9NI) 
* FastAI: [Practical Deep Learning for Coders](https://course.fast.ai/) 
* Yann leCun: [Deep Learning](https://atcold.github.io/NYU-DLSP21/)
* Durham: [Deep Learning Lectures](https://www.youtube.com/playlist?list=PLMsTLcO6etti_SObSLvk9ZNvoS_0yia57)<span style="text-decoration:underline;"> </span>
* Hugging Face: [Deep Reinforcement Learning Class](https://github.com/huggingface/deep-rl-class)
* OpenAI: [Spinning Up in Deep RL](https://openai.com/blog/spinning-up-in-deep-rl/)
* Amazon: [Machine Learning University](https://github.com/aws-samples/aws-machine-learning-university-accelerated-nlp)
* Kaggle: [How Models Work](https://www.kaggle.com/dansbecker/how-models-work)
* Kaggle: [Train Model with TensorFlow Cloud](https://www.kaggle.com/rosebv/train-model-with-tensorflow-cloud)  
* [ML Basics in plain Python](https://github.com/zotroneneis/machine_learning_basics)
* [Full Stack Deep Learning](https://course.fullstackdeeplearning.com/)
* Google: [Machine Learning Crash Course with TensorFlow APIs](https://developers.google.com/machine-learning/crash-course/?authuser=0) 
* Google: [TensorFlow, Keras and deep learning, without a PhD](https://codelabs.developers.google.com/codelabs/cloud-tensorflow-mnist/?authuser=0#0)
* Google: [650k+ datasets, 150+ notebooks](https://aihub.cloud.google.com/u/0/)
* [In-depth introduction to machine learning in 15 hours of expert videos](https://www.r-bloggers.com/in-depth-introduction-to-machine-learning-in-15-hours-of-expert-videos/)
* MIT: [Deep Learning in Life Sciences (Spring 2021](https://www.youtube.com/playlist?list=PLypiXJdtIca5sxV7aE3-PS9fYX3vUdIOX)) 
* Deep Learning Course Forums: [Recommended Python learning resources (2019)](https://forums.fast.ai/t/recommended-python-learning-resources/26888)
* KDNuggets [Best Resources to Learn Natural Language Processing in 2021](https://www.kdnuggets.com/2021/09/best-resources-learn-natural-language-processing-2021.html) 
* [Machine Learning and Deep Learning Courses](https://elvissaravia.substack.com/p/machine-learning-and-deep-learning)
* Wiki of courses: [drizzle](https://deep-learning-drizzle.github.io/)

ML Resources

* Keras: [Code examples](https://keras.io/examples/)
* [Curated list of references for MLOps](https://github.com/visenger/awesome-mlops) 
* [Datasets for Machine Learning and Deep Learning](https://sebastianraschka.com/blog/2021/ml-dl-datasets.html)
* Towards Data Science: [Linear algebra cheat sheet for deep learning](https://towardsdatascience.com/linear-algebra-cheat-sheet-for-deep-learning-cd67aba4526c) 
* TensorFlow Quantum: [library for hybrid quantum-classical machine learning](https://www.tensorflow.org/quantum)  

ML Research:
* [Annotated Research Papers](https://github.com/AakashKumarNain/annotated_research_papers)
* [Papers With Code](https://paperswithcode.com/sota) and [Methods](https://paperswithcode.com/methods)
* [Computer Science Open Data](https://jeffhuang.com/computer-science-open-data/) (for PhD application)
* Eric Jang: [How to Understand ML Papers Quickly](https://evjang.com/2021/01/25/understanding-ml.html) 
* John Schulman: [An Opinionated Guide to ML Research](http://joschu.net/blog/opinionated-guide-ml-research.html)
* Tom Silver: [Lessons from My First Two Years of AI Research](https://web.mit.edu/tslvr/www/lessons_two_years.html)
* Chris Albon: [Notes On Using Data Science & Machine Learning To Fight For Things That Matter](https://chrisalbon.com/)
* [Facebook AI's full logbook for training OPT-175B](https://github.com/facebookresearch/metaseq/tree/main/projects/OPT/chronicles) 
* [From Statistical to Causal Learning](https://arxiv.org/abs/2204.00607), Schölkopf et al. 2022
* [The worst of both worlds: A comparative analysis of errors in learning from data in psychology and machine learning](http://users.eecs.northwestern.edu/~jhullman/AIES22Learning_errors_in_psych_and_ML.pdf), Hullman et al. 2022

![](/images/2022-06-05-AGI-Scale-Is-All-You-Need/image18.png)

 _Replication crisis in ML research._


Transformers

* [Attention Is All You Need](https://arxiv.org/abs/1706.03762), Vaswani et al. 2017
* [Transformers for software engineers](https://blog.nelhage.com/post/transformers-for-software-engineers/)
* Jay Alammar: [Visualizing A Neural Machine Translation Model](https://jalammar.github.io/visualizing-neural-machine-translation-mechanics-of-seq2seq-models-with-attention/), [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/), and [How GPT-3 Works](https://jalammar.github.io/how-gpt3-works-visualizations-animations/)
* [One Model To Learn Them All](https://arxiv.org/abs/1706.05137), Kaiser et al. 2017
* [Image Transformer](https://arxiv.org/abs/1802.05751), Parmar et al. 2018
* [Language Models are Few-Shot Learners](https://arxiv.org/pdf/2005.14165.pdf), Brown et al. 2020
* [Offline Pre-trained Multi-Agent Decision Transformer: One Big Sequence Model Tackles All SMAC Tasks](https://arxiv.org/abs/2112.02845), Meng et al. 2021
* [µTransfer: A technique for hyperparameter tuning of enormous neural networks](https://www.microsoft.com/en-us/research/blog/%c2%b5transfer-a-technique-for-hyperparameter-tuning-of-enormous-neural-networks/) ([paper](https://www.microsoft.com/en-us/research/publication/tuning-large-neural-networks-via-zero-shot-hyperparameter-transfer/)) 
* [FlashAttention](https://twitter.com/tri_dao/status/1531437619791290369) ([paper](https://arxiv.org/abs/2205.14135)): 2-4x faster and requires 5-20x less memory than PyTorch standard attention by making attention algorithm IO-aware i.e. accounting for reads and writes between levels of GPU memory like large but (relatively) slow high-bandwidth memory (HBM) vs small but fast SRAM
* [Least-to-Most Prompting Enables Complex Reasoning in Large Language Models](https://arxiv.org/abs/2205.10625), Zhou et al. 2022
* DeepMind’s [AlphaCode](https://www.lesswrong.com/posts/ZmxkmCjXJBpwJkgrw/competitive-programming-with-alphacode) ([paper](https://arxiv.org/abs/2203.07814)) 
* Nvidia: [Improving Diffusion Models as an Alternative To GANs](https://developer.nvidia.com/blog/improving-diffusion-models-as-an-alternative-to-gans-part-1/) and [Part 2 ](https://developer.nvidia.com/blog/improving-diffusion-models-as-an-alternative-to-gans-part-2/)
* Google Brain’s CLIP competitor: [CoCa: Contrastive Captioners are Image-Text Foundation Models](https://arxiv.org/abs/2205.01917), Yu et al. 2022 
* [Probing Vision Transformers](https://github.com/sayakpaul/probing-vits/) 
* Book: [The Principles of Deep Learning Theory](https://arxiv.org/abs/2106.10165), Roberts et al. 2021

Interpretability research

* [A Mathematical Framework for Transformer Circuits](https://transformer-circuits.pub/2021/framework/index.html), Elhage et al. 2021 
* [In-context Learning and Induction Heads](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html), Olsson et al. 2022
* [Attention and Augmented Recurrent Neural Networks](https://distill.pub/2016/augmented-rnns/), Olah et al. 2016 
* [Research Debt](https://distill.pub/2017/research-debt/), Olah et al. 2017
* [Feature Visualization](https://distill.pub/2017/feature-visualization/), Olah et al. 2017 
* [The Building Blocks of Interpretability](https://distill.pub/2018/building-blocks/), Olah et al. 2018

Implicit meta-learning

* [One-shot Learning with Memory-Augmented Neural Networks](https://www.gwern.net/docs/www/arxiv.org/50d160a8f07248e8eafabde96cdcff2873eca47c.pdf#deepmind), Santoro et al. 2016 
* [AI-GAs: AI-generating algorithms, an alternate paradigm for producing general artificial intelligence](https://www.gwern.net/docs/www/arxiv.org/8fea76b2ff6379b574b6f1eb348db27c7b0203f5.pdf#uber), Clune et al. 2020
* [On Learning to Think: Algorithmic Information Theory for Novel Combinations of Reinforcement Learning Controllers and Recurrent Neural World Models](https://www.gwern.net/docs/www/arxiv.org/b85a4e82b077f63433d9694332c2407e7e0f9e02.pdf), Schmidhuber 2015  
* Lilian Weng on [Meta-Learning: Learning to Learn Fast](https://www.gwern.net/docs/www/lilianweng.github.io/1a0416d7e2ddbb8b7e715e1ba46ba56c5c95e34d.html#openai) and [Meta Reinforcement Learning](https://www.gwern.net/docs/www/lilianweng.github.io/cd77384c87df9718ec5d6f7ce2f7180f3b6e072b.html#openai) 

ML Scaling

* ​​[Understanding the generalization of 'lottery tickets' in neural networks](https://ai.facebook.com/blog/understanding-the-generalization-of-lottery-tickets-in-neural-networks/), Morcos et al. 2019
* [Bayesian Deep Learning and a Probabilistic Perspective of Generalization](https://www.gwern.net/docs/www/arxiv.org/aea56633ef88d71aadfb45b62bb1a218cda38102.pdf), Wilson et al. 2020
* [On Linear Identifiability of Learned Representations](https://www.gwern.net/docs/www/arxiv.org/98ad3320bdb3cbab2681220ed6b4dc44c455f14d.pdf#google), Roeder et al. 2020
* [Logarithmic Pruning is All You Need](https://www.gwern.net/docs/www/arxiv.org/30ce90addac851033c6e3521cc4ca59d43093066.pdf#deepmind), Orseau et al. 2020
* [Direct Fit to Nature: An Evolutionary Perspective on Biological and Artificial Neural Networks](https://www.gwern.net/docs/ai/scaling/2020-hasson.pdf), Hasson et al. 2020
* [The Shape of Learning Curves: a Review](https://www.gwern.net/docs/www/arxiv.org/658b4a13863e88e856c6cfcf686a5e9eb01776b3.pdf#page=22), Viering et al. 2021
* Nostalgebraist: [larger language models may disappoint you](https://www.lesswrong.com/posts/pv7Qpu8WSge8NRbpB/larger-language-models-may-disappoint-you-or-an-eternally)

Neuroscience

* [The Brain as a Universal Learning Machine](https://www.lesswrong.com/posts/9Yc7Pp7szcjPgPsjf/the-brain-as-a-universal-learning-machine) 
* [The remarkable, yet not extraordinary, human brain as a scaled-up primate brain and its associated cost](https://www.gwern.net/docs/psychology/neuroscience/2012-herculanohouzel.pdf), Herculano-Houzel et al. 2012 
* [Prefrontal cortex as a meta-reinforcement learning system](https://www.gwern.net/docs/reinforcement-learning/meta-learning/2018-wang.pdf#deepmind), Wang et al. 2018
* [Reinforcement Learning, Fast and Slow](https://www.cell.com/trends/cognitive-sciences/fulltext/S1364-6613(19)30061-0#deepmind), Botvinick et al. 2019  

AI Safety

* [How to pursue a career in technical AI alignment](https://forum.effectivealtruism.org/posts/7WXPkpqKGKewAymJf/how-to-pursue-a-career-in-technical-ai-alignment)
* OpenPhil: [Some Background on Our Views Regarding Advanced Artificial Intelligence](https://www.openphilanthropy.org/blog/some-background-our-views-regarding-advanced-artificial-intelligence), [Potential Risks from Advanced Artificial Intelligence: The Philanthropic Opportunity](https://www.openphilanthropy.org/blog/potential-risks-advanced-artificial-intelligence-philanthropic-opportunity), [What Do We Know about AI Timelines?](https://www.openphilanthropy.org/focus/global-catastrophic-risks/potential-risks-advanced-artificial-intelligence/ai-timelines), and [How Much Computational Power Does It Take to Match the Human Brain?](https://www.openphilanthropy.org/brain-computation-report)
* Future of Life Institute: ​​[AI Governance: A Research Agenda](https://www.fhi.ox.ac.uk/wp-content/uploads/GovAI-Agenda.pdf)
* Machine Intelligence Research Institute: [Agent Foundations for Aligning Machine Intelligence with Human Interests: A Technical Research Agenda](https://intelligence.org/technical-agenda/)  
* DeepMind: [Building safe artificial intelligence: specification, robustness, and assurance](https://deepmindsafetyresearch.medium.com/building-safe-artificial-intelligence-52f5f75058f1) 
* OpenAI: [Aligning Language Models to Follow Instructions](https://openai.com/blog/instruction-following/) ([paper](https://arxiv.org/abs/2203.02155)) and [Learning from Human Preferences](https://openai.com/blog/deep-reinforcement-learning-from-human-preferences/) 
* Paul Christiano: [Current work in AI alignment](https://forum.effectivealtruism.org/posts/63stBTw3WAW6k45dY/paul-christiano-current-work-in-ai-alignment) ([video](https://youtu.be/-vsYtevJ2bc))
* Alex Flint: [AI Risk for Epistemic Minimalists](https://www.alignmentforum.org/posts/8fpzBHt7e6n7Qjoo9/ai-risk-for-epistemic-minimalists)
* Rohin Shah: [FAQ: Advice for AI alignment researchers](https://rohinshah.com/faq-career-advice-for-ai-alignment-researchers/) 
* Thane Ruthenis: [Reshaping the AI Industry](https://www.lesswrong.com/posts/mF8dkhZF9hAuLHXaD/reshaping-the-ai-industry)
* Victoria Krakovna: [specification gaming examples in AI](https://docs.google.com/spreadsheets/d/e/2PACX-1vRPiprOaC3HsCf5Tuum8bRfzYUiKLRqJmbOoC-32JorNdfyTiRRsR7Ea5eWtvsWzuxo8bjOxCG84dAg/pubhtml) 
* Scott Alexander: [Practically-A-Book Review: Yudkowsky Contra Ngo On Agents](https://astralcodexten.substack.com/p/practically-a-book-review-yudkowsky?s=r) 
* Zvi: [Attempted Gears Analysis of AGI Intervention Discussion With Eliezer](https://www.lesswrong.com/posts/xHnuX42WNZ9hq53bz/attempted-gears-analysis-of-agi-intervention-discussion-with-1) 
* Gwern: [Why Tool AIs Want to Be Agent AIs](https://www.gwern.net/Tool-AI) and [Complexity no Bar to AI](https://www.gwern.net/Complexity-vs-AI) 
* [The Ethics of Artificial Intelligence](https://nickbostrom.com/ethics/artificial-intelligence.pdf), Bostrom et al. 2011
* [AGI Safety Literature Review](https://arxiv.org/pdf/1805.01109.pdf), Everitt et al. 2018 
* [Unsolved Problems in ML Safety](https://arxiv.org/pdf/2109.13916.pdf), Hendrycks et al. 2022
* [An overview of 11 proposals for building safe advanced AI](https://arxiv.org/abs/2012.07532), Hubinger 2020

List of lists on AI safety

* Victoria Krakovna: regularly updated [AI safety resource](https://vkrakovna.wordpress.com/ai-safety-resources/)
* 80,000 Hours: [AI safety syllabus](https://80000hours.org/articles/ai-safety-syllabus/) 
* Future of Life Institute: ​​[Benefits & Risks of Artificial Intelligence](https://futureoflife.org/background/benefits-risks-of-artificial-intelligence/) 
* Lark: annual [AI Alignment Literature Review and Charity Comparison](https://www.lesswrong.com/posts/C4tR3BEpuWviT7Sje/2021-ai-alignment-literature-review-and-charity-comparison)
* Richard Ngo: [Paul Christiano's writings](https://forum.effectivealtruism.org/posts/wfvAgFgdJEf9w7ZFb/ea-reading-list-paul-christiano) 
* Steve Byrnes: [AGI safety](https://sjbyrnes.com/agi.html) 
* Rohin Shah: [Alignment Newsletter](https://rohinshah.com/alignment-newsletter/)

For updates and links on narrow AI, [subscribe](https://subcriticalappraisal.substack.com/) to my monthly newsletter ([archive](https://subcriticalappraisal.com/newsletters/)).

## Endnotes

[^1]: Markov chain & n-gram models start to fall behind; they can memorize increasingly large chunks of the training corpus, but they can’t solve increasingly critical syntactic tasks like balancing parentheses or quotes, much less start to ascend from syntax to semantics.

[^2]: As Hofstadter puts it, capabilities must disintegrate — if you successfully reduce "human reasoning", it must be to un-reasoning atoms, not to little reasoning homunculi; or as Gwern likes to say: AI succeeds not when you anthropomorphize models, but unanthropomorphize humans.

[^3]: DALL·E 2 results have been so stunning that some mistake the gibberish to be a [secret language](https://twitter.com/benjamin_hilton/status/1531780892972175361); we’re genuinely seeing some kind of AI astrology emerge in real time.

[^4]: With 2D images solved by AI, are we following the footsteps of image/sound recording: photography -> silent movie -> movies with sound?
