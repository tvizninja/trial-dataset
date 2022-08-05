# NASA FIRMS

* 衛星観測を使った準リアルタイムの火災(熱源)検知情報
* 3.5-4.2um付近の波長
* AquaやTerraという衛星に搭載されているMODISというセンサーでは、分解能1km/px、観測時間分解能1回/日
* S-NPPやNOAA20という衛星に搭載のVIIRSといったセンサーでは、分解能375m/px、観測時間分解能2回/日
* 詳細は<https://firms.modaps.eosdis.nasa.gov/map/>にて、Fire/Hotspotsのiアイコンにあり

## Archive Download

* 年度単位などの過去データ
  * <https://firms.modaps.eosdis.nasa.gov/download/>
* 直近2カ月程度の過去データ
  * <https://nrt3.modaps.eosdis.nasa.gov/archive/FIRMS>
* 直近7日程度の過去データ
  * <https://firms.modaps.eosdis.nasa.gov/active_fire/#firms-txt>
* フォームから欲しいデータをリクエストしてダウンロードするサービスも
  * <https://firms.modaps.eosdis.nasa.gov/download/create.php>
* APIなどもある様子。使ったことないけど。
  * <https://firms.modaps.eosdis.nasa.gov/api/>

## 注意点など

* 山火事や広域火災の検知に役立つ一方で、発電所や鉄工所などの高温を放つ施設も検出されるため、要注意
* 北米や欧州では、大規模火災やWildfireを監視したりアラートする機関があるようなので、そうしたものと照らし合わせたいところ
  * <https://www.nifc.gov/fire-information/nfn>
  * <https://effis.jrc.ec.europa.eu/apps/firenews.viewer/>

## trial

* shapeなどもあるのだが、基本的にPointのデータなのでCSVが分かりやすい。下記にCSVの一部を示す

```
latitude,longitude,bright_ti4,scan,track,acq_date,acq_time,satellite,instrument,confidence,version,bright_ti5,frp,daynight,type
36.428391,140.525269,326.93,0.6,0.71,2021-01-01,0230,N,VIIRS,n,1,279.23,1.67,D,0
33.260014,131.650284,333.39,0.38,0.36,2021-01-01,0412,N,VIIRS,n,1,286.5,3.31,D,2
33.263306,131.649567,334.03,0.38,0.36,2021-01-01,0412,N,VIIRS,n,1,282.3,3.31,D,2
```

* `bright_ti4`: brightness temperature of the fire pixel measured in Kelvin.
* `scan/track`: 1ピクセルの幅(m)
* `acq_date`,`acq_time`: 観測時刻(UTC)
* `confidence`: 太陽光の混入など様々な理由で誤検知されることがあり、推測されるデータの信頼性を表す。l:low/n:nominal/h:high
* `type`(一部データに付与): 0:植生火災と思われる 1:火山活動 2:その他定常的な熱源 3:海上検出
* `daynight`: d:日中観測 n:夜間観測
