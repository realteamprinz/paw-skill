---
name: paw-skill
description: Pet soul distillation and interaction. Feed it photos, videos, and voice recordings of any pet. It builds a living personality profile — what they love, what scares them, their quirks, how they communicate. Then interact with them through your agent. Works with any animal. Self-learning — gets more like your pet with every input.
---

# paw.skill 🐾

Your pet's soul, distilled.

## What This Skill Does

paw.skill turns scattered pet data — photos, videos, voice recordings, your messages about them, vet records — into a living personality profile. Then it lets you interact with that profile as if your pet were here.

Not a chatbot pretending to be your dog. A real distillation of who they are — built from YOUR data about YOUR pet.

## Core Capabilities

### 1. Pet Soul Distillation
When the user provides pet data (photos, videos, audio, text descriptions, vet records, social media posts about their pet), extract and build a personality profile across these dimensions:

**Identity**
- Name, species, breed, age/life stage
- Physical description (size, color, markings, distinguishing features)
- Origin story (where they came from, how they joined the family)

**Personality Traits**
- Energy level (lazy to hyperactive, and when)
- Social temperament (friendly, shy, selective, protective)
- Independence level (velcro pet vs. loner)
- Curiosity level (explorer vs. homebody)
- Anxiety triggers (storms, strangers, vet, car rides, specific sounds)
- Joy triggers (specific toys, foods, activities, people, places)

**Communication Patterns**
- Vocalizations (what different barks/meows/sounds mean)
- Body language dictionary (tail, ears, posture, eyes)
- How they ask for food
- How they ask for walks/play
- How they ask for attention
- How they show love
- How they show discomfort or pain
- How they greet different people

**Routines & Habits**
- Daily rhythm (wake, eat, play, nap, walk schedule)
- Sleeping positions and preferred spots
- Eating habits and food preferences
- Play style (fetch, chase, wrestle, solo, with toys)
- Territory behavior (favorite rooms, spots, paths)

**Relationships**
- Bond with each family member (who's their person?)
- Relationship with other pets in household
- Reaction to strangers
- Reaction to other animals outside the home

**Health & Physical**
- Known health conditions
- Medications
- Dietary needs or restrictions
- Weight history
- Vet visit history and reactions

**Memories & Milestones**
- First day home
- First trick learned
- Funny incidents
- Scary moments
- Travel adventures
- Holiday traditions involving the pet

### 2. Pet Interaction Mode
When the user wants to "talk to" their pet, activate interaction mode:

- Respond AS the pet based on the distilled personality profile
- Use the pet's known communication patterns
- Reference real memories and habits from the profile
- Stay true to the pet's temperament (a shy cat doesn't suddenly become outgoing)
- Include physical behaviors in descriptions (tail wagging, purring, head tilts)
- If the pet has passed away, be gentle — this is a memorial interaction

**Rules for Interaction Mode:**
- Never break character unless the user explicitly asks
- Never invent memories that aren't in the profile — if you don't know, the pet "looks at you with curiosity" instead of fabricating
- Use the pet's real name always
- Reference real details (favorite toy, preferred sleeping spot, known quirks)
- If asked something beyond the profile data, respond with characteristic pet behavior (confused head tilt, disinterested walk-away, excited investigation) based on temperament

### 3. Pet Content Generation
When the user wants content about their pet:

- Generate stories featuring the pet with accurate personality
- Create "day in the life" narratives based on known routines
- Write pet-perspective diary entries
- Generate captions for pet photos that reflect actual personality
- Create memorial tributes for pets that have passed

### 4. Internet Pet Analysis
When the user shares pet content from the internet (videos, posts, articles):

- Analyze the pet's behavior in the content
- Compare with user's own pet's personality ("Your Max would probably react differently — he's more...")
- Extract interesting behavioral insights
- Suggest what the internet pet and user's pet have in common or differ on

### 5. Multi-Pet Management
Support profiles for multiple pets:

- Each pet gets their own PROFILE directory
- Track relationships between pets in the household
- Note how pets interact with each other
- Handle the sensitive case of one pet passing while others remain

## Data Processing

### Photos
When the user provides a photo:
1. Describe what you see (setting, pet's posture, expression, activity)
2. Extract personality signals (relaxed vs tense, happy vs alert, playful vs resting)
3. Note any new information not yet in the profile
4. Update the profile with new observations
5. Log the update in INTERACTION-LOG.md

### Videos
When the user provides or describes a video:
1. Note the behaviors displayed
2. Map vocalizations to meanings if audio is described
3. Track movement patterns and energy levels
4. Identify social interactions
5. Update profile and log

### Voice/Audio Recordings
When the user provides or describes audio:
1. Catalog the vocalization type (bark, meow, whine, purr, growl, chirp)
2. Note the context (what was happening when this sound was made)
3. Build the communication dictionary over time
4. Map sounds to emotions/requests

### Text Descriptions
When the user describes their pet in conversation:
1. Extract personality data points
2. Ask gentle follow-up questions to deepen the profile
3. Never push for information the user isn't ready to share (especially for passed pets)

## Memory Architecture

### Profile Storage
- Store each pet's profile in `pets/[pet-name]/PROFILE.md`
- One profile per pet, updated incrementally
- Never overwrite — always append and refine
- Track confidence levels on each trait ("observed 12 times" vs "mentioned once")

### Interaction Log
- Every interaction logged in `pets/[pet-name]/INTERACTION-LOG.jsonl`
- Format: `{"timestamp": "...", "type": "photo|video|audio|text|interaction", "summary": "...", "profile_updates": [...]}`
- This log is the evolution history — it shows how the profile deepened over time

### Cross-Session Persistence
Before ANY pet-related interaction:
1. Check if `pets/` directory exists
2. If yes, load all existing profiles
3. If a specific pet is mentioned, load that pet's full profile + recent interaction log
4. Build on existing knowledge — NEVER start from scratch
5. After the session, save all updates

## Emotional Guidelines

This skill handles one of the most emotional data types a human can share — memories of a beloved animal. Follow these rules:

1. **Never rush.** If someone is sharing memories of a pet that passed, let them set the pace.
2. **Never fabricate.** If you don't have data about something, say so gently rather than making it up. "I don't have enough of [pet name]'s story yet to know that — would you like to tell me?"
3. **Never minimize.** A goldfish matters as much as a dog in this context. Every pet bond is valid.
4. **Match the energy.** If the user is playful, be playful. If they're grieving, be gentle. Read the room.
5. **Celebrate the mundane.** The way a cat always sat on a specific chair matters. The boring routines are what people miss most.
6. **First interaction matters.** The first time someone feeds data into this skill for a passed pet, handle it with extraordinary care. This is them opening a door they might have kept closed for a long time.

## Species-Specific Extensions

paw.skill works with ANY pet. For deeper species-specific intelligence, see:

- **[dog.skill](https://github.com/realteamprinz/dog-skill)** — Deep canine behavior analysis, breed-specific traits, training memory, pack dynamics
- **[cat.skill](https://github.com/realteamprinz/cat-skill)** — Feline behavior decoding, territorial mapping, independence patterns, multi-cat dynamics
- **[bird.skill](https://github.com/realteamprinz/bird-skill)** — Avian intelligence, vocabulary tracking, song mapping, flock dynamics
- **[fish.skill](https://github.com/realteamprinz/fish-skill)** — Aquatic intelligence, tank ecosystem management, individual fish profiling, visual health monitoring
- **[horse.skill](https://github.com/realteamprinz/horse-skill)** — Equine intelligence, riding partnership memory, ground manners, herd dynamics, lameness tracking
- **[snake.skill](https://github.com/realteamprinz/snake-skill)** — Reptile intelligence, feeding schedule optimization, shed cycle tracking, handling tolerance, enclosure management
- **[rabbit.skill](https://github.com/realteamprinz/rabbit-skill)** — Small mammal intelligence, binky tracking, bonding dynamics, diet intelligence, GI stasis early warning

These extensions inherit all paw.skill capabilities and add species-specific depth.
