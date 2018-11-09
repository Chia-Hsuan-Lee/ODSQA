
# ODSQA: OPEN-DOMAIN SPOKEN QUESTION ANSWERING DATASET

This repository contains dataset for the paper:
> ODSQA: OPEN-DOMAIN SPOKEN QUESTION ANSWERING DATASET

> Chia-Hsuan Lee, Shang-Ming Wang, Huan-Cheng Chang and Hung-Yi Lee

If you have any questions and suggestions, feel free to contact **chiahsuan.li@gmail.com**

# Introduction
Text-based reading comprehension has been widely studied , on which machine is already comparable with human. On the other hand, accessing large collections of multimedia or spoken content is much more difficult and time-consuming than plain text content for humans. It’s therefore highly attractive to develop machines
which can automatically understand spoken content. 
One spoken question answering corpus is Spoken-SQuAD (https://github.com/chiahsuan156/Spoken-SQuAD/), which is generated from SQuAD dataset through Google Text-to-Speech (TTS) system. Although Spoken-SQuAD is large enough to train state-of-the-art QA models, it is artificially generated, so it is still one step away from real SQA. Therefore, we release an SQA dataset, ODSQA, with more than three thousand questions. ODSQA is a Chinese dataset, and  to the best of our knowledge, the largest real SQA dataset for extraction-based QA task. 

# Corpus Description
In ODSQA, both the document and the question are in spoken form and the text-formed answer to each question is always a span in the document. Our reference texts are from Delta Reading Comprehension Dataset (DRCD)(https://arxiv.org/abs/1806.00920), which is an open domain traditional Chinese machine reading comprehension (MRC) dataset. 

20 speakers were recruited to read the questions and paragraphs in the development set of DRCD. All the recruited speakers were native Chinese speakers and used Chinese as their primary language. For document, each sentence was shown to speaker respectively. The speaker was required to speak one sentence at a time. All the sentences of the same document were guaranteed to be spoken by the same speaker. The document and the question from the same data example do not have to be recorded by the same speakers.
We collected 3,654 question answer pairs as the ODSQA testing set and the speech was all sampled at 16 kHz.

To train machine comprehension models, we used iFLYTEK ASR system (https://www.xfyun.cn/doccenter/asr) to transcribe the collected data into ASR transcriptions.

We provide two versions of ODSQA that are already transcribed by iFLYTEK ASR system

In the first version, we keep the questions in text form as in DRCD (no ASR errors):

**ODSQA_textq_test-v1.1.json**

In the second version, we provide the more challenging one with spoken questions (hypothese that contain ASR errors):

**ODSQA_spokenq_test-v1.1.json**


#  Artificially Generated Corpus
To augment the training data, we conduct the following procedures to generate transcriptions of spoken version DRCD. First, we used iFLYTEK Text-to-Speech system (https://www.xfyun.cn/doccenter/tts) to generate the spoken version of the articles in DRCD. Then we utilized iFLYTEK ASR system to obtain the corresponding ASR transcriptions. In this corpus, we left the questions in the text form. This artificially generated corpus is called DRCD-TTS.

#  Back-translation Corpus
To improve the robustness to speech recognition errors of QA model, we augmented DRCD training dataset with back-translation. We conduct the following procedures to generate an augmented training set. First, the DRCD training set is translated using Google Translation system into English. Then this set is translated back into Chinese through Google Translation system. This resulting dataset is called DRCD-backtrans.


|Dataset| QA-pairs   | Hours      | M-spkrs  | F-spkrs  | WER-D(%)  | WER-Q(%)  | Avg D Len  | AvgQ Len  | 
|:---------:|:---------: |:--------:| :--------:| :--------:|:--------:|:--------:|:--------:|:--------:|
|ODSQA| 3654| 25.28|7|13|19.11|18.57|428|22|
|DRCD-TTS|16746|--|--|--|33.63|--|332|20|
|DRCD-backtrans|15238|--|--|--|45.64|--|439|20|

# Citation
If you use the dataset in your work, please cite the following paper as:

```
@article{lee2018odsqa,
  title={ODSQA: Open-domain Spoken Question Answering Dataset},
  author={Lee, Chia-Hsuan and Wang, Shang-Ming and Chang, Huan-Cheng and Lee, Hung-Yi},
  journal={arXiv preprint arXiv:1808.02280},
  year={2018}
}
```
