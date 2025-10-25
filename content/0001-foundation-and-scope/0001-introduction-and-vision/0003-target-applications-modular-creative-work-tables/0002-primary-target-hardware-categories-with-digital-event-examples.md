# 2 Primary Target Hardware Categories with Digital Event Examples


#### 1 Macro Keyboards and Shortcut Controllers

      - Digital Events: Key press/release, modifier combinations, macro triggers
      - LED Feedback: Key backlighting, status indicators, caps lock state
      - Use Cases: Video editing shortcuts, software automation, accessibility aids
      - Performance Requirements: <3ms key response, N-key rollover

> **Event Schema Required: Key event message formats and timing specifications**


#### 2 Video Editing Control Surfaces (Avid, DaVinci panels)

      - Digital Events: Transport controls (play, stop, scrub), jog wheel steps, timeline navigation
      - Analog-to-Digital Conversion: Color correction wheels, audio faders, trim knobs
      - Visual Feedback: OLED displays, LED rings, status lights
      - Performance Requirements: <5ms control response, smooth jog wheel operation

> **Control Surface Schema Required: Video editing event types and parameter ranges**


#### 3 Color Grading Panels and Video Mixers

      - Digital Events: Color wheel position changes, lift/gamma/gain adjustments
      - Precision Requirements: 12-16 bit resolution for smooth color transitions
      - Real-Time Feedback: LED rings showing parameter values, OLED parameter names
      - Workflow Integration: DaVinci Resolve, Final Cut Pro, Adobe Premiere

> **Color Control Schema Required: Color correction parameter event formats**


#### 4 DJ Controllers and Mixing Surfaces

      - Digital Events: Crossfader movement, EQ knob adjustments, cue button presses
      - Motorized Controls: Scratch precision (±0.1°), motor feedback <2ms
      - Beat-Sync Requirements: Tempo detection, BPM sync, loop controls
      - Performance Standards: <1ms pad velocity response, scratch accuracy

> **DJ Control Schema Required: DJ-specific event types and performance timing**


#### 5 Digital MIDI Controllers and Music Production Interfaces

      - Digital Events: Note On/Off with velocity (7-14 bit), aftertouch, pitch bend
      - Control Change Events: CC messages, program changes, NRPN parameters
      - Timing Requirements: <3ms note latency, velocity curve accuracy
      - MIDI 2.0 Compatibility: High-resolution control, property exchange

> **MIDI Event Schema Required: MIDI message mapping and extended control formats**


#### 6 Live Streaming Switchers and Broadcast Controls

      - Digital Events: Scene transitions, source selection, graphics overlay triggers
      - Real-Time Requirements: Frame-accurate switching, minimal latency
      - Status Monitoring: Live indicator LEDs, source preview displays
      - Integration Targets: OBS Studio, ATEM switchers, Livestream Studio

> **Broadcast Control Schema Required: Streaming control event types and timing**


#### 7 Audio Production Control Surfaces and Mixing Consoles

      - Digital Events: Fader movements, mute/solo buttons, send level adjustments
      - Motorized Fader Systems: Position accuracy ±0.1mm, touch detection <5ms
      - Channel Strip Controls: EQ, dynamics, aux sends, plugin parameters
      - Protocol Compatibility: MCU (Mackie Control), HUI, OSC integration

> **Audio Control Schema Required: Audio mixing event formats and automation**

