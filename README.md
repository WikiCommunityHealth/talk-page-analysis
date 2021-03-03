# Wikiconv talk page analysis
Main repository to gather everything related to talk page analysis using the wikiconv dataset

### Wikiconv dataset specs

#### Errors
Some records are missing even in the original provided dataset.

Edits and replies on a restored comment have the original comment as the parent,instead of the restored node.

[YuBot](https://it.wikipedia.org/wiki/Utente:YuBot) messes up the dataset for the italian wikipedia.
* Firstly the bot generates a table that wikiconv isn't able to parse (addition);
* Later it edits that table (modification);
* As a result in the dataset there are some modification actions without a parent.

#### Records sorting
The `id` field of each record consists of three integers following the format `a.b.c` where a is the id of the revision from which the records comes.

To sort the dataset by page, you need to use five fields:
* `pageId`
* `timestamp`
* `a.b.c` (from the `id` field) where a, b, c are int



#### Graph creation
To build the graph of the actions of page:
* Creations and additions use the `replytoId` field
* Modifications, deletions and restorations use the `parentId` field
Deletions and restorations are always leaves.

#### Others
The `authorlist` field has all the users that have edited the message and the original creator.

The thresholds for Perspective API used in the original paper are 0.64 and 0.92 for `toxicity` and `severe_toxicity` respectively.

To be considered a restore, a message needs to stay deleted for no more than two weeks.

### Papers
* [WikiConv: A Corpus of the Complete Conversational History of a Large
Online Collaborative Community](https://arxiv.org/pdf/1810.13181.pdf)
* [WAC: A Corpus of Wikipedia Conversations for Online
Abuse Detection](https://hal.archives-ouvertes.fr/hal-02497514/document)