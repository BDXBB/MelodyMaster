<p align="center">
<img src="https://scrutinizer-ci.com/g/dotX12/ShazamIO/badges/quality-score.png?b=master" alt="https://scrutinizer-ci.com/g/dotX12/ShazamIO/">
<img src="https://scrutinizer-ci.com/g/dotX12/ShazamIO/badges/code-intelligence.svg?b=master" alt="https://scrutinizer-ci.com/g/dotX12/ShazamIO/">
<img src="https://scrutinizer-ci.com/g/dotX12/ShazamIO/badges/build.png?b=master" alt="https://scrutinizer-ci.com/g/dotX12/ShazamIO/">
<img src="https://badge.fury.io/py/shazamio.svg" alt="https://badge.fury.io/py/shazamio">
<img src="https://pepy.tech/badge/shazamio" alt="https://pepy.tech/project/shazamio">
<img src="https://pepy.tech/badge/shazamio/month" alt="https://pepy.tech/project/shazamio">
<img src="https://img.shields.io/github/license/dotX12/shazamio.svg" alt="https://github.com/dotX12/ShazamIO/blob/master/LICENSE.txt">
<br><br>
  
  <img width="1000" src="https://user-images.githubusercontent.com/64792903/109359596-ca561a00-7896-11eb-9c93-9cf1f283b1a5.png">
  🎵 Is a FREE asynchronous library from reverse engineered Shazam API written in Python 3.8+ with asyncio and aiohttp. Includes all the methods that Shazam has, including searching for a song by file.
 
-----
</p>

## 💿 Installation

```
💲 pip install MelodyMaster
```

## 💻 Example


<details> 
<summary>
<i>🔎🎵 Recognize track</i>
</summary>

Recognize a track based on a file<br>

  ```python3
import asyncio
from MelodyMaster import Shazam


async def main():
    shazam = Shazam()
    # out = await shazam.recognize_song('dora.ogg') # slow and deprecated, don't use this!
    out = await shazam.recognize('dora.ogg')  # rust version, use this!
    print(out)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>👨‍🎤 About artist</i>
</summary>

Retrieving information from an artist profile<br>
<a href="https://www.shazam.com/artist/43328183/nathan-evans">https://www.shazam.com/artist/43328183/nathan-evans</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    artist_id = 43328183
    about_artist = await shazam.artist_about(artist_id)
    serialized = Serialize.artist(about_artist)

    print(about_artist)  # dict
    print(serialized)  # serialized from dataclass factory

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>


<details> 
<summary>
<i>🎵📄 About track</i>
</summary>

Get track information<br>
<a href="https://www.shazam.com/track/552406075/ale-jazz">https://www.shazam.com/track/552406075/ale-jazz</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    track_id = 552406075
    about_track = await shazam.track_about(track_id=track_id)
    serialized = Serialize.track(data=about_track)

    print(about_track)  # dict
    print(serialized)  # serialized from dataclass factory

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🎵⌛ Track listenings count</i>
</summary>

Returns the number of times a particular song has been played<br>
<a href="https://www.shazam.com/track/559284007/rampampam">https://www.shazam.com/track/559284007/rampampam</a>

  ```python3
import asyncio
from MelodyMaster import Shazam


async def main():
    # Example: https://www.shazam.com/track/559284007/rampampam

    shazam = Shazam()
    track_id = 559284007
    count = await shazam.listening_counter(track_id=track_id)
    print(count)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🎶💬 Similar songs</i>
</summary>

Similar songs based song id<br>
<a href="https://www.shazam.com/track/546891609/2-phu%CC%81t-ho%CC%9Bn-kaiz-remix">https://www.shazam.com/track/546891609/2-phu%CC%81t-ho%CC%9Bn-kaiz-remix</a>

  ```python3
import asyncio
from MelodyMaster import Shazam


async def main():
    shazam = Shazam()
    track_id = 546891609
    related = await shazam.related_tracks(track_id=track_id, limit=5, offset=2)
    # ONLY №3, №4 SONG
    print(related)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🔎👨‍🎤 Search artists</i>
</summary>

Search all artists by prefix<br>
  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    artists = await shazam.search_artist(query='Lil', limit=5)
    for artist in artists['artists']['hits']:
        serialized = Serialize.artist(data=artist)
        print(serialized)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

  ```
</details>

<details> 
<summary>
<i>🔎🎶 Search tracks</i>
</summary>

Search all tracks by prefix<br>

  ```python3
import asyncio
from MelodyMaster import Shazam


async def main():
    shazam = Shazam()
    tracks = await shazam.search_track(query='Lil', limit=5)
    print(tracks)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

  ```
</details>

<details> 
<summary>
<i>🔝🎶👨‍🎤 Top artist tracks</i>
</summary>

Get the top songs according to Shazam<br>
<a href="https://www.shazam.com/artist/201896832/kizaru">https://www.shazam.com/artist/201896832/kizaru</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize
from MelodyMaster.schemas.artists import ArtistQuery
from MelodyMaster.schemas.enums import ArtistView


async def main():
    shazam = Shazam()
    artist_id = 1081606072

    about_artist = await shazam.artist_about(
        artist_id,
        query=ArtistQuery(
            views=[
                ArtistView.TOP_SONGS,
            ],
        ),
    )
    serialized = Serialize.artist_v2(about_artist)
    for i in serialized.data[0].views.top_songs.data:
        print(i.attributes.name)


loop = asyncio.get_event_loop_policy().get_event_loop()
loop.run_until_complete(main())


  ```
</details>

<details> 
<summary>
<i>🔝🎶🏙️ Top tracks in city</i>
</summary>

Retrieving information from an artist profile<br>
<a href="https://www.shazam.com/charts/top-50/russia/moscow">https://www.shazam.com/charts/top-50/russia/moscow</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    top_ten_moscow_tracks = await shazam.top_city_tracks(country_code='RU', city_name='Moscow', limit=10)
    print(top_ten_moscow_tracks)
    # ALL TRACKS DICT
    for track in top_ten_moscow_tracks['tracks']:
        serialized = Serialize.track(data=track)
        # SERIALIZE FROM DATACLASS FACTORY
        print(serialized)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())

  ```
</details>

<details> 
<summary>
<i>🔝🎶 Top tracks in country</i>
</summary>

Get the best tracks by country code<br>
<a href="https://www.shazam.com/charts/discovery/netherlands">https://www.shazam.com/charts/discovery/netherlands</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    top_five_track_from_amsterdam = await shazam.top_country_tracks('NL', 5)
    for track in top_five_track_from_amsterdam['tracks']:
        serialized = Serialize.track(data=track)
        print(serialized)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🔝🎶🎸 Top tracks in country by genre</i>
</summary>

The best tracks by a genre in the country<br>
<a href="https://www.shazam.com/charts/genre/spain/hip-hop-rap">https://www.shazam.com/charts/genre/spain/hip-hop-rap</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, GenreMusic


async def main():
    shazam = Shazam()
    top_spain_rap = await shazam.top_country_genre_tracks(
        country_code='ES',
        genre=GenreMusic.HIP_HOP_RAP,
        limit=4
    )
    print(top_spain_rap)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🔝🎶🌏🎸 Top tracks in world by genre</i>
</summary>

Get world tracks by certain genre<br>
<a href="https://www.shazam.com/charts/genre/world/rock">https://www.shazam.com/charts/genre/world/rock</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize, GenreMusic


async def main():
    shazam = Shazam()
    top_rock_in_the_world = await shazam.top_world_genre_tracks(genre=GenreMusic.ROCK, limit=10)

    for track in top_rock_in_the_world['tracks']:
        serialized_track = Serialize.track(data=track)
        print(serialized_track.spotify_url)


loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>🔝🎶🌏Top tracks in world</i>
</summary>

Get the best tracks from all over the world<br>
<a href="https://www.shazam.com/charts/top-200/world">https://www.shazam.com/charts/top-200/world</a>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    top_world_tracks = await shazam.top_world_tracks(limit=10)
    print(top_world_tracks)
    for track in top_world_tracks['tracks']:
        serialized = Serialize.track(track)
        print(serialized)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>


## How to use data serialization

<details> 
<summary>
<i>Open Code</i>
</summary>

  ```python3
import asyncio
from MelodyMaster import Shazam, Serialize


async def main():
    shazam = Shazam()
    top_five_track_from_amsterdam = await shazam.top_country_tracks('NL', 5)
    for track in top_five_track_from_amsterdam['tracks']:
        serialized = Serialize.track(data=track)
        print(serialized.title)

loop = asyncio.get_event_loop()
loop.run_until_complete(main())
  ```
</details>

<details> 
<summary>
<i>Open photo: What song information looks like (Dict)</i>
</summary>
<img src="https://user-images.githubusercontent.com/64792903/109454521-75b4c980-7a65-11eb-917e-62da3abefb8a.png">

</details>

<details> 
<summary>
<i>Open photo: what song information looks like (Custom serializer)</i>
</summary>
<img src="https://user-images.githubusercontent.com/64792903/109454465-57e76480-7a65-11eb-956c-1bcac41d7de5.png">

</details>

Agree, thanks to the serializer, you no longer need to manually select the necessary data from the dictionary. Now the serializer contains the most necessary information about an artist or a track.


## How to use in Terminal

1. **recognize_song**: Used to recognize songs.

   Example:
   ```
   MelodyMaster recognize_song --file_path "path/to/audio_file"
   ```
   This example indicates that you want to recognize the song using the audio file located at "path/to/audio_file".

2. **about_artist**: Used to get information about an artist.

   Example:
   ```
   MelodyMaster about_artist --artist_id "Artist id"
   ```
   This example requests information about the artist named "Artist id".

3. **recognize_and_search**: Used to recognize songs and search for the song's name.

   Example:
   ```
   MelodyMaster recognize_and_search --file_path "path/to/audio_file"
   ```
   This example means you want to recognize the song using the audio file located at "path/to/audio_file" and search for the song's name.

4. **search_album**: Used to search for an album using the album ID.

   Example:
   ```
   MelodyMaster search_album --album_id 123
   ```
   This example searches for the album with the ID 123.

5 .**get_default_lyrics**: Used to get the default lyrics of a song.

   Example:
   ```
   MelodyMaster get_default_lyrics --title "Song Title" --srt "true"
   ```
   This example means you want to get the lyrics of the song titled "Song Title" and --srt if true give you lyrics with time if --srt false just lyrics
   
6 .**get_alternative_lyrics**: Used to get alternative lyrics of a song.

   Example:
   ```
   MelodyMaster get_alternative_lyrics --title "Song Title" --artist "Artist Name" --duration "Duration" --str "true"
   ```
   This example means you want to get the alternative lyrics of the song titled "Song Title" by the artist "Artist Name" with duration "Duration". duration and Artist name optional

 7. **recognize_text**: Used to recognize text from an audio file.

   Example:
   ```
   MelodyMaster recognize_text --file_path "path/to/audio_file" --lang "en-GB"
   ```
   This example means you want to recognize the text from the audio file located at "path/to/audio_file" the lang for language you can find it .
   <details> 
<summary>
<i>here</i>
</summary>
     
 Afrikaans (South Africa) : af-ZA  
 Albanian (Albania) : sq-AL  
 Albanian (Albania) : sq-AL  
 Amharic (Ethiopia) : am-ET  
 Amharic (Ethiopia) : am-ET  
 Arabic (Algeria) : ar-DZ  
 Arabic (Algeria) : ar-DZ  
 Arabic (Bahrain) : ar-BH  
 Arabic (Bahrain) : ar-BH  
 Arabic (Egypt) : ar-EG  
 Arabic (Egypt) : ar-EG  
 Arabic (Iraq) : ar-IQ  
 Arabic (Iraq) : ar-IQ  
 Arabic (Israel) : ar-IL  
 Arabic (Israel) : ar-IL  
 Arabic (Jordan) : ar-JO  
 Arabic (Jordan) : ar-JO  
 Arabic (Kuwait) : ar-KW  
 Arabic (Kuwait) : ar-KW  
 Arabic (Lebanon) : ar-LB  
 Arabic (Lebanon) : ar-LB  
 Arabic (Morocco) : ar-MA  
 Arabic (Morocco) : ar-MA  
 Arabic (Oman) : ar-OM  
 Arabic (Oman) : ar-OM  
 Arabic (Qatar) : ar-QA  
 Arabic (Qatar) : ar-QA  
 Arabic (Saudi Arabia) : ar-SA  
 Arabic (Saudi Arabia) : ar-SA  
 Arabic (Palestine) : ar-PS  
 Arabic (Palestine) : ar-PS  
 Arabic (Tunisia) : ar-TN  
 Arabic (Tunisia) : ar-TN  
 Arabic (UAE) : ar-AE
 Arabic (Yemen) : ar-YE  
 Arabic (Yemen) : ar-YE  
 Armenian (Armenia) : hy-AM  
 Armenian (Armenia) : hy-AM  
 Azerbaijani (Azerbaijan) : az-AZ  
 Azerbaijani (Azerbaijan) : az-AZ  
 Basque (Spain) : eu-ES  
 Basque (Spain) : eu-ES  
 Bengali (Bangladesh) : bn-BD  
 Bengali (Bangladesh) : bn-BD  
 Bengali (India) : bn-IN  
 Bengali (India) : bn-IN  
 Bosnian (Bosnia Herzegovina) : bs-BA  
 Bosnian (Bosnia Herzegovina) : bs-BA  
 Bulgarian (Bulgaria) : bg-BG  
 Bulgarian (Bulgaria) : bg-BG  
 Burmese (Myanmar) : my-MM  
 Burmese (Myanmar) : my-MM  
 Catalan (Spain) : ca-ES  
 Catalan (Spain) : ca-ES  
 Chinese, Cantonese (Traditional Hong Kong) : yue-Hant-HK  
 Chinese, Mandarin (Simplified, China) : zh (cmn-Hans-CN)
 Chinese, Mandarin (Traditional, Taiwan) : zh-TW (cmn-Hant-TW)
 Croatian (Croatia) : hr-HR  
 Croatian (Croatia) : hr-HR  
 Czech (Czech Republic) : cs-CZ
 Czech (Czech Republic) : cs-CZ
 Danish (Denmark) : da-DK
 Danish (Denmark) : da-DK
 Dutch (Belgium) : nl-BE  
 Dutch (Belgium) : nl-BE  
 Dutch (Netherlands) : nl-NL
 Dutch (Netherlands) : nl-NL
 English (Australia) : en-AU
 English (Australia) : en-AU
 English (Canada) : en-CA
 English (Canada) : en-CA  
 English (Ghana) : en-GH
 English (Ghana) : en-GH
 English (Hong Kong) : en-HK
 English (Hong Kong) : en-HK
 English (India) : en-IN
 English (India) : en-IN
 English (Ireland) : en-IE
 English (Ireland) : en-IE
 English (Kenya) : en-KE
 English (Kenya) : en-KE
 English (New Zealand) : en-NZ
 English (New Zealand) : en-NZ
 English (Nigeria) : en-NG
 English (Nigeria) : en-NG
 English (Pakistan) : en-PK
 English (Pakistan) : en-PK
 English (Philippines) : en-PH
 English (Philippines) : en-PH  
 English (Singapore) : en-SG
 English (Singapore) : en-SG
 English (South Africa) : en-ZA
 English (South Africa) : en-ZA
 English (Tanzania) : en-TZ
 English (Tanzania) : en-TZ  
 English (United Kingdom) : en-GB      
 English (United States) : en-US    
 English (United States) : en-US    
 Estonian (Estonia) : et-EE  
 Estonian (Estonia) : et-EE  
 Filipino (Philippines) : fil-PH  
 Filipino (Philippines) : fil-PH  
 Finnish (Finland) : fi-FI
 Finnish (Finland) : fi-FI
 French (Belgium) : fr-BE
 French (Belgium) : fr-BE
 French (Canada) : fr-CA
 French (Canada) : fr-CA
 French (France) : fr-FR   
 French (France) : fr-FR  
 French (Switzerland) : fr-CH
 French (Switzerland) : fr-CH
 Galician (Spain) : gl-ES  
 Galician (Spain) : gl-ES  
 Georgian (Georgia) : ka-GE  
 Georgian (Georgia) : ka-GE  
 German (Austria) : de-AT  
 German (Austria) : de-AT  
 German (Germany) : de-DE
 German (Germany) : de-DE
 German (Switzerland) : de-CH  
 German (Switzerland) : de-CH  
 Greek (Greece) : el-GR  
 Greek (Greece) : el-GR  
 Gujarati (India) : gu-IN  
 Gujarati (India) : gu-IN  
 Hebrew (Israel) : iw-IL
 Hebrew (Israel) : iw-IL
 Hindi (India) : hi-IN
 Hindi (India) : hi-IN
 Hungarian (Hungary) : hu-HU  
 Hungarian (Hungary) : hu-HU  
 Icelandic (Iceland) : is-IS  
 Icelandic (Iceland) : is-IS  
 Indonesian (Indonesia) : id-ID
 Indonesian (Indonesia) : id-ID
 Italian (Italy) : it-IT
 Italian (Italy) : it-IT
 Italian (Switzerland) : it-CH  
 Italian (Switzerland) : it-CH  
 Japanese (Japan) : ja-JP     
 Japanese (Japan) : ja-JP    
 Javanese (Indonesia) : jv-ID  
 Javanese (Indonesia) : jv-ID  
 Kannada (India) : kn-IN  
 Kannada (India) : kn-IN  
 Kazakh (Kazakhstan) : kk-KZ  
 Kazakh (Kazakhstan) : kk-KZ  
 Khmer (Cambodia) : km-KH  
 Khmer (Cambodia) : km-KH  
 Korean (South Korea) : ko-KR
 Korean (South Korea) : ko-KR
 Lao (Laos) : lo-LA  
 Lao (Laos) : lo-LA  
 Latvian (Latvia) : lv-LV  
 Latvian (Latvia) : lv-LV  
 Lithuanian (Lithuania) : lt-LT  
 Lithuanian (Lithuania) : lt-LT  
 Macedonian (North Macedonia) :
mk-MK  
 Macedonian (North Macedonia) : mk-MK  
 Malay (Malaysia) : ms-MY  
 Malay (Malaysia) : ms-MY  
 Malayalam (India) : ml-IN
 Malayalam (India) : ml-IN
 Marathi (India) : mr-IN  
 Marathi (India) : mr-IN  
 Mongolian (Mongolia) : mn-MN  
 Mongolian (Mongolia) : mn-MN  
 Nepali (Nepal) : ne-NP  
 Nepali (Nepal) : ne-NP  
 Norwegian Bokmål (Norway): no-NO
 Norwegian Bokmål (Norway): no-NO
 Persian (Iran) : fa-IR  
 Persian (Iran) : fa-IR  
 Polish (Poland) : pl-PL
 Polish (Poland) : pl-PL
 Portuguese (Brazil) : pt-BR
 Portuguese (Brazil) : pt-BR
 Portuguese (Portugal) : pt-PT
 Portuguese (Portugal) : pt-PT
 Punjabi (Gurmukhi India) : pa-Guru-IN  
 Punjabi (Gurmukhi India) : pa-Guru-IN  
 Romanian (Romania) : ro-RO  
 Romanian (Romania) : ro-RO  
 Russian (Russia) : ru-RU
 Russian (Russia) : ru-RU
 Russian (Russia) : ru-RU     
 Russian (Russia) : ru-RU    
 Serbian (Serbia) : sr-RS  
 Serbian (Serbia) : sr-RS  
 Sinhala (Sri Lanka) : si-LK  
 Sinhala (Sri Lanka) : si-LK  
 Slovak (Slovakia) : sk-SK  
 Slovak (Slovakia) : sk-SK  
 Slovenian (Slovenia) : sl-SI  
 Slovenian (Slovenia) : sl-SI  
 Spanish (Argentina) : es-AR  
 Spanish (Argentina) : es-AR  
 Spanish (Bolivia) : es-BO  
 Spanish (Bolivia) : es-BO  
 Spanish (Chile) : es-CL  
 Spanish (Chile) : es-CL  
 Spanish (Colombia) : es-CO  
 Spanish (Colombia) : es-CO  
 Spanish (Costa Rica) : es-CR  
 Spanish (Costa Rica) : es-CR  
 Spanish (Dominican Rep.) : es-DO
 Spanish (Ecuador) : es-EC  
 Spanish (Ecuador) : es-EC  
 Spanish (El Salvador) : es-SV  
 Spanish (El Salvador) : es-SV  
 Spanish (Guatemala) : es-GT  
 Spanish (Guatemala) : es-GT  
 Spanish (Honduras) : es-HN  
 Spanish (Honduras) : es-HN  
 Spanish (Mexico) : es-MX  
 Spanish (Mexico) : es-MX  
 Spanish (Nicaragua) : es-NI  
 Spanish (Nicaragua) : es-NI  
 Spanish (Panama) : es-PA  
 Spanish (Panama) : es-PA  
 Spanish (Paraguay) : es-PY  
 Spanish (Paraguay) : es-PY  
 Spanish (Peru) : es-PE  
 Spanish (Peru) : es-PE  
 Spanish (Puerto Rico) : es-PR  
 Spanish (Puerto Rico) : es-PR  
 Spanish (Spain) : es-ES
 Spanish (Spain) : es-ES    
 Spanish (United States) : es-US    
 Spanish (Uruguay) : es-UY  
 Spanish (Uruguay) : es-UY  
 Spanish (Venezuela) : es-VE  
 Spanish (Venezuela) : es-VE  
 Sundanese (Indonesia) : su-ID  
 Sundanese (Indonesia) : su-ID  
 Swahili (Kenya) : sw-KE  
 Swahili (Kenya) : sw-KE  
 Swahili (Tanzania) : sw-TZ  
 Swahili (Tanzania) : sw-TZ  
 Swedish (Sweden) : sv-SE
 Swedish (Sweden) : sv-SE
 Tamil (India) : ta-IN  
 Tamil (India) : ta-IN  
 Tamil (Malaysia) : ta-MY  
 Tamil (Malaysia) : ta-MY  
 Tamil (Singapore) : ta-SG  
 Tamil (Singapore) : ta-SG  
 Tamil (Sri Lanka) : ta-LK  
 Tamil (Sri Lanka) : ta-LK  
 Telugu (India) : te-IN  
 Telugu (India) : te-IN  
 Thai (Thailand) : th-TH  
 Thai (Thailand) : th-TH  
 Turkish (Turkey) : tr-TR
 Turkish (Turkey) : tr-TR
 Ukrainian (Ukraine) : uk-UA  
 Ukrainian (Ukraine) : uk-UA  
 Urdu (India) : ur-IN  
 Urdu (India) : ur-IN  
 Urdu (Pakistan) : ur-PK  
 Urdu (Pakistan) : ur-PK  
 Uzbek (Uzbekistan) : uz-UZ  
 Uzbek (Uzbekistan) : uz-UZ  
 Vietnamese (Vietnam) : vi-VN  
 Vietnamese (Vietnam) : vi-VN  
 Zulu (South Africa) : zu-ZA  
 Zulu (South Africa) : zu-ZA  
</details>

# MelodyMaster

MelodyMaster is a modified version of the Shazamio library.

## Acknowledgements

We would like to express our gratitude to everyone who contributed to the modification of the MelodyMaster library, which is based on the Shazamio library.


## Contact Us

For any inquiries or feedback, you can reach us on Telegram at [@BDXBB](https://t.me/BDXBB).
