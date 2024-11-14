# Creepy Crawly Halloween Challenge

How close can you get to the ghoul without touching?  This is like
driving down the road and braking before you hit the pumpkins. OK,
Emily wants them to be spooky persons like witches, goblins, and
zombies?

For this in-class-challenge, you will be rewarded if you can bring
your crawler within 10cm of the ghoul. Of course, it needs to be
driving itsef and start at least 5m from the target.

Hit the target and it doesn't count.

Trick or treat if you can get within 10cm without touching. 


## Approach

If we were doing this, we would build out the following:

- Forward sensor capable of ranging distance (pick your favorite)
- Motor control with ESC (not too fast, not too slow)
- Steering (want to keep it straight for dead-reconing)
- Forward speed control that converges on a target distance (when
  distance to target = target distance, then there you are)

