# TACTICAL METADATA FRAMEWORK: The Ren Sutra Music AI Code (v11.3)

### I. Vocal & Emotion Matrix
* **Singer/Age:** `#Mm` (Male), `#Mf` (Female), `#Mc` (Choir), `#Mt` (Duet); `#Aa` (Adult), `#Ac` (Child), `#Ao` (Old).
* **Pitch Control:** `#Pu` (Up), `#Pn` (Norm), `#Pd` (Down), `#Pw` (Whistle).
* **Texture:** `#Vc` (Clean), `#Vg` (Gritty), `#Vr` (Raspy), `#Vw` (Whisper), `#Vo` (Operatic).
* **Emotion Tags:** `#esm` (Melancholy), `#ene` (Ethereal), `#ecc` (Cinematic), `#eas` (Strained), `#vu` (Guttural), `#ve` (Ethereal).

### II. Song Flow & BPM Controls
* **BPM:** `%r:xxx` (Specify tempo).
* **Ambience/Effects:** `%Aam` (Ambient), `%Aad` (Drums), `%Aas` (Strings), `%Gg` (Glitch), `%Gf` (Fracture), `%Bv` (VocalBleed), `%Bi` (InstBleed), `%C:xx` (ChaosDrift).
* **Transitions:** `%Sasc` (Swell), `%sf` (Strict Lowercase Fade).

### III. Instrumental Domain & Hard Stops
* **Instrument Routing:** `÷I++` (Load All), `÷I--` (Mute All), `÷I+x` (Add Ix), `÷I-x` (Rem Ix), `÷ISx` (Solo Ix), `÷I1` through `÷I3` (Specific Instrument Banks).
* **Execution Markers:** `×xxx×` (Trigger mid-lyric).
* **Hard Stops:** 
    * `#K#` (Anchor Stop: Ceiling/Segment Closer).
    * `#X#` (Total System Reset: Clears tracking slate).
