# Emotional-computing-brain-computer-interface

Brain-computer interface circuit

I introduction of the basic information of the competition
1.	Competition background
Emotional computing technology, which enables machines to understand human emotions, is becoming a research hotspot in the fields of human-computer interaction, mental health and artificial intelligence. Compared with speech, expression, heart rate and other behaviors and peripheral physiological signals, EEG can directly reflect individual emotional experience information, and EEG emotional computing/emotional brain-computer interface has been widely concerned by academic circles in recent years.
Due to the individual differences in emotional experience, how to realize cross-individual robust emotional recognition has always been a major challenge for the practical application of EEG emotional computing/emotional brain-computer interface (Hu et al. 2019). Facing this challenge, this contest provides participants with a batch of EEG data from 80 subjects with known emotional state information. Participants are required to establish an EEG calculation model with cross-individual emotional recognition ability, conduct real-time emotional recognition on another batch of subjects' EEG data, and determine the competition results according to the accuracy of emotional recognition.
2.	Competition task
Preliminary stage: Participants build a real-time cross-individual EEG emotion recognition model according to the provided training data set. The training data included 28 emotional videos from 80 subjects (9 kinds of emotions: anger, nausea, fear, sadness, neutrality,
Entertainment, motivation, happiness, warmth) of the 32-channel EEG signal. EEG emotion recognition model needs to be in 1 second time scale.
Identify the above nine kinds of emotional states.
The performance evaluation of the algorithm model constructed by the contestants is carried out on the test data set. The test data set contains data from 18 people who were
Participants watched the EEG data of the same 28 emotional videos. The preliminary results are those of the contestants' algorithm model on the test data set.
1 second time scale emotion recognition accuracy. The final rules will be announced later.
 
II. Data and Evaluation
1.	Data acquisition process


The EEG data acquisition process is shown in the above figure. Subjects watch a total of 28 emotional videos in 7 block. The 28 videos are composed of 4 negative emotions (anger, nausea, fear, sadness), 3 videos each, 4 videos of neutral emotions, and
Four kinds of positive emotions (pleasure, motivation, happiness and warmth) are composed of three videos. These video materials are taken from Chinese Emotional Fragments Standard Database (Ge et al., 2019), Positive Emotion Database (Hu et al., 2017, 2019) and FilmStim Database (Schaefer et al., 2010). The average length of video clips is 67s, ranging from 34s to 129s. Chinese subtitles have been re-added to the segments of the video that contain non-Chinese conversations to ensure that Chinese native speakers can fully understand the content of the video. For specific video information, please refer to Schedule 1- Emotional Inducing Materials.
Subjects watch 4 videos (positive, negative or neutral) with the same titer in each block, and watching one video is a trial. Each trial consists of five seconds of black screen gaze point presentation, video playback and emotional experience self-report. At the end of each trial, the subjects need to complete a simple emotional experience report, rest for at least 30 seconds, calm their emotions as much as possible and continue the experiment. At the end of each block, the subjects were asked to complete 20 math problems, so as to minimize the influence of previous emotional state on the follow-up experiments. See Li et al., 2020 and Hu et al., 2022 for more detailed information on data acquisition process.
EEG data were collected in two batches. The first batch collected valid data of 54 people (No.1~54), and the second batch collected valid data.
According to 80 people (26 people in public, No.55~80), the experimental process is the same (but the sequence and names of channels are slightly different), and all of them are carried out by Boruikang Neusen.W32 equipment, with CPz as the reference electrode and AFz as the ground electrode, and 32 channels of EEG data are recorded.
The first batch of 54 people, the channel sequence is:
 
['Fp1', 'Fp2', 'Fz', 'F3', 'F4', 'F7', 'F8', 'FC1', 'FC2', 'FC5', 'FC6', 'Cz', 'C3', 'C4', 'T3', 'T4', 'A1',
'A2', 'CP1', 'CP2', 'CP5', 'CP6', 'Pz', 'P3', 'P4', 'T5', 'T6', 'PO3', 'PO4', 'Oz', 'O1', 'O2']
The second batch of 26 people, the channel sequence is:
['Fp1', 'Fp2', 'Fz', 'F3', 'F4', 'F7', 'F8', 'FC1', 'FC2', 'FC5', 'FC6', 'Cz', 'C3', 'C4', 'T7', 'T8', 'CP1',

'CP2', 'CP5', 'CP6', 'Pz', 'P3', 'P4', 'P7', 'P8', 'PO3', 'PO4', 'Oz', 'O1', 'O2', 'A2', 'A1']
The channel T3/4 of the first batch corresponds to the channel T7/8 of the second batch; The first batch T5/6 and the second batch P7/8
Correspondence, that is, the position of the electrodes on the scalp is exactly the same.
The test set was taken from the unpublished part of the second batch. Therefore, players need to adjust the order of the first batch of channels by themselves based on the second batch of channels (the channel adjustment code is provided in the sample code for reference).


2.	Introduction to data format

(1)	Training data set
(a)	Data composition
The training data set contains EEG data from 80 subjects watching emotional videos.
The EEG data of each subject is a pkl matrix with a shape of 33*N, in which the first 32 lines correspond to 32 leads of EEG signals, and the last line corresponds to Trigger, and N indicates the number of sampling points. The size of N is related to the data acquisition time, which is about 1.5 hours for each subject. The training data set provides unprocessed original EEG signals.
(b)	Event guide number
Training data events are as follows:


definition	
Start the experiment.	
Block, start	
Video number	Current trial
Video start	Current trial
End of video	
End of Block	
End of experiment
Trigger	25  0 	24  2 	1~28	24  0 	24  one	24  three	25  one


Experiment Start Event 250: This event indicates that the experiment is officially started. Start Event 242: This event indicates the start of Block.
Video 1-28: Different events correspond to different experimental video materials (see Table 1).
Current trial Video Start Event 240: This event occurs 0.1s after the video event, indicating that the video starts playing.
 
Current trial Video End Event 241: This event indicates that the video ends playing. End event 243: This event indicates the end of the Block.
Experiment End Event 251: This event indicates the end of the experiment.
(2)	Test data set
(a)	Data composition
The test data set contains raw EEG data from 18 subjects. The data structure of the test data set is consistent with that of the training data set, the data acquisition process is the same as that of the training data set, and the event codes are slightly different. The test data set randomly confuses the video sequence, and corrects the baseline of the data between every two videos, so the adjacent two videos are not necessarily the same price.
These 18 subjects do not overlap with the 80 subjects in the training data set.
The test data set can't be downloaded, stored in the competition server, and only visible to the contestants' algorithms in the framework.

(b)	Event guide number
The serial number and starting position information of the video are no longer provided in the test data, and the Trigger numbers visible to the players are as follows:

definition	Start the experiment.	Block, start	End of Block	End of experiment
Trigger	25  0 	24  2 	24  three	25  one


Experiment Start Event 250: This event indicates that the experiment is officially started, and the test frame will start data transmission.
Block start event 242: This event indicates the start of Block, and the contest frame will call the algorithm model of the player to obtain the emotion recognition result.
End event 243: This event indicates the end of the Block, and the contest frame will stop calling the algorithm model of the player.
End of experiment event 251: This event indicates the end of the experiment, and the contest frame will stop sending data until the next experiment start event 250.
(3)	Lead table
As shown in Attached Tables 2.1 and 2.2, A1/A2 corresponds to the left and right mastoids, and the physical reference electrode site is CPz and the ground electrode site is AFz during the collection process. (This lead sequence corresponds to the number of rows in the matrix, that is, the first row in pkl data, that is, Fp1 channel of EEG cap)
 
III. Competition requirements and algorithm specifications
1.	Competition requirements



This competition requires participants to build an EEG emotion recognition model, and receive the data packets issued by the competition framework in real time to
1 second time scale to identify 9 kinds of emotional states. The process of the competition is as follows:
（1）	Model initialization
After the title framework is started, an instance of the player's MyAlgorithm class will be created-players need to complete the initialization of models and the like in the MyAlgorithm class.
（2）	data procurement
The test frame will read and analyze the test data in real time. After detecting the 250 events at the beginning of the experiment, the test frame will pack the data packet in units of 0.2s and send it. Players can get the latest data packet by calling the get_data function, and the data packet contains 0.2s experimental EEG data (250Hz, 32 EEG +1 Trigger).
（3）	Result return
After the contest frame detects the 242 event at the beginning of block, the contest frame will call the EEG emotion recognition function algorithm completed by the player once every five packets (1s data) while sending data packets, recognize the emotion of the latest 1s EEG data, and receive the return result in the prescribed format (see Code Specification (3)).
The algorithm needs to return the result of int structure from 0 to 8. The corresponding emotional labels from 0 to 8 are: anger is 0, nausea is 1, fear is 2, sadness is 3, neutrality is 4, pleasure is 5, motivation is 6, happiness is 7, and warmth is 8. (see attached table 1)
The contestant's algorithm needs to give emotion to all the data from event 242 to event 243 in the test data in 1s units.
Identify the result. The scoring program will automatically extract the information of the video playing stage to count the players' scores (since the experiment uses serial port to mark the events, there is a difference of tens of milliseconds between the lengths of different subjects' videos, so the first and last 1s of the video are not counted in the score settlement).
 
The returned results of the non-video playing stage are not involved in scoring.
After the title frame detects the 243 event of the end of block, it will continue to provide data packets, and at the same time, it will no longer call the EEG emotion recognition function algorithm of the player until it receives the start event of block again, and so on.
（4）	Next subject
After receiving the end event 251 of the current subject, the system stops providing data packets and waits for the next subject's experiment.
Start the 250 event and repeat the above operation.
（5）	Real time requirement
There is no limit to the duration of single discrimination in the preliminary competition. However, for the algorithm with time-consuming and abnormal resource consumption, the Organizing Committee will stop the operation of the algorithm and inform the contestant to optimize the algorithm after the expert group judges and confirms it.
The final stage will limit the time of single judgment. If the single judgment time exceeds 0.5s, the judgment will be skipped and counted as 0. Therefore, in order to ensure the smooth progress of the final, the algorithm team that takes too long to make a single judgment in the preliminary round may not be able to achieve good results in the final.
2.	Code specification

In this competition, players need to complete the myAlgorithm class in MyAlgorithm.py under the algorithm folder, and realize the get_data function of receiving data and the algorithm function of emotion recognition. The title also provides a reference code for players' reference format.
(1)	MyAlgorithm class under MyAlgorithm.py
This class is the calling interface when initializing the player model in the running process of the competition framework, and the player will complete the initialization of parameters and models in this step.
(2)	Get_data function under MyAlgorithm class
This function is used to input the latest EEG data packet (0.2s, 250Hz, 32 EEG +1 Trigger).
(3)	The algorithm function under MyAlgorithm class
This method is used to return the emotion tag corresponding to the current 1s EEG. Players need to return a result of 0~8 with the data format of int, corresponding to different emotional labels (see Table 1). When the contestant returns the result that does not meet the requirements (such as array, null value or out-of-range value, etc.), this judgment will score 0 points.
* Note:
Note that in this competition, players are not allowed to change the above class names or function names, otherwise the results will be invalid.
 
3.	Scoring standards and reports
The final score is expressed by the average accuracy (Acc) of 18 subjects, and the calculation rules are as follows:
 

𝒄𝒄 =
 


 

 

∑

 


 

 

∑

 


 

 

Correct samples _ in _ current _ trial: the number of samples (1 sample per second) with correct emotional recognition results in seconds corresponding to the video in the current trial;
TotalSamples_in_current_trial: the total number of samples in seconds corresponding to the video in the current trial (1 sample per second, regardless of the beginning and end of the video);
Trials: the number of trials in each subject, which is 28 in this experiment; Subs: the number of subjects in the test set, which is 18 in this competition;
In the debugging stage, players need to supplement the scoring program according to the provided sample code.
In the preliminary stage, the average accuracy rate of the feedback test set is taken as the final score of the players in the competition question framework.
 
attached table

Schedule 1. Emotion-inducing materials

Video sequence number	Duration (seconds)	valence	Emotion category	Emotional label
one	81  	negative	angry	0  
2  	63  	negative	angry	0  
three	73  	negative	angry	0  
four	seventy-eight	negative	feel sick	one
five	sixty-nine	negative	feel sick	one
six	90  	negative	feel sick	one
seven	fifty-six	negative	frightened	2  
eight	60  	negative	frightened	2  
nine	81  	negative	frightened	2  
10  	45  	negative	sad	three
11  	60  	negative	sad	three
12  	81  	negative	sad	three
13  	35  	neutral	neutral	four
14  	forty-four	neutral	neutral	four
15  	38  	neutral	neutral	four
16  	43  	neutral	neutral	four
17  	55  	positive	make happy	five
18  	sixty-nine	positive	make happy	five
19  	73  	positive	make happy	five
20  	12  nine	positive	encourage	six
21  	77  	positive	encourage	six
22  	83  	positive	encourage	six
23  	34  	positive	happy	seven
24  	37  	positive	happy	seven
25  	67  	positive	happy	seven
26  	63  	positive	tender loving care	eight
27  	83  	positive	tender loving care	eight
28  	77  	positive	tender loving care	eight
 
(Note:
1.	In this experiment, serial port is used to mark events, and the data length of different subjects is about tens of milliseconds different. To correct this error, the scoring system will not score the first and second of the video;
2.	In the first batch, the average length of video No.22 of subjects No.26~54 is 83s, which is about 7s more than that of other subjects (including the second batch of subjects) (most of the clips are the forward part of the original clip);
3.	We found that the length of No.27 video of No.31 subjects in the first batch was longer because it was not recorded, and the contestants could handle it according to their own needs)
Attached Table 2.1 Lead Table of the First Batch (No.1~54)

one	Fp1	nine	FC2	17  	A1	25  	P4
2  	Fp2	10  	FC5	18  	A2	26  	T5
three	Fz	11  	FC6	19  	CP1	27  	T6
four	F3	12  	Cz	20  	CP2	28  	PO3
five	F4	13  	C3	21  	CP5	29  	PO4
six	F7	14  	C4	22  	CP6	30  	Oz
seven	F8	15  	T3	23  	Pz	31  	O1
eight	FC1	16  	T4	24  	P3	32  	O2
Attached Table 2.2 Lead Table of the Second Batch (No.55~80)

one	Fp1	nine	FC2	17  	Cp1	25  	P8
2  	Fp2	10  	FC5	18  	Cp2	26  	Po3
three	Fz	11  	FC6	19  	Cp5	27  	Po4
four	F3	12  	Cz	20  	Cp6	28  	Oz
five	F4	13  	C3	21  	Pz	29  	O1
six	F7	14  	C4	22  	P3	30  	O2
seven	F8	15  	T7	23  	P4	31  	A2
eight	FC1	16  	T8	24  	P7	32  	A1

references
Ge, Y., Zhao, G., Zhang, Y., Houston, R.J., Song, J., (2019). A standardised database of Chinese emotional film clips. Cognition and Emotion, 33(5): 976-990.
Hu, X., Yu, J., Song, M., Yu, C., Wang, F., Sun, P., Wang, D.* & Zhang, D.* (2017). EEG Correlates
 
of Ten Positive Emotions. Frontiers in Human Neuroscience, 11(796), 2765.
Hu, X., Chen, J., Wang, F. & Zhang, D. Ten challenges for EEG-based affective computing. Brain Science Advances, 5, 1–20 (2019).
Hu, X., Zhuang, C., Wang, F., Liu, Y.-J., Im, C. H., & Zhang, D.* (2019). fNIRS Evidence for Recognizably Different Positive Emotions. Frontiers in Human Neuroscience, 13, 120.
Hu, X., Wang, F. & Zhang, D. (2022). Similar brains blend emotion in similar ways: Neural representations of individual difference in emotion profiles. Neuroimage 247, 118819.
Li, W., Hu, X., Long, X., Tang, L., Chen, J., Wang, F., Zhang, D. (2020). EEG responses to emotional videos can quantitatively predict big-five personality traits. Neurocomputing 415, 368–381.
Schaefer, A., Nils, F., Sanchez, X., Philippot, P., (2010). Assessing the effectiveness of a large
database of emotion-eliciting films: a new tool for emotion researchers. Cognition and Emotion, 24 (7), 1153–1172.
