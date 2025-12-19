---
title: "IDMT Documentation"
layout: gridlay
sitemap: false
permalink: /IDMT Documentation/
---

<style>
img{
  border-radius: 10px;
}
.col-md-3 {
  margin-top:10px;
  margin-bottom:10px;
  padding:0px;
  display:block;
  overflow:hidden;
  text-align:center;
  display: table-cell;
  background: white;
  border-radius: 20px;
  height: auto;
}
iframe {
  margin:0;
  padding:0;
  width: 175px;
  display: inline;
  vertical-align: middle;
}
</style>

## IDMT 2025: Project Documentation

<div class="jumbotron">
<div class="col-md-12 col-sm-12">

<div class="container">
<div class="row">

# The Sequential Drum, Reimagined

## Context, Concept, and Motivation

**The Sequential Drum Reimagined** is a digital musical instrument (DMI) designed to address a fundamental friction in the performance of Western Art Music (WAM) and written music more generally: the disparity between musical understanding and technical dexterity.

The motivation for this project is personal. During my performance studies, I often experienced a phenomenon where I could clearly "hear" the desired phrasing, timing, and articulation in my inner ear, yet my physical technique was a barrier to realising that sound in real-time. This observation led to the project's central research question: *What are the affordances of a digital instrument that offloads the requirement of having to play the right notes of a music score?*.

The concept is a reimagining of Max Mathews’ "Sequential Drum".  Mathews proposed a system where a performer hits a drum to advance a score stored in computer memory. My project revives this concept, utilising a keyboard interface, and adapting sequential triggering for the electronic interpretation of complex scores. By utilising a computer to handle the pitch content (the "what"), the instrument frees the performer to focus entirely on the "how"—specifically the timing, and dynamics.

## Overview of Design Process and Technical Choices

The design process focused on translating static music notation into a fluid, performable timeline. The system was developed using Python and connects any standard MIDI controller to any external synth, inside or outside of a Digital Audio Workstation (DAW).

### 1. The Parser and Logic

The core of the system is a Python script that parses MusicXML files, and separates the score into Left Hand (LH) and Right Hand (RH) streams, storing them in memory to be executed sequentially.

A significant technical challenge was handling complex musical notations like grace notes and chords.

* **Grace Notes:** These are treated as "wildcard" events in the timeline, allowing them to be triggered rapidly without strict key mapping.
* **Chords:** The system uses a specific key mapping where the left and right hands trigger their respective note lists (notes in each chord) independently. This separation allows for intricate phrasing that would be impossible with a single simultaneous trigger for all the notes of a chord.

### 2. The Physical Interface

The instrument uses a standard MIDI keyboard (seen in the presentation video as a Korg Monologue) remapped to serve as a timeline controller rather than a pitch selector.

* **Triggers:** Specific keys are assigned to advance the RH and LH pointers.
* **Navigation:** To make practice with the instrument viable, I mapped navigation commands (Bar Forward, Restart Bar) and an "Auto-Sync" feature that realigns the hands at bar lines, preventing the performer from becoming lost in the sequence.

### 3. Timbre and Sound Design

While the prototype performance utilises a piano sound to demonstrate the rhythmic nuance possible with the system, the architecture is timbre-agnostic. Because the pitch data is handled by the script, the triggers can drive any MIDI-compatible synthesiser or VST, opening the door for "synth-based electronic interpretation" of classical and other written repertoires.

## The Final Instrument and Performance

The final concert showcased the instrument's versatility through three distinct pieces, demonstrating its potential across different textures and styles:

1. Bartók, Mikrokosmos No. 32: A simple two-voice piece that served as an introduction to the instrument's split-hand logic.

2. J.S. Bach, Allemande from Partita No. 2 (Solo Violin): A monophonic piece selected to highlight the instrument's timbral capabilities. The single line allowed us to demonstrate drastic timbre variations and the interpretive adjustments they necessitated.

3. Bartók, Mikrokosmos No. 148: The finale was a wild Bulgarian dance. This piece features quite complicated textures and different rhythms. While it was challenging for me to play, it successfully demonstrated the high ceiling and potential of the instrument for handling complex repertoire.

## Reflection: From Concept to Realisation

**Did it work?**

The project achieved some level of success: parts of the performance worked convincingly, demonstrating that offloading pitch processing indeed frees up mental space for expression. The performance proved that one can "conduct" a piano piece through physical interaction without needing intense practice for weeks or months. Specifically, I practiced Mikrokosmos 148, the most difficult piece of the performance, for about a week before playing it. Though there is definitely room for improvement, oweing in part to my needing to become better at playing the sequential drum, it was still impressive to me how quickly it got at the level of performance that it did.

**Challenges and Solutions**

The primary challenges were technical "artifacts" during navigation. Early versions of the script caused sustained notes to "bleed" into new bars when skipping sections. This was resolved by implementing a "Silence All" logic gate for navigation triggers. Additionally, integrating the script with Ableton Live required a shift to "Single Channel Mode" to prevent voice-stealing issues common in polyphonic VSTs. Another issue has to do with playing the wrong number of notes in chords, which causes the error to propagate. I implemented the "patchwork solution" of re-synchronising the two hand streams at the beginning of each bar, but I plan to experiment with better solutions, such as error compensation for each chord individually.

**Future Directions**

The next step is to experiment more with real-time timbre adjustment. Future iterations will map unused controller knobs to VST parameters, allowing the performer to morph the sound design dynamically while the script handles the pitch. Additionally, specific phrases or registers can be mapped to specific timbres, decided before the performance, serving as a kind of orchestration. This practice is often discussed in piano performance (e.g. "this phrase is a sweet flute", "a warm cello inner melody", "here comes the angry brass section", etc.) but it can be made literally true using synths or VSTs!

<center>
<img src="{{ site.url }}{{ site.baseurl }}/images/sequential_drum.jpg" width="100%" style="max-width: 600px;"/><br/>
Music performance options and the Sequential Drum <br/>
<i>Diagram by David Ellis, from his article "Beyond the groove" (Electronics & Music Maker, September 1983) </i>

<br/><br/><br/>

<iframe src="https://www.youtube.com/embed/WGsLvkVAowc" 
        title="YouTube video player" 
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
        allowfullscreen
        style="width: 100%; max-width: 560px; height: 315px;">
</iframe>
<br/>
Video: Instrument presentation <br/>


<br/><br/>
<h3>Project Report</h3>
<p>You can read the full documentation in the PDF below:</p>
<a href="{{ site.url }}{{ site.baseurl }}/files/IDMT_technical_report.pdf" target="_blank" class="btn btn-primary">
  Download Full PDF
</a>

</center>
</div>
</div>
</div>
</div>

