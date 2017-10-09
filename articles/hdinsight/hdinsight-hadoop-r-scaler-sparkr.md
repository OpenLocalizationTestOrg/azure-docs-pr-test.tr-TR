---
title: "aaaUse ScaleR ve Azure Hdınsight ile SparkR | Microsoft Docs"
description: "R Server ve Hdınsight ile ScaleR ve SparkR kullanma"
services: hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5a76f897-02e8-4437-8f2b-4fb12225854a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: da732ff0235cf465a1452b81750c7cdd0351eed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="combine-scaler-and-sparkr-in-hdinsight"></a>ScaleR ve hdınsight'ta SparkR birleştirin

Bu makalede nasıl toopredict uçuş kullanarak varış gecikmeler gösterilmektedir bir **ScaleR** uçuş gecikmeleri ve hava durumu verileri Lojistik regresyon modelinden birleştirilmiş ile **SparkR**. Bu senaryo ScaleR hello yeteneklerini analizi için Microsoft R Server ile birlikte kullanılan Spark üzerinde veri işleme için gösterir. Bu teknolojiler Hello birleşimi dağıtılmış işlem tooapply hello en son özellikleri sağlar.

Her iki paket Hadoop'ın Spark yürütme altyapısı üzerinde çalışsa da bunlar her kendi ilgili Spark oturumları gerektiği paylaşımı bellek içi verilerden engellenir. R Server gelecek bir sürümünde bu sorun giderilinceye kadar toomaintain çakışmayan Spark oturumlar ve Ara dosyaları tooexchange verilerine hello geçici bir çözüm değildir. Burada Hello yönergeleri Bu gereksinimleri basit tooachieve olduğunu gösterir.

Burada başlangıçta Strata 2016 konumundaki konuşma Mario Inchiosa ve ayrıca hello Web Semineri kullanılabilir Roni Burd tarafından paylaşılan örnek kullanırız [R ölçeklenebilir bir veri bilimi platformuyla derleme](http://event.on24.com/eventRegistration/console/EventConsoleNG.jsp?uimode=nextgeneration&eventid=1160288&sessionid=1&key=8F8FB9E2EB1AEE867287CD6757D5BD40&contenttype=A&eventuserid=305999&playerwidth=1000&playerheight=650&caller=previewLobby&text_language_id=en&format=fhaudio). hello örnek SparkR toojoin hello kullanır iyi bilinen airlines varış gecikme veri kümesiyle ayrılma ve varış havaalanları hava durumu verileri. Birleştirilmiş hello veri sonra uçuş varış gecikme etmede giriş tooa ScaleR Lojistik regresyon modeli olarak kullanılır.

Merhaba kod biz izlenecek R Spark Azure Hdınsight kümesinde çalışan sunucusu yazıldı. Ancak hello kullanımda SparkR ve ScaleR tek bir betik karıştırma hello kavramı da şirket içi ortamları hello bağlamında geçerli. Merhaba Aşağıda, biz Ara bir R ve R hello bilgisi düzeyini varsayın [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction) R Server kitaplığı. Biz de kullanımını tanıtmak [SparkR](https://spark.apache.org/docs/2.1.0/sparkr.html) bu senaryo taramasını oluştu.

## <a name="hello-airline-and-weather-datasets"></a>Merhaba uçak ve hava durumu veri kümeleri

Merhaba **AirOnTime08to12CSV** airlines ortak dataset gelen uçuş varış ve hello ABD, içindeki tüm ticari uçuşları ayrılma ayrıntılarını hakkında bilgi içeren Ekim 1987 tooDecember 2012. Bu büyük bir veri kümesidir: toplam neredeyse 150 milyon kayıtları vardır. Bunu açılmış yalnızca altında 4 GB'tır. Hello kullanılabilir [ABD hükümeti arşivler](http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236). Daha rahat 303 ayrı aylık CSV dosyalarından hello kümesini içeren bir zip dosyası (AirOnTimeCSV.zip) olarak kullanılabilir [Revolution Analytics veri deposu](http://packages.revolutionanalytics.com/datasets/AirOnTime87to12/)

toosee hello etkileri hava durumu uçuş gecikmeler, ayrıca her hello havaalanları hello hava veri ihtiyacımız var. Bu verileri ham formunda, ZIP dosyaları olarak aya hello indirilebilir [National Oceanic ve hava yönetim deposu](http://www.ncdc.noaa.gov/orders/qclcd/). Bu örnek hello amacıyla, hava durumu veri Mayıs 2007'den – Kasım 2012 çekmek ve hello saatlik veri dosyaları her hello 68 aylık zips içinde kullanılan. Merhaba aylık ZIP dosyaları ayrıca hello hava durumu İstasyon Kimliği (WBAN), (CallSign) ile ilişkili olduğunu hello havaalanı arasında bir eşleme (YYYYMMstation.txt) içerir ve Havaalanı'nın saat dilimi UTC (saat dilimi) uzaklığı hello. Bu bilgilerin tümünü hello uçak gecikmesi ve hava durumu verilerle katılırken gereklidir.

## <a name="setting-up-hello-spark-environment"></a>Merhaba Spark ortamını ayarlama

Merhaba ilk tooset hello Spark çevresi adımdır. Bizim giriş veri dizinlerini içeren toohello dizine işaret eden, Spark işlem bağlamı oluşturma ve bilgilendirici günlük toohello Konsolu için günlüğe kaydetme işlevi oluşturarak başlayın:

```
workDir        <- '~'  
myNameNode     <- 'default' 
myPort         <- 0
inputDataDir   <- 'wasb://hdfs@myAzureAcccount.blob.core.windows.net'
hdfsFS         <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

# create a persistent Spark session tooreduce startup times 
#   (remember toostop it later!)
 
sparkCC        <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort, persistentRun=TRUE)

# create working directories 

rxHadoopMakeDir('/user')
rxHadoopMakeDir('user/RevoShare')
rxHadoopMakeDir('user/RevoShare/remoteuser')

(dataDir <- '/share')
rxHadoopMakeDir(dataDir)
rxHadoopListFiles(dataDir) 

setwd(workDir)
getwd()

# version of rxRoc that runs in a local CC 
rxRoc <- function(...){
  rxSetComputeContext(RxLocalSeq())
  roc <- RevoScaleR::rxRoc(...)
  rxSetComputeContext(sparkCC)
  return(roc)
}

logmsg <- function(msg) { cat(format(Sys.time(), "%Y-%m-%d %H:%M:%S"),':',msg,'\n') } 
t0 <- proc.time() 

#..start 

logmsg('Start') 
(trackers <- system("mapred job -list-active-trackers", intern = TRUE))
logmsg(paste('Number of task nodes=',length(trackers)))
```

Sonraki böylece biz SparkR kullanın ve SparkR oturum başlatma biz "Spark_Home" toohello arama yolu R paketleri ekleyin:

```
#..setup for use of SparkR  

logmsg('Initialize SparkR') 

.libPaths(c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib"), .libPaths()))
library(SparkR)

sparkEnvir <- list(spark.executor.instances = '10',
                   spark.yarn.executor.memoryOverhead = '8000')

sc <- sparkR.init(
  sparkEnvir = sparkEnvir,
  sparkPackages = "com.databricks:spark-csv_2.10:1.3.0"
)

sqlContext <- sparkRSQL.init(sc)
```

## <a name="preparing-hello-weather-data"></a>Merhaba hava durumu verileri hazırlama

tooprepare hello hava durumu verileri, biz alt Bu model için gerekli toohello sütunları: 

- "Görünürlük"
- "DryBulbCelsius"
- "DewPointCelsius"
- "RelativeHumidity"
- "WindSpeed"
- "Altimeter"

Daha sonra hello hava durumu istasyonla ilişkilendirilmiş bir havaalanındaki kodu ekleyin ve yerel saat tooUTC hello ölçümleri Dönüştür.

Bir dosya toomap hello hava durumu istasyon (WBAN) bilgisi tooan havaalanı kodu oluşturarak başlayın. Merhaba hava durumu verilerle dahil hello eşleme dosyasından Biz bu bağıntı alabilirsiniz. Eşleme hello tarafından *CallSign* (örneğin, LAX) hello hava veri dosyasında çok alan*kaynak* hello hava yolu veri. Ancak, biz yalnızca toohave başka bir yandan eşleyen eşleme oldu *WBAN* çok*AirportID* (örneğin, 12892 LAX için) ve içerir *saat dilimi* tooa kaydedildi CSV dosyası olarak adlandırılan "wban-için-havaalanı-kimliği-tz. CSV"biz kullanabilirsiniz. Örneğin:

| AirportID | WBAN | saat dilimi
|-----------|------|---------
| 10685 | 54831 | -6
| 14871 | 24232 | -8
| .. | .. | ..

Merhaba kod okumaları her hello saatlik ham hava durumu verileri aşağıdaki dosyaları, biz gerekir, hello hava durumu istasyon eşleme dosyası birleştirir, ölçümleri tooUTC tarih zamanları hello ayarlar ve hello dosyanın yeni bir sürümünü yazar alt kümelerini toohello sütunları:

```
# Look up AirportID and Timezone for WBAN (weather station ID) and adjust time

adjustTime <- function(dataList)
{
  dataset0 <- as.data.frame(dataList)
  
  dataset1 <- base::merge(dataset0, wbanToAirIDAndTZDF1, by = "WBAN")

  if(nrow(dataset1) == 0) {
    dataset1 <- data.frame(
      Visibility = numeric(0),
      DryBulbCelsius = numeric(0),
      DewPointCelsius = numeric(0),
      RelativeHumidity = numeric(0),
      WindSpeed = numeric(0),
      Altimeter = numeric(0),
      AdjustedYear = numeric(0),
      AdjustedMonth = numeric(0),
      AdjustedDay = integer(0),
      AdjustedHour = integer(0),
      AirportID = integer(0)
    )
    
    return(dataset1)
  }
  
  Year <- as.integer(substr(dataset1$Date, 1, 4))
  Month <- as.integer(substr(dataset1$Date, 5, 6))
  Day <- as.integer(substr(dataset1$Date, 7, 8))
  
  Time <- dataset1$Time
  Hour <- ceiling(Time/100)
  
  Timezone <- as.integer(dataset1$TimeZone)
  
  adjustdate = as.POSIXlt(sprintf("%4d-%02d-%02d %02d:00:00", Year, Month, Day, Hour), tz = "UTC") + Timezone * 3600

  AdjustedYear = as.POSIXlt(adjustdate)$year + 1900
  AdjustedMonth = as.POSIXlt(adjustdate)$mon + 1
  AdjustedDay   = as.POSIXlt(adjustdate)$mday
  AdjustedHour  = as.POSIXlt(adjustdate)$hour
  
  AirportID = dataset1$AirportID
  Weather = dataset1[,c("Visibility", "DryBulbCelsius", "DewPointCelsius", "RelativeHumidity", "WindSpeed", "Altimeter")]
  
  data.set = data.frame(cbind(AdjustedYear, AdjustedMonth, AdjustedDay, AdjustedHour, AirportID, Weather))
  
  return(data.set)
}

wbanToAirIDAndTZDF <- read.csv("wban-to-airport-id-tz.csv")

colInfo <- list(
  WBAN = list(type="integer"),
  Date = list(type="character"),
  Time = list(type="integer"),
  Visibility = list(type="numeric"),
  DryBulbCelsius = list(type="numeric"),
  DewPointCelsius = list(type="numeric"),
  RelativeHumidity = list(type="numeric"),
  WindSpeed = list(type="numeric"),
  Altimeter = list(type="numeric")
)

weatherDF <- RxTextData(file.path(inputDataDir, "WeatherRaw"), colInfo = colInfo)

weatherDF1 <- RxTextData(file.path(inputDataDir, "Weather"), colInfo = colInfo,
                filesystem=hdfsFS)

rxSetComputeContext("localpar")
rxDataStep(weatherDF, outFile = weatherDF1, rowsPerRead = 50000, overwrite = T,
           transformFunc = adjustTime,
           transformObjects = list(wbanToAirIDAndTZDF1 = wbanToAirIDAndTZDF))
```

## <a name="importing-hello-airline-and-weather-data-toospark-dataframes"></a>Merhaba uçak ve hava durumu veri tooSpark DataFrames içeri aktarma

Merhaba SparkR kullanırız artık [read.df()](https://docs.databricks.com/spark/latest/sparkr/functions/read.df.html) tooimport hello hava durumu ve uçak veri tooSpark DataFrames işlev. Bu işlev, diğer birçok Spark yöntemi gibi yürütüldüğünde gevşek, bunlar yürütülmek üzere sıraya ancak gerekli kadar yürütülmedi olduğunu anlamına gelir.

```
airPath     <- file.path(inputDataDir, "AirOnTime08to12CSV")
weatherPath <- file.path(inputDataDir, "Weather") # pre-processed weather data
rxHadoopListFiles(airPath) 
rxHadoopListFiles(weatherPath) 

# create a SparkR DataFrame for hello airline data

logmsg('create a SparkR DataFrame for hello airline data') 
# use inferSchema = "false" for more robust parsing
airDF <- read.df(sqlContext, airPath, source = "com.databricks.spark.csv", 
                 header = "true", inferSchema = "false")

# Create a SparkR DataFrame for hello weather data

logmsg('create a SparkR DataFrame for hello weather data') 
weatherDF <- read.df(sqlContext, weatherPath, source = "com.databricks.spark.csv", 
                     header = "true", inferSchema = "true")
```

## <a name="data-cleansing-and-transformation"></a>Veri temizleme ve dönüştürme

Biz bazı temizleme yapılacağına hello uçak verileri biz toorename sütunları aldığınız. Biz yalnızca gerekli hello değişkenleri tutun ve zamanlanmış ayrılma kez ayrılma hello son hava durumu verileri ile birleştirme saat tooenable en yakın toohello aşağı yuvarlar:

```
logmsg('clean hello airline data') 
airDF <- rename(airDF,
                ArrDel15 = airDF$ARR_DEL15,
                Year = airDF$YEAR,
                Month = airDF$MONTH,
                DayofMonth = airDF$DAY_OF_MONTH,
                DayOfWeek = airDF$DAY_OF_WEEK,
                Carrier = airDF$UNIQUE_CARRIER,
                OriginAirportID = airDF$ORIGIN_AIRPORT_ID,
                DestAirportID = airDF$DEST_AIRPORT_ID,
                CRSDepTime = airDF$CRS_DEP_TIME,
                CRSArrTime =  airDF$CRS_ARR_TIME
)

# Select desired columns from hello flight data. 
varsToKeep <- c("ArrDel15", "Year", "Month", "DayofMonth", "DayOfWeek", "Carrier", "OriginAirportID", "DestAirportID", "CRSDepTime", "CRSArrTime")
airDF <- select(airDF, varsToKeep)

# Apply schema
coltypes(airDF) <- c("character", "integer", "integer", "integer", "integer", "character", "integer", "integer", "integer", "integer")

# Round down scheduled departure time toofull hour.
airDF$CRSDepTime <- floor(airDF$CRSDepTime / 100)
```

Artık hello hava durumu verileri benzer işlemler gerçekleştirebilir:

```
# Average weather readings by hour
logmsg('clean hello weather data') 
weatherDF <- agg(groupBy(weatherDF, "AdjustedYear", "AdjustedMonth", "AdjustedDay", "AdjustedHour", "AirportID"), Visibility="avg",
                  DryBulbCelsius="avg", DewPointCelsius="avg", RelativeHumidity="avg", WindSpeed="avg", Altimeter="avg"
                  )

weatherDF <- rename(weatherDF,
                    Visibility = weatherDF$'avg(Visibility)',
                    DryBulbCelsius = weatherDF$'avg(DryBulbCelsius)',
                    DewPointCelsius = weatherDF$'avg(DewPointCelsius)',
                    RelativeHumidity = weatherDF$'avg(RelativeHumidity)',
                    WindSpeed = weatherDF$'avg(WindSpeed)',
                    Altimeter = weatherDF$'avg(Altimeter)'
)
```

## <a name="joining-hello-weather-and-airline-data"></a>Merhaba hava durumu ve uçak verileri birleştirme

Şimdi hello SparkR kullanırız [join()](https://docs.databricks.com/spark/latest/sparkr/functions/join.html) toodo bir sol dış birleşim ayrılma AirportID tarafından hello uçak ve hava durumu verilerinin ve datetime işlev. Merhaba dış birleşim bize hello uçak verilerinin tümünü kaydeder eşleşen hava durumu verileri olsa bile tooretain sağlar. Merhaba birleştirme, aşağıdaki biz bazı gereksiz sütunları kaldırmak ve hello birleştirme tarafından sunulan tutulan hello sütunları tooremove hello gelen DataFrame öneki yeniden adlandırın.

```
logmsg('Join airline data with weather at Origin Airport')
joinedDF <- SparkR::join(
  airDF,
  weatherDF,
  airDF$OriginAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF1 <- select(joinedDF, varsToKeep)

joinedDF2 <- rename(joinedDF1,
                    VisibilityOrigin = joinedDF1$Visibility,
                    DryBulbCelsiusOrigin = joinedDF1$DryBulbCelsius,
                    DewPointCelsiusOrigin = joinedDF1$DewPointCelsius,
                    RelativeHumidityOrigin = joinedDF1$RelativeHumidity,
                    WindSpeedOrigin = joinedDF1$WindSpeed,
                    AltimeterOrigin = joinedDF1$Altimeter
)
```

Benzer bir şekilde hello hava durumu ve uçak veri varış AirportID ve datetime göre Katıl:

```
logmsg('Join airline data with weather at Destination Airport')
joinedDF3 <- SparkR::join(
  joinedDF2,
  weatherDF,
  airDF$DestAirportID == weatherDF$AirportID &
    airDF$Year == weatherDF$AdjustedYear &
    airDF$Month == weatherDF$AdjustedMonth &
    airDF$DayofMonth == weatherDF$AdjustedDay &
    airDF$CRSDepTime == weatherDF$AdjustedHour,
  joinType = "left_outer"
)

# Remove redundant columns
vars <- names(joinedDF3)
varsToDrop <- c('AdjustedYear', 'AdjustedMonth', 'AdjustedDay', 'AdjustedHour', 'AirportID')
varsToKeep <- vars[!(vars %in% varsToDrop)]
joinedDF4 <- select(joinedDF3, varsToKeep)

joinedDF5 <- rename(joinedDF4,
                    VisibilityDest = joinedDF4$Visibility,
                    DryBulbCelsiusDest = joinedDF4$DryBulbCelsius,
                    DewPointCelsiusDest = joinedDF4$DewPointCelsius,
                    RelativeHumidityDest = joinedDF4$RelativeHumidity,
                    WindSpeedDest = joinedDF4$WindSpeed,
                    AltimeterDest = joinedDF4$Altimeter
                    )
```

## <a name="save-results-toocsv-for-exchange-with-scaler"></a>Exchange için sonuçları tooCSV ScaleR ile kaydetme

Merhaba birleştirmeler SparkR ile toodo ihtiyacımız tamamlanan. Biz hello son Spark DataFrame "joinedDF5" tooa CSV giriş tooScaleR için hello veri kaydetmek ve hello SparkR oturumu kapatın. Biz açıkça SparkR toosave söyleyin 80 ayrı bölümlere tooenable yeterli paralellik ScaleR işlem içinde sonuç CSV hello:

```
logmsg('output hello joined data from Spark tooCSV') 
joinedDF5 <- repartition(joinedDF5, 80) # write.df below will produce this many CSVs

# write result toodirectory of CSVs
write.df(joinedDF5, file.path(dataDir, "joined5Csv"), "com.databricks.spark.csv", "overwrite", header = "true")

# We can shut down hello SparkR Spark context now
sparkR.stop()

# remove non-data files
rxHadoopRemove(file.path(dataDir, "joined5Csv/_SUCCESS"))
```

## <a name="import-tooxdf-for-use-by-scaler"></a>İçeri aktarma tooXDF ScaleR tarafından kullanılmak üzere

Biz, birleştirilmiş uçak ve hava durumu verilerinin olarak hello CSV dosyasını kullanabilirsiniz-ScaleR metin veri kaynağına aracılığıyla modelleme içindir. Ancak, hello veri kümesi üzerinde birden çok işlemleri çalışırken daha etkili olduğundan biz bunu tooXDF ilk olarak, içeri:

```
logmsg('Import hello CSV toocompressed, binary XDF format') 

# set hello Spark compute context for R Server 
rxSetComputeContext(sparkCC)
rxGetComputeContext()

colInfo <- list(
  ArrDel15 = list(type="numeric"),
  Year = list(type="factor"),
  Month = list(type="factor"),
  DayofMonth = list(type="factor"),
  DayOfWeek = list(type="factor"),
  Carrier = list(type="factor"),
  OriginAirportID = list(type="factor"),
  DestAirportID = list(type="factor"),
  RelativeHumidityOrigin = list(type="numeric"),
  AltimeterOrigin = list(type="numeric"),
  DryBulbCelsiusOrigin = list(type="numeric"),
  WindSpeedOrigin = list(type="numeric"),
  VisibilityOrigin = list(type="numeric"),
  DewPointCelsiusOrigin = list(type="numeric"),
  RelativeHumidityDest = list(type="numeric"),
  AltimeterDest = list(type="numeric"),
  DryBulbCelsiusDest = list(type="numeric"),
  WindSpeedDest = list(type="numeric"),
  VisibilityDest = list(type="numeric"),
  DewPointCelsiusDest = list(type="numeric")
)

joinedDF5Txt <- RxTextData(file.path(dataDir, "joined5Csv"),
                           colInfo = colInfo, fileSystem = hdfsFS)
rxGetInfo(joinedDF5Txt) 

destData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

rxImport(inData = joinedDF5Txt, destData, overwrite = TRUE)

rxGetInfo(destData, getVarInfo = T)

# File name: /user/RevoShare/dev/delayDataLarge/joined5XDF 
# Number of composite data files: 80 
# Number of observations: 148619655 
# Number of variables: 22 
# Number of blocks: 320 
# Compression type: zlib 
# Variable information: 
#   Var 1: ArrDel15, Type: numeric, Low/High: (0.0000, 1.0000)
# Var 2: Year
# 26 factor levels: 1987 1988 1989 1990 1991 ... 2008 2009 2010 2011 2012
# Var 3: Month
# 12 factor levels: 10 11 12 1 2 ... 5 6 7 8 9
# Var 4: DayofMonth
# 31 factor levels: 1 3 4 5 7 ... 29 30 2 18 31
# Var 5: DayOfWeek
# 7 factor levels: 4 6 7 1 3 2 5
# Var 6: Carrier
# 30 factor levels: PI UA US AA DL ... HA F9 YV 9E VX
# Var 7: OriginAirportID
# 374 factor levels: 15249 12264 11042 15412 13930 ... 13341 10559 14314 11711 10558
# Var 8: DestAirportID
# 378 factor levels: 13303 14492 10721 11057 13198 ... 14802 11711 11931 12899 10559
# Var 9: CRSDepTime, Type: integer, Low/High: (0, 24)
# Var 10: CRSArrTime, Type: integer, Low/High: (0, 2400)
# Var 11: RelativeHumidityOrigin, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 12: AltimeterOrigin, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 13: DryBulbCelsiusOrigin, Type: numeric, Low/High: (-46.1000, 47.8000)
# Var 14: WindSpeedOrigin, Type: numeric, Low/High: (0.0000, 81.0000)
# Var 15: VisibilityOrigin, Type: numeric, Low/High: (0.0000, 90.0000)
# Var 16: DewPointCelsiusOrigin, Type: numeric, Low/High: (-41.7000, 29.0000)
# Var 17: RelativeHumidityDest, Type: numeric, Low/High: (0.0000, 100.0000)
# Var 18: AltimeterDest, Type: numeric, Low/High: (28.1700, 31.1600)
# Var 19: DryBulbCelsiusDest, Type: numeric, Low/High: (-46.1000, 53.9000)
# Var 20: WindSpeedDest, Type: numeric, Low/High: (0.0000, 136.0000)
# Var 21: VisibilityDest, Type: numeric, Low/High: (0.0000, 88.0000)
# Var 22: DewPointCelsiusDest, Type: numeric, Low/High: (-43.0000, 29.0000)

finalData <- RxXdfData(file.path(dataDir, "joined5XDF"), fileSystem = hdfsFS)

```

## <a name="splitting-data-for-training-and-test"></a>Verileri eğitim ve test için bölme

Merhaba 2012 veri çıkışı rxDataStep toosplit test etmek için kullanır ve eğitim hello rest tutun:

```
# split out hello training data

logmsg('split out training data as all data except year 2012')
trainDS <- RxXdfData( file.path(dataDir, "finalDataTrain" ),fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = trainDS,
            rowSelection = ( Year != 2012 ), overwrite = T )

# split out hello testing data

logmsg('split out hello test data for year 2012') 
testDS <- RxXdfData( file.path(dataDir, "finalDataTest" ), fileSystem = hdfsFS)

rxDataStep( inData = finalData, outFile = testDS,
            rowSelection = ( Year == 2012 ), overwrite = T )

rxGetInfo(trainDS)
rxGetInfo(testDS)
```

## <a name="train-and-test-a-logistic-regression-model"></a>Eğitme ve test Lojistik regresyon modeli

Artık hazır toobuild bir model bulunur. Merhaba geliş saati gecikme üzerinde toosee hello etkisi hava durumu verilerinin ScaleR'ın Lojistik regresyon yordamı kullanın. 15 dakikadan daha büyük bir alma gecikme hello hava hello ayrılma ve varış havaalanları adresindeki etkilediği olup olmadığını biz bunu toomodel kullanın:

```
logmsg('train a logistic regression model for Arrival Delay > 15 minutes') 
formula <- as.formula(ArrDel15 ~ Year + Month + DayofMonth + DayOfWeek + Carrier +
                     OriginAirportID + DestAirportID + CRSDepTime + CRSArrTime + 
                     RelativeHumidityOrigin + AltimeterOrigin + DryBulbCelsiusOrigin +
                     WindSpeedOrigin + VisibilityOrigin + DewPointCelsiusOrigin + 
                     RelativeHumidityDest + AltimeterDest + DryBulbCelsiusDest +
                     WindSpeedDest + VisibilityDest + DewPointCelsiusDest
                   )

# Use hello scalable rxLogit() function but set max iterations too3 for hello purposes of 
# this exercise 

logitModel <- rxLogit(formula, data = trainDS, maxIterations = 3)

base::summary(logitModel)
```

Şimdi nasıl hello üzerinde veri bazı tahminleri yapma ve ROC ve AUC arayarak test görelim.

```
# Predict over test data (Logistic Regression).

logmsg('predict over hello test data') 
logitPredict <- RxXdfData(file.path(dataDir, "logitPredict"), fileSystem = hdfsFS)

# Use hello scalable rxPredict() function

rxPredict(logitModel, data = testDS, outData = logitPredict,
          extraVarsToWrite = c("ArrDel15"), 
          type = 'response', overwrite = TRUE)

# Calculate ROC and Area Under hello Curve (AUC).

logmsg('calculate hello roc and auc') 
logitRoc <- rxRoc("ArrDel15", "ArrDel15_Pred", logitPredict)
logitAuc <- rxAuc(logitRoc)
head(logitAuc)
logitAuc

plot(logitRoc)
```

## <a name="scoring-elsewhere"></a>Başka bir yerde Puanlama

Biz de hello modeli Puanlama verileri başka bir platformda kullanabilirsiniz. Tooan RDS dosyası kaydedilirken aktarma ve SQL Server R Hizmetleri gibi ortam Puanlama hedef bu RDS alma tarafından. Hangi hello üzerinde model yerleşik skoru hello veri toobe hello faktörü düzeyleri eşleştiğinden önemli tooensure olur. Eşleşme elde edilebilir çıkartarak ve hello sütun bilgileri kaydedilirken ilişkili veri ScaleR'ın aracılığıyla modelleme hello `rxCreateColInfo()` işlevi ve bu sütun bilgileri toohello giriş veri kaynağı tahmini için uygulanıyor. Merhaba aşağıdaki biz hello test kümesinin birkaç satırları kaydetmek ve ayıklamak ve hello tahmin komut dosyasında bu örnek hello sütun bilgileri kullanın:

```
# save hello model and a sample of hello test dataset 

logmsg('save serialized version of hello model and a sample of hello test data')
rxSetComputeContext('localpar') 
saveRDS(logitModel, file = "logitModel.rds")
testDF <- head(testDS, 1000)  
saveRDS(testDF    , file = "testDF.rds"    )
list.files()

rxHadoopListFiles(file.path(inputDataDir,''))
rxHadoopListFiles(dataDir)

# stop hello spark engine 
rxStopEngine(sparkCC) 

logmsg('Done.')
elapsed <- (proc.time() - t0)[3]
logmsg(paste('Elapsed time=',sprintf('%6.2f',elapsed),'(sec)\n\n'))
```

## <a name="summary"></a>Özet

Bu makalede, biz nasıl SparkR olası toocombine kullanım modeli geliştirme Hadoop Spark ScaleR ile veri işleme için olan gösterilen. Bu senaryo, bir kerede yalnızca bir oturum çalışan ayrı Spark oturumlar kullanan ve CSV dosyaları aracılığıyla veri değişimi gerektirir. SparkR ve ScaleR bir Spark oturumu paylaşabilir ve bu nedenle Spark DataFrames paylaşmak basit olsa da bu işlem yaklaşan bir R Server sürümde daha kolay olması gerekir.

## <a name="next-steps-and-more-information"></a>Sonraki adımlar ve daha fazla bilgi

- R Server Spark üzerinde kullanımı hakkında daha fazla bilgi için bkz: Merhaba [MSDN'de Başlarken Kılavuzu](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started)

- R Server hakkında genel bilgi için bkz: Merhaba [R ile çalışmaya başlama](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node) makalesi.

- Hdınsight'ta R Server hakkında daha fazla bilgi için bkz: [Azure Hdınsight genel bakış R Server'a](hdinsight-hadoop-r-server-overview.md) ve [Azure hdınsight'ta R Server](hdinsight-hadoop-r-server-get-started.md).

SparkR kullanımı hakkında daha fazla bilgi için bkz:

- [Apache SparkR belge](https://spark.apache.org/docs/2.1.0/sparkr.html)

- [SparkR genel bakış](https://docs.databricks.com/spark/latest/sparkr/overview.html) Databricks gelen
