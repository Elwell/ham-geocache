# Ham Geocache idea
This repo contains the hopes and dreams of a vague plan to 'Value Add' the fine art of ham radio foxhunting (aka direction finding - see https://en.wikipedia.org/wiki/Transmitter_hunting) 

I'm not sure which variant of the game would work best: 
1. Each cache has a separate transmitter - traditional foxhunt skills required. Multiple caches in an game zone need to be on separate frequencies (if simultaneous) or have timed windows. Do we want a fixed run order where caches only start up once a previous one has been found? Need RX / control channel (LoRA? - needs to be OOB for the main competition and restricted)

2. Coordinator acts more like an orienteering course - sends out 'hints' of where to find the caches. Perhaps with low accuracy (higher resolution available to those who've found a message on a previous cache with an offset or suffix to the GPS coords.) 

## Components Required
### Fancy Cache
This can be a traditional low power transmitter, however it should also have an ID (can be broadcast or visual label) and a means of displaying a Time-Based One-Time Password (TOTP, see https://datatracker.ietf.org/doc/html/rfc6238) 

GPS lock (for timing, possible uplink of position to admin side) is power hungry, need to power down for best battery life. Do we also only want TOTP dispayed on button press? Keep internal log for later validation (we at least will know *time* someone pressed button, even if we don't know *who*

### coordinator / scoring system
Likely a simple web application - A participant can register a 'find' by sending the cache ID and TOTP code to the coordinator. If the code is valid (secret hash decodes OK within time window) the participant (validated via their Callsign / APRS passphrase) gains a score. 

Using the TOTP in addition to the cache ID should prevent replay attacks (only the first valid decode of TOTP + cacheID is credited - This will rate limit the throughput of cache scorers - if multiple people arrive at a cache at the same time, each participant will have to wait for a unique code before they can claim the find. If the window is set small (high throughput of cache finders) there is a risk TOTP clocks will be out of sync. Too large a validity window reduces the risk of clock skew, but slows down the rate people can claim a cache. Adjust as needed (I suspect the standard 30s will be sufficient)

Some sort of database / dashboard showing a leaderboard of finders, how many people have found each cache, fastest time to find etc could add to the competitive feel. 

### APRS radio system 
While the submission of cache finds *can* be done via a web based form, the size of the message lends itself to being submitted via an APRS message. How to incorporate this into the scoring is left as an exercise for the reader. 
The coordinator shoud monitor APRS (either directly if using a non-standard frequency) or via aprs-is. 


## Work In progress...
All of this is subject to change, random ideas etc. Likely to be thrashed around on the REAST discord or over coffee at VK7CMS. 
