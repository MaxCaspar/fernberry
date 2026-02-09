# AVAudioEngine Graph

## Baseline Graph
- Input -> EQ -> Mixer -> Output
- Add taps for metering and analysis.

## Safety
- Start/stop on a dedicated queue.
- Handle route change and interruption notifications.
