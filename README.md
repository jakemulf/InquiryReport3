#Problem

We want to be able to generate an audio file that is a combination of 2 audio files that take a given transition between them.

#Questions

How do you generate an mp3 file that is a mix of 2 songs?

What is the best way to store a transition, and how do you use that transition?

#Resources
1: [songshift.py]

###Mini-abstract and relevance of [songshift.py]

A python script I wrote previously for this project solves the problem of writing to an mp3 file.  However, I hope to find a better solution, since the given solution is computationally inefficient for simply writing an audio file.

An mp3 file can be written by generating an array of audio data, and writing to an audio file using this array of audio data.  In order to make a transition between 2 songs, the transition indexs can be used as bounds for generating the audio data.

```python
import dirac
from echonest.remix import audio
from pyechonest import track

audiofile1 = audio.LocalAudioFile(first_filename)
beats1 = audiofile1.analysis.beats
collect = []


while (beat_count < start_beat + shift_length and beat_count < len(beats1)):
  beat_audio = beats1[beat_count].render()
  scaled_beat = dirac.timeScale(beat_audio.data, 1.0)
  ts = audio.AudioData(ndarray=scaled_beat, shape=scaled_beat.shape,
            sampleRate=audiofile1.sampleRate, numChannels=scaled_beat.shape[1])
  collect.append(ts)
  beat_count = beat_count + 1

beat_count = second_start

audiofile2 = audio.LocalAudioFile(second_filename)
beats2 = audiofile2.analysis.beats

while (beat_count < len(beats2)):
  beat_audio = beats2[beat_count].render()
  scaled_beat = dirac.timeScale(beat_audio.data, 1.0)
  ts = audio.AudioData(ndarray=scaled_beat, shape=scaled_beat.shape,
      sampleRate=audiofile2.sampleRate, numChannels=scaled_beat.shape[1])
  collect.append(ts)
  beat_count = beat_count + 1

out = audio.assemble(collect, numChannels=2)
out.encode(output_filename)
```

For this problem, the next issue will be how to determin which indexs to transition between.  Using [twosongshift.py], you can determin the best transition between 2 songs.  [twosongshift.py] writes the transition to a text file, and you can read this text file to get the ideal transition.

[songshift.py]: https://github.com/mulfordjc/BeatShift/blob/master/songmix.py
[twosongshift.py]: https://github.com/mulfordjc/TwoBeatShift/blob/master/twosongshift.py
