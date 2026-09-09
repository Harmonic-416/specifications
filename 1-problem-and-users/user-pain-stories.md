# Real Stories: Users Struggling with Music Learning

Verbatim quotes from real users, collected September 2026 from app-store reviews,
Trustpilot, ComplaintsBoard, Metacritic, Steam, community forums, Substack essays,
and one academic study. Typos are original. Every quote links to its source.

These are the humans behind the market-gap claims in
[competitors-and-examples.md](competitors-and-examples.md) — organized by the
problem theme they illustrate.

---

## The headline number

Fender's CEO: **90% of people who pick up a guitar quit within the first year.**
"We have a member retention issue." The industry monetizes the surviving 10%
(~$10k lifetime value each).
([MusicRadar](https://www.musicradar.com/news/90-of-beginner-guitar-players-give-up-within-a-year-says-fender))

---

## Theme 1: Detection failures — "did I play wrong, or did the app hear wrong?"

> "This app litterly cannot register acoustic guitar on the g string. It even failed to register an open note on the g string."
>
> — D. Jast, ComplaintsBoard, on Yousician with a properly tuned acoustic. [source](https://www.complaintsboard.com/yousician-b149861)

> "I'll play a chord perfectly sometimes and it'll tell me that it's wrong even though I'll stop and check every string."
>
> — App Store review of Yousician (2021); the same reviewer hit a 4-level difficulty jump and abandoned the app. [source](https://apps.apple.com/us/app/yousician-learn-play-guitar/id959883039?see-all=reviews)

> "The other issue is that SimplyGuitar doesn't really know when you hit the note or not. The registration is terrible and I stopped halfway through a song to see the next 4/7 notes pop up green even tho I'm not even playing."
>
> — Paying subscriber, App Store review of Simply Guitar. [source](https://justuseapp.com/en/app/1476695335/simply-guitar-by-joytunes/reviews)

> "If I'm playing the right cords with my right hand but the wrong key with my left hand then it says I'm right. Now I purposely played the wrong chords to see if it says I'm right and it did."
>
> — Simply Piano annual subscriber, proving false-pass detection. [source](https://justuseapp.com/en/app/1019442026/simply-piano-by-joytunes/reviews)

> "I paid $90 in total for SimplyPiano, and I was surprised to learn that it STILL can't recognize the keys I'm playing! … How am I supposed to improve my piano skills if SimplyPiano won't let me progress?"
>
> — Simply Piano user after two 3-month subscriptions. [source](https://justuseapp.com/en/app/1019442026/simply-piano-by-joytunes/reviews)

> "RS+ constantly grades me as 50-60% accuracy, even if there are only a handful of notes in the song at beginner difficulty"
>
> — lemurcozy, Metacritic 0/10 review of Rocksmith+ after a $100 year subscription. [source](https://www.metacritic.com/game/rocksmith-plus/user-reviews/)

> "sometimes it doesn't recognize when I successfully hit a note. It'll report it as 'missed'"
>
> — 7heAngryVe7eran, Steam thread "Why it has extremely negative reviews?" (Rocksmith+). [source](https://steamcommunity.com/app/2834910/discussions/0/597389252535308982/?ctp=2)

> "said I was correct when I hadn't even gad tim to sing the notes yet"
>
> — Dulciquilt, App Store review of "Voice Training - Learn to Sing." [source](https://apps.apple.com/us/app/voice-training-learn-to-sing/id894620096?see-all=reviews&platform=iphone)

A professional reviewer made the point most vividly: a Guitar.com tester's **cough
registered as a perfect Fmaj7**, and a muted string scrape as E minor.
([Guitar.com Simply Guitar review](https://guitar.com/reviews/accessories/simply-guitar-review/))

**Why it matters to Harmonic:** our reliability requirement (N2) and diagnostic
feedback (F11–F21) exist because of this. If the detection can't be trusted, the
whole product inherits this trust deficit.

---

## Theme 2: Getting stuck and quitting — progression gated on broken feedback

> "Hi my name is David im 10 years old and I'm trying to learn guitar and the thing that's is really makeing me mad is that the em cord dose not work I strum it and the thing will not pick up so I just throw my guitar in the corner there's no videos that will help me so I'm going to give up in 2 months 😐 in less that I beat that stoopid em cord."
>
> — David, 10 years old, App Store review of Simply Guitar. [source](https://justuseapp.com/en/app/1476695335/simply-guitar-by-joytunes/reviews)

> "I'm stuck on ONE level for the past weeks or so… I've been playing it for DAYS, but any mistake I make, it unnecessary sends me back all the way to the beginning. … ever since that level I've been hesitating on touching my guitar again."
>
> — First-time reviewer, App Store review of Simply Guitar. [source](https://justuseapp.com/en/app/1476695335/simply-guitar-by-joytunes/reviews)

> "I've tried all the recommended advice of slowing down until I can play it comfortably then gradually increasing it, until I hit a wall and end up regressing and going backwards."
>
> — rick111, JustinGuitar community thread "Hit a plateau." [source](https://community.justinguitar.com/t/hit-a-plateau/403010)

> "I gave up on guitar a while ago when I hit one of my first plateaus: I couldn't get the solo at the proper speed. … Still stuck on the solo after 10 months. … it's difficult to figure out what is blocking me."
>
> — thelight, same thread. [source](https://community.justinguitar.com/t/hit-a-plateau/403010)

> "I would say i am intermediate although feel free to say otherwise. I feel stuck as in i don't know where to go next."
>
> — Noobix, JustinGuitar thread "Don't know what to practice" — 2 years in, knows scales, CAGED, chord construction. [source](https://community.justinguitar.com/t/dont-know-what-to-practice/242745)

> "The potential has opened up but direction is hard."
>
> — jkahn, replying in the same thread after having posted the identical question himself. [source](https://community.justinguitar.com/t/dont-know-what-to-practice/242745)

> "In grade 2 Im kinda lost and stuck. … I feel like Justin is going way to fast. … I kinda need someone showing me what to play instead of Justin saying, just try it it's the blues!"
>
> — Sam from Holland, JustinGuitar community, 3 years into the video course. [source](https://community.justinguitar.com/t/sam-from-holland-bit-stuck-on-grade-2-and-need-some-motivation/75220)

> "I feel like I have lost motivation here and have been stuck on these two for some weeks."
>
> — marcus104, JustinGuitar Grade 2 thread. [source](https://community.justinguitar.com/t/hallelujah-grade-2-module-11/394204)

**Why it matters to Harmonic:** this is exactly what our guided-mode failsafes
(3-miss auto-skip, hints, manual override — F13) and the unlocking-but-incremental
lesson map are designed to prevent.

---

## Theme 3: No feedback, no diagnosis

> "I struggled, I didn't sing well and my guitar playing was choppy at best. I didn't receive any good feedback which really discouraged me. … I slowly and gradually lost motivation and gave up."
>
> — abhiralla, JustinGuitar learning log; barely touched the guitar through his 20s before restarting. [source](https://community.justinguitar.com/t/abhis-log-what-guitar-taught-me-a-journey-of-failure-persistence-and-happiness/413914)

> "it doesn't provide any rhythm feedback other than telling you that you maybe got it wrong by sending you to practice mode. … It would also be helpful if there was different color coding for timing being wrong versus the note being wrong."
>
> — Simply Piano learner, App Store review — literally requesting Harmonic's hit/late/missed distinction. [source](https://justuseapp.com/en/app/1019442026/simply-piano-by-joytunes/reviews)

> "doesn't even let you choose the tempo! How do you expect for a beginner to all of a sudden know all the notes?"
>
> — C. Upton, ComplaintsBoard, on Yousician. [source](https://www.complaintsboard.com/yousician-b149861)

> "Game is UNREADABLE. Repeatable chords are impossible to sight read. Don't get me started on arpeggios"
>
> — Szmittu, Metacritic 1/10 review of Rocksmith+ — the note-highway UI teaches the game, not music reading. [source](https://www.metacritic.com/game/rocksmith-plus/user-reviews/)

> "I guess I should just take the time to learn it myself...but really I don't understand why none of the websites actually test them out first."
>
> — BlancoNino, AnandTech thread "Why are guitar tabs so damn wrong all the time?" [source](https://forums.anandtech.com/threads/why-are-guitar-tabs-so-damn-wrong-all-the-time.8490/)

> "My favorite tabs are the ones that people post where the whole song is played on one string...wtf????"
>
> — Fritzo, same thread. [source](https://forums.anandtech.com/threads/why-are-guitar-tabs-so-damn-wrong-all-the-time.8490/)

---

## Theme 4: Voice & pitch struggles — "am I tone deaf?"

> "Me. Absolutely terrible. Totally tone deaf and not a shred of any musical ability."
>
> — GagHalfrunt, AnandTech thread "Anyone else suck at singing?" — self-diagnosed tone-deafness, though true amusia is rare and pitch-matching is trainable. [source](https://forums.anandtech.com/threads/anyone-else-suck-at-singing.310883/post-28339327)

> "I can pick out notes with pretty amazing accuracy. I just can't reproduce them with my voice no matter what."
>
> — PrinceofWands, same thread — the perception/production gap no app diagnoses. [source](https://forums.anandtech.com/threads/anyone-else-suck-at-singing.310883/post-28339327)

> "the idea of showing up alone to a room full of strangers who all knew each other — especially when I wasn't sure how well I'd sight-read after 20 years or what my voice would sound like — was, frankly, terrifying."
>
> — Melinda Wenner Moyer, essay on rejoining a choir after 20 years. [source](https://melindawmoyer.substack.com/p/i-joined-a-choir-and-embarrassed)

> "while singing Arvo Pärt's gorgeous Nunc Dimittis, I brazenly started singing — by myself — a beat too early. Was I mortified? Absolutely."
>
> — Same essay. [source](https://melindawmoyer.substack.com/p/i-joined-a-choir-and-embarrassed)

> "was rejected by the University Choir in my undergraduate school because I didn't know what vocal sight reading was"
>
> — Sara, comment on a "Tone-Deaf" essay; she had piano training and later earned a vocal performance doctorate. [source](https://kathleenkellymusic.substack.com/p/tone-deaf/comments)

> "My musical knowledge isn't vast enough to sing a note by name without hearing it first"
>
> — RandomGirl16, App Store review of "Voice Training - Learn to Sing" — the audiation gap our "hint" feature addresses. [source](https://apps.apple.com/us/app/voice-training-learn-to-sing/id894620096?see-all=reviews&platform=iphone)

> "a bombardment of advertisements during what should be your dedicated practice time"
>
> — Simon Blaise, 1-star App Store review of Sing Sharp. [source](https://apps.apple.com/us/app/sing-sharp-singing-lessons/id772052329)

**Why it matters to Harmonic:** our acapella sight-reading feature targets exactly
these people — trained-adjacent adults embarrassed in choir, and beginners who've
written themselves off as tone deaf.

---

## Theme 5: The physical and emotional burnout wall

> "now my finger is mad bruised damn barre chords 🙁"
>
> — phatj, AnandTech thread "barre chords hurt :(". [source](https://forums.anandtech.com/threads/barre-chords-hurt.1923817/post-21135648)

> "my fingers got so sensitive after fretting, it would give me burning sensation while showering."
>
> — "E equals MC2", same thread. [source](https://forums.anandtech.com/threads/barre-chords-hurt.1923817/post-21135648)

> "Sometimes they switch to another instrument (piano, glockenspiel) to avoid the barre chords completely."
>
> — Andrea La Rose, guitar teacher, on barre chords as the make-or-break stage. [source](https://twochords.substack.com/p/two-chords-teaching-iii)

> "I feel like I'm not just plateauing, but actually sliding into a trough."
>
> — Jeremy D. Nichols, adult guitar learner; also wrote "I sincerely sound like I did weeks ago." [source](https://toolatesmart.substack.com/p/apologies-to-bryan-adams)

> "Everytime I take a day off of anything...that day seems to turn into two, then a week, month, year—then years."
>
> — Same author; his usual pattern is "to quit when it started to get hard." [source](https://toolatesmart.substack.com/p/apologies-to-bryan-adams)

> "The feeling I've been trying to avoid my entire adult life - the mortification specific to public failure - sat on my chest like an ogre's turd."
>
> — Leigh Belanger, adult beginner pianist on freezing at a recital; she boycotted the next one. [source](https://makereleaserepeat.substack.com/p/when-in-doubt-slow-down)

> "And so you suck, and repeat the sucking."
>
> — Same piece, on daily beginner practice. [source](https://makereleaserepeat.substack.com/p/when-in-doubt-slow-down)

One under-appreciated detail from a guitar teacher: parents sometimes ask kids to
**stop practicing because of the sound** — negative feedback at home exactly when
encouragement matters most.
([Two Chords](https://twochords.substack.com/p/two-chords-teaching-iii))

---

## Theme 6: Paywall & billing anger (the loudest 1-star theme)

> "it gave me just enough to get started and excited, but then cut me off unless I signed up for premium."
>
> — App Store review of Yousician (2024). [source](https://apps.apple.com/us/app/yousician-learn-play-guitar/id959883039?see-all=reviews)

> "a charge of $180 on my bank account from Yousician (money I did NOT have)"
>
> — J. Rau, ComplaintsBoard — a "free 7 day trial" billed a full year up front, no refund. [source](https://www.complaintsboard.com/yousician-b149861)

> "Started a 7 day free trial, cancelled it after a day and got charged 99$ a week later"
>
> — Hugo Falk, 1-star Trustpilot review of Ultimate Guitar (2026). [source](https://www.trustpilot.com/review/www.ultimate-guitar.com)

> "Since 2023, I've emailed UG PRO to cancel my early subscription, and every year, they email me back saying that my subscription has been cancelled. And yet, every year I still get charged."
>
> — FastLane Devs, 1-star Trustpilot review of Ultimate Guitar. [source](https://www.trustpilot.com/review/www.ultimate-guitar.com)

> "I purchased one $6.49 piece of sheet music. MuseScore then enrolled me in a recurring subscription I did not knowingly intend to purchase and charged me $324.95"
>
> — Sarah, 1-star Trustpilot review of MuseScore.com. [source](https://www.trustpilot.com/review/musescore.com)

> "I went to download ONE piano score required for my child's piano lessons....only to find out several days later that I had been enrolled in a 3-month premium membership costing $44.99. Bait and switch at its finest"
>
> — Golden Girl, 1-star Trustpilot review of MuseScore.com. [source](https://www.trustpilot.com/review/musescore.com)

> "There's no reason to have to pay monthly. You should at least allow people to pay for the game and then add DLC"
>
> — dxcool223, Metacritic 0/10 review of Rocksmith+. [source](https://www.metacritic.com/game/rocksmith-plus/user-reviews/)

---

## Theme 7: Gamification's double edge

> "I don't even want to learn Spanish anymore, but I simply can't stop. The streak has grown too powerful. I'm in its grip."
>
> — Rik, "The end of the streak," day 1,139 of a Duolingo streak. [source](https://theconversationstarter.substack.com/p/the-end-of-the-streak)

> "Mainly...I still can't speak Spanish. Read a bit, sure. But formulating more than basic sentences? Or having an actual convo? Not even close."
>
> — James Hornick, "I rage quit Duolingo today," after a multi-year daily streak. [source](https://talentandsarcasm.substack.com/p/i-rage-quit-duolingo-today)

> "I wasn't learning Spanish, I was learning how to keep a streak alive."
>
> — Nuzair Nuwais, dev.to, on escaping the streak trap. [source](https://dev.to/nuzairnuwais/how-i-got-out-of-the-duolingo-streaks-trap-by-building-my-own-app-eg1)

> "Through the many nights of XP farming, I lost my drive to learn [new languages]."
>
> — Study participant P1, arXiv, "When Gamification Spoils Your Learning." [source](https://ar5iv.labs.arxiv.org/html/2203.16175)

> "My brother lost his 110-day streak, and now [he] is an abandoned account."
>
> — Duolingo forum user quoted in the same study — the retention mechanic is also the churn mechanic. [source](https://ar5iv.labs.arxiv.org/html/2203.16175)

> "In the end, I completely lost my confidence in truly learning Chinese."
>
> — Study participant P14, same study. [source](https://ar5iv.labs.arxiv.org/html/2203.16175)

> "I started practicing just to keep the streak, which isn't why I started singing."
>
> — Yousician singing user, via Bloom Vocal's 2026 review. [source](https://www.bloomvocal.site/en/blog/yousician-review-2026)

**Why it matters to Harmonic:** we're borrowing the Duolingo map because the habit
loop demonstrably works (~3× session time vs. Babbel) — but rewards must track real
musical skill, and a missed day must be recoverable, not catastrophic.

---

## What these stories tell us (summary)

1. **Untrustworthy feedback is the #1 product killer** — users quit not because
   they're graded, but because they can't tell if the grade is real.
2. **Getting hard-stuck is the quit trigger** — every stuck story ends with the
   instrument in a corner. Failsafes are a retention feature, not a nicety.
3. **The post-beginner vacuum is unserved** — "I don't know where to go next" recurs
   across every platform.
4. **Emotional stakes are high** — embarrassment (choir, recitals) and self-diagnosed
   tone-deafness stop people before they start. Kind, private, diagnostic practice is
   the antidote.
5. **Transparent pricing is a differentiator** — billing anger dominates 1-star
   reviews across the entire category.
