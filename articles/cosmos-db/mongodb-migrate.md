---
title: "aaaUse mongoimport ve mongorestore ile hello Azure Cosmos DB API MongoDB için | Microsoft Docs"
description: "Bilgi nasıl toouse mongoimport ve mongorestore tooimport veri tooan API MongoDB hesabı"
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: Alma MongoDB veri 

MongoDB tooan Azure Cosmos DB hesabı ile kullanılmak üzere hello API MongoDB için toomigrate verileri, aşağıdakileri yapmalısınız:

* Ya da indirme *mongoimport.exe* veya *mongorestore.exe* hello gelen [MongoDB Yükleme Merkezi'nden](https://www.mongodb.com/download-center).
* Al, [API MongoDB bağlantı dizesi için](connect-mongodb-account.md).

Veri içe aktarıyorsanız MongoDB ve planı toouse ile Merhaba Azure Cosmos DB, hello kullanması gereken [veri geçiş aracı](import-data.md) tooimport veri.

Bu öğretici hello aşağıdaki görevleri içerir:

> [!div class="checklist"]
> * Bağlantı dizesi alınıyor
> * Mongoimport kullanarak MongoDB veri alma
> * Mongorestore kullanarak MongoDB veri alma

## <a name="prerequisites"></a>Ön koşullar

* Verimliliğini artırmak: hello ayarladığınız Koleksiyonlarınız için işleme miktarı veri geçişinizi hello süresi bağlıdır. Büyük veri geçişler için emin tooincrease hello işleme olabilir. Merhaba geçişi tamamladıktan sonra hello verimlilik toosave maliyetleri azaltmak. Merhaba performansı artırma hakkında daha fazla bilgi için [Azure portal](https://portal.azure.com), bkz: [performans düzeyleri ve Azure Cosmos veritabanı fiyatlandırma katmanlarına](performance-levels.md).

* SSL'yi etkinleştirin: Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartları vardır. Hesabınız ile etkileşim emin tooenable SSL olabilir. Merhaba makalenin devamında, hello Hello yordamlarda dahil nasıl tooenable SSL mongoimport ve mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>(Konak, bağlantı noktası, kullanıcı adı ve parola) bağlantı dizesi bilgilerinizi Bul

1. Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Cosmos DB** girişi.
2. Merhaba, **abonelikleri** bölmesinde, hesabınızın adını seçin.
3. Merhaba, **bağlantı dizesi** dikey penceresinde tıklatın **bağlantı dizesi**.  
Hello bölmesini toosuccessfully gereken tüm hello bilgileri içermektedir sağ tooyour hesabı bağlayın.

    ![Bağlantı dizesi dikey penceresi](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Mongoimport kullanarak veri toohello API MongoDB için içeri aktarma

tooimport veri tooyour Azure Cosmos DB hesap şablonu aşağıdaki hello kullanın. Doldurmak *konak*, *kullanıcıadı*, ve *parola* belirli tooyour hesabı hello değerlere sahip.  

Şablonu:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Örnek:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Mongorestore kullanarak veri toohello API MongoDB için içeri aktarma

toorestore veri tooyour API MongoDB hesabı için şablonu tooexecute hello alma aşağıdaki hello kullanın. Doldurmak *konak*, *kullanıcıadı*, ve *parola* belirli tooyour hesabı hello değerlere sahip.

Şablonu:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Örnek:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Başarılı bir geçiş Kılavuzu

1. Önceden oluşturma ve koleksiyonlarınızı ölçeği:
        
    * Varsayılan olarak, Azure Cosmos DB 1.000 istek birimleri (RUs) ile yeni bir MongoDB koleksiyon sağlar. Mongoimport, mongorestore veya mongomirror kullanarak hello Geçişe başlamadan önce tüm hello koleksiyonlarından önceden oluştur [Azure portal](https://portal.azure.com) veya MongoDB sürücüleri ve araçları. Koleksiyonunuz 10 GB'den büyükse emin toocreate olun bir [parçalı/bölümlenmiş koleksiyonu](partition-data.md) uygun parça anahtara sahip.

    * Merhaba gelen [Azure portal](https://portal.azure.com), tek bölümlü bir koleksiyon için 1.000 RUs ve hello geçiş için yalnızca parçalı bir koleksiyon için 2.500 RUs koleksiyonlarınızı verimliliğini artırmak. Merhaba daha yüksek işleme ile azaltma önlemek ve daha kısa sürede geçirilir. Azure Cosmos DB'de saatlik faturalandırma ile hemen hello geçiş toosave maliyetlerini sonra hello verimlilik azaltabilir.

2. Tek belge yazmak için yaklaşık RU ücret Hello Hesapla:

    a. Tooyour Azure Cosmos DB MongoDB veritabanı MongoDB Kabuk hello bağlayın. ' Ndaki yönergeleri bulabilirsiniz [MongoDB uygulama tooAzure Cosmos DB bağlanmak](connect-mongodb-account.md).
    
    b. Örnek belgelerinizi hello MongoDB Kabuk birini kullanarak bir örnek INSERT komutu çalıştırın:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Çalıştırma ```db.runCommand({getLastRequestStatistics: 1})``` ve bunun gibi bir yanıtı alırsınız:
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    d. Merhaba isteği ücret not edin.
    
3. Merhaba gecikme, makine toohello Azure Cosmos DB bulut hizmeti gelen belirleyin:
    
    a. Bu komutu kullanarak hello MongoDB Kabuğu'ndan ayrıntılı günlük kaydını etkinleştir:```setVerboseShell(true)```
    
    b. Merhaba veritabanına karşı basit bir sorgu çalıştırın: ```db.coll.find().limit(1)```. Bunun gibi bir yanıtı alırsınız:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Yinelenen belge yok hello geçiş tooensure önce eklenen hello belge kaldırın. Bu komutu kullanarak belgeler kaldırabilirsiniz:```db.coll.remove({})```

5. Merhaba yaklaşık hesaplamak *batchSize* ve *numInsertionWorkers* değerler:

    * İçin *batchSize*, bölme hello toplam RUs adım 3'te, tek bir belge yazma gelen tüketilen hello RUs tarafından sağlanan.
    
    * Merhaba hesaplanıyorsa *batchSize* < = 24, bu sayı olarak kullanmak, *batchSize* değeri.
    
    * Merhaba hesaplanıyorsa *batchSize* > 24, kümesi hello *batchSize* değeri too24.
    
    * İçin *numInsertionWorkers*, bu denklemi kullanın: *numInsertionWorkers = (sağlanan işleme * gecikme süresini saniye cinsinden) / (yığın boyutu * RUs için tek bir yazma tüketilen)*.
        
    |Özellik|Değer|
    |--------|-----|
    |batchSize| 24 |
    |Sağlanan RUs | 10000 |
    |Gecikme süresi | 0.100 s |
    |RU 1 belge yazmak için sizden ücret | 10 RUs |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (0,1 x 10000 RUs s) / (24 x 10 RUs) 4.1666 =*

6. Merhaba son geçiş komutu çalıştırın:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Sonraki adımlar

Toohello sonraki öğretici devam etmek ve bilgi nasıl tooquery Azure Cosmos DB kullanarak MongoDB veri. 

> [!div class="nextstepaction"]
>[Nasıl tooquery MongoDB veri?](../cosmos-db/tutorial-query-mongodb.md)
