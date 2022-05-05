## Introduction

This is the Obsidian vault I created to track my learning of the “[Frequently Encountered Words](https://www.shakespeareswords.com/Public/LanguageCompanion/Few.aspx)” (*FEW*) of William Shakespeare’s works.

I have been thinking about learning to read Shakespeare for a while. Watching *[The Tragedy of Macbeth](https://tv.apple.com/us/movie/the-tragedy-of-macbeth/umc.cmc.4wpfk1xmi22h3zyv4a10lj1tw)*, an Apple TV+ reinterpretation of the classical story, has only intrigued me more. However, with little prior knowledge of English literature, the archaic vocabulary and twisted grammar turn out to be too demanding for me as an ESL speaker.

One day I discovered by chance [ShakespearesWords.com](https://www.ShakespearesWords.com), a great online library of Shakespeare-related resources. Among the “Starting Points” it provided, there is a list of “Frequently Encountered Words,” comprised of 100 words that the [editors](https://www.shakespeareswords.com/Public/DavidAndBen.aspx) deem most important. I bookmarked the page outright but failed to find an initiative to actually start learning.

Yesterday, a friend of mine posted on WeChat that she was starting a study group where members would motivate and encourage each other to, well, learn vocabulary. There would be no mandated syllabus; members are expected to bring their own vocabulary book and schedule. The one and only rule is that learning outcomes shall be reported on a daily basis during the monthlong sprint, or the violator would be kicked out.

I signed up for the challenge on a whim and the *FEW* occured to me while I was thinking about what to learn; a hundred words spreading over thirty-some days sounds a reasonable goal. So I pulled the *FEW* page, reformatted it into an Obsidian vault — I will explain the process with more details in the coming days — and started to work. Obsidian is my preferred knowledge management software and with the help of built-in and community plugins such as random note and Dataview, it’s trivial to track progress and take notes along the way.

The repo reflects exactly the current status of the said vault on my computer. I will use git commits as daily check-ins. Hopefully it would end up a stuffed database after a month. Public supervision and suggestion are certainly welcomed.

## [TODO] How do I plan to learn

Each day I will use the “random note” feature of Obsidian to pull up three words from the `words` directory. Then, I will read the definition and example usage, locate the occurence in the original context, and supplement it with a Chinese translation. I will also 

For each play referred to in the examples, I will also create an entry in the `works` directory, in which, among other notes of interest, the corresponding Wikipedia page will be included in form of an `iframe` embedment for the convenience of future references.

[TO BE COMPLETED]

## [TODO] How did I creat the repo

First, the *FEW* page was downloaded as a Markdown document with the browser extension [MarkDownload](https://github.com/deathau/markdownload), with each word corresponding to an `h3` element:

```markdown
### afeard (adj.)  
afraid, frightened, scared

[Cym IV.ii.94](https://www.shakespeareswords.com/Public/Play.aspx?Act=4&Scene=2&WorkId=7#139609) \[Cloten to Guiderius\] *Art not afeard?*

...

### anon (adv.)  
soon, shortly, presently

...
```

A full list of words was then retrieved with the regular expression `/^### .*$` and saved to a file named `LIST` .

Next, after some cosmetic fixes (e.g., removing trailing spaces), the long document was split into 100 separate documents with `csplit`:

```bash
csplit -f 'few_' few.md '/^###.*/' {100}
```

The command above would generate a hundred separate files, named `few_00` to `few_99`, with each file containing the definitions and examples for one of the *FEW*. The filenames were then modified to include the words themselves prepared in advance in `LIST`. (The `vidir` command in `moreutils` and VIM were used to facilitate the renaming.) The resulting `few` directory looks as follows:

```bash
00_afeard.md
01_anon.md
02_apace.md
...
98_wont.md
99_wot.md
```

### Create a dashboard with Dataview

Dataview is used to create the dashboard (see [`DASHBD.md`](DASHBD.md)) for tracking and reviewing.

Dashview uses an SQL-like syntax for retrieving and presentating notes from the vault. For example, the following block retrieves all notes of which the property `learned_on` equals to the current date, i.e., it is learned today:

```text
table title as "Title"
from "words"
where learned_on = date(today)
sort title
```

[TO BE COMPLETED]