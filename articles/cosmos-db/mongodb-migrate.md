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
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="290b3-104">Azure Cosmos DB: Alma MongoDB veri</span><span class="sxs-lookup"><span data-stu-id="290b3-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="290b3-105">MongoDB tooan Azure Cosmos DB hesabı ile kullanılmak üzere hello API MongoDB için toomigrate verileri, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="290b3-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="290b3-106">Ya da indirme *mongoimport.exe* veya *mongorestore.exe* hello gelen [MongoDB Yükleme Merkezi'nden](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="290b3-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="290b3-107">Al, [API MongoDB bağlantı dizesi için](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="290b3-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="290b3-108">Veri içe aktarıyorsanız MongoDB ve planı toouse ile Merhaba Azure Cosmos DB, hello kullanması gereken [veri geçiş aracı](import-data.md) tooimport veri.</span><span class="sxs-lookup"><span data-stu-id="290b3-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="290b3-109">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="290b3-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="290b3-110">Bağlantı dizesi alınıyor</span><span class="sxs-lookup"><span data-stu-id="290b3-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="290b3-111">Mongoimport kullanarak MongoDB veri alma</span><span class="sxs-lookup"><span data-stu-id="290b3-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="290b3-112">Mongorestore kullanarak MongoDB veri alma</span><span class="sxs-lookup"><span data-stu-id="290b3-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="290b3-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="290b3-113">Prerequisites</span></span>

* <span data-ttu-id="290b3-114">Verimliliğini artırmak: hello ayarladığınız Koleksiyonlarınız için işleme miktarı veri geçişinizi hello süresi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="290b3-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="290b3-115">Büyük veri geçişler için emin tooincrease hello işleme olabilir.</span><span class="sxs-lookup"><span data-stu-id="290b3-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="290b3-116">Merhaba geçişi tamamladıktan sonra hello verimlilik toosave maliyetleri azaltmak.</span><span class="sxs-lookup"><span data-stu-id="290b3-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="290b3-117">Merhaba performansı artırma hakkında daha fazla bilgi için [Azure portal](https://portal.azure.com), bkz: [performans düzeyleri ve Azure Cosmos veritabanı fiyatlandırma katmanlarına](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="290b3-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="290b3-118">SSL'yi etkinleştirin: Azure Cosmos DB sıkı güvenlik gereksinimlerine ve standartları vardır.</span><span class="sxs-lookup"><span data-stu-id="290b3-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="290b3-119">Hesabınız ile etkileşim emin tooenable SSL olabilir.</span><span class="sxs-lookup"><span data-stu-id="290b3-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="290b3-120">Merhaba makalenin devamında, hello Hello yordamlarda dahil nasıl tooenable SSL mongoimport ve mongorestore.</span><span class="sxs-lookup"><span data-stu-id="290b3-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="290b3-121">(Konak, bağlantı noktası, kullanıcı adı ve parola) bağlantı dizesi bilgilerinizi Bul</span><span class="sxs-lookup"><span data-stu-id="290b3-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="290b3-122">Merhaba, [Azure portal](https://portal.azure.com), buna hello sol bölmesinde, hello tıklatın **Azure Cosmos DB** girişi.</span><span class="sxs-lookup"><span data-stu-id="290b3-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="290b3-123">Merhaba, **abonelikleri** bölmesinde, hesabınızın adını seçin.</span><span class="sxs-lookup"><span data-stu-id="290b3-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="290b3-124">Merhaba, **bağlantı dizesi** dikey penceresinde tıklatın **bağlantı dizesi**.</span><span class="sxs-lookup"><span data-stu-id="290b3-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="290b3-125">Hello bölmesini toosuccessfully gereken tüm hello bilgileri içermektedir sağ tooyour hesabı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="290b3-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Bağlantı dizesi dikey penceresi](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="290b3-127">Mongoimport kullanarak veri toohello API MongoDB için içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="290b3-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="290b3-128">tooimport veri tooyour Azure Cosmos DB hesap şablonu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="290b3-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="290b3-129">Doldurmak *konak*, *kullanıcıadı*, ve *parola* belirli tooyour hesabı hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="290b3-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="290b3-130">Şablonu:</span><span class="sxs-lookup"><span data-stu-id="290b3-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="290b3-131">Örnek:</span><span class="sxs-lookup"><span data-stu-id="290b3-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="290b3-132">Mongorestore kullanarak veri toohello API MongoDB için içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="290b3-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="290b3-133">toorestore veri tooyour API MongoDB hesabı için şablonu tooexecute hello alma aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="290b3-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="290b3-134">Doldurmak *konak*, *kullanıcıadı*, ve *parola* belirli tooyour hesabı hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="290b3-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="290b3-135">Şablonu:</span><span class="sxs-lookup"><span data-stu-id="290b3-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="290b3-136">Örnek:</span><span class="sxs-lookup"><span data-stu-id="290b3-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="290b3-137">Başarılı bir geçiş Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="290b3-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="290b3-138">Önceden oluşturma ve koleksiyonlarınızı ölçeği:</span><span class="sxs-lookup"><span data-stu-id="290b3-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="290b3-139">Varsayılan olarak, Azure Cosmos DB 1.000 istek birimleri (RUs) ile yeni bir MongoDB koleksiyon sağlar.</span><span class="sxs-lookup"><span data-stu-id="290b3-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="290b3-140">Mongoimport, mongorestore veya mongomirror kullanarak hello Geçişe başlamadan önce tüm hello koleksiyonlarından önceden oluştur [Azure portal](https://portal.azure.com) veya MongoDB sürücüleri ve araçları.</span><span class="sxs-lookup"><span data-stu-id="290b3-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="290b3-141">Koleksiyonunuz 10 GB'den büyükse emin toocreate olun bir [parçalı/bölümlenmiş koleksiyonu](partition-data.md) uygun parça anahtara sahip.</span><span class="sxs-lookup"><span data-stu-id="290b3-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="290b3-142">Merhaba gelen [Azure portal](https://portal.azure.com), tek bölümlü bir koleksiyon için 1.000 RUs ve hello geçiş için yalnızca parçalı bir koleksiyon için 2.500 RUs koleksiyonlarınızı verimliliğini artırmak.</span><span class="sxs-lookup"><span data-stu-id="290b3-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="290b3-143">Merhaba daha yüksek işleme ile azaltma önlemek ve daha kısa sürede geçirilir.</span><span class="sxs-lookup"><span data-stu-id="290b3-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="290b3-144">Azure Cosmos DB'de saatlik faturalandırma ile hemen hello geçiş toosave maliyetlerini sonra hello verimlilik azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="290b3-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="290b3-145">Tek belge yazmak için yaklaşık RU ücret Hello Hesapla:</span><span class="sxs-lookup"><span data-stu-id="290b3-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="290b3-146">a.</span><span class="sxs-lookup"><span data-stu-id="290b3-146">a.</span></span> <span data-ttu-id="290b3-147">Tooyour Azure Cosmos DB MongoDB veritabanı MongoDB Kabuk hello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="290b3-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="290b3-148">' Ndaki yönergeleri bulabilirsiniz [MongoDB uygulama tooAzure Cosmos DB bağlanmak](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="290b3-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="290b3-149">b.</span><span class="sxs-lookup"><span data-stu-id="290b3-149">b.</span></span> <span data-ttu-id="290b3-150">Örnek belgelerinizi hello MongoDB Kabuk birini kullanarak bir örnek INSERT komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="290b3-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="290b3-151">c.</span><span class="sxs-lookup"><span data-stu-id="290b3-151">c.</span></span> <span data-ttu-id="290b3-152">Çalıştırma ```db.runCommand({getLastRequestStatistics: 1})``` ve bunun gibi bir yanıtı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="290b3-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="290b3-153">d.</span><span class="sxs-lookup"><span data-stu-id="290b3-153">d.</span></span> <span data-ttu-id="290b3-154">Merhaba isteği ücret not edin.</span><span class="sxs-lookup"><span data-stu-id="290b3-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="290b3-155">Merhaba gecikme, makine toohello Azure Cosmos DB bulut hizmeti gelen belirleyin:</span><span class="sxs-lookup"><span data-stu-id="290b3-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="290b3-156">a.</span><span class="sxs-lookup"><span data-stu-id="290b3-156">a.</span></span> <span data-ttu-id="290b3-157">Bu komutu kullanarak hello MongoDB Kabuğu'ndan ayrıntılı günlük kaydını etkinleştir:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="290b3-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="290b3-158">b.</span><span class="sxs-lookup"><span data-stu-id="290b3-158">b.</span></span> <span data-ttu-id="290b3-159">Merhaba veritabanına karşı basit bir sorgu çalıştırın: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="290b3-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="290b3-160">Bunun gibi bir yanıtı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="290b3-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="290b3-161">Yinelenen belge yok hello geçiş tooensure önce eklenen hello belge kaldırın.</span><span class="sxs-lookup"><span data-stu-id="290b3-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="290b3-162">Bu komutu kullanarak belgeler kaldırabilirsiniz:```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="290b3-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="290b3-163">Merhaba yaklaşık hesaplamak *batchSize* ve *numInsertionWorkers* değerler:</span><span class="sxs-lookup"><span data-stu-id="290b3-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="290b3-164">İçin *batchSize*, bölme hello toplam RUs adım 3'te, tek bir belge yazma gelen tüketilen hello RUs tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="290b3-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="290b3-165">Merhaba hesaplanıyorsa *batchSize* < = 24, bu sayı olarak kullanmak, *batchSize* değeri.</span><span class="sxs-lookup"><span data-stu-id="290b3-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="290b3-166">Merhaba hesaplanıyorsa *batchSize* > 24, kümesi hello *batchSize* değeri too24.</span><span class="sxs-lookup"><span data-stu-id="290b3-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="290b3-167">İçin *numInsertionWorkers*, bu denklemi kullanın: *numInsertionWorkers = (sağlanan işleme * gecikme süresini saniye cinsinden) / (yığın boyutu * RUs için tek bir yazma tüketilen)*.</span><span class="sxs-lookup"><span data-stu-id="290b3-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="290b3-168">Özellik</span><span class="sxs-lookup"><span data-stu-id="290b3-168">Property</span></span>|<span data-ttu-id="290b3-169">Değer</span><span class="sxs-lookup"><span data-stu-id="290b3-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="290b3-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="290b3-170">batchSize</span></span>| <span data-ttu-id="290b3-171">24</span><span class="sxs-lookup"><span data-stu-id="290b3-171">24</span></span> |
    |<span data-ttu-id="290b3-172">Sağlanan RUs</span><span class="sxs-lookup"><span data-stu-id="290b3-172">RUs provisioned</span></span> | <span data-ttu-id="290b3-173">10000</span><span class="sxs-lookup"><span data-stu-id="290b3-173">10000</span></span> |
    |<span data-ttu-id="290b3-174">Gecikme süresi</span><span class="sxs-lookup"><span data-stu-id="290b3-174">Latency</span></span> | <span data-ttu-id="290b3-175">0.100 s</span><span class="sxs-lookup"><span data-stu-id="290b3-175">0.100 s</span></span> |
    |<span data-ttu-id="290b3-176">RU 1 belge yazmak için sizden ücret</span><span class="sxs-lookup"><span data-stu-id="290b3-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="290b3-177">10 RUs</span><span class="sxs-lookup"><span data-stu-id="290b3-177">10 RUs</span></span> |
    |<span data-ttu-id="290b3-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="290b3-178">numInsertionWorkers</span></span> | <span data-ttu-id="290b3-179">?</span><span class="sxs-lookup"><span data-stu-id="290b3-179">?</span></span> |
    
    <span data-ttu-id="290b3-180">*numInsertionWorkers = (0,1 x 10000 RUs s) / (24 x 10 RUs) 4.1666 =*</span><span class="sxs-lookup"><span data-stu-id="290b3-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="290b3-181">Merhaba son geçiş komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="290b3-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="290b3-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="290b3-182">Next steps</span></span>

<span data-ttu-id="290b3-183">Toohello sonraki öğretici devam etmek ve bilgi nasıl tooquery Azure Cosmos DB kullanarak MongoDB veri.</span><span class="sxs-lookup"><span data-stu-id="290b3-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="290b3-184">Nasıl tooquery MongoDB veri?</span><span class="sxs-lookup"><span data-stu-id="290b3-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
