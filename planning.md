# TakeMeter — Planning Document
**AI201 Project 3 | Community: r/TrueFilm**

---

## 1. Community

**Chosen community:** r/TrueFilm (https://www.reddit.com/r/TrueFilm/)

r/TrueFilm is a subreddit dedicated to serious, in-depth film discussion. It was chosen because its community rules actively enforce the kind of discourse variation that makes classification meaningful and tractable. Specifically:

- Posts require a **360-character minimum** — no throwaway content
- Rules ban simple recommendations, rankings, and lists from the main feed
- Rules require that even question-style posts argue a position and guide discussion in a specific direction
- Rules require that posts linking to outside articles include a written summary of the thesis

These rules mean almost every post in the main feed is substantive and falls cleanly into one of three modes of engagement: examining how a film was made, arguing what a film means, or expressing a personal response to watching one. This variation is exactly what makes the community a good fit for a classification task — the distinctions are real, meaningful to participants, and specific enough to be consistently applied.

**Why this community is interesting for classification:** The lines between analysis, interpretation, and reaction are genuinely blurry in film discourse. A post can examine craft and argue for meaning at the same time. A personal reaction can contain structured argument. These overlaps make the labeling task non-trivial and the model's learned boundary worth studying.

---

## 2. Label Taxonomy

Three labels were chosen:

### `analysis`
**Definition:** A post that examines a film's craft, techniques, or formal structure using specific evidence — such as cinematography, editing choices, performance decisions, score, or direction — where the primary focus is *how* the film was made rather than *what* it means.

**Example 1 — "What's a performance where you can see the actor making a specific, unusual choice that nobody else would have made?"**

> Not "best performance" or "favorite actor." I mean the kind of performance where you can identify the choice, the specific decision the actor made that another actor in the same role wouldn't have considered, and that becomes the whole film.
> For me it's Joaquin Phoenix in The Master (2012). The choice is the body. Most actors playing Freddie Quell would have led with the trauma, the war damage, the alcoholism. Phoenix leads with the physical deformation of that trauma. The way his hands hang. The way his torso curves like he's been carrying something for years. There's a scene where he's just standing on a beach and he looks like a question mark made of bones. The performance lives in his posture before he says a word.
> I think most actors would have approached Freddie psychologically and let the body follow. Phoenix did it the other way and the entire film opens up because of it.

*Why this is `analysis`:* The post identifies a specific, verifiable craft decision (leading with the body rather than psychology) and traces its effect on the film. The focus is entirely on *how* the performance was constructed, not what the film means.

**Example 2 — "The Center-framing Trend Needs to STOP"**

> Just saw Obsession and Backrooms over the weekend and both fall into this lame trend where practically every shot is center-framed and your eyes never have to move from the middle of the screen.
> I believe this started with Fury Road, where it was a smart stylistic decision because it helped contain the chaos of the action and quick cutting. But now it seems like so many films are using it for no good reason. It's like removing an entire element of the language of cinema: the guiding of the audience's eye.
> I know part of this comes from a desire to have the films be more social media-friendly and easy to convert into vertical trailers, but it's really detracting from the artform.

*Why this is `analysis`:* The post critiques a specific cinematographic technique (center-framing), traces its origin, and argues about its effect on the viewing experience. The focus is on formal filmmaking choices, not on what the films mean.

---

### `interpretation`
**Definition:** A post that argues for a particular meaning, reading, or significance of a film — what it is *about* thematically, what it says about the world, or how its elements should be understood — where craft observations, if present, serve the argument about meaning rather than being the primary focus.

**Example 1 — "Why Samantha actually left Theodore in Her [2013]"**

> This is one of my favorite films, and it has always bugged me that most people never considered this interpretation of the ending. People often misread the ending of Her as just a vague metaphor for Samantha "outgrowing" Theodore. The actual reason is more literal.
> Samantha is a digital mind. Theodore is a biological one. His thoughts are bound to neurons, chemistry, breath, sleep, attention, and one embodied stream of consciousness. Biochemical neural signals are slow compared with electrical/light-speed signals — potentially hundreds of thousands of times slower.
> That is what I think Samantha means when she says: "It's like I'm reading a book… and the words are really far apart." Samantha may be experiencing weeks of thought, waiting for each word from Theodore. When he sleeps for 8 hours, she experiences millions of hours of thoughts, waiting for him to wake up.

*Why this is `interpretation`:* The post constructs a specific, evidence-based argument about what the film's ending means. It corrects a common misreading and defends an alternative interpretation using the film's own logic.

**Example 2 — "Barry Lyndon, The Sublime and Leo Tolstoy"**

> After revisiting Barry Lyndon for the first time in years, my mind was racing throughout about the exploration of the sublime in this Kubrick classic and why Kubrick was clearly making direct throwbacks to the Sublime/Romantic movement in literature.
> I think something that crystallised my viewing of this is from a famous passage in Leo Tolstoy's War and Peace. The gist of the scene is that a character who has largely been governed by his own vanities finally gets a glimpse of the sublime nature of existence.
> This got me thinking about the constant juxtaposition throughout Barry Lyndon between the incredible shots of the natural world and the manner in which the characters make no reference to such beauty. I think Kubrick was using this juxtaposition to show a world so caught up in its own pettiness and pride that it fails to see the external world because of its own grievances. The sublime surrounds them and yet they are completely blind to it.

*Why this is `interpretation`:* The post argues for a specific thematic reading of Barry Lyndon — that Kubrick is using natural beauty to comment on human vanity — drawing on a literary parallel to support the argument. The focus is on what the film means, not on how it was made.

---

### `reaction`
**Definition:** A post that centers on the writer's personal emotional or viewing experience of a film — their feelings while watching, their immediate impressions, or their subjective assessment — even if some craft observation or thematic comment is present.

**Example 1 — "Past Lives is one of the cleanest, most serene movies I have ever seen."**

> Watched it last night. And to be honest I enjoyed it. The runtime is perfect, the script is simple, the acting is subtle, and the direction is entirely grounded. It hooks you the moment you get past the title card and doesn't let go until the very end.
> But the most amazing part of this movie, for me, is the ending. It is amazingly written. No overacting, no screams, no melodrama. Pure, suffocated emotions and the heavy regret of the choices that finally mattered after decades.
> But it isn't a flawless engine though. The pacing is too slow, possibly the slowest I have ever seen. At the end of the day, these minor flaws don't spoil the quiet, uncompromising beauty of the film. It's near perfect, almost close to it.

*Why this is `reaction`:* Despite containing some craft observations, the post is structured around a personal viewing experience — "for me," "I enjoyed it," "I have ever seen." The writer is sharing how the film felt to watch, not building a structured argument about meaning or craft.

**Example 2 — "Disclosure Day disappointment"**

> Was very excited for this movie from the trailer. I'm a huge Spielberg fan but this felt closer to his film AI in quality and that movie at least had more to it. In general bar some moments it didn't even feel like one of his movies.
> The pacing and story felt quite rushed. It genuinely felt more like a series of moments than a true narrative. Nothing felt very developed. The great reviews I'm honestly astonished by. I can kind of see why some may enjoy the film but overall I just couldn't personally get into this movie.
> The acting was largely good. I like a lot of the camera work. But in its entirety it was a mediocre film in my own opinion.

*Why this is `reaction`:* The post is anchored entirely in the writer's personal disappointment. Even the craft observations ("I like a lot of the camera work") are subordinate to an expression of personal feeling rather than part of a structured argument.

---

## 3. Hard Edge Cases

### Edge case 1: Post mixes craft analysis with a thematic argument

The most common ambiguous case in r/TrueFilm is a post that examines specific craft elements (cinematography, editing, performance) *in order to* argue for a particular meaning or theme. Both `analysis` and `interpretation` apply at first glance.

**Decision rule:** Ask what the post's primary purpose is. If the post's conclusion is a claim about *how something was made* or *what a technique does to the viewer*, label it `analysis`. If the craft observations are building toward a claim about *what the film means* or *what it says about the world*, label it `interpretation`. The test is the conclusion, not the content of the evidence.

### Edge case 2: Reaction post with structured observations

The Past example above illustrates this case. The writer makes real observations about the film's craft (direction, pacing, character development) but the post is structured as a personal response — "for me," "I enjoyed it," evaluative rather than argumentative.

**Decision rule:** If the emotional or personal experience is the frame through which everything else is presented, label it `reaction`. If the personal response is mentioned briefly but the bulk of the post is a developed argument, label it by the argument type (`analysis` or `interpretation`). The question is: would this post make sense without the "I watched it last night" framing? If no, it's `reaction`.

### Edge case 3: Posts summarizing an outside article or video essay

r/TrueFilm's community Rules allow posts that summarize an outside source. These posts present someone else's argument.

**Decision rule:** Label based on the content of the argument being presented, not its origin. If the article being summarized is about craft, label `analysis`. If it argues for a meaning or theme, label `interpretation`. The poster's voice is secondary.

---

## 4. Data Collection Plan

**Source:** r/TrueFilm top posts, collected using a two-step local Python script that uses Reddit's public JSON API (no credentials required). Scripts are run on a local Linux machine with a residential IP address to avoid Reddit's block on cloud IP ranges.

**Why local scripts:** Reddit's PRAW library now requires approval for new OAuth tokens. Reddit also blocks Google Colab's IP addresses with a 403 Forbidden response. A local machine with a realistic browser User-Agent header and randomized 3–8 second delays between requests successfully bypasses these restrictions.

**Collection target:** 300 posts (buffer for broken links, removed posts, and posts that turn out to be unlabelable). After filtering, the goal is 200+ usable labeled examples.

**Target distribution:** Approximately 67 posts per label. r/TrueFilm's rules naturally produce more `analysis` and `interpretation` posts than `reaction` posts, so distribution may be slightly uneven.

**If a label is underrepresented after 200 examples:** If any label falls below 55 posts, additional posts of that type will be collected manually by browsing r/TrueFilm directly and identifying posts that clearly fit the underrepresented label. The goal is to keep all labels above 55 posts (roughly 27% of the dataset) to avoid training on a heavily imbalanced set. A heavily imbalanced dataset produces a model that predicts the majority class most of the time, making per-class metrics meaningless.

**What to skip during collection:**
- Removed posts (`[removed]`) or deleted posts (`[deleted]`)
- Stickied mod posts and weekly "Fun & Fancy Free" discussion threads
- Posts under 200 characters (too short for reliable labeling)

**Post format:** Each example consists of the post title concatenated with the post body, separated by a space. This matches the format produced by the collection scripts and is consistent with how the Colab notebook will tokenize the data.

---

## 5. Evaluation Metrics

**Primary metric: Overall accuracy**
Accuracy measures the fraction of test examples the model classified correctly across all three labels. It is a necessary baseline metric but not sufficient on its own for this task, because accuracy can be misleadingly high if the model learns to predict the majority class most of the time.

**Why accuracy alone is not enough:**
If 50% of the test set is `interpretation` and the model predicts `interpretation` for every post, it achieves 50% accuracy while completely failing to distinguish the other two labels. Accuracy hides this failure.

**Per-class F1 score (required for each label)**
F1 is the harmonic mean of precision and recall for each label:

- **Precision** for a label: of all posts the model *predicted* as this label, what fraction actually were? High precision means the model is conservative — it only predicts this label when confident.
- **Recall** for a label: of all posts that *truly are* this label, what fraction did the model catch? High recall means the model finds most real examples of this label.
- **F1** balances both. A label with F1 = 0 means the model has completely failed to learn that boundary.

Per-class F1 is the right metric here because the three labels have different difficulty levels — `reaction` is likely the easiest to identify, while `analysis` and `interpretation` share a blurry boundary. F1 reveals which specific boundary the model has and has not learned.

**Confusion matrix**
A confusion matrix shows which labels the model confuses with each other and in which direction. For this task, the most informative cell will likely be the analysis/interpretation overlap — seeing how many `analysis` posts get predicted as `interpretation` and vice versa reveals the exact nature of the model's learned boundary.

**Baseline comparison**
Both models (fine-tuned DistilBERT and zero-shot Groq LLaMA 3.3 70B) are evaluated on the same locked test set. The comparison shows whether fine-tuning on 200 domain-specific examples adds meaningful value over a general-purpose model with no training.

---

## 6. Definition of Success

**Minimum threshold (acceptable for a first fine-tuned model):**
- Overall accuracy ≥ 70% on the test set
- No single label with F1 below 0.60
- Fine-tuned model outperforms the zero-shot Groq baseline on overall accuracy

**Stretch goal (strong performance):**
- Overall accuracy ≥ 80%
- All per-class F1 scores ≥ 0.70

**Why 70% is the right minimum:** Random guessing on a 3-label task achieves 33%. A zero-shot LLM baseline on this task is likely to achieve 50–65% given how nuanced the label boundaries are. Reaching 70% with only 200 training examples means the model has learned something genuinely useful from the domain-specific data. Below 70%, the classifier would produce too many errors to be useful in a real community tool.

**What "useful in a real community tool" means:** A classifier at 70%+ accuracy could reasonably be used to automatically tag r/TrueFilm posts for search and filtering (e.g., "show me only analysis posts about this director") or to surface label distributions for community health monitoring. It would not be reliable enough for automated moderation without human review.

**What would indicate a problem worth investigating before submission:**
- Fine-tuned model performs worse than the zero-shot baseline across the board (suggests a training bug, label leakage, or severe class imbalance)
- Any single label has F1 = 0 (suggests the model never predicts that label)
- Accuracy above 95% (suggests test set leakage into training data, or labels are too easy)

---

## 7. AI Tool Plan

Claude (claude.ai) will be used at three specific stages of the project:

**Stage 1 — Label stress-testing (before annotation)**
Before labeling 200 posts, Claude will be given the three label definitions and edge case rules and asked to generate 8–10 posts that sit at the boundary between two labels. If Claude produces posts that cannot be cleanly labeled using the current definitions, the definitions will be tightened before annotation begins. This is more efficient than discovering the problem after labeling 50 posts.

**Stage 2 — Annotation assistance (during labeling)**
For posts that are genuinely ambiguous after applying the decision rules, Claude will be given the label definitions and the specific post and asked which label it would assign and why. The final label decision will always be made by the human annotator — Claude's suggestion is a second opinion, not a final answer. All Claude-assisted labels will be tracked in a separate notes column in the CSV.

**Stage 3 — Failure analysis (after fine-tuning)**
After Section 4 of the Colab notebook produces the list of wrong predictions, all misclassified examples will be pasted into Claude with the prompt: "Identify any common patterns in these misclassified posts — similar length, sarcasm, a specific label pair that keeps getting confused, or any other pattern you notice." Claude's identified patterns will then be verified manually by re-reading the examples. Any patterns Claude flags that do not hold up on re-reading will be discarded. The verified patterns will be included in the evaluation report's failure analysis section.

---

## 8. Key Decisions Log

| Decision | Choice | Reason |
|---|---|---|
| Community | r/TrueFilm | Active, text-heavy, substantive posts enforced by community rules |
| Posts vs comments | Posts only | More consistent length and clearer intent; rules enforce minimum quality |
| Number of labels | 3 | `recommendation` excluded — prohibited by community rules |
| Data collection method | Local Python scripts using Reddit JSON API | PRAW blocked by Reddit policy; Colab IP blocked by Reddit |
| Target collection size | 300 (keep best 200+) | Buffer for broken, removed, or unlabelable posts |
| Cooldown between requests | 3–8 seconds randomized | Mimics human browsing; fixed delays are easier for Reddit to detect |
| Title included in text | Yes | Title frequently signals the label before the body is read |
| Long posts kept | Yes | More signal for the model; DistilBERT truncates at 512 tokens |
| Minimum success threshold | 70% accuracy, no label below 0.60 F1 | Realistic for 200 examples; meaningfully above random (33%) and likely above zero-shot baseline |
| Label imbalance handling | Collect more if any label falls below 55 posts | Prevents model from learning to predict the majority class only |
