
Analysis

    - Temperature seems to be highest among 20 to 30 degrees of latitude.
    - In most of the cities within -10 to 10 degrees of latitude, the humidity is above 50%
    - Cloudiness and wind speed doesn't really have any relationship with the latitude.


```python
import openweathermapy as owm
import pandas as pd
import numpy as np
from config import api_key
from citipy import citipy
import random
import matplotlib.pyplot as plt
```


```python
#Create list of random cities.

settings = {"units": "imperial", "appid": api_key}
city_list = []
weather_data= []
while len(weather_data)<500:
    r_lat = round(random.uniform(-90, 90),2)
    r_lng = round(random.uniform(-180, 180),2)
    city = citipy.nearest_city(r_lat,r_lng).city_name
    if not city in city_list:
        city_list.append(city)
        try:
            data = owm.get_current(city, **settings)
            weather_data.append(data)
            print(f"processing {city},{len(weather_data)}")
        except:
            pass
```

    processing kruisfontein,1
    processing yellowknife,2
    processing zyryanka,3
    processing la roda,4
    processing woodland,5
    processing ushuaia,6
    processing mataura,7
    processing cabo san lucas,8
    processing avarua,9
    processing jamestown,10
    processing gariaband,11
    processing kapaa,12
    processing punta arenas,13
    processing oktyabrskoye,14
    processing whitefish,15
    processing henties bay,16
    processing pechenga,17
    processing samur,18
    processing rikitea,19
    processing faya,20
    processing kimbe,21
    processing aklavik,22
    processing ilulissat,23
    processing sao filipe,24
    processing provideniya,25
    processing lebu,26
    processing bethel,27
    processing poum,28
    processing evensk,29
    processing victor harbor,30
    processing castro,31
    processing tuktoyaktuk,32
    processing lavrentiya,33
    processing taoudenni,34
    processing fairbanks,35
    processing vila velha,36
    processing bambous virieux,37
    processing batamshinskiy,38
    processing cabedelo,39
    processing hilo,40
    processing chilca,41
    processing diamantino,42
    processing tiznit,43
    processing arraial do cabo,44
    processing sibolga,45
    processing hobart,46
    processing ribeira grande,47
    processing shizunai,48
    processing umm lajj,49
    processing paamiut,50
    processing vao,51
    processing albany,52
    processing trapani,53
    processing puerto ayora,54
    processing vaini,55
    processing takayama,56
    processing xichang,57
    processing busselton,58
    processing victoria,59
    processing yeppoon,60
    processing hamilton,61
    processing luziania,62
    processing havre-saint-pierre,63
    processing abu samrah,64
    processing aranos,65
    processing nanortalik,66
    processing necochea,67
    processing lac du bonnet,68
    processing kuytun,69
    processing barrow,70
    processing bolu,71
    processing porbandar,72
    processing bichena,73
    processing cape town,74
    processing tasiilaq,75
    processing bluff,76
    processing east london,77
    processing dikson,78
    processing kerrville,79
    processing hithadhoo,80
    processing terrace bay,81
    processing atuona,82
    processing saskylakh,83
    processing rantepao,84
    processing ruidoso,85
    processing mayo,86
    processing esperance,87
    processing leningradskiy,88
    processing los llanos de aridane,89
    processing kedrovyy,90
    processing ponta do sol,91
    processing vardo,92
    processing hambantota,93
    processing bembereke,94
    processing port alfred,95
    processing thompson,96
    processing venice,97
    processing mar del plata,98
    processing camden,99
    processing kisangani,100
    processing baruun-urt,101
    processing flinders,102
    processing port lincoln,103
    processing bredasdorp,104
    processing new norfolk,105
    processing kaitangata,106
    processing chokurdakh,107
    processing caetes,108
    processing itarema,109
    processing constitucion,110
    processing araouane,111
    processing coquimbo,112
    processing torbay,113
    processing pedernales,114
    processing benguela,115
    processing anloga,116
    processing hinton,117
    processing kahului,118
    processing carnarvon,119
    processing cidreira,120
    processing port augusta,121
    processing turzovka,122
    processing port elizabeth,123
    processing christchurch,124
    processing norman wells,125
    processing saint-philippe,126
    processing mount isa,127
    processing makakilo city,128
    processing huarmey,129
    processing butaritari,130
    processing parana,131
    processing cherskiy,132
    processing san patricio,133
    processing upernavik,134
    processing mahebourg,135
    processing lompoc,136
    processing lorengau,137
    processing severo-kurilsk,138
    processing sitka,139
    processing husavik,140
    processing qaanaaq,141
    processing senador pompeu,142
    processing hermanus,143
    processing iqaluit,144
    processing goderich,145
    processing saint george,146
    processing southbridge,147
    processing luderitz,148
    processing adrar,149
    processing ust-kalmanka,150
    processing narsaq,151
    processing namatanai,152
    processing scarborough,153
    processing nakamura,154
    processing ondjiva,155
    processing gorontalo,156
    processing black river,157
    processing pochutla,158
    processing bima,159
    processing itaituba,160
    processing atbasar,161
    processing souillac,162
    processing hobyo,163
    processing pisco,164
    processing bandipur,165
    processing tiksi,166
    processing waingapu,167
    processing bonavista,168
    processing damietta,169
    processing ayan,170
    processing srandakan,171
    processing dire,172
    processing georgetown,173
    processing shache,174
    processing gamba,175
    processing cayenne,176
    processing acajutla,177
    processing kuandian,178
    processing hay river,179
    processing fort nelson,180
    processing maryville,181
    processing cairns,182
    processing sabang,183
    processing airai,184
    processing pingliang,185
    processing sorong,186
    processing gat,187
    processing meadow lake,188
    processing thaton,189
    processing tura,190
    processing burns lake,191
    processing conakry,192
    processing melfort,193
    processing praia da vitoria,194
    processing pendleton,195
    processing sorland,196
    processing ancud,197
    processing vila franca do campo,198
    processing phaltan,199
    processing hays,200
    processing luis correia,201
    processing santa rosa,202
    processing tarrafal,203
    processing nome,204
    processing alghero,205
    processing sattahip,206
    processing nouadhibou,207
    processing maniitsoq,208
    processing fort frances,209
    processing omsukchan,210
    processing xique-xique,211
    processing kavieng,212
    processing jaisalmer,213
    processing muzhi,214
    processing rabat,215
    processing kavaratti,216
    processing bathsheba,217
    processing honiara,218
    processing lata,219
    processing muravlenko,220
    processing fayaoue,221
    processing tomatlan,222
    processing izhma,223
    processing kalmunai,224
    processing potiskum,225
    processing saint-pierre,226
    processing orsha,227
    processing qaqortoq,228
    processing avera,229
    processing adrian,230
    processing keti bandar,231
    processing valparaiso,232
    processing kodiak,233
    processing chala,234
    processing inhambane,235
    processing yining,236
    processing geraldton,237
    processing calintaan,238
    processing tsabong,239
    processing codrington,240
    processing berdigestyakh,241
    processing maple creek,242
    processing grand gaube,243
    processing bam,244
    processing talnakh,245
    processing shelburne,246
    processing nuuk,247
    processing chuy,248
    processing richards bay,249
    processing grenfell,250
    processing dudinka,251
    processing atasu,252
    processing inisa,253
    processing tabuk,254
    processing moron,255
    processing imeni babushkina,256
    processing darnah,257
    processing saldanha,258
    processing shahada,259
    processing cartagena del chaira,260
    processing dong hoi,261
    processing nikolskoye,262
    processing hwange,263
    processing rio gallegos,264
    processing pouebo,265
    processing menongue,266
    processing lovozero,267
    processing broome,268
    processing belaya gora,269
    processing tuatapere,270
    processing wajima,271
    processing nova olinda do norte,272
    processing dawson creek,273
    processing mersing,274
    processing coracao de jesus,275
    processing ust-maya,276
    processing kozhva,277
    processing tazovskiy,278
    processing urengoy,279
    processing xuddur,280
    processing dingle,281
    processing roald,282
    processing la libertad,283
    processing bilma,284
    processing ellensburg,285
    processing te anau,286
    processing gaspe,287
    processing gillette,288
    processing ardakan,289
    processing visby,290
    processing poya,291
    processing zharkent,292
    processing coos bay,293
    processing sisimiut,294
    processing kaeo,295
    processing coswig,296
    processing praya,297
    processing healdsburg,298
    processing port blair,299
    processing banikoara,300
    processing yichun,301
    processing puerto madero,302
    processing ekibastuz,303
    processing olenegorsk,304
    processing lavumisa,305
    processing pauini,306
    processing zhemtala,307
    processing pevek,308
    processing sinnar,309
    processing vestmanna,310
    processing shira,311
    processing general roca,312
    processing kasongo-lunda,313
    processing puerto colombia,314
    processing weyburn,315
    processing kandrian,316
    processing ilawe,317
    processing katsuura,318
    processing namibe,319
    processing fruitvale,320
    processing cap malheureux,321
    processing abalak,322
    processing olyka,323
    processing vila,324
    processing bilibino,325
    processing yulara,326
    processing turan,327
    processing praxedis guerrero,328
    processing komsomolskiy,329
    processing magalia,330
    processing faanui,331
    processing salalah,332
    processing bonga,333
    processing paita,334
    processing bouar,335
    processing kurilsk,336
    processing khatanga,337
    processing elgin,338
    processing muros,339
    processing jumla,340
    processing thinadhoo,341
    processing ginda,342
    processing bereda,343
    processing pital,344
    processing eregli,345
    processing karratha,346
    processing caravelas,347
    processing raudeberg,348
    processing port-cartier,349
    processing grande prairie,350
    processing bubaque,351
    processing anadyr,352
    processing sovetskiy,353
    processing northam,354
    processing lanxi,355
    processing livingston,356
    processing lima,357
    processing pitkyaranta,358
    processing vestmannaeyjar,359
    processing whitehaven,360
    processing omboue,361
    processing sao gabriel,362
    processing merauke,363
    processing tessalit,364
    processing buritizeiro,365
    processing petropavlovsk-kamchatskiy,366
    processing la baneza,367
    processing sinnamary,368
    processing tautira,369
    processing salinas,370
    processing palu,371
    processing klaksvik,372
    processing nhulunbuy,373
    processing miraflores,374
    processing calama,375
    processing njombe,376
    processing benjamin hill,377
    processing ouallam,378
    processing magdalena,379
    processing maracacume,380
    processing boende,381
    processing doka,382
    processing road town,383
    processing yinchuan,384
    processing malumfashi,385
    processing petauke,386
    processing maunabo,387
    processing kishtwar,388
    processing lasa,389
    processing marshfield,390
    processing pathein,391
    processing berea,392
    processing antofagasta,393
    processing astoria,394
    processing natal,395
    processing chor,396
    processing tianpeng,397
    processing juru,398
    processing berestechko,399
    processing pierre,400
    processing vertientes,401
    processing udachnyy,402
    processing hofn,403
    processing mhasla,404
    processing gladstone,405
    processing pangoa,406
    processing kysyl-syr,407
    processing port hedland,408
    processing launceston,409
    processing mindelo,410
    processing lagoa,411
    processing brae,412
    processing shimoda,413
    processing sayaxche,414
    processing peachland,415
    processing abidjan,416
    processing patos,417
    processing mayumba,418
    processing maltahohe,419
    processing guerrero negro,420
    processing mwinilunga,421
    processing kiunga,422
    processing poronaysk,423
    processing cururupu,424
    processing porto velho,425
    processing labuhan,426
    processing shar,427
    processing nishihara,428
    processing luangwa,429
    processing willowmore,430
    processing bar harbor,431
    processing praia,432
    processing chivay,433
    processing sarankhola,434
    processing tanout,435
    processing talara,436
    processing yar-sale,437
    processing barra patuca,438
    processing kloulklubed,439
    processing pomabamba,440
    processing villa carlos paz,441
    processing ternate,442
    processing lewistown,443
    processing krabi,444
    processing eirunepe,445
    processing pangai,446
    processing viedma,447
    processing sur,448
    processing suntar,449
    processing skjervoy,450
    processing ixtapa,451
    processing hoquiam,452
    processing aripuana,453
    processing talikota,454
    processing mogadishu,455
    processing iturama,456
    processing vilyuysk,457
    processing maragogi,458
    processing csaszar,459
    processing kisber,460
    processing san policarpo,461
    processing kenai,462
    processing kondoa,463
    processing linhai,464
    processing indian head,465
    processing rugby,466
    processing porto novo,467
    processing charters towers,468
    processing chenzhou,469
    processing zemio,470
    processing nador,471
    processing san pedro,472
    processing rawson,473
    processing teguldet,474
    processing hasaki,475
    processing madison,476
    processing campos altos,477
    processing severiano melo,478
    processing yuxia,479
    processing makubetsu,480
    processing saint charles,481
    processing amapa,482
    processing zhigansk,483
    processing isangel,484
    processing adwa,485
    processing sisophon,486
    processing sulangan,487
    processing chadiza,488
    processing colares,489
    processing basco,490
    processing ballina,491
    processing myanaung,492
    processing banda aceh,493
    processing ierapetra,494
    processing bangarapet,495
    processing fukue,496
    processing amga,497
    processing palmer,498
    processing banjarmasin,499
    processing troitsko-pechorsk,500
    


```python
#Save it into Dataframe

city_index = [city['name'] for city in weather_data]
county = [city['sys']['country'] for city in weather_data]
lat = [city['coord']['lat'] for city in weather_data]
temp = [city['main']['temp'] for city in weather_data]
humidity = [city['main']['humidity'] for city in weather_data]
cloudiness = [city['clouds']['all'] for city in weather_data]
wind_speed = [city['wind']['speed'] for city in weather_data]

weather_df = pd.DataFrame({'city':city_index,'country':county,'lat':lat,'temp':temp,'humidity':humidity,'cloudiness':cloudiness,'wind_speed':wind_speed})
weather_df.to_csv("Results/Weather_df.csv")
weather_df.head(5)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>cloudiness</th>
      <th>country</th>
      <th>humidity</th>
      <th>lat</th>
      <th>temp</th>
      <th>wind_speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kruisfontein</td>
      <td>0</td>
      <td>ZA</td>
      <td>88</td>
      <td>-34.00</td>
      <td>57.34</td>
      <td>14.16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Yellowknife</td>
      <td>75</td>
      <td>CA</td>
      <td>40</td>
      <td>62.45</td>
      <td>73.40</td>
      <td>8.05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Zyryanka</td>
      <td>0</td>
      <td>RU</td>
      <td>26</td>
      <td>65.73</td>
      <td>75.07</td>
      <td>3.87</td>
    </tr>
    <tr>
      <th>3</th>
      <td>La Roda</td>
      <td>0</td>
      <td>ES</td>
      <td>52</td>
      <td>39.21</td>
      <td>69.80</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Woodland</td>
      <td>90</td>
      <td>US</td>
      <td>68</td>
      <td>45.91</td>
      <td>68.95</td>
      <td>5.82</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Scatter plot (Temperature vs Latitude)

plt.scatter(weather_df['lat'],weather_df['temp'],alpha=0.675,marker='o')
plt.title("2018-06-21 Temperature (F) vs. Latitude")
plt.ylabel("Temperature (F)")
plt.xlabel("Latitude")
plt.savefig("Results/Temperature")
```


![png](output_4_0.png)



```python
#Scatter plot (Humidity vs Latitude)
plt.scatter(weather_df['lat'],weather_df['humidity'],alpha=0.675,marker='o')
plt.title("2018-06-21 humidity vs. Latitude")
plt.ylabel("humidity")
plt.xlabel("Latitude")
plt.savefig("Results/Humidity")
```


![png](output_5_0.png)



```python
#Scatter plot (Cloudiness vs Latitude)
plt.scatter(weather_df['lat'],weather_df['cloudiness'],alpha=0.675,marker='o')
plt.title("2018-06-21 cloudiness vs. Latitude")
plt.ylabel("cloudiness")
plt.xlabel("Latitude")
plt.savefig("Results/Cloudiness")
```


![png](output_6_0.png)



```python
#Scatter plot (Wind_Speed vs Latitude)
plt.scatter(weather_df['lat'],weather_df['wind_speed'],alpha=0.675,marker='o')
plt.title("2018-06-21 wind_speed vs. Latitude")
plt.ylabel("wind_speed")
plt.xlabel("Latitude")
plt.savefig("Results/Wind_Speed")
```


![png](output_7_0.png)

