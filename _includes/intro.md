<h1 class="no-numbering" id="intro">导言</h1>

旨在作为一本手册，帮助学习现代AI系统的关键概念。鉴于AI领域最近的迅猛发展，目前也还没有出比较完善的能紧跟LLMs(巨型语言模型)等生成式AI模型最新进展的教科书。当然，网上已经有很多这方面的好资料了，比如博客文章和视频等，只是都散落各处。我的目标就是把这些"最佳"的资料串起来，形成一本教科书的样子，作为各位在AI学习时的Roadmap。我希望这本书是"活"的书，也就是后面有新突破、新范式时，本书也会更新，如果能得到社区的输入和贡献就更理想了。本书面向的是有一定技术背景的、对AI感兴趣的以及希望从事这一方向的同学们。这需要同学们有一定的编程经验，同时高中数学还没忘记，当然这些前置条件不具备的话，我也会给一份如何填补的指引。如果你觉得本书需要添加某一块的内容，也请告知！(译者注：当下国内特别喜欢"大模型"这些媒体用语，还造出对应的英文叫"Big Model"，既然有"大模型"就对应有"小模型"，为了不落“大”与“小”的俗套，特此更正为"巨型语言模型"！)

<h2 class="no-numbering no-toc">The AI Landscape</h2>

截至2024年6月，石破天惊的[ChatGPT](http://chat.openai.com)已经发布整整18个月了，全世界都在讨论AI。 [Meta](https://llama.meta.com/)和[Google](https://gemini.google.com/)这些科技巨头都发布了自己的模型，[Mistral](https://mistral.ai/)和[Anthropic](https://www.anthropic.com/)这些新兴的AI公司也不甘人后，无数的初创公司拿着这些模型API来做AI应用，无数的人在疯抢[scrambling](https://finance.yahoo.com/news/customer-demand-nvidia-chips-far-013826675.html)Nvidia的GPU，无数的AI相关论文发在了[ArXiv](https://arxiv.org/list/cs.AI/recent)上， at a breakneck pace, demos circulate of [physical robots](https://www.figure.ai/) and [artificial programmers](https://www.cognition-labs.com/introducing-devin) powered by LLMs, and it seems like [chatbots](https://www.businessinsider.com/chat-gpt-effect-will-likely-mean-more-ai-chatbots-apps-2023-2) are finding their way into all aspects of online life (to varying degrees of success). In parallel to the LLM race, there’s been rapid development in image generation via diffusion models; [DALL-E](https://openai.com/dall-e-3) and [Midjourney](https://www.midjourney.com/showcase) are displaying increasingly impressive results that often stump humans on social media, and with the progress from [Sora](https://openai.com/sora), [Runway](https://runwayml.com/), and [Pika](https://pika.art/home), it seems like high-quality video generation is right around the corner as well. There are ongoing debates about when “AGI” will arrive, what “AGI” even means, the merits of open vs. closed models, value alignment, superintelligence, existential risk, fake news, and the future of the economy. Many are concerned about jobs being lost to automation, or excited about the progress that automation might drive. And the world keeps moving: chips get faster, data centers get bigger, models get smarter, contexts get longer, abilities are augmented with tools and vision, and it’s not totally clear where this is all headed. If you’re following “AI news” in 2024, it can often feel like there’s some kind of big new breakthrough happening on a near-daily basis. It’s a lot to keep up with, especially if you’re just tuning in.

With progress happening so quickly, a natural inclination by those seeking to “get in on the action” is to pick up the latest-and-greatest available tools (likely [GPT-4o](https://openai.com/index/hello-gpt-4o/), [Gemini 1.5 Pro](https://deepmind.google/technologies/gemini/pro/), or [Claude 3 Opus](https://www.anthropic.com/news/claude-3-family) as of this writing, depending on who you ask) and try to build a website or application on top of them. There’s certainly a lot of room for this, but these tools will change quickly, and having a solid understanding of the underlying fundamentals will make it much easier to get the most out of your tools, pick up new tools quickly as they’re introduced, and evaluate tradeoffs for things like cost, performance, speed, modularity, and flexibility. Further, innovation isn’t only happening at the application layer, and companies like [Hugging Face](https://huggingface.co/), [Scale AI](https://scale.com/), and [Together AI](https://www.together.ai/) have gained footholds by focusing on inference, training, and tooling for open-weights models (among other things). Whether you’re looking to get involved in open-source development, work on fundamental research, or leverage LLMs in settings where costs or privacy concerns preclude outside API usage, it helps to understand how these things work under the hood in order to debug or modify them as needed. From a broader career perspective, a lot of current “AI/ML Engineer” roles will value nuts-and-bolts knowledge in addition to high-level frameworks, just as “Data Scientist” roles have typically sought a strong grasp on theory and fundamentals over proficiency in the ML framework *du jour*. Diving deep is the harder path, but I think it’s a worthwhile one. But with the pace at which innovation has occurred over the past few years, where should you start? Which topics are essential, what order should you learn them in, and which ones can you skim or skip? 

<h2 class="no-numbering no-toc">The Content Landscape</h2>

Textbooks are great for providing a high-level roadmap of fields where the set of “key ideas” is more stable, but as far as I can tell, there really isn’t a publicly available post-ChatGPT “guide to AI” with textbook-style comprehensiveness or organization. It’s not clear that it would even make sense for someone to write a traditional textbook covering the current state of AI right now; many key ideas (e.g. QLoRA, DPO, vLLM) are no more than a year old, and the field will likely have changed dramatically by the time it’d get to print. The oft-referenced [Deep Learning](https://www.deeplearningbook.org/) book (Goodfellow et al.) is almost a decade old at this point, and has only a cursory mention of language modeling via RNNs. The newer [Dive into Deep Learning](http://d2l.ai) book includes coverage up to Transformer architectures and fine-tuning for BERT models, but topics like RLHF and RAG (which are "old" by the standards of some of the more bleeding-edge topics we'll touch on) are missing. The upcoming [“Hands-On Large Language Models”](https://www.oreilly.com/library/view/hands-on-large-language/9781098150952/) book might be nice, but it’s not officially published yet (available online behind a paywall now) and presumably won’t be free when it is. The Stanford [CS224n](https://web.stanford.edu/class/cs224n/index.html#coursework) course seems great if you’re a student there, but without a login you’re limited to slide-decks and a reading list consisting mostly of dense academic papers. Microsoft's ["Generative AI for Beginners"](https://microsoft.github.io/generative-ai-for-beginners/#/) guide is fairly solid for getting your hands dirty with popular frameworks, but it's more focused on applications rather than understanding the fundamentals.

The closest resource I'm aware of to what I have in mind is Maxime Labonne's [LLM Course](https://github.com/mlabonne/llm-course) on Github. It features many interactive code notebooks, as well as links to sources for learning the underlying concepts, several of which overlap with what I'll be including here. I'd recommend it as a primary companion guide while working through this handbook, especially if you're interested in applications; this document doesn't include notebooks, but the scope of topics I'm covering is a bit broader, including some research threads which aren't quite "standard" as well as multimodal models.

Still, there's an abundance of other high-quality and accessible content which covers the latest advances in AI --- it’s just not all organized. The best resources for quickly learning about new innovations are often one-off blog posts or YouTube videos (as well as Twitter/X threads, Discord servers, and discussions on Reddit and LessWrong). My goal with this document is to give a roadmap for navigating all of this content, organized into a textbook-style presentation without reinventing the wheel on individual explainers. Throughout, I’ll include multiple styles of content where possible (e.g. videos, blogs, and papers), as well as my opinions on goal-dependent knowledge prioritization and notes on “mental models” I found useful when first encountering these topics.

I’m creating this document **not** as a “generative AI expert”, but rather as someone who’s recently had the experience of ramping up on many of these topics in a short time frame. While I’ve been working in and around AI since 2016 or so (if we count an internship project running evaluations for vision models as the “start”), I only started paying close attention to LLM developments 18 months ago, with the release of ChatGPT. I first started working with open-weights LLMs around 12 months ago. As such, I’ve spent a lot of the past year sifting through blog posts and papers and videos in search of the gems; this document is hopefully a more direct version of that path. It also serves as a distillation of many conversations I’ve had with friends, where we’ve tried to find and share useful intuitions for grokking complex topics in order to expedite each other’s learning. Compiling this has been a great forcing function for filling in gaps in my own understanding as well; I didn’t know how FlashAttention worked until a couple weeks ago, and I still don’t think that I really understand state-space models that well. But I know a lot more than when I started.


<h2 class="no-numbering no-toc">Resources</h2>

Some of the sources we’ll draw from are:   

- Blogs:
    - [Hugging Face](https://huggingface.co/blog) blog posts
    - [Chip Huyen](https://huyenchip.com/blog/)’s blog
    - [Lilian Weng](https://lilianweng.github.io/)’s blog
    - [Tim Dettmers](https://timdettmers.com/)’ blog
    - [Towards Data Science](https://towardsdatascience.com/)
    - [Andrej Karpathy](https://karpathy.github.io/)'s blog
    - Sebastian Raschka’s [“Ahead of AI”](https://magazine.sebastianraschka.com/) blog
- YouTube:
    - Andrej Karpathy’s [“Zero to Hero”](https://karpathy.ai/zero-to-hero.html) videos
    - [3Blue1Brown](https://www.youtube.com/c/3blue1brown) videos
    - Mutual Information
    - StatQuest
- Textbooks
    - The [d2l.ai](http://d2l.ai) interactive textbook
    - The [Deep Learning](https://www.deeplearningbook.org/) textbook
- Web courses:
    - Maxime Labonne's [LLM Course](https://github.com/mlabonne/llm-course)
    - Microsoft's ["Generative AI for Beginners"](https://microsoft.github.io/generative-ai-for-beginners/#/)
    - Fast.AI's ["Practical Deep Learning for Coders"](https://course.fast.ai/)
- Assorted university lecture notes
- Original research papers (sparingly)

I’ll often make reference to the original papers for key ideas throughout, but our emphasis will be on expository content which is more concise and conceptual, aimed at students or practitioners rather than experienced AI researchers (although hopefully the prospect of doing AI research will become less daunting as you progress through these sources). Pointers to multiple resources and media formats will be given when possible, along with some discussion on their relative merits.

<!--
For some topics, in the spirit of embracing the “latest and greatest” in AI, I’ll also include explainer articles written by an LLM — ****these will always be clearly flagged as AI-written****, and will be manually edited for clarity and correctness, but should nonetheless be treated as an “experimental feature” of the document. Despite the usefulness of ChatGPT and its colleagues as instructional tools for subjects like physics and history, for which innumerable relevant tokens are floating around the internet, the training datasets for these models likely have little (if any, depending on cutoff date) content on some of the topics we’ll consider, and some hallucinations may slip through. Grounding this generation via RAG over the original papers helps a bit.
-->

<h2>Preliminaries</h2>
<h3 class="no-numbering no-toc">Math</h3>

Calculus and linear algebra are pretty much unavoidable if you want to understand modern deep learning, which is largely driven by matrix multiplication and backpropagation of gradients. Many technical people end their formal math educations around multivariable calculus or introductory linear algebra, and it seems common to be left with a sour taste in your mouth from having to memorize a suite of unintuitive identities or manually invert matrices, which can be discouraging towards the prospect of going deeper in one’s math education. Fortunately, we don’t need to do these calculations ourselves --- programming libraries will handle them for us --- and it’ll instead be more important to have a working knowledge of concepts such as:

- Gradients and their relation to local minima/maxima
- The chain rule for differentiation
- Matrices as linear transformations for vectors
- Notions of basis/rank/span/independence/etc.

Good visualizations can really help these ideas sink in, and I don’t think there’s a better source for this than these two YouTube series from [3Blue1Brown](https://www.youtube.com/@3blue1brown/playlists):

- [Essence of calculus](https://www.youtube.com/watch?v=WUvTyaaNkzM&list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr&pp=iAQB)
- [Essence of linear algebra](https://www.youtube.com/watch?v=fNk_zzaMoSs&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab&pp=iAQB)

If your math is rusty, I’d certainly encourage (re)watching these before diving in deeper. To test your understanding, or as a preview of where we’re headed, the shorter [Neural networks](https://www.youtube.com/watch?v=aircAruvnKk&list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) video series on the same channel is excellent as well, and the latest couple videos in the series give a great overview of Transformer networks for language modeling. 

These [lecture notes](https://links.uwaterloo.ca/math227docs/set4.pdf) from Waterloo give some useful coverage of multivariable calculus as it relates to optimization, and ["Linear Algebra Done Right"](https://linear.axler.net/LADR4e.pdf) by Sheldon Axler is a nice reference text for linear algebra. ["Convex Optimization"](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf) by Boyd and Vandenberghe shows how these topics lay the foundations for the kinds of optimization problems faced in machine learning, but note that it does get fairly technical, and may not be essential if you're mostly interested in applications. 

Linear programming is certainly worth understanding, and is basically the simplest kind of high-dimensional optimization problem you'll encounter (but still quite practical); this illustrated [video](https://www.youtube.com/watch?v=E72DWgKP_1Y) should give you most of the core ideas, and Ryan O'Donnell's [videos](https://www.youtube.com/watch?v=DYAIIUuAaGA&list=PLm3J0oaFux3ZYpFLwwrlv_EHH9wtH6pnX&index=66) (17a-19c in this series, depending on how deep you want to go) are excellent if you want to go deeper into the math. These lectures ([#10](https://www.youtube.com/watch?v=v-chgwlwqTk), [#11](https://www.youtube.com/watch?v=IWzErYm8Lyk)) from Tim Roughgarden also show some fascinating connections between linear programming and the "online learning" methods we'll look at [later](#online-learning-and-regret-minimization), which will form the conceptual basis for [GANs](#generative-adversarial-nets) (among many other things).

<h3 class="no-numbering no-toc">Programming</h3>

Most machine learning code is written in Python nowadays, and some of the references here will include Python examples for illustrating the discussed topics. If you’re unfamiliar with Python, or programming in general, I’ve heard good things about Replit’s [100 Days of Python](https://replit.com/learn/100-days-of-python) course for getting started. Some systems-level topics will also touch on implementations in C++ or CUDA — I’m admittedly not much of an expert in either of these, and will focus more on higher-level abstractions which can be accessed through Python libraries, but I’ll include potentially useful references for these languages in the relevant sections nonetheless.

<h2 class="no-numbering no-toc">Organization</h2>

This document is organized into several sections and chapters, as listed below and in the sidebar. You are encouraged to jump around to whichever parts seem most useful for your personal learning goals. Overall, I'd recommend first skimming many of the linked resources rather than reading (or watching) word-for-word. This should hopefully at least give you a sense of where your knowledge gaps are in terms of dependencies for any particular learning goals, which will help guide a more focused second pass.
