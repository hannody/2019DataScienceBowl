# 2019DataScienceBowl

https://www.kaggle.com/c/data-science-bowl-2019/data

Uncover the factors to help measure how young children learn, Kaggle Competition, Tools:Python Stack.

In this dataset, you are provided with game analytics for the PBS KIDS Measure Up! app. In this app, children navigate a map and complete various levels, which may be activities, video clips, games, or assessments. Each assessment is designed to test a child's comprehension of a certain set of measurement-related skills. There are five assessments: Bird Measurer, Cart Balancer, Cauldron Filler, Chest Sorter, and Mushroom Sorter.

The intent of the competition is to use the gameplay data to forecast how many attempts a child will take to pass a given assessment (an incorrect answer is counted as an attempt). Each application install is represented by an installation_id. This will typically correspond to one child, but you should expect noise from issues such as shared devices. In the training set, you are provided the full history of gameplay data. In the test set, we have truncated the history after the start event of a single assessment, chosen randomly, for which you must predict the number of attempts. Note that the training set contains many installation_ids which never took assessments, whereas every installation_id in the test set made an attempt on at least one assessment.

## The outcomes in this competition are grouped into 4 groups (labeled accuracy_group in the data):

3: the assessment was solved on the first attempt
2: the assessment was solved on the second attempt
1: the assessment was solved after 3 or more attempts
0: the assessment was never solved
The file train_labels.csv has been provided to show how these groups would be computed on the assessments in the training set. Assessment attempts are captured in event_code 4100 for all assessments except for Bird Measurer, which uses event_code 4110. If the attempt was correct, it contains "correct":true.

Note that this is a synchronous rerun code competition and the private test set has approximately 8MM rows. You should be mindful of memory in your notebooks to avoid submission errors.

## Files
### train.csv & test.csv
These are the main data files which contain the gameplay events.

event_id - Randomly generated unique identifier for the event type. Maps to event_id column in specs table.
game_session - Randomly generated unique identifier grouping events within a single game or video play session.
timestamp - Client-generated datetime
event_data - Semi-structured JSON formatted string containing the events parameters. Default fields are: event_count, event_code, and game_time; otherwise fields are determined by the event type.
installation_id - Randomly generated unique identifier grouping game sessions within a single installed application instance.
event_count - Incremental counter of events within a game session (offset at 1). Extracted from event_data.
event_code - Identifier of the event 'class'. Unique per game, but may be duplicated across games. E.g. event code '2000' always identifies the 'Start Game' event for all games. Extracted from event_data.
game_time - Time in milliseconds since the start of the game session. Extracted from event_data.
title - Title of the game or video.
type - Media type of the game or video. Possible values are: 'Game', 'Assessment', 'Activity', 'Clip'.
world - The section of the application the game or video belongs to. Helpful to identify the educational curriculum goals of the media. Possible values are: 'NONE' (at the app's start screen), TREETOPCITY' (Length/Height), 'MAGMAPEAK' (Capacity/Displacement), 'CRYSTALCAVES' (Weight).
specs.csv
This file gives the specification of the various event types.

event_id - Global unique identifier for the event type. Joins to event_id column in events table.
info - Description of the event.
args - JSON formatted string of event arguments. Each argument contains:
name - Argument name.
type - Type of the argument (string, int, number, object, array).
info - Description of the argument.

### train_labels.csv
This file demonstrates how to compute the ground truth for the assessments in the training set.

### sample_submission.csv
A sample submission in the correct format.
