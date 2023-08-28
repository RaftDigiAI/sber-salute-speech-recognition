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
  AudioEncoding.MP3
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
