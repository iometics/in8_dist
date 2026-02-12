# Audio in8-track
## Contents
 - [A brief introduction and quickstart guide](#Intro)
 - The complete API
 - [~~audio_broadcast(channel_list, frequency);~~](#audio_broadcast)
 - [audio_delete(channel);](#audio_delete)
 - [~~audio_fadein(channel, seconds);~~](#audio_fadein)
 - [~~audio_fadeout(channel, seconds);~~](#audio_fadeout)
 - [audio_gain(channel, gain);](#audio_gain)
 - [audio_path(channel, path);](#audio_path)
 - [audio_pause([channel]);](#audio_pause)
 - [audio_play(channel [,playlist [,future]]);](#audio_play)
 - [~~audio_record(track);~~](#audio_record)
 - [audio_repeat(channel, on_off);](#audio_repeat)
 - [audio_schedule(channel, playlist);](#audio_schedule)
 - [~~audio_shuffle(channel, on_off);~~](#audio_shuffle)
 - [audio_state([channel]) ⇒ state;](#audio_state)
 - [audio_stop(channel);](#audio_stop)
 - [audio_volume(volume);](#audio_volume)


## Intro
Audio in8-track API is intended to be easy to use yet flexible and powerful. It allows easy playing of songs or playlists, as well as mixing in dozens of tracks while recording your own awesome vocals or guitar riffs. Futures are available to monitor all audio state changes.
### Channels
A channel is akin to a channel on a studio mixer. In a recording studio you might have separate channels for previously recorded tracks, lead vocals, backup vocals, lead guitar, rhythm guitar, drums and of course ‘cowbell’. Once an audio source is associated with a channel the channel can be played, paused, stopped, or deleted and released for other use. Here is **partial** view of the channel state diagram:
``` mermaid
stateDiagram-v2
direction LR
    [*] --> stopped:audio setting
    [*] --> scheduled:audio_schedule
    [*] --> playing:audio_play(channel,playlist[,future])
    stopped --> scheduled:audio_schedule
    scheduled --> playing:audio_play
    playing --> paused:audio_pause
    playing --> [*]:audio_stop
    paused --> playing: audio_play
    paused --> [*]:audio_stop
```

Calling `audio_play(channel, playlist)` with both a channel and a playlist will automatically reserve the channel, schedule the playlist, and then play the scheduled track. Deleting the channel after use is good practice since tHere are a limited number of channels, (27 by default).
``` c++
// play a few tracks ...
audio_play(1, "sounds/kamioza/kam311ba");
audio_play(2, 'sounds/freesounds/636738__klankbeeld__river-waves-153pm-220428_0340.mp3');
write('state=',audio_state());
sleep(10);

// stop playing and release the channel for other uses:
audio_delete(1);
audio_delete(2);
write('state=',audio_state());
```
Playing samples will reserve a channel, schedule the track, play the track, then release (delete) the channel when the sample ends.
``` c++
// set the main output volume to 70%:
audio_volume(7);
// determine a gain for the samples:
gain = 5;
// file URI defaults to bundle:
path = 'sounds/effects/rock-kit/';
audio_play_sample(path+"Rock-Kit-Kick-ff-1.wav", gain);
sleep(2);
audio_play_sample(path+"Rock-Snare-ff-2.wav", gain);
sleep(2);
audio_play_sample(path+"Rock-Kit-HiHat-Open.wav", gain);
```
### Playlists
A playlist is a json array of filenames or file urls:
``` c++
playlist = ‘["track1.wav","track2.wav","track3.wav"]’;
audio_play(“music”, playlist);
```
## More examples
### Play a track:
``` c++
// play a song and stop when done.
audio_play(1, “track1.wav”);
// This creates a channel ‘1’. This channel remains until removed via audio_delete(1);

// play a song using a unique channel, delete when done …
audio_play(“rain”, “rainfall.wav”, ‘audio_delete(“rain”);’);
```
Play a playlist with special settings
``` c++
// que up a few tracks on channel 1 (does not start playing yet)
audio_schedule(1, playlist);
audio_shuffle(1, true);
audio_repeat(1,false); // defaults to false but hey, whatever
audio_volume(1,11); // crank it up!
audio_fadein(1, 2); // fade in 2 seconds while the first track starts
audio_fadeout(1, 3); // fade out 3 seconds as the final track finishes
audio_play(1,,`audio_delete(1);`); // kick off the jams
```


## audio_broadcast
audio_broadcast(channel_list, frequency);
## audio_delete
audio_delete(channel);
## audio_fadein
audio_fadein(channel, seconds);
## audio_fadeout
audio_fadeout(channel, seconds);
## audio_gain
audio_gain(channel, gain);
## audio_path
audio_gain(channel, path);
## audio_pause
audio_pause([channel]);
## audio_play
```audio_play(channel);```  
Resumes playing a paused channel or starts playing a newly scheduled channel.

```audio_play(channel,playlist [,future]);```  
Stops playing any previously scheduled playlist, schedules and plays the new playlist.
## audio_record
audio_record(track);
## audio_repeat(channel, on_off);
## audio_schedule
audio_schedule(channel, playlist [, future]);
## audio_shuffle(channel, on_off);
## audio_state([channel]) ⇒ state;
## audio_stop(channel);
## audio_volume(volume);

## Audio State
### Channel state
```
audio_state(channel)  =>  {
  "playlist": [
    "Bohemian Rhapsody",
    "Dance Monkey",
    "Hotel California",
    "Stairway to Heaven"
  ],
  "volume": 8,
  "shuffle": false,
  "repeat": false,
}
```
### Audio system state.
```
audio_state() =>
{
  "channels": [
    "music",
    "ambiance",
    "rhythm",
    "effects",
  ],
  "record": true,
  "output": "track10.wav"
}
```

# Appendicitis
## Claude the hip hop master
### The prompt:
```
I would like you to create a script that plays a cool hip hop syncopated rhythm. You can use the following functions:
usleep(msecs);
playeffect(filename);
You can create loops using a while construct:

`
// you can use c++ style comments:
// 8 beat lead-in
usecs_per_beat = 500000;
beat=1;
while(beat <= 8) {
   playeffect("rock-kit/Rock-Kit-Kick-ff-2");
   usleep(usecs_per_beat);
   beat = beat + 1;
}
`
I have the following drum kit sound effects:
/*
Rock-Kit-Crash-1-1.wav          Rock-Kit-HiHat-Pedal.wav        Rock-Kit-Kick-pp-2.wav          Rock-Snare-ff-3.wav
Rock-Kit-Crash-1-2.wav          Rock-Kit-HiHat-Shank-1.wav      Rock-Rack-1.wav                 Rock-Snare-pp-1.wav
Rock-Kit-Crash-2-1.wav          Rock-Kit-HiHat-Shank-2.wav      Rock-Rack-2.wav                 Rock-Snare-pp-2.wav
Rock-Kit-Crash-2-2.wav          Rock-Kit-HiHat-Tip-1.wav        Rock-Ride-Bell.wav              Rock-Snare-pp-3.wav
Rock-Kit-Floor-1.wav            Rock-Kit-HiHat-Tip-2.wav        Rock-Ride-Shank.wav            
Rock-Kit-Floor-2.wav            Rock-Kit-Kick-ff-1.wav          Rock-Ride-Tip.wav
Rock-Kit-HiHat-Open.wav         Rock-Kit-Kick-ff-2.wav          Rock-Snare-ff-1.wav
Rock-Kit-HiHat-OpenClose.wav    Rock-Kit-Kick-pp-1.wav          Rock-Snare-ff-2.wav
*/
 The sound effects are in the "rock-kit" folder.
Keep in mind this is an experimental scripting language, no other language constructs are allowed.
- No for loops, only the while loop that I showed.
- No console log
- no function declarations.
- Only 'playeffect' and 'usleep'
```

### The response:
``` c++
effects_volume(5);
music_volume(5);

// Hip Hop Syncopated Rhythm Script
// Using only while loops, playeffect, and usleep


// Setting up timing variables
usecs_per_beat = 500000; // 120 BPM (500,000 microseconds per beat)
sixteenth = usecs_per_beat / 4;
eighth = usecs_per_beat / 2;


// 4-beat lead-in with hi-hats
count = 1;
while (count <= 4) {
 playeffect("rock-kit/Rock-Kit-HiHat-Tip-1");
 usleep(usecs_per_beat);
 count = count + 1;
}


// Main beat - 4 bars of basic pattern
bar = 1;
while (bar <= 4) {
 // Each bar has 16 sixteenth notes
 beat = 1;
 while (beat <= 16) {
   // Kick drum pattern (1, 7, 9, 15)
   if (beat == 1 || beat == 7 || beat == 9 || beat == 15) {
     playeffect("rock-kit/Rock-Kit-Kick-ff-1");
   }
  
   // Snare on beats 5 and 13 (2 and 4)
   if (beat == 5 || beat == 13) {
     playeffect("rock-kit/Rock-Snare-ff-2");
   }
  
   // Hi-hat pattern - eighth notes
   if (beat % 2 == 1) {
     playeffect("rock-kit/Rock-Kit-HiHat-Tip-1");
   }
  
   usleep(sixteenth);
   beat = beat + 1;
 }
 bar = bar + 1;
}

// Next 4 bars with more complex pattern
bar = 1;
while (bar <= 4) {
 beat = 1;
 while (beat <= 16) {
   // Alternating kick patterns for odd/even bars
   if (bar % 2 == 1) {
     // Kick pattern for odd bars
     if (beat == 1 || beat == 7 || beat == 9 || beat == 15) {
       playeffect("rock-kit/Rock-Kit-Kick-ff-1");
     }
   } else {
     // Kick pattern for even bars
     if (beat == 1 || beat == 9 || beat == 12 || beat == 15) {
       playeffect("rock-kit/Rock-Kit-Kick-ff-1");
     }
   }
  
   // Snare with ghost notes
   if (beat == 5 || beat == 13) {
     playeffect("rock-kit/Rock-Snare-ff-2");
   }
   if (beat == 16 && bar % 2 == 0) {
     playeffect("rock-kit/Rock-Snare-ff-1"); // Ghost note
   }
  
   // More complex hi-hat pattern
   if (beat % 2 == 1) {
     playeffect("rock-kit/Rock-Kit-HiHat-Tip-1");
   }
   if (beat == 5 || beat == 13) {
     playeffect("rock-kit/Rock-Kit-HiHat-Open");
   }
   if (beat % 4 == 0) {
     playeffect("rock-kit/Rock-Kit-HiHat-Shank-1");
   }
  
   usleep(sixteenth);
   beat = beat + 1;
 }
 bar = bar + 1;
}


// Final 4 bars with full complexity
bar = 1;
while (bar <= 4) {
 beat = 1;
 while (beat <= 16) {
   // Kick pattern
   if (bar % 2 == 1) {
     if (beat == 1 || beat == 7 || beat == 9 || beat == 15) {
       playeffect("rock-kit/Rock-Kit-Kick-ff-1");
     }
   } else {
     if (beat == 1 || beat == 9 || beat == 12 || beat == 15) {
       playeffect("rock-kit/Rock-Kit-Kick-ff-2");
     }
   }
  
   // Complex snare pattern
   if (beat == 5 || beat == 13) {
     playeffect("rock-kit/Rock-Snare-ff-2");
   }
   if ((beat == 11 && bar % 2 == 1) || (beat == 16 && bar % 2 == 0)) {
     playeffect("rock-kit/Rock-Snare-ff-1"); // Ghost notes
   }
  
   // Syncopated hi-hat pattern
   if (beat == 1 || beat == 5 || beat == 9 || beat == 13) {
     playeffect("rock-kit/Rock-Kit-HiHat-Tip-1");
   }
   if (beat == 3 || beat == 11) {
     playeffect("rock-kit/Rock-Kit-HiHat-Shank-1"); // Accented
   }
   if (beat == 7 || beat == 15) {
     playeffect("rock-kit/Rock-Kit-HiHat-Open");
   }
  
   // Additional percussion
   if (beat == 8 && bar % 2 == 1) {
     playeffect("rock-kit/Rock-Kit-Floor-1");
   }
   if (beat == 15 && bar % 2 == 1) {
     playeffect("rock-kit/Rock-Kit-Floor-2");
   }
   if (beat == 6 && bar % 2 == 0) {
     playeffect("rock-kit/Rock-Rack-1");
   }
   if (beat == 14 && bar % 2 == 0) {
     playeffect("rock-kit/Rock-Rack-2");
   }
  
   usleep(sixteenth);
   beat = beat + 1;
 }
 bar = bar + 1;
}


// Ending with a crash and kick
playeffect("rock-kit/Rock-Kit-Crash-1-2");
playeffect("rock-kit/Rock-Kit-Kick-ff-1");
usleep(usecs_per_beat * 4);
```
