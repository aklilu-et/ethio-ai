Open-source speech-to-text and language models for Ethiopian languages, written only in Fidel (ፊደል).

This project builds AI models that listen to and write Amharic, Afaan Oromo, Sidaama and Wolaytta using the Ge'ez (Fidel) 
script for every language. The long-term goal is voice-to-voice translation between Ethiopian languages.

Core rule: Fidel only. Every Ethiopian language in this project is written, trained and evaluated in Fidel. 
No Latin-script Ethiopian text is used for training, and no Latin-to-Fidel converter is used anywhere. See The Fidel-only rule.

Languages
Language	Script in this project	Tag
Amharic (አማርኛ)	Fidel	[AMH]
Afaan Oromo	Fidel	[ORM]
Sidaama	Fidel	[SID]
Wolaytta	Fidel	[WAL]

The tag is placed at the start of every transcript, so one model can both transcribe speech and identify its language.

What this project builds
1. Speech-to-text (ASR)

Turns speech into Fidel text.

Path	Starting model	Licence	Notes
Strict (main)	facebook/w2v-bert-2.0	Check model card	Base speech model that has never learned any alphabet; trained here with a Fidel-only output layer
Benchmark	snapwre/hohe-asr-amharic	CC BY 4.0	Best open Amharic model found (about 16% word error). Used as the score to beat
2. Language model (LLM)

Reads, writes and follows instructions in Fidel for all four languages.

Starting model	Licence	Notes
Qwen3 (4B–8B)	Apache 2.0	Recommended base; Fidel tokens added, then further trained on Fidel text
Gemma 3 (4B–8B)	Google's own terms	Comparison candidate
3. Two-speaker transcription

Separates conversations between two people before transcribing:
audio → who spoke when (pyannote Community-1) → split overlapping voices (SpeechBrain SepFormer) → ASR → labeled transcript

The Fidel-only rule
Output alphabet: the speech model's vocabulary contains only Fidel characters, Ethiopic punctuation (። ፣ ፡), the word separator, and the language tags. It cannot produce Latin letters.
Training data: any transcript or document containing Latin-script Ethiopian text is rejected, not converted.
Oromo, Sidaama and Wolaytta text comes only from our own Fidel-transcribed recordings.
Spelling standard: every language follows a written standard in standards/ covering long vowels, doubled consonants, and sounds Amharic Fidel lacks.
Numbers are written as Fidel words (ሃያ ሁለት, not 22).
Automatic check: every transcript is tested against the allowed alphabet before training. Anything outside it is rejected.
