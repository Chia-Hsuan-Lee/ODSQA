
# ODSQA: OPEN-DOMAIN SPOKEN QUESTION ANSWERING DATASET

This repository contains dataset for the IEEE SLT 2018 paper:
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

## Data format 資料格式

- version : <String> (version of the dataset)
- data : <Array>
  - title : <String> (article title)
  - id : <String> (article id)
  - paragraphs : <Array>
    - id : <String> (articleid_paragrpahid) 
    - context : <String> (content of paragraph)
    - qas : <Array>
      - question : <String> (content of quesiton)
      - id :<String> (articleid_paragrpahid_questionid) 
      - answers : <Arrays>
        - answer_start : <int> (the start index of answer span in paragrpah)
        - id : <String> (answer id)
        - text : <string> (answer content)


## Example
  
  ```json
{
  "version": "1.3",
  "data": [
    {
      "title": "德國總理",
      "id": "6331",
      "paragraphs": [
        {
          "context": "聯邦總理是德意志聯邦共和國的政府首腦。他只要聯邦部長，並圈定德國聯邦政府的政治方針。張力是由德國聯邦會議，根據聯邦總統的建議，未經辯論的選舉產生，再經聯邦總統任命，就可以正式成爲總理，而聯邦總統不能拒絕任命總理。總理，通常我一會再打妲己，執政黨的領袖，另外設有副總理，一直作爲副手。在神聖羅馬帝國時代，總理掌管的機構是重要機構之一。在普魯士和奧地利，19世紀的帝國結束之後，總理的職位又重新被引入。俾斯麥在北德意志邦聯是祈願聯邦總理，他在1871年德意志帝國建立後，讓帝國總理或者翻譯爲宰相。納粹德國時代，希特勒再次使用帝國總理的支撐，最後希特勒更元首的身份兼任帝國總理，成爲納粹德國的最高統治者。二戰之後的一支聯邦共和國成立，其政府首腦，簡稱聯邦總理，但是不僅德國聯邦政府的首腦被稱爲聯邦總理，奧地利政府的首腦也稱聯邦總理。另一方面，同樣在二戰成立的德意志民主共和國，也有設立總統一職，稱爲部長會議主席，不過這一職務的權利還得爲在德國統一社會黨總書記之下。",
          "id": "6331-1",
          "qas": [
            {
              "id": "6331-1-1",
              "question": "誰負責指派聯邦部長?",
              "answers": [
                {
                  "id": "1",
                  "text": "聯邦總理",
                  "answer_start": 0
                },
                {
                  "id": "2",
                  "text": "聯邦總理",
                  "answer_start": 0
                }
              ]
            },
            {
              "id": "6331-1-2",
              "question": "聯邦總統能不能不任命聯邦總理?",
              "answers": [
                {
                  "id": "1",
                  "text": "不能",
                  "answer_start": 97
                },
                {
                  "id": "2",
                  "text": "不能",
                  "answer_start": 97
                }
              ]
            },
            {
              "id": "6331-1-3",
              "question": "德意志帝國與何年建立。",
              "answers": [
                {
                  "id": "1",
                  "text": "1871年",
                  "answer_start": 219
                },
                {
                  "id": "2",
                  "text": "1871年",
                  "answer_start": 219
                }
              ]
            }
          ]
        }
      ]
    }
  ]
}
  
  ```



#  Artificially Generated Corpus
To augment the training data, we conduct the following procedures to generate transcriptions of spoken version DRCD. First, we used iFLYTEK Text-to-Speech system (https://www.xfyun.cn/doccenter/tts) to generate the spoken version of the articles in DRCD. Then we utilized iFLYTEK ASR system to obtain the corresponding ASR transcriptions. In this corpus, we left the questions in the text form. This artificially generated corpus is called DRCD-TTS.

#  Back-translation Corpus
To improve the robustness to speech recognition errors of QA model, we augmented DRCD training dataset with back-translation. We conduct the following procedures to generate an augmented training set. First, the DRCD training set is translated using Google Translation system into English. Then this set is translated back into Chinese through Google Translation system. This resulting dataset is called DRCD-backtrans.


|Dataset| QA-pairs   | Hours      | M-spkrs  | F-spkrs  | WER-D(%)  | WER-Q(%)  | Avg D Len  | AvgQ Len  | 
|:---------:|:---------: |:--------:| :--------:| :--------:|:--------:|:--------:|:--------:|:--------:|
|ODSQA| 1,465 | 25.28|7|13|19.11|18.57|428|22|
|DRCD-TTS|16746|--|--|--|33.63|--|332|20|
|DRCD-backtrans|15238|--|--|--|45.64|--|439|20|

# Citation
If you use the dataset in your work, please cite the following paper as:

```
@inproceedings{lee2018odsqa,
  title={ODSQA: Open-Domain Spoken Question Answering Dataset},
  author={Lee, Chia-Hsuan and Wang, Shang-Ming and Chang, Huan-Cheng and Lee, Hung-Yi},
  booktitle={2018 IEEE Spoken Language Technology Workshop (SLT)},
  pages={949--956},
  year={2018},
  organization={IEEE}
}
```
