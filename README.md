# German Text to Speech Voice (thorsten)

Voice and vocoder models for [larynx](https://github.com/rhasspy/larynx) based on the free [thorsten dataset](https://github.com/thorstenMueller/deep-learning-german-tts/).

Used in [Rhasspy](https://github.com/rhasspy) in the [rhasspy-tts-larynx-hermes](https://github.com/rhasspy/rhasspy-tts-larynx-hermes) service.

[Samples](samples)

## Usage

```sh
$ larynx \
    --model /path/to/tts-checkpoint.pth.tar \
    --vocoder-model /path/to/vocoder-checkpoint.pth.tar \
    --output-file /path/to/output.wav \
    'Mir geht es gut, danke!'
```

### Docker

Run a web server at http://localhost:5002

```sh
$ docker run -it -p 5002:5002 \
    --device /dev/snd:/dev/snd \
    rhasspy/larynx:de-thorsten-1
```

Endpoints:

* `/api/tts` - returns WAV audio for text
    * `GET` with `?text=...`
    * `POST` with text body
* `/api/phonemize` - returns phonemes for text
    * `GET` with `?text=...`
    * `POST` with text body
* `/process` - compatibility endpoint to emulate [MaryTTS](http://mary.dfki.de/)
    * `GET` with `?INPUT_TEXT=...`

## Model Details

* Type: [Glow-TTS](https://arxiv.org/abs/2005.11129)
* Sample rate: 22050 Hz
* Frequency range: 0-8000 Hz

See [configuration](config.json) for details.

## Vocoder Details

* Type: [Multi-band MelGAN](https://arxiv.org/abs/2005.05106)
* Sample rate: 22050 Hz
* Frequency range: 0-8000 Hz

See [configuration](vocoder/config.json) for details.

## Files

Some files are split into multiple parts so that they can be uploaded to GitHub. This is done with the `split` command:

```bash
split -d -b 25M FILE FILE.part-
```

They can be recombined simply with:

```bash
cat FILE.part-* > FILE
```
