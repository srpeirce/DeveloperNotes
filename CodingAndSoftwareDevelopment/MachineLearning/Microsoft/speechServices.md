# Speech Services

Microsoft speech has higher accuracy than humans…apparrently.

- The switchboard test
  - Recorded conversations between strangers about things like sport or politics
  - Use this data, get human transcriptions to rate error rate
  - Azure Word error rate: 5.1%
  - Humans 5.9%...althought humans they fudged the number to match lol
  - [Article MS talked about - Researchesr achieve ne conversational speech recognition milestone](https://www.microsoft.com/en-us/research/blog/microsoft-researchers-achieve-new-conversational-speech-recognition-milestone/)

## Bing speech

- Speech recognition platform
- API
- SDK For windows, IOS, android
- Send it order, comed back with text
- Same tech as Cortana

Different types of speech

- Short commandy
- Conversation
- Dictation
- Real time

Availble

- End of senteance determination
- Profanity detection

Example:
http://aka.ms/blackradley

Bing Speech + Luis = Take what perople are saying, then run it against sentiment analysis

Cortana listens and also predicts what is coming next.

Use speech to understand, and read out text.
Cool to use in conjection with bot framework/Q&A etc

## Speaker Recogntiion

- Ideentify from voice
- Real time speech recognition - https://azure.microsoft.com/en-gb/services/cognitive-services/speech/
  - Can test
  - Transalation between languages
    - Seems quite good, not perfect though!

## Custom Speech

2 most important components.

- Language model
  - Probability discttubution between words…how to choose words between similar sounding words
- Acoustic model
  - How words are made up

Built on Bing speech, allows custom language models.

- Might have keywords or product names, so it isn't trying to convert to words it knows
- Custom environments - e.g. field engineers on train line, office etc
  - Create own model to help train out background noise

Microsoft say they have the best speech recognition.