---
layout: default
title: Third-party notices
---

[Back to the documentation](./)

```text
SynthVox -- Third-Party Notices
========================================

This plugin performs 100% offline, on-device text-to-speech. It bundles or
depends on the following third-party components. No GPL, LGPL, or other
copyleft-licensed code or content is used anywhere in this plugin.


1. Kokoro-82M (acoustic model + English/Chinese/Spanish/French/Hindi voice style vectors, and the
   fm_lucien / gm_nikos / gf_eleni voices mixed from them)
-------------------------------------------------------------------------------------
Source:  https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX
         (ONNX export of https://huggingface.co/hexgrad/Kokoro-82M)
License: Apache License 2.0
Used as: Content/Models/Kokoro82M.uasset (the acoustic model, run via NNE/
         ONNX Runtime), Content/Voices/*.uasset (per-voice style vectors).

Copyright 2024 hexgrad and contributors.
Licensed under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License. You may obtain a copy
of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
License for the specific language governing permissions and limitations
under the License.


2. misaki (pronunciation dictionary data only -- no code used or shipped)
--------------------------------------------------------------------------
Source:  https://github.com/hexgrad/misaki (misaki/data/{us,gb}_{gold,silver}.json)
License: MIT License
Used as: Content/Data/LexiconUS.uasset, Content/Data/LexiconGB.uasset --
         merged, English word -> phoneme dictionaries. Only the dictionary
         *data* is used; no misaki source code is included in this plugin,
         and its optional espeak-ng-based fallback is deliberately NOT used
         anywhere (see Source/SynthVox/Private/TTSPhonemizer.cpp for
         this plugin's own GPL-free rule-based fallback for out-of-dictionary
         words).

Copyright (c) hexgrad.
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.


3. DeepPhonemizer (neural grapheme-to-phoneme fallback for unknown words)
--------------------------------------------------------------------------
Source:  https://github.com/spring-media/DeepPhonemizer
License: MIT License
Used as: Content/Models/G2PEnUS.uasset -- a small Transformer model (ONNX
         export of the pretrained en_us_cmudict_ipa_forward checkpoint),
         used only for words missing from the US/GB lexicons. Trained
         entirely on CMUdict-IPA (CMUdict is public domain / BSD-2-Clause,
         Carnegie Mellon University); no espeak-ng involvement anywhere in
         this model's training data or lineage.

Copyright (c) DeepPhonemizer contributors (spring-media / as-ideas).


4. ONNX Runtime
-----------------
Source:  https://github.com/microsoft/onnxruntime
License: MIT License
Used as: the inference backend behind Epic's own NNERuntimeORT plugin
         (Engine/Plugins/NNE/NNERuntimeORT), which ships with Unreal Engine
         itself. Not bundled by this plugin; enabled as a plugin dependency.

Copyright (c) Microsoft Corporation.


5. Mandarin Chinese lexicon (jieba, pypinyin, pinyin-to-ipa -- data only)
--------------------------------------------------------------------------
Used as: Content/Data/LexiconZH.uasset -- a pre-computed Chinese word ->
         phoneme dictionary plus word-segmentation statistics, generated
         offline by Tools/model_prep/build_zh_lexicon.py. No Python code
         from any of these projects is included in this plugin; the C++
         word segmenter in Source/SynthVox/Private/TTSChineseLexicon.cpp
         is this plugin's own reimplementation of jieba's algorithm.

  a) jieba -- word list, word frequencies and HMM probability tables
     Source:  https://github.com/fxsjy/jieba
     License: MIT License
     Copyright (c) 2013 Sun Junyi

  b) pypinyin, pinyin-data, phrase-pinyin-data -- character/phrase readings
     Source:  https://github.com/mozillazg/python-pinyin
              https://github.com/mozillazg/pinyin-data
              https://github.com/mozillazg/phrase-pinyin-data
     License: MIT License
     Copyright (c) 2016 mozillazg, 闲耘 <hotoo.cn@gmail.com>
     Copyright (c) 2016-2017 mozillazg

  c) pinyin-to-ipa (pinyin -> IPA mapping, via misaki's adaptation of it)
     Source:  https://github.com/stefantaubert/pinyin-to-ipa
              https://github.com/hexgrad/misaki (misaki/transcription.py, zh.py)
     License: MIT License
     Copyright (c) Stefan Taubert; Copyright (c) hexgrad

All of the above are distributed under the MIT License:

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.


6. Greek phonemes
-----------------
Greek text is converted to phonemes by this plugin's own rules
(Source/SynthVox/Private/TTSGreekG2P.cpp); no espeak-ng is included.


7. Noto Sans Devanagari (demo UI font)
--------------------------------------
Source:  https://github.com/notofonts/devanagari
Used as: Content/Demo/Fonts/FF_NotoSansDevanagari.uasset (inside the composite font F_DemoText),
         so Hindi text in the demo UI renders. Not needed for speech synthesis.
License: SIL Open Font License 1.1:

Copyright 2022 The Noto Project Authors (https://github.com/notofonts/devanagari)

This Font Software is licensed under the SIL Open Font License, Version 1.1.
This license is copied below, and is also available with a FAQ at:
https://scripts.sil.org/OFL


-----------------------------------------------------------
SIL OPEN FONT LICENSE Version 1.1 - 26 February 2007
-----------------------------------------------------------

PREAMBLE
The goals of the Open Font License (OFL) are to stimulate worldwide
development of collaborative font projects, to support the font creation
efforts of academic and linguistic communities, and to provide a free and
open framework in which fonts may be shared and improved in partnership
with others.

The OFL allows the licensed fonts to be used, studied, modified and
redistributed freely as long as they are not sold by themselves. The
fonts, including any derivative works, can be bundled, embedded, 
redistributed and/or sold with any software provided that any reserved
names are not used by derivative works. The fonts and derivatives,
however, cannot be released under any other type of license. The
requirement for fonts to remain under this license does not apply
to any document created using the fonts or their derivatives.

DEFINITIONS
"Font Software" refers to the set of files released by the Copyright
Holder(s) under this license and clearly marked as such. This may
include source files, build scripts and documentation.

"Reserved Font Name" refers to any names specified as such after the
copyright statement(s).

"Original Version" refers to the collection of Font Software components as
distributed by the Copyright Holder(s).

"Modified Version" refers to any derivative made by adding to, deleting,
or substituting -- in part or in whole -- any of the components of the
Original Version, by changing formats or by porting the Font Software to a
new environment.

"Author" refers to any designer, engineer, programmer, technical
writer or other person who contributed to the Font Software.

PERMISSION & CONDITIONS
Permission is hereby granted, free of charge, to any person obtaining
a copy of the Font Software, to use, study, copy, merge, embed, modify,
redistribute, and sell modified and unmodified copies of the Font
Software, subject to the following conditions:

1) Neither the Font Software nor any of its individual components,
in Original or Modified Versions, may be sold by itself.

2) Original or Modified Versions of the Font Software may be bundled,
redistributed and/or sold with any software, provided that each copy
contains the above copyright notice and this license. These can be
included either as stand-alone text files, human-readable headers or
in the appropriate machine-readable metadata fields within text or
binary files as long as those fields can be easily viewed by the user.

3) No Modified Version of the Font Software may use the Reserved Font
Name(s) unless explicit written permission is granted by the corresponding
Copyright Holder. This restriction only applies to the primary font name as
presented to the users.

4) The name(s) of the Copyright Holder(s) or the Author(s) of the Font
Software shall not be used to promote, endorse or advertise any
Modified Version, except to acknowledge the contribution(s) of the
Copyright Holder(s) and the Author(s) or with their explicit written
permission.

5) The Font Software, modified or unmodified, in part or in whole,
must be distributed entirely under this license, and must not be
distributed under any other license. The requirement for fonts to
remain under this license does not apply to any document created
using the Font Software.

TERMINATION
This license becomes null and void if any of the above conditions are
not met.

DISCLAIMER
THE FONT SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT
OF COPYRIGHT, PATENT, TRADEMARK, OR OTHER RIGHT. IN NO EVENT SHALL THE
COPYRIGHT HOLDER BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
INCLUDING ANY GENERAL, SPECIAL, INDIRECT, INCIDENTAL, OR CONSEQUENTIAL
DAMAGES, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF THE USE OR INABILITY TO USE THE FONT SOFTWARE OR FROM
OTHER DEALINGS IN THE FONT SOFTWARE.


Explicitly NOT used anywhere in this plugin: espeak-ng, piper/piper-phonemize,
or any other GPL/LGPL-licensed code, model, or data.

```
