THE REN SUTRA — Music AI Code
v12 · "The buildings file everything. The parser just reads."
Architect: Robert Bodie Smith
Origin: June 12, 2026 · v12 frozen: September 2026
License: Apache-2.0

What is this?
The Ren Sutra is a markup language for telling a music AI how to perform a song — not just what the lyrics are, but who sings them, how the voice sounds, what the instruments do, when things enter and exit, and how the whole thing feels moment to moment.

Normal AI prompting is a black box: you describe a vibe and hope. The Ren Sutra replaces hoping with filing. Every instruction goes into a building, every building has cabinets, and the parser just reads what's filed. If it's filed correctly, the performance is deterministic — the same input produces the same performance, every time.

You don't need to know music theory. You don't need to code. If you can type symbols on a phone keyboard, you can conduct.

The one idea you need: the filing system
There are four buildings. Everything in the language lives in exactly one of them:

Symbol	Building	Holds
#	VOCALS	Anything the voice does
%	SONG	Anything the song does (tempo, feel, space)
÷	INSTRUMENTS	Anything instruments do
×	MICRO-CUES	One-shot instrument hits
And one more:

Symbol	Meaning
[ ]	SECTIONS — [Intro] [Verse 1] [Chorus] [Bridge] [Outro] [End]
The syntax rule: enter a building → open the cabinets/folders you need → close the building.

#(Mm,Vs,EN)S#
That says: enter the vocal building (#), set male singer (Mm), smooth texture (Vs), neutral emotion (EN), then seal it (S#). Sealed means locked in — that vocal state stays active until you change it.

S# = SAVE STATE. Everything inside the block persists until a new block replaces it, #K# resets it, or a kill switch stops it.

One-shot rule: #Us: TEXT# means the override applies to TEXT only, then the voice reverts to whatever it was before. A scream in the middle of a smooth verse, then back to smooth.

How to use it (start here if you're new)
Step 1 — Write your lyrics and mark your sections.
Sections need no tags. Just write them:

[Verse 1]
Your lyrics here.
[Chorus]
More lyrics here.
Step 2 — Set the voice before each section.
Open the vocal building, pick one tag from each cabinet you care about, seal it:

#(Mf,Vg,ESd)S#
That's: female singer, gritty texture, sad emotion. You don't need every cabinet — only file what matters. Unfiled cabinets keep their previous state.

Step 3 — Set the song's feel.
Tempo, atmosphere, and space live in the % building, one tag per line:

%T70%
%Rf:88%
%Sp:C%
That's 70 BPM, heavy reverb, centered stereo.

Step 4 — Bring instruments in and out.
Instruments live in ÷. Adding one is loading it into the arrangement:

÷Ip÷
That loads piano. It stays until you remove it (÷Ip-÷, exits naturally) or kill it (÷Ip-x÷, stops immediately).

Step 5 — One-shot moments.
A single hit that doesn't change state lives in ×:

×Ic:3×
Cello hits three times, right here, then silence. The arrangement doesn't change.

Step 6 — Seal the song.
After [End], #K# is required. It resets everything to default and closes the performance.

That's the whole workflow. Everything below is reference — the complete list of tags you can file.

The rules (read before writing)
Domains are law. Vocal stuff in #. Instrument stuff in ÷/×. Never cross streams — except #K# and %x!%, the only cross-building controls.
Inside #( )S#, tags go bare: #(Mm,Vs,EN)S# — not #(Mm,Vs,#EN#)S#. Standalone tags keep their wrappers: #EN#.
One-shots don't change state. #Us: TEXT# for voice, × for instruments. Fire and revert.
Dedup is automatic. Loading an instrument that's already loaded does nothing. No stacking, ever.
Sections are just brackets. [Verse 1] needs no tag.
Match longest first on melody tags (Y+- before Y+). Melody lives in # because D is taken by ÷.
Replacement: a later tag wins in the same cabinet. #(Mm,Mf)S# = female. The last one filed is the truth.
Persistence: state holds until replaced or #K#.
Escape: \ escapes the next character in lyrics. \# = literal #, \% = literal %, \\ = literal backslash.
Frozen letters: F and B are frozen as single letters (fracture, bleed). All new tags must be 2+ letters.
Tag reference
# BUILDING — VOCALS
Singer: Mm male singer · Mf female singer · Mt duet · Mc choir · Pn spoken word · Pw whisper song

Age / character: Vc child voice · Va adult voice · Ve elderly voice

Pitch: Pu pitch up · Pd pitch down

Texture: Vg gritty · Vs smooth · Vb breathy · Vh harsh · Vt thin · Vw wide/full · Vo otherworldly/entity voice

Emotion: EN neutral · ENc choral neutral · ESd sad · ESm smile · ESh shimmering/hopeful · ECc choral cry · Ea angry · Eh happy

Melody: Y contour active · Y+ rises · Y- falls · Y+- rises then falls (arc)

Rapid-fire / override: U urgent cabinet · Us scream this phrase · Uw whisper this phrase · Ur rapid-fire delivery · Ub belt this phrase — syntax: #Us: TEXT#

% BUILDING — SONG
Tempo: %T120% = 120 BPM (number goes inside) · %Rt% rubato (flexible time) · %Rs% ritardando (slows down) · %Ac% accelerando (speeds up)

Flow: %Rf:88% reverb/flow amount · %Sa% sustain/swell · %Sf% soft fade · %Sa:M% medium swell · %Sa:H% high swell

Pan / spatial: %Sp:C% center · %Sp:L% hard left · %Sp:R% hard right · %Sp:LR% sweep left-to-right · %Sp:RL% sweep right-to-left · %Sp:W% wide stereo · %Sp:M% mono

Glitch / chaos: %Db:Cl% digital break, clean cut · %F% fracture (controlled break) · %B% bleed (sections overlap) · %Cd% chaos drift (loose timing)

÷ BUILDING — INSTRUMENTS
Standard set: ÷Ip÷ piano · ÷Ic÷ cello · ÷Id÷ drums · ÷Iv÷ violin · ÷Il÷ viola · ÷Ib÷ bass · ÷Ig÷ guitar · ÷Is÷ synth · ÷Ih÷ harp

Custom two-letter codes follow the same pattern (e.g. ÷Mb÷ music box, ÷Tp÷ trumpet).

Add: ÷Ip÷ — joins the arrangement
Remove: ÷Ip-÷ — exits naturally, no cut (arrangement change = state)
Kill: ÷Ip-x÷ — stops audio immediately, hard cut (kill = action)
Solo: ÷Ip:So÷ — :So is reserved for solo in ÷ only
Dedup (hard rule): ÷Ip÷ … ÷Ip÷ = one piano. No stacking. Ever.

Sets (optional batch loading):

I1{ a; piano, b; cello, c; viola }
÷I(1)÷      load whole set
÷I-(1)÷     remove whole set
÷I(+a,-b)÷  add a, remove b
Re-load rule: reloading a set restores ALL members, undoing individual removals. Priority: individual tags beat sets.

× BUILDING — MICRO-CUES
×Ip×     piano hits once here, then silent
×a×      set instrument "a" fires once
×Ic:3×   cello hits 3 times rapid
Address rule: × uses the same address as ÷. In ×, :N = repeat count (:3 = 3 hits), not intensity. Fires at this exact position. No state change.

MODIFIERS — intensity suffixes (any building)
:H high · :M medium · :L low · :Sh super high · :Sl super low · :NN numeric value (e.g. %Rf:88%)

:So is reserved — solo, ÷ building only.

CONTROL
#K# — anchor stop. Ends the segment, clears active tags, resets to default. Does NOT stop audio (that's x).

Default state: #(Mm,Vs,EN)S# %T120% %Sp:C% — male, smooth, neutral, 120 BPM, center. All instruments off. Swells/fades off.

#K# after [End] is required. It seals the song.

x MARKER — KILL SWITCH (lowercase x, not ×)
× is a building. x is a marker that modifies whatever building it's inside.

x = quick kill (fast but clean, ~1 beat fade)
x! = hard kill (immediate, no fade)
#x#      kill vocals        #x!#  hard kill vocals
%x%      kill song          %x!#  FULL STOP
÷x÷      kill all instruments
÷Ip-x÷   kill just piano
Kill executes immediately and overrides sustain, swell, and fade. Kill is king.

Copy-paste shorthand
The entire language compressed for AI parsers. Rules first, every tag with its meaning. Paste this into any system prompt:

RULES:#=vocals,%=song,÷=instruments,×=one-shot hits.[ ]=sections.Only #K#,%x!% cross domains.#( ):tags bare:#(Mm,Vs,EN)S#.Standalone wrapped:#EN#.#Us:TEXT#=vocal one-shot,×=instrument one-shot.Dedup:no stacking.Same cabinet:later wins.Persist until replaced/#K#.Y+- longest-first.\#=literal#.F,B frozen;new tags 2+ letters.
#VOCALS:Mm male singer|Mf female|Mt duet|Mc choir|Pn spoken|Pw whisper|Vc child|Va adult|Ve elderly|Pu pitch up|Pd pitch down|Vg gritty|Vs smooth|Vb breathy|Vh harsh|Vt thin|Vw wide|Vo otherworldly|EN neutral|ENc choral neutral|ESd sad|ESm smile|ESh hopeful|ECc choral cry|Ea angry|Eh happy|Y contour|Y+ rise|Y- fall|Y+- arc|U urgent|Us scream|Uw whisper|Ur rapid-fire|Ub belt|S# save state
%SONG:T### BPM|Rt rubato|Rs ritardando|Ac accelerando|Rf:## reverb|Sa swell|Sf fade|Sa:M medium swell|Sa:H high swell|Sp:C center|L left|R right|LR left-to-right|RL right-to-left|W wide|M mono|Db:Cl clean cut|F fracture|B bleed|Cd chaos drift
÷INST:Ip piano|Ic cello|Id drums|Iv violin|Il viola|Ib bass|Ig guitar|Is synth|Ih harp|÷Ip÷ add|÷Ip-÷ remove=arrange change|÷Ip-x÷ kill=stop now|÷Ip:So÷ solo|I1{a,b,c} set|÷I(1)÷ load set|÷I-(1)÷ unload|÷I(+a,-b)÷ modify|reload restores all|individual>sets
×HITS:×Ip× one hit|×a× set-a hit|×Ic:3× 3 hits|address=same as ÷|:N=repeat count
MOD::H high|:M medium|:L low|:Sh super-high|:Sl super-low|:NN number|:So ÷-solo only
CONTROL:#K#=reset to #(Mm,Vs,EN)S# %T120% %Sp:C%,instruments off.Required after [End].
KILL:x=marker:x soft,x! hard|#x# %x% %x!% ÷x÷ ÷Ip-x÷|kill overrides everything.
Annotated example
Watch how a real passage moves. This is from the reference song:

#(Mm,Vs,EN)S#          ← default voice: male, smooth, neutral
%T70%                  ← slow it down: 70 BPM
%Rf:88% %Db:Cl%        ← drown it in reverb, then a clean digital cut
÷Mb÷                   ← a lone music box opens the song
[Intro]
[Verse 1]
Time and time it inserts itself,
The voice inside your head keeps telling you why even try.
#(Mm,Vc,EN)S#          ← voice shifts younger, more vulnerable
÷Rh÷ ÷Mb-÷ ÷Cl-÷       ← rhodes enters, music box and clarinet exit naturally
#Us: Well, I'm the voice that's telling you what you hear is a lie.#
                       ← SCREAMED, then voice reverts automatically
#(Mf,Vg,EN,ESm,ESd)S#  ← female, gritty, smiling AND sad at once — the mask
Every line is a filing decision. Nothing is vibes. The parser reads top to bottom and the performance follows.

Why this gets closer to actual performance
1. State, not wishes. Normal prompting re-describes the vibe every line and hopes the model remembers. The Ren Sutra files state once (S# seals it) and it persists until changed. That's how a real conductor works — you don't re-explain the tempo to the orchestra every four bars.

2. Domains don't collide. Vocals, song feel, and instruments are physically separated by their wrappers. A texture tag can never be misread as an instrument instruction, because it can't appear in the instrument building. Most prompt failures are category errors; the buildings make category errors structurally impossible.

3. One-shots vs. state are different verbs. A scream in the middle of a verse (#Us: TEXT#) and a permanent voice change (#(… )S#) look different, parse different, and behave different. Natural language blurs them — "scream this line but stay smooth otherwise" is a paragraph; here it's eleven characters.

4. Kill is separate from remove. Ending an arrangement (÷Ip-÷, the piano finishes its phrase and leaves) versus stopping audio (÷Ip-x÷, silence now) is a distinction real mixers make every session. The language makes it.

5. Deterministic. Same input, same performance. You can capture a vision, refine it tag by tag, and replicate it exactly. That's the "fighting chance" — moving from black-box prompting to orchestration.

Not the same as the old systems
System	What it does	What the Ren Sutra does instead
Helmholtz pitch notation (1863)	Labels static notes at fixed frequencies	Dictates dynamic performance — velocity, register morphing, vocal tract behavior in real time
ABC notation (1990s)	Encodes note pitches and durations into sheet music	Functions as macro/micro automation lanes for timbre, age, grit, and mixing-board transitions
Roman numeral analysis	Maps harmonic chord relationships in a key	Issues programmatic behavioral instructions: who sings, how, with what, when it stops
Those systems transcribe music that already exists. This one directs performances that don't exist yet.

Reference song (full)
The complete v12 orchestration this language was built to conduct. Lyrics by Robert Bodie Smith — free to use (see license).

#(Mm,Vs,EN)S#
%T70%
%Rf:88% %Db:Cl%
÷Mb÷
[Intro]
[Verse 1]
Time and time it inserts itself,
The voice inside your head keeps telling you why even try.
#(Mm,Vc,EN)S#
÷Rh÷ ÷Mb-÷ ÷Cl-÷
#Us: Well, I’m the voice that’s telling you what you hear is a lie.#
#(Mf,Vg,EN,ESm,ESd)S#
÷Rh-÷
That you don’t have a spark of light,
So often we hold the weight of that mask.
And that a small spark can’t fracture the night,
A convenience based on the questions we never dare to ask.
It sinks to the bottom of your heart like a tide made of liquid lead,
The “almost” and the “never” that still sleeps in your head.
[Chorus]
#(Mm,Vc,EN)S#
÷Il÷ ÷Ig÷
A simple drop of water in the expanse of the ocean blue,
Do not let that voice take over; no, do not let it sink in;
#(Pu,ENc)S#
÷Fh÷ ÷Il-÷
You are beautiful and your existence is not a sin,
One that changes everything, and that one could be you.
I know that you’re used to the garden of salt and fire,
But you’re worth more than what anyone could desire.
[Verse 2]
#(Mf,Vg,EN,ESm,ESd)S#
%Rs%
÷Il-÷ ÷Ig-÷ ÷Mn÷
It loves the version of you that’s easy to hold,
The fire in your mind screams virtuosity is not mine.
That version of you that stays silent, the one who stays gold,
Everything you do comes back like a vintage bitter wine.
The poetic proximity of how close you hold to a dream,
And unravels the fabric of your mind and your heart at the seam.
[Chorus]
#(Mm,Pu,Vc,ENc)S#
÷Ib-÷ ÷Mn-÷ ÷Fh÷ ÷Iv÷
A simple drop of water in the expanse of the ocean blue,
Do not let that voice take over; no, do not let it sink in;
You are beautiful and your existence is not a sin,
One that changes everything, and that one could be you.
I know that you’re used to the garden of salt and fire,
But you’re worth more than what anyone could desire.
[Verse 3]
#(Mf,Vg,EN)S#
%Rs% %Sf%
÷Ip-÷ ÷Ic-÷ ÷Rh-÷ ÷Fh-÷ ÷Fl÷ ÷Iv÷
The soft turning of the ruin that you were born to survive,
I see the way you dream like the starvation in your soul.
That hit your heart like a heartbeat the world didn’t want alive,
#(Mm,Vc,ESh)S#
Keep fighting because one day you’ll be happy and whole.
#(Mf,Vg,EN)S#
Unravel the tension and the static friction within thought,
You are the beautiful prismatic refractors of a supernova.
One more epitaph for my dream graveyard to rot,
#(Mm,Vc,ESh)S#
So shine bright, you beautiful star in the dark end of the nebula.
#(Pd,Vc,EN)S#
÷Rh-÷ ÷Fh-÷ ÷Mn:Sh÷ ÷Fl:Sh÷ ÷Iv÷ ÷Ip:Sh÷ ÷Ic:Sh÷
#(Pu,ECc)S#
%Sa:M%
÷Tp÷ ÷Mn-÷ ÷Fl-÷
[Chorus]
A simple drop of water in the expanse of the ocean blue,
Do not let that voice take over; no, do not let it sink in;
You are beautiful and your existence is not a sin,
One that changes everything, and that one could be you.
I know that you’re used to the garden of salt and fire,
But you’re worth more than what anyone could desire.
[Bridge]
#(Mt,Pu,Vo,ECc)S#
%Sa:H%
÷Tp÷ ÷Fh÷ ÷Ip:Sh÷ ÷Ic:Sh÷ ÷Mn:Sh÷ ÷Fl:Sh÷ ÷Iv:Sh÷
I know the feeling; each time you take a breath, it fills up like a lung full of dust,
The periodic grinding of the hope and the desolating rust;
Keep the iron hot with renovating,
Soon you will be the one innovating.
Tell the rhythmic, poetic rot to not drive you insane,
For you are stronger and will last beyond this pain.
A simple drop of water in the expanse of the nebula,
Do not let that voice take over; screaming virtuosity is not mine.
You are beautiful and life’s not as simple as a vintage bitter wine.
One that changes everything, You can be that one that’s supernova,
I know that you’re used to holding the heavy weight of that mask,
But you’re worth more than the questions we never dare to ask.
[Outro]
#(Mf,Pn,EN,ESm,ESd)S#
%Rs% %Sf%
÷x÷ ÷Ip÷ ÷Ic÷ ÷Iv÷
A lion’s fire inside your soul… starts with a fleeting, lonely spark…
Living in the mind’s temple… of twisted, fabricating strifes…
A small spark of light… can illuminate the path… in the ruins of the dark…
Or the bitter, salty end… that can grind in deep… like a back full of serrated knives…
#K#
To ascend… is to be fractured… but it doesn’t have to be…
#(Mt,Pu,Vo,EN)S#
%Sf%
÷x÷ ÷Mb÷
Look to the stars… and set yourself free.
[End]
#K#
License
The language (this syntax, these rules, these tags) is released under the Apache-2.0 License — use it, fork it, build on it, commercial or otherwise.

The reference song lyrics are a separate gift: you are free to use them, change the tune, rearrange them, record them, release them. Steal them with love. The message matters more than the ownership. The only ask: credit Robert Bodie Smith for writing them.

Honest disclaimer
Technical reliability is not 100% guaranteed — AI token limits, style constraints, model quirks, and backend updates all exist. Treat this as a sophisticated steering mechanism, not a rigid programming language. It gives your vision a fighting chance. The rest is still music.

THE REN SUTRA v12 — frozen September 2026. The buildings file everything. The parser just reads.

