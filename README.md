# Dialog System Technology Challenges 7 (DSTC 7) Track 1 - Sentence Selection

This challenge provides a partial conversation, and requires participants to select the correct next utterances from a set of candidates.
Unlike previous similar challenges, this task tries to push towards real world problems by introducing:

- A larges number of candidates
- Cases where no candidate is correct
- External data

This challenge is offered with two goal oriented dialog datasets, used in 5 subtasks.
A participant may participate in one, several, or all the subtasks.
A full description of the track is available [here](http://workshop.colips.org/dstc7/proposals/DSTC%207%20Task%20Description%20-%20NOESIS_final.pdf "here").

### Ubuntu dataset

A new set of disentangled Ubuntu IRC dialogs will be provided in this challenge.
The dataset consists of two party conversations extracted from the Ubuntu IRC channel.
A typical dialog starts with a question that was asked by *participant_1*, and then someone else, *participant_2*, responds with either an answer or follow-up questions that then lead to a back-and-forth conversation.
In this challenge, the context of each dialog contains more than 3 turns which occured between the two participants and the next turn of *participant_2* should be selected from the given set of candidate utterances.
We focus on *participant_2* to set the task up as creating a bot that could help provide answers.
Relavent external information of the form of Linux manual pages is also provided.

### Advising dataset

This dataset contains two party dialogs that simulate a discussion between a *student* and an academic *advisor*.
The purpose of the dialogs is to guide the student to pick courses that fit not only their curriculum, but also personal preferences about time, difficulty, areas of interest, etc.
These conversations were collected by having students at the University of Michigan act as the two roles using provided personas.
Structured information in the form of a database of course information will be provided, as well as the personas (though at test time only information available to the advisor will be provided, i.e. not the explicit student preferences).
The data also includes paraphrases of the sentences and of the target responses.

### Sub-tasks

We are considered several subtasks that have similar structure, but vary in the output space and available context.
In the table below, [x] indicates that the subtask is evaluated on the marked dataset. 

|Subtask number|  Description | Ubuntu  | Advising   |
|--------------| ------------ | ------------ | ------------ |
|1|Select the next utterance from a candidate pool of 100 sentences |  [x] |  [x]  |
|2|Select the next utterance from a candidate pool of 120000  |  [x]  |   |
|3|Select the next utterance and its paraphrases from candidate pool of 100||[x]  |
|4|Select the next utterance from a candidate pool of 100 which might not contain the correct next utterance|  [x] |  [x]  |
|5|Select the next utterance from a candidate pool of 100 incorporating the provided external knowledge|  [x] |  [x]  |

In **subtask 1**, for each partial dialog and a candidate pool of 100 is given and the contenstants are expected to select the best next utterance from the given pool.

In **subtask 2**, one large candidate pool of 120000 utterances is shared by training and validation datasets.
The next best utterance should be selected from this large pool of candidate utterances.

For **subtask 3**, in addition to the the training and validation dialog datasets, and extra dataset which includes paraphrases for utterances is provided.
The contestants are required to use the paraphrase informaton to select the next utterance as well as its paraphrases from the given set of 100 candidates.

The candidate sets that are provided for some dialogs in **subtask 4** does not include the correct next utterance.
The contestants are expected to train their models in a way that during testing they can identify such cases.

In **subtask 5**, additional external information which will be important for dialog modeling will be provided.
For Ubuntu dataset, this external information comes in the form of Linux manual pages and for Advising dataset, extra information about courses will be given.
The same training, validation and test data files in subtask 1 will be reused for this subtask.
The contestants can use the provided knowledge sources as is, or transform them to appropriate representations (e.g. knowledge graphs, continuous embeddings, etc.) that can be integrated with end-to-end dialog systems to improve accuracy.


## Data

#### Datasets
The datasets can be downloaded from the following links.

| Subtask  | Training  | Validation   | Other|
| ------------ | ------------ | ------------ | ------------ |
| 1  | [Ubuntu](https://ibm.box.com/s/fsk885se8ieoape46uzk7ylhx1097kk9) <br>[Advising](https://ibm.box.com/s/sb5wloejbsbhrpfws0yuj1wbb28you2w) | [Ubuntu](https://ibm.box.com/s/rqb6bocovby1jau112y5wq99tz1fffp2) <br> [Advising](https://ibm.box.com/s/f53kcojriaqrj5taevtw3doaatq3sfjv) |None|
| 2  | [Ubuntu](https://ibm.box.com/s/i9o9gz37leycvxfqgdabh7478ep1dqo7)| [Ubuntu](https://ibm.box.com/s/ha4lcw6cjcwq6wseq5qv0t6ogxat2fhl) |[Candidate pool](https://ibm.box.com/s/uvwrmpzyt231ktl0kpcneheba8qi2ytf)|
| 3  |[Advising](https://ibm.box.com/s/kfev11bqpsvhwl8u2ko4fxb11kl9satq) |  [Advising](https://ibm.box.com/s/vhwmnt0kg1j1vx1j5wijez67mhjxjlnc) | None |
| 4  | [Ubuntu](https://ibm.box.com/s/ss7vaagg83qsycjv38bce6i8wsze8p9k) <br>[Advising](https://ibm.box.com/s/4p31ja8p83fehes0f6cuakr2wbdd4px9) | [Ubuntu](https://ibm.box.com/s/6jmxiavc50achlr7k4g5i5lgyspcsqbg) <br> [Advising](https://ibm.box.com/s/6jq99o1cz9m3env319s6e02ibtwksc1b) |None|
| 5  | Same as subtask 1| Same as subtask 1 |[Linux man pages for Ubuntu](https://ibm.box.com/s/7ro3t72tp0rcnggq5cgq9hq80fvh5pkh) <br> [Course information for Advising](https://ibm.box.com/s/lslz39r951fys52qqa3enl0ccods5lus)|

Additionally, for the Advising data, we are providing a form of the data with the original dialogues and their paraphrases before remixing, which can be used for training in any subtask ([here](https://ibm.box.com/s/qh9gbkjo8pg8uph3vysv9fjhp18407fx)|).

#### Data format
Each dialog contains in training, validation and test datasets follows the JSON format which is similar to the below example.
```
{
    "data-split": "train",
    "example-id": 1100001,
    "messages-so-far": [
        {
            "speaker": "participant_1",
            "utterance": "hey guys, does your livecd have chroot installed? and bash?"
        },
        {
            "speaker": "participant_2",
            "utterance": "sure"
        },
        ...
    ],
    "options-for-correct-answers": [
        {
            "candidate-id": "TLSHF16Y4J4L",
            "utterance": "what are you missing in apt ?"
        }
    ],
    "options-for-next": [
        {
            "candidate-id": "YWOA49156J9P",
            "utterance": "issues with msn?. I'm experiencing them on windows atm, current msn version"
        },
        {
            "candidate-id": "RYBI7QRD9QZN",
            "utterance": "<> AmaroqWolf: alias='sudo admincommand'.  <AmaroqWolf>  aw, can't make myself type sudo? I like it better that way."
        },
        ...
    ],
    "scenario": 1
}
```

## Evaluation

For each test instance, we will expect you to return a set of 10 choices from the set of possible follow-up sentences and a probability distribution over those 10 choices.
For the competition metric we will consider the choices that cover 90% of the distribution, and compute an F-score as the harmonic mean of precision and recall:

- Precision = (number of correct sentences selected) / (total number of sentences selected)
- Recall = (number of correct sentences selected) / (total number of correct sentences in all sets)

We are also considering a number of other metrics for the purpose of analysing system behaviour, but those will not be the official metric used for ranking.

### Submission

Information regarding how to submit will be released later in the development period.

### Organizers

[Lazaros Polymenakos](mailto:lcpolyme@us.ibm.com), [Chulaka Gunasekara](mailto:chulaka.gunasekara@ibm.com) – IBM Research AI

[Walter Lacecki](mailto:wlasecki@umich.edu), [Jonathan K. Kummerfeld](www.jkk.name) – University of Michigan
