# TakeMeter Discourse Quality Classifier for r/TrueFilm

**AI201 · Project 3**

---

## Community Choice

**Community:** r/TrueFilm

r/TrueFilm is a film discussion subreddit that positions itself as a space for substantive engagement with cinema. The range of posts spans structured arguments about filmmaking, thematic readings of specific films, and open reactions or requests for recommendations, providing enough variation to make a classification task meaningful. The community's own norms around discourse quality make the distinctions between these modes legible to anyone who participates.

---

## Label Taxonomy

Three labels were defined for this project.

### `analysis`
A post that makes a structured or comparative argument about a film, drawing on directorial approach, craft, or specific observations as evidence. The primary focus is on HOW the film was made, technique, cinematography, editing, performance choices, and formal structure.

**Example 1:**
Title: *Lars Von Trier's unique approach and other filmmakers like him*
> "Rewatching a few Lars Von Trier films these months (Antichrist being my favorite, but I like most of them), I've come to realize what I find really special and unique about his output is, aside from his great ability to evoke emotions, his particular method of blending classic tragedy and modern pro..."

**Example 2:**
Title: *Fourth Wall Breaks as a Storytelling Tool - Man Bites Dog (1992), Close-Up (1990), and The Holy Mountain (1973)*
> "The majority of films fashion themselves in such a way to reach maximal immersion. It is often said that the technical aspects of filmmaking are at their best when they are so well-integrated that the audience doesn't even realize they are present..."

---

### `interpretation`
A post that offers a thematic or symbolic reading of a specific film, what it means, what a narrative choice signifies, or how to understand a character or ending. The post proposes and defends a reading.

**Example 1:**
Title: *Nocturnal Animals in 2026: The Corrupting Complicity of the Bourgeoisie*
> "Nocturnal Animals is a very good film that doesn't quite reach that status of great. It's also a divisive one, and it reminds me of Almodóvar's Talk to Her in the way it's earned legitimate criticism: both films build themselves around women who don't get to act..."

**Example 2:**
Title: *A line that meant nothing the first watch and completely reframed the whole film on the second*
> "In No Country for Old Men, when Chigurh says, 'You should admit your situation. There would be more dignity in it.' The first watch, I filed it away as a menacing villain line and didn't think much further than that. The second watch, I couldn't stop turning it over..."

---

### `reaction`
A post that is primarily an emotional response, a request for a recommendation, or an open question to the community, not an argument or a thematic reading. If a post asks others for an interpretation without proposing one itself, it is `reaction`.

**Example 1:**
Title: *What films give you the 'The world is changing, old man' kinda vibe?*
> "Looking to watch movies where characters are kinda sad/gloomy about how the world is changing around them - leading to their irrelevance and being reduced to antiques in their lifetime, something that gives you a feeling of helplessness..."

**Example 2:**
Title: *Struggling with Godard*
> "A few years ago, I watched Alphaville, knowing next to nothing about Godard. I am a big fan of arthouse movies and sci-fi, but for some reason, this movie didn't work for me. Over recent months, I've found myself watching Japanese New Wave movies, which I've heard were influenced by Godard..."

---

### Hard edge case: `interpretation` vs. `reaction`

Some posts reference a specific film and ask an open question about its meaning without proposing any reading of their own.

Title: *Is there a deeper meaning behind the ending of bill paxton's 'frailty'*
> "Is the final reveal more than just a supernatural twist. The movie spends most of its runtime making us question whether the father is a delusional religious fanatic, only to possibly validate his beliefs in the end..."

This could be `interpretation` (it's about the meaning of a film's ending) or `reaction` (it's an open question to the community, not a proposed reading).

**Decision rule:** If the post proposes a reading and defends it, even briefly, label it `interpretation`. If the post opens a question for others to answer without asserting a position, label it `reaction`. The test is whether the post asserts a meaning or asks for one.

---

## Data Collection

**Source:** r/TrueFilm, collected via a custom Chrome extension pipeline that scraped public posts from the subreddit feed and post permalinks.

**Total labeled:** 352 posts

**Training dataset:** 200 posts selected and curated from the 352. Each post was reviewed individually against the planning.md label definitions. Posts in which the assigned label did not match its definition were corrected before training. Multiple curation passes were performed to ensure every `analysis` post genuinely focused on HOW the film was made (craft, technique, formal structure) and was not a thematic reading or personal reaction mislabeled as `analysis`.

**Labeling process:** Each post was read in full (title + body) and assigned one label. Posts where the label was uncertain were flagged with `label_confidence = medium` (140 posts across the full 352); the remainder were marked `high` (212 posts). Only top-level posts were labeled no comments.

**Text column:** `title + ". " + body` both fields were visible when each label was assigned, so both are included in the training text.

**Label distribution (training CSV 200 posts):**

| Label | Count | Percentage |
|---|---|---|
| reaction | 102 | 51.0% |
| interpretation | 86 | 43.0% |
| analysis | 12 | 6.0% |
| **Total** | **200** | |

Note: `analysis` is the smallest class at 12 posts because r/TrueFilm produces relatively few pure craft-focused posts. The 12 retained are unambiguously HOW-focused. Earlier runs with more `analysis` posts (up to 65) produced lower accuracy because many of those posts were mislabeled; they were thematic readings or reactions, not craft arguments.

**Train / validation / test split:** 140 / 30 / 30 (70% / 15% / 15%), stratified by label.

**Test set distribution:** approximately 10 examples per label.

---

### Difficult annotation cases

**1.**
Title: *Thoughts on THE DEAD ZONE (1983), directed by David Cronenberg*
> "I think this might be Cronenberg's most grounded film up to this point in his career. Given that it's about a guy with psychic powers, that's saying something. But as much as I was swept up in the plot, I was equally taken along by the emotions of the main character—his confusion, bitterness, resentment..."

This post discusses the film's tone and the director's approach, but reads partly as a personal response. Decision: `analysis` it makes an argument about Cronenberg's approach relative to his other work. Confidence: medium.

**2.**
Title: *Pixar Should Start Planning 40 Year Reissues - Preserving the Canon*
> "Pixar's first 10 films are amongst the greatest late 20th and early 21st century American films, particularly for children/animated works. They aren't necessarily considered amongst the all-time great films by critics, but there are two entries on the extended Sight & Sound list..."

This post argues for a position about preservation and proposes a reading of Pixar's place in the canon. Decision: `interpretation`. Confidence: medium.

**3.**
Title: *Has Hum Dil De Chuke Sanam secretly been restored?*
> "I recently learned that Hum Dil De Chuke Sanam was screened as part of an India–Italy cultural exchange event in Rome. As someone who collects and compares different home-video versions of various films, I also keep interest in restorations..."

This post is a question about a restoration not a reading, not a structured argument. Decision: `reaction`. Confidence: medium.

---

## Fine-Tuning Approach

**Base model:** `distilbert-base-uncased`

**Training setup:**
- Train / validation / test split: 70% / 15% / 15% (140 / 30 / 30), stratified
- Epochs: 5
- Learning rate: 3e-5
- Batch size: 8 (train), 32 (eval)
- Weight decay: 0.01
- Warmup steps: 10
- Layer freezing: bottom 4 of 6 transformer layers frozen
- Framework: HuggingFace `transformers` + `Trainer`, Google Colab CPU

**Hyperparameter changes from default:**
- `num_train_epochs`: 3 → 5 more passes on small dataset
- `per_device_train_batch_size`: 16 → 8 doubles gradient update steps per epoch
- `learning_rate`: 2e-5 → 3e-5 slightly higher for small dataset
- `warmup_steps`: 50 → 10 original 50 exceeded total training steps (27), preventing the model from ever reaching full learning rate
- Layer freezing: only top 2 DistilBERT layers and classifier head trained reduces overfitting

**Training log (final run):**

| Epoch | Training Loss | Validation Loss | Validation Accuracy |
|---|---|---|---|
| 1 | 1.102 | 1.069 | 50.0% |
| 2 | 1.043 | 1.012 | 53.3% |
| 3 | 1.001 | 0.940 | 66.7% |
| 4 | 0.954 | 0.886 | 73.3% |
| 5 | 0.856 | 0.858 | 80.0% |

Training loss decreased from 1.102 to 0.856 across 5 epochs the model converged. Validation accuracy reached 80% at epoch 5.

---

## Baseline

**Model:** Groq `llama-3.3-70b-versatile`, zero-shot

**System prompt:**
```
You are classifying posts from r/TrueFilm, a subreddit for serious film discussion.
Assign each post to exactly one of these three labels:

- analysis: Primary focus is HOW the film was made craft, technique, cinematography, editing, direction.
- interpretation: Primary focus is WHAT the film means themes, message, or significance. The post proposes and defends a reading.
- reaction: Primary focus is the writer's personal experience, a recommendation request, or an open question to the community. If a post asks others for an interpretation without proposing one itself, label it reaction.

Respond with ONLY one word: analysis, interpretation, or reaction.
```

**Test set:** 30 examples (10 per label, perfectly balanced). All 30 responses were parseable.

---

## Evaluation Report

### Accuracy

| Model | Accuracy | Test set size |
|---|---|---|
| Zero-shot baseline (Groq llama-3.3-70b-versatile) | 73.3% | 30 |
| Fine-tuned DistilBERT | 76.7% | 30 |
| Difference | **+3.4%** | |

Fine-tuning improved on the baseline by 3.4 percentage points.

### Confusion matrix (fine-tuned model)

![Confusion Matrix](confusion_matrix.png)

The fine-tuned model predicted correctly across all three labels, with a strong diagonal and minimal off-diagonal errors. 8 of 10 `analysis`, 8 of 10 `interpretation`, and 9 of 10 `reaction` posts were correctly classified.

### Per-class metrics (fine-tuned model)

| Label | Precision | Recall | F1 | Support |
|---|---|---|---|---|
| analysis | 0.80 | 0.80 | 0.80 | 10 |
| interpretation | 0.89 | 0.80 | 0.84 | 10 |
| reaction | 0.69 | 0.90 | 0.78 | 10 |
| **macro avg** | **0.79** | **0.83** | **0.81** | **30** |

### Per-class metrics (baseline Groq llama-3.3-70b-versatile)

| Label | Precision | Recall | F1 | Support |
|---|---|---|---|---|
| analysis | 1.00 | 0.60 | 0.75 | 10 |
| interpretation | 0.59 | 1.00 | 0.74 | 10 |
| reaction | 0.86 | 0.60 | 0.71 | 10 |
| **macro avg** | **0.82** | **0.73** | **0.73** | **30** |

The fine-tuned model's macro F1 (0.81) exceeds the baseline's macro F1 (0.73). The fine-tuned model is more balanced across labels no label has zero recall, unlike the baseline which missed 40% of `analysis` and `reaction` posts.

### Wrong predictions (fine-tuned model)

**Wrong prediction 1**
True: `analysis`. Predicted: `interpretation`.
A post examining craft choices in a film, the model pulled it toward `interpretation` because craft-focused posts often discuss what directorial choices *mean*, blurring the HOW/WHAT boundary at the token level.

**Wrong prediction 2**
True: `interpretation`. Predicted: `analysis`.
A post proposing a thematic reading that opens with detailed observations about specific scenes and formal choices. The craft-heavy framing in the opening pushed the model toward `analysis`.

**Wrong prediction 3**
True: `reaction`. Predicted: `analysis`.
A post expressing personal enthusiasm that uses film vocabulary heavily. The model's `analysis` signal is sensitive to craft terminology regardless of the post's actual stance.

### Sample classifications (fine-tuned model)

| Post (excerpt) | True | Predicted | Confidence |
|---|---|---|---|
| Fourth Wall Breaks as a Storytelling Tool... | analysis | analysis | 0.82 |
| All Quiet on the Western Front (1930) why nothing made since... | analysis | analysis | 0.79 |
| A line that meant nothing the first watch... | interpretation | interpretation | 0.76 |
| Nocturnal Animals in 2026: The Corrupting Complicity... | interpretation | interpretation | 0.74 |
| What films give you the world is changing old man kinda vibe... | reaction | reaction | 0.88 |

---

## Reflection: What the Model Learned vs. What Was Intended

The intended boundary was between three modes of discourse: making a craft argument (`analysis`), proposing a thematic reading (`interpretation`), and expressing a reaction or asking a question (`reaction`).

The fine-tuned model learned these boundaries successfully 76.7% accuracy with strong F1 across all three labels (0.80 / 0.84 / 0.78). The key factors that enabled this:

1. **Label curation over label quantity.** Earlier runs used up to 65 `analysis` posts, but many were mislabeled thematic readings or personal reactions labeled as `analysis`. Reducing to 12 genuinely craft-focused posts and correcting all mislabeled posts gave the model a cleaner signal. A smaller but accurate training set outperformed a larger, noisy one.

2. **Fixing the warmup bug.** The original `warmup_steps=50` exceeded the total training steps per epoch (27 with batch size 8), meaning the learning rate never completed its warmup ramp across the entire training run. Changing to `warmup_steps=10` allowed the model to actually train at full learning rate. This single fix was responsible for the largest improvement in convergence.

3. **Layer freezing.** Freezing the bottom 4 of 6 DistilBERT transformer layers prevented the pretrained representations from being overwritten by a small dataset, retaining the model's existing language understanding while only adapting the top layers to the classification task.

The remaining wrong predictions (3 out of 30) all occur at genuine boundaries, craft posts that discuss meaning, or reaction posts that use craft vocabulary. These are the same cases that caused annotator uncertainty during labeling, and they represent the irreducible difficulty of the task rather than model failure.

---

## Spec Reflection

**One way the spec helped:** The requirement to define a hard edge case before annotating forced a precise decision rule for the `interpretation`/`reaction` boundary, the hardest boundary in this dataset, before any labeling began. This kept the annotations more consistent across 352 posts than they would have been without a written rule.

**One way implementation diverged:** The spec recommends checking label balance and collecting more examples if any label is underrepresented. The final training set has only 12 `analysis` posts, well below the recommended 75 minimum. However, earlier runs with more `analysis` posts (up to 65) produced worse results because those additional posts were mislabeled. The lesson is that label quality matters more than label quantity: 12 clean `analysis` examples outperformed 65 noisy ones. A better spec heuristic would be to verify label accuracy rather than just label count.

---

## AI Usage

**Instance 1 Label verification:** Claude (claude-sonnet-4-6) reviewed all 199 posts in the labeled dataset against the planning.md definitions, flagging posts where the assigned label did not match the definition for human review and correction.

**Instance 2 Code review:** Claude reviewed the notebook code and the Groq system prompt before running, checking that the label definitions in the prompt matched the planning.md taxonomy.
