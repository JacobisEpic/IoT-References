# Secure Key

This quest implements a secure key as a fob. You carry this fob with
you and when you press the button on the fob, a hub will grant you
access.

## Skill Cluster:

- [Databases](/skills/tingodb)
- [IR TX/RX](/skills/ir-tx-rx-remote)
- [Security Issues](/skills/security)
- [~~Leader Election~~](/skills/leader-election)
- [State Models](/skills/state-models)


## Description

<p align="center">
<img src="/docs/images/smart-key1.png" width="100%" />
</p>
<p align="center">
<i>System Components </i>
</p>

The secure key fob works like this:
- You (or someone else) carries a key fob (ESP device)
- When you want to unlock something:
  - A button on the fob is pressed
  - The button press initiates a short range near-field communications
  (NFC) message to transmit to the hub (we will use IR for NFC)
  - The hub then logs your presence [by sending the data to the RPi DB] and verifies your identity
  - On verification, the hub unlocks and sends an acknowledgement back to fob **[The intent is for the RPi to do authentication, not the receiver-ESP]**

Security is provided by the NFC message and perhaps some
encryption on top of the message. A dubious key should not open the lock.

Your job is to build and program the key fob for each of your team
members and then build and program the hub. This quest requires you to
incorporate several key skills including data persistence with
databases, communication with IR TX/RX, and a multi-device system.

<p align="center">
<img src="/images/smart-key-flow1.png" width="100%" />
</p>
<p align="center">
<i> Smart Key Data Flow</i>
</p>



Secure Key System Dataflow</center>

#### Additional Notes

- ***A key-open request*** is a successful exchange of data by a fob_ID at a hub_ID
- You may have multiple hubs in the system; therefore, each hub will have a unique ID
- Your "code" can be what your team defines. Consider a 4 digit number (PIN) or passphrase (text string)
- The design of the fob is the same as the transceiver in the IR TX/RX skill
- If you are short of ESP32s, you can build a fob with a switch to toggle the ID used (programmable ID)

<p align="center">
<img src="/images/ir-beacon.jpg" width="70%" />
</p>
<p align="center">
<i>IR TX/RX Transceiver </i>
</p>

## Solution Requirements
- Database logs each key-open request including time stamp, fob_ID,
 hub_ID, and name of person with fob
- Queries to database will reveal
  - Time series for (fob_ID)
  - Presence (indicates if a device has 'checked-in') to a room
- Button press received at hub is passed to RPi where it is validated.
RPi contacts the key fob by WiFi and then the key fob turns on a green LED to indicate that key granted access.
- The Hub is intended to be connected via WiFi to the network (not direclty connected via USB to the RPi)

## Assignment
1. Design and build your solution to meet criteria
specified in the rubric
2. Demonstrate your work
3. Reporting as per quest reporting instructions
4. Investigative question: comment on the
security of your system.  How would you best hack into this system if
you were so inclined? How could you prevent this attack? Describe the
steps.

## Rubric

| Objective Criterion | Rating | Max Value  | 
|---------------------------------------------|:-----------:|:---------:|
| Does A  |  |  1     | |
| Does B  |  |  1     | |
| Does C  |  |  1     | |
| Does D  |  |  1     | |
| Does E  |  |  1     | |
| Does F  |  |  1     | |
| Does G  |  |  1     | |

