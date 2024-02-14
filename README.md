# sber-salute-speech-recognition

A library for getting audio transcriptions from the SBER Salute Speech service https://developers.sber.ru/docs/ru/salutespeech/recognition/recognition-sync.

## Getting started

1. Create an account on https://developers.sber.ru/portal/products/smartspeech
2. Generate a client secret
3. Capture the auth key

## Install

```bash
npm install sber-salute-speech-recognition
```

## Usage

```ts
import {
  SberSaluteSpeechRecognitionService,
  AudioEncoding,
} from 'sber-salute-speech-recognition';

const recognitionService = new SberSaluteSpeechRecognitionService(AUTH_KEY);
const { text, normalizedText } = await recognitionService.speechToText(
  pathToAudioFile,
  AudioEncoding.MP3,
);
```

## AccessToken Scope

The `scope` property is set during the instantiation of the `SberSaluteSpeechRecognitionService` class.
If no value is provided, it defaults to `Scope.Personal`.

Here is an example of how to use the `scope` property:

```typescript
import {
  SberSaluteSpeechRecognitionService,
  Scope,
} from 'sber-salute-speech-recognition';

const service = new SberSaluteSpeechRecognitionService(
  AUTH_KEY,
  undefined,
  Scope.Corporate
);
```

In this example, the `scope` property is set to `Scope.Corporate` what equals `SALUTE_SPEECH_CORP`.
If you want to use the `SALUTE_SPEECH_PERS` scope,
you can either pass `Scope.Personal` as the third argument or omit the third argument entirely,
as it defaults to `Scope.Personal`.

## Hints param

For improve speech recognition you can pass in `speechToText` method hints param

Here is example of how to use the `hints` param:

```typescript
import {
  SberSaluteSpeechRecognitionService,
  AudioEncoding,
} from 'sber-salute-speech-recognition';

const recognitionService = new SberSaluteSpeechRecognitionService(AUTH_KEY);
const { text, normalizedText } = await recognitionService.speechToText(
  pathToAudioFile,
  AudioEncoding.MP3,
  {
    words: ['card', 'name'],
    enable_letters: true,
    eou_timeout: "2s"
  }
);
```

In this example , we pass object with props `words`, `enable_letters`, `eou_timeout`. 

`words` - A list of words or phrases whose recognition we want to strengthen. 
Here you can list the words that the user is likely to pronounce

`enable_letters` - A short phrase model that improves recognition of single letters and short words. 
Possible values: `true` and `false`

`eou_timeout` - Setting up recognition of the end of a phrase (End of Utterance - eou). 
Such recognition will be expected after the end of the phrase for as many seconds as set in this parameter. 
Possible values are from 0.5 to 5 seconds.

# Channels count

The channels_count allows to override the number of channels to recognize in the audio file. If not specified, the number of channels will be determined automatically.

Possible values:
undefined - channels count will be determined automatically
1 - mono
2 - stereo

```ts
import {
  SberSaluteSpeechRecognitionService,
  AudioEncoding,
} from 'sber-salute-speech-recognition';

const recognitionService = new SberSaluteSpeechRecognitionService(AUTH_KEY);
const { text, normalizedText } = await recognitionService.speechToText(
  pathToAudioFile,
  AudioEncoding.MP3,
  1
);
```

In this example we set channels count to 1.