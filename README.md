# Dialog System Technology Challenges 7 (DSTC 7)

## Track 1 - Sentence Selection
This challenge is offered with two goal oriented dialog datasets and consists of 5 subtasks which are described below. A participant may participate in one, several or all the subtasks. The general goal of the track is that *given a partial conversation, select the correct next utterances from a set of candidates* and even indicate that none of the proposed utterances is a good candidate. The objective is to push the utterance classification towards real world problems.

A full description of the track is available [here](http://workshop.colips.org/dstc7/proposals/DSTC%207%20Task%20Description%20-%20NOESIS_final.pdf "here").

### Ubuntu dataset
A new version of disentangled Ubuntu IRC dialogs will be provided in this challenge. The dataset consists of two party conversations extracted from the Ubuntu IRC. A typical dialog starts with a question that was asked by *participant_1*, and then the *participant_2* offers an answer or asks further questions from the *participant_1*, which leads to a two party dialog. In this challenge, the context of each dialog contains more than 3 turns which occured between the two participants and the next turn of *participant_2* should be selected from the given set of candidate utterances. Relavent external information of the form of Linux manual pages is also provided, which is useful for the subtask 5 which is explained below.

### FLEX dataset
This dataset contains two party dialogs that occured between a *student* and his academic *advisor*. The purpose of the dialogs is to guide the student to pick courses that fit not only their curriculum, but also personal preferences about time, difficulty, career path, etc. These conversations were collected by having students at the University of Michigan act as the two roles using provided personas. Structured information (such as a database of course information) will be provided, as well as the personas (though at test time only information available to the advisor will be provided, i.e. not the explicit student preferences). The data also includes paraphrases of the sentences and of the target responses.


### Sub-tasks
The description of the subtasks is given in the table below. [x] suggest that the subtask is evaluated on the marked dataset. 

|Subtask number|  Description | Ubuntu  |Flex   |
|--------------| ------------ | ------------ | ------------ |
|1|Baseline – Select the next utterance from a candidate pool of 100  |  [x] |  [x]  |
|2|Select the next utterance from a candidate pool of 120000  |  [x]  |   |
|3|Select the next utterance and its paraphrases from candidate pool of 100||[x]  |
|4|Select the next utterance from a candidate pool of 100 which might not contain the correct next utterance|  [x] |  [x]  |
|5|Select the next utterance from a candidate pool of 100 incorporating the provided external knowledge|  [x] |  [x]  |

### Data
#### Datasets
The datasets can be downloaded from the following links.

| Subtask  | Training  | Validation   | Other|
| ------------ | ------------ | ------------ |
| 1  | [Ubuntu](https://ibm.box.com/s/fsk885se8ieoape46uzk7ylhx1097kk9) <br>[Flex](https://ibm.box.com/s/sb5wloejbsbhrpfws0yuj1wbb28you2w) | [Ubuntu](https://ibm.box.com/s/rqb6bocovby1jau112y5wq99tz1fffp2) <br> [Flex](https://ibm.box.com/s/f53kcojriaqrj5taevtw3doaatq3sfjv) |None|
| 2  | [Ubuntu](https://ibm.box.com/s/i9o9gz37leycvxfqgdabh7478ep1dqo7)| [Ubuntu](https://ibm.box.com/s/ha4lcw6cjcwq6wseq5qv0t6ogxat2fhl) |[Candidate pool](https://ibm.box.com/s/uvwrmpzyt231ktl0kpcneheba8qi2ytf)|
| 3  |[Flex](https://ibm.box.com/s/kfev11bqpsvhwl8u2ko4fxb11kl9satq) |  [Flex](https://ibm.box.com/s/vhwmnt0kg1j1vx1j5wijez67mhjxjlnc) |[Paraphrase information](https://ibm.box.com/s/qh9gbkjo8pg8uph3vysv9fjhp18407fx)|
| 4  | [Ubuntu](https://ibm.box.com/s/ss7vaagg83qsycjv38bce6i8wsze8p9k) <br>[Flex](https://ibm.box.com/s/4p31ja8p83fehes0f6cuakr2wbdd4px9) | [Ubuntu](https://ibm.box.com/s/6jmxiavc50achlr7k4g5i5lgyspcsqbg) <br> [Flex](https://ibm.box.com/s/6jq99o1cz9m3env319s6e02ibtwksc1b) |None|
| 5  | Same as subtask 1| Same as subtask 1 |[Linux]|||



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

### Evaluation

### Submission

### Organizers
[Lazaros Polymenakos](mailto:lcpolyme@us.ibm.com), [Chulaka Gunasekara](mailto:chulaka.gunasekara@ibm.com) – IBM Research AI <br>
[Walter Lasecki](mailto:wlasecki@umich.edu), [Jonathan K. Kummerfeld](mailto:jkummerf@umich.edu) – University of Michigan
