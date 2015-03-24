#Problem

We want to be able to generate an audio file that is a combination of 2 audio files that take a given transition between them.

#Questions

How do you generate an mp3 file that is a mix of 2 songs?

What is the best way to store a transition, and how do you use that transition?

#Resources
1: [songshift.py]

###Mini-abstract and relevance of [songshift.py]

A python script I wrote previously for this project solves the problem of writing to an mp3 file.  However, I hope to find a better solution, since the given solution is computationally inefficient.

An mp3 file can be written by generating an array of audio data, and writing to an audio file using this array of audio data.  

[songshift.py]: https://github.com/mulfordjc/BeatShift/blob/master/songmix.py
