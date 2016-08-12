# SimpleTune
SimpleTune is a small JS library for making simple tunes.

# Why SimpleTune over other audio libraries?
There are many great WebAudio libraries out there, but I often found that I only needed to play a few notes here or there. Many existing libraries include advanced functionality that I don't need, so I created SimpleTune to provide a small and easy way to quickly generate a few notes.

# Usage
To build:

    git clone https://github.com/christopherwk210/SimpleTune.git
    cd SimpleTune
    npm install
    grunt

To use, just include SimpleTune.min.js:

    <script src="dist/SimpleTune.min.js"></script>

# Quick Start

## Initializing

Before using SimpleTune, it has to be initialized:

    var myTune = new SimpleTune('sine');

The constructor takes a single argument, which is the type of wave you wish to use. This can be sine, square, sawtooth, or triangle. Alternatively, you can omit the argument to use the default type which is sine wave.

## Playing Notes

To play a note, simply:

    myTune.playNote('C5');

That's it! By default, the default duration the note is held is 100ms (1/10th of a second). This can be changed by passing in a duration in milliseconds as a second argument:

    //Play A4 for 1 second
    myTune.playNote(440, 1000);

As you can see above, this method also accepts a real number to use as the note frequency. In this case, we use 440 Hz which is equal to the music note A4.

If you supply a duration of 0, then the note will play indefinitely. It will then need to be stopped later on manually, with the stop method:

    //Stop playing the current note
    myTune.stop();

## Changing Audio Options

You can change the wave type and gain with the following methods:

    //Change the wave type to triangle
    myTune.setType('triangle');

    //Change the gain to .5
    myTune.setGain(0.5);

The `setGain` method takes a number between 0 and 1, 0 being no volume and 1 being full volume.

## Handling Promises
Whenever you play a note with the `playNote` method, a promise is returned. The Promise is fulfilled as soon as the note finished playing:

    //Play a note and log the promise resolve
    myTune.playNote('G6', 1500).then(function(e) {
      console.log(e);
    });

The Promise resolve provides access to the audio context, oscillator node, and gain node.

You can also chain notes together this way:

    //Outline a C major chord
    myTune.playNote('C5').then(function() {
      myTune.playNote('E5').then(function() {
        myTune.playNote('G5');
      });
    });

## Accessing the audio context
If you need to access the audio context being used at any time, you can use the following method:

    var audioCtx = myTune.getAudio();

# Browser compatibility
SimpleTune will work in browsers that support the Web Audio API and Promises:

* Microsoft Edge 12+
* Firefox 29+
* Chrome 33+
* Safari 7.1+
* iOS Safari 8+
* Opera 20+

Note that IE is _NOT_ supported, since IE does not support the Web Audio API.
