# miBlam
MIcrocontroller based ButtonLess Audio player with Mono speaker

This project is a follow-up to "blast" with mucher cheaper hardware and it is much simpler to build.
Read https://github.com/metalmax83/blast to get information on why I built a device like this and what's the idea behind it.

While being used by at least three happy little kids (I built it three times), blast had certain disadvantages:
* expensive
* lots of components and thus
* complicated assembly
* hardware was kind of "overkill"

With miBlam, I'm trying to eliminate these disadvantages and at the same time make the device more robust and also faster.
The relatively high price of blast came mainly from its brain: a RPi(3). While I absolutely love these little rascals, they do not really come cheap. 35€ plus at least 10€ for a camera and another 8€ for a soundcard is quite a lot, especially if you plan to build several of these devices as gifts for the ever growing number of kids in our circle of friends and acquaintances. The overall price came out north of a hundred bucks and that made me think about a cheaper alternative without giving up the virtues. What does the RPi actually do in blast? It plays mp3 files, little else. There has to be a way to do this much cheaper. I did some thinking and out came a solution, that replaces the RPi, the camera, the soundcard, the audio transformer, the mono summing, the lighting, the class D board, the switch for the slot and the stepdown converter by just three cheap little components.

As its name already suggests, a microcontroller will be heart and brain of miBlam. From my tinkering around with Arduinos I already have some experience with the ATmega series, so the choice of the uC came quite naturally: an ATmega 328P-PU it is! While I do not require all the pins, I will need the memory and RAM it has to offer. 

But what about the key feature of blast, the little plywood "media" cards with the QR code? The 328 is quite beefy for a uC, but image processing powerful enough for a QR decoding seems a little out of his range. I opted for a different approach while keeping the feature of having discrete "physical media". When I found a little module for a price well below 1.50€ that is NFC capable and offers SPI communication it came clear: Mifare cards are the way to go!

Ok, the uC is told what to play via NFC, but where does the music come from? I did some searching in the shallows of chinese trading platforms and found an mp3 player module with DAC and an uSD slot that is controlled via serial interface. Perfect! It is also really cheap, around 2€/piece. 

The uC cannot be left naked of course, so I designed a PCB that offers, aside from the uC and its additional components, the mono summing in a little preamplifier, an audio amplifier based on the good old LM386 (1W max, but that should be sufficient for driving parents crazy) and pin interfaces for connecting the components. I designed it for home production, so it isn't too crowded, one sided and has enough room between tracks so that it can be hand drawn. The mp3 module could be soldered directly to the PCB, but the NFC module should be connected by wires, as this makes the placing a lot simpler. The board takes 12V which are taken directly for the audio circuitery and are converted to 5V (by LM7805) for the uC and the rest of the components.

Another feature I borrowed from a commerical product is the skipping function. It will be realized by two piezo disks as knock detectors. Tracks can be skipped forward by a knock to the right and backward by a knock to the left. That is virtually free (2c for a piezo disk), impossible to break and I can ditch the KY040 from blast, which has shown to be not sturdy enough for an average two year old. Volume can than be controlled by a normal analog potentiometer, which is much more robust.

I will update this side once I have assembled a prototype, which will be in a few weeks, as I'm waiting for several components to be delivered from China.
