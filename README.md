# Resonate AI

AI-powered personalized music with binaural beats for focus and relaxation.

## Concept

Generate original music compositions personalized to your taste (artists, genres) combined with scientifically-backed binaural beats for focus, relaxation, or sleep.

## Key Differentiators

1. **100% Original Compositions** - No copyright issues, AI-generated from scratch
2. **Binaural Beat Integration** - Proven frequency entrainment (40Hz gamma for focus, 8-12Hz alpha for relaxation)
3. **Personalization Engine** - Learns your preferences, creates taste-matched music
4. **Mobile-First** - Native apps, offline capable

## Tech Stack (Proposed - CTO Review Needed)

### Music Generation (Open Source)
- **MusicGen** (Meta) - Apache 2.0 license, free, high quality
- **AudioLDM 2** - Open source text-to-audio
- **Alternative**: Self-hosted Stable Audio or fine-tuned MusicGen

### Binaural Beats
- Python DSP generation (numpy, pydub)
- Real-time audio synthesis
- Frequency: 40Hz (focus/gamma), 10Hz (relaxation/alpha), 1-4Hz (sleep/delta)

### Mobile App
- **React Native** or **Flutter** (CTO decision)
- Offline-first architecture
- Local audio generation (edge AI) or API calls

### Backend (if needed for API)
- Node.js or Python FastAPI
- MusicGen inference API
- User preference storage
- Firebase or PostgreSQL

## Open Source Model Comparison

| Model | License | Cost | Quality | Speed | Mobile? |
|-------|---------|------|---------|-------|---------|
| MusicGen (Meta) | Apache 2.0 | Free | High | Medium | No (needs GPU) |
| AudioLDM 2 | Open | Free | Medium | Slow | No |
| Riffusion | MIT | Free | Low-Med | Fast | Possible |
| Stable Audio | Commercial | $ | High | Fast | No |
| Suno API | Commercial | $$$ | Very High | Fast | No |

**Recommendation**: MusicGen for MVP (free, high quality), consider fine-tuning for style transfer.

## Architecture Decision Needed

**Option A: Cloud API (easier, costs $)**
- User → Mobile App → Backend API → MusicGen inference → Audio stream
- Pros: Faster generation, works on any phone
- Cons: Server costs, needs internet, latency

**Option B: Edge/On-Device (harder, no server costs)**
- User → Mobile App → On-device ML → Local audio generation
- Pros: No server costs, works offline, private
- Cons: Large app size, needs powerful phone, slower generation

**CTO Decision Required**: Which architecture for MVP?

## Product Structure (SelectAgent-Style)

```
resonate-ai/
├── mobile-app/              # React Native or Flutter
│   ├── src/
│   │   ├── components/      # UI components
│   │   ├── screens/         # App screens
│   │   ├── services/        # Audio generation, API calls
│   │   ├── store/           # State management
│   │   └── utils/           # Helpers
│   ├── assets/              # Images, fonts
│   └── package.json
├── backend/                 # Optional API server
│   ├── src/
│   │   ├── api/             # REST endpoints
│   │   ├── models/          # ML inference
│   │   └── utils/
│   └── requirements.txt
├── ml-models/               # MusicGen, training scripts
│   ├── musicgen/            # Meta's MusicGen
│   ├── training/            # Fine-tuning scripts
│   └── binaural/            # Beat generation
├── docs/                    # Documentation
└── README.md
```

## MVP Features

1. **Onboarding**
   - Select favorite artists/genres
   - Choose intention (focus, relax, sleep)

2. **Music Generation**
   - Generate 3-5 minute track
   - Binaural beats layered in
   - Save to library

3. **Player**
   - Play/pause
   - Skip/loop
   - Background audio support

4. **Library**
   - Saved tracks
   - Favorites
   - History

## Monetization (Future)

- **Free**: 3 generations/day, ads
- **Premium ($4.99/mo)**: Unlimited, no ads, offline, higher quality
- **Lifetime ($49.99)**: One-time purchase

## Next Steps (CTO Priority)

1. **Architecture Decision**: Cloud API vs. Edge/On-device
2. **Framework Choice**: React Native vs. Flutter
3. **MusicGen Integration**: API wrapper or mobile optimization
4. **Audio Pipeline**: Generation → Binaural mixing → Playback
5. **Offline Strategy**: How much works without internet?

## Resources

- MusicGen: https://github.com/facebookresearch/audiocraft
- AudioLDM 2: https://github.com/haoheliu/AudioLDM2
- Binaural Beats: https://github.com/binaural-dev/binaural
- React Native Audio: https://github.com/react-native-audio

---

**Status**: Awaiting CTO technical architecture decisions
