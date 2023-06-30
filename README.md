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
import { SberSaluteSpeechRecognitionService } from 'sber-salute-speech-recognition';

const recognitionService = new SberSaluteSpeechRecognitionService(AUTH_KEY);
const { text, normalizedText } = await recognitionService.speechToText(
  pathToAudioFile,
  'MP3'
);
```
