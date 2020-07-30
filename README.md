# Invoking DTMF Tones for Physical Access Grant on Fermax Lift Intercom System (CVE-2017-16778)
## Special Mention(s)
- First and foremost, @dizijoyjoy for assisting on the demo set in order for a successful shoot.
- Special acknowledgement to Fermax for the prompt response to the security bug report on their product. They were communicating and coordinating closely, and constantly providing updates on their fix and patch activities. Thank you for the pleasant collaboration!

## Brief description
A Fermax intercom system product was found to be vulnerable to an authorization bypass attack via Dual-tone Multiple Frequencies (DTMF) tones. Such bypass could allow an attacker to gain unauthorized access to residential level without proper approval or knowledge of the residential unit owner. All restricted floors could possibly be accessed if said Intercom is integrated with the elevator.
Fermax has since remediated this on affected product lines. 

## Details 
It was observed that an outdoor panel belonging to Fermax’s line of products, specifically a Fermax Outdoor Panel customized to be integrated with lift systems was found to be vulnerable to an authorization bypass attack via Dual-tone Multiple Frequencies (DTMF) tones impersonation. 
By design, the integrated lift intercom system is configured to assign various unit numbers of a building (e.g. #03-010) to owner's phone numbers such as a landline or a mobile number. When a visitor arrives at the publicly accessible level such as basement level 1 or ground level, the visitor will punch in the unit number and press the 'bell' icon to contact the owner. If the owner picks up the phone and wishes to allow the visitor to gain access to the unit's floor, the owner can choose to press '1' and '#' on his/her telecommunication device (e.g. mobile device) to trigger an 'access grant'. This would cause the intercom to summon the lift to the visitor's level, and grant level access to the visitor. 
![Standard Use Case](https://github.com/breaktoprotect/CVE-2017-16778-Intercom-DTMF-Injection/blob/master/illustration_1.PNG)
In normal circumstances, a user can only be granted access to a level if he/she scans his/her access card, or get access authorization through the Intercom system mentioned above. However, it was observed that this mechanism can be bypassed by playing a loud DTMF tone representing '1' and a long blast '#' through the intercom system.
As a result, an attacker with a sound playback device such as a mobile phone or a Bluetooth speaker would be able to play back a '1' and a long blast '#' to perform a 'access grant' execution on the Intercom, gaining unauthorized physical access to the victim's level. The victim, in this case, is the owner of the unit number that was entered into the Intercom system.
![Attack Use Case](https://github.com/breaktoprotect/CVE-2017-16778-Intercom-DTMF-Injection/blob/master/illustration_2.PNG)

## Proof of Concept Demo
To watch the demo, please click on the below image to be redirected to the Youtube video:

[![Demo!](https://github.com/breaktoprotect/CVE-2017-16778-Intercom-DTMF-Injection/blob/master/video_thumbnail.PNG)](https://youtu.be/1ym8WNvxxUk)

_Sorry, Youtube doesn't allow embedding of videos here_ 

## FAQ on POC Demo
**Q1. Why did the first 3 times failed and only the 4th time worked?**

**Ans:** The first 3 DTMF playback over the mailbox automated voice. The signal-to-noise ratio wasn't good enough for the intercom to pick up. It's akin to having difficulty to get Google Home or Alexa to listen to you when you have something loud playing on the background. The noise may range from dial-dead or engaged tones, voicemail message, etc. To fix this, increase the volume of the DTMF tones playback.

**Q2. Why not just use the dial pad on the intercom?**

**Ans:** The dial pad does not generate real-time DTMF tones. It only does do that only when you press the 'bell' (symbol) button and dial only the number assigned to the unit number you keyed in. Additionally, it does not work when the speaker-receiver is already active. 

## Affected Product
Fermax Outdoor Panel - FER-VCP-NNN (e.g. FER-VCP-100)

## Attack Vector
DTMF Tones using a secondary audio playback device (e.g. phone or Bluetooth speaker) delivered over the Audio Speaker-Receiver component.

## Steps to reproduce finding
1.	At the intercom, dial a unit number. Either wait for the owner to pick up, OR wait for the owner to reject the call. 
2.	While the speaker is activated, play the DTMF tone: 1 (short) and # (long).
3.	Observe that the Intercom interactive panel showing "Connected >>>>>>>>>>>>>>" and the lift button's LED getting lit up.
4.	Enter the lift and press the corresponding unit's level (e.g. if you dial 0301 + [BELL], you should be selecting floor 3). You should see that you have successfully bypassed the security mechanism via the Intercom.

## Impact
Physical premise installed with this integrated lift intercom system has increased risk of an unauthorized physical access to the building restricted floors.

## Recommendation
It is recommended that the integrated lift intercom system validates the source of the DTMF tones, which in this case is the DTMF tone ‘1’ and ‘#’ keys. It should differentiate and only allow authorization to be performed by the apartment unit owner's device rather than from the system’s audio speaker-receiver.

## Further Information
### Disclaimer
All activities conducted on assets were within the jurisdiction of Unit Owner and with prior permission Unit Owner.

### Disclosure Timeline
Date | Activity
---- | --------
2017-09-20 | Discovered and documented the vulnerability. Reported to <undisclosed> with vulnerability details and specific attack vectors.
2017-09-28 | Fermax acknowledged and the engineers confirmed the vulnerability.
2017-09-28 | Further details shared to inform of additional attack vectors.
2017-10-27 | Fermax responded to confirm patch solution was formulated and will be applied to all affected project.
2017-11-10 | Requested an estimated timeline of patch completion.
2017-11-11 | CVE ID issued by Mitre.org
2017-12-21 | Started patching the intercoms. Fermax requested for an extended period of time to patch as requires deployment of technicians on-site to perform said action.
2018-12-03 |Confirmation from Fermax that all affected lift intercom systems have been patched. Fermax authorizes us to release security advisory.
2019-MM-DD | Clearance granted.
2019-12-20 | Coordinated disclosure with security advisory published.
