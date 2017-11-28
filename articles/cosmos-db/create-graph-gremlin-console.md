---
title: "Azure Cosmos DB öğreticisi: Apache TinkerPop tarafından kullanıma sunulan Gremlin Console'da oluşturma, sorgulama ve çapraz geçiş yapma | Microsoft Docs"
description: "Bir Azure Cosmos DB hızlı başlangıç toocreates köşeleri, kenarları ve hello Azure Cosmos DB grafik API'sini kullanarak sorgular."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="da5c3-103">Azure Cosmos DB: oluşturma, sorgu ve bir grafik hello Gremlin konsolunda geçiş</span><span class="sxs-lookup"><span data-stu-id="da5c3-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="da5c3-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="da5c3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="da5c3-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da5c3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="da5c3-106">Bu hızlı başlangıç Azure portal'ı ve ardından kullanımı hello toocreate bir Azure Cosmos DB hesap, veritabanı ve grafik (kapsayıcı) kullanarak nasıl hello gösteren [Gremlin konsol](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) gelen [Apache TinkerPop](http://tinkerpop.apache.org) toowork ile Grafik API'si (Önizleme) verileri.</span><span class="sxs-lookup"><span data-stu-id="da5c3-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="da5c3-107">Bu öğreticide oluşturun ve köşeleri sorgu ve köşe özelliği güncelleniyor kenarlar köşeleri sorgu, hello grafik çapraz geçiş ve bir köşe bırakın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![Merhaba Apache Gremlin konsolundan Azure Cosmos DB](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="da5c3-109">Merhaba Gremlin Groovy/Java tabanlı ve Linux, Mac ve Windows çalıştıran konsoludur.</span><span class="sxs-lookup"><span data-stu-id="da5c3-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="da5c3-110">Hello karşıdan [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="da5c3-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da5c3-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="da5c3-111">Prerequisites</span></span>

<span data-ttu-id="da5c3-112">Bu Hızlı Başlangıç için toohave bir Azure aboneliği toocreate Azure Cosmos DB hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="da5c3-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="da5c3-113">Tooinstall hello etmeniz [Gremlin konsol](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="da5c3-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="da5c3-114">3.2.5 veya daha yüksek bir sürüm kullanın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="da5c3-115">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="da5c3-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="da5c3-116">Grafik ekleme</span><span class="sxs-lookup"><span data-stu-id="da5c3-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="da5c3-117"><a id="ConnectAppService"></a>Tooyour app service bağlanma</span><span class="sxs-lookup"><span data-stu-id="da5c3-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="da5c3-118">Merhaba Gremlin Konsolu'nu başlatmadan önce oluşturun veya hello apache-tinkerpop-gremlin-console-3.2.5/conf dizinindeki hello uzaktan secure.yaml yapılandırma dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="da5c3-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="da5c3-119">*ana bilgisayar*, *bağlantı noktası*, *kullanıcı adı*, *parola*, *bağlantı havuzu* ve *serileştirici* değerlerini girin:</span><span class="sxs-lookup"><span data-stu-id="da5c3-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="da5c3-120">Ayar</span><span class="sxs-lookup"><span data-stu-id="da5c3-120">Setting</span></span>|<span data-ttu-id="da5c3-121">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="da5c3-121">Suggested value</span></span>|<span data-ttu-id="da5c3-122">Açıklama</span><span class="sxs-lookup"><span data-stu-id="da5c3-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="da5c3-123">hosts</span><span class="sxs-lookup"><span data-stu-id="da5c3-123">hosts</span></span>|<span data-ttu-id="da5c3-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="da5c3-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="da5c3-125">Aşağıdaki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-125">See screenshot below.</span></span> <span data-ttu-id="da5c3-126">Merhaba Gremlin URI değeri hello hello sondaki ile köşeli ayraçlar içinde Azure Portalı'nın hello genel bakış sayfasında budur: 443 / kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="da5c3-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="da5c3-127">Bu değer ayrıca hello anahtarları sekmesinden, https:// kaldırma belgeleri toographs değiştirme ve hello sondaki kaldırma hello URI değeri kullanılarak alınabilir: 443 /.</span><span class="sxs-lookup"><span data-stu-id="da5c3-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="da5c3-128">port</span><span class="sxs-lookup"><span data-stu-id="da5c3-128">port</span></span>|<span data-ttu-id="da5c3-129">443</span><span class="sxs-lookup"><span data-stu-id="da5c3-129">443</span></span>|<span data-ttu-id="da5c3-130">Too443 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-130">Set too443.</span></span>
    <span data-ttu-id="da5c3-131">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="da5c3-131">username</span></span>|<span data-ttu-id="da5c3-132">*Kullanıcı adınız*</span><span class="sxs-lookup"><span data-stu-id="da5c3-132">*Your username*</span></span>|<span data-ttu-id="da5c3-133">Merhaba hello formunun kaynak `/dbs/<db>/colls/<coll>` nerede `<db>` veritabanı adınız ve `<coll>` koleksiyon adı.</span><span class="sxs-lookup"><span data-stu-id="da5c3-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="da5c3-134">password</span><span class="sxs-lookup"><span data-stu-id="da5c3-134">password</span></span>|<span data-ttu-id="da5c3-135">*Birincil anahtarınız*</span><span class="sxs-lookup"><span data-stu-id="da5c3-135">*Your primary key*</span></span>| <span data-ttu-id="da5c3-136">Aşağıdaki ikinci ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-136">See second screenshot below.</span></span> <span data-ttu-id="da5c3-137">Merhaba anahtarları sayfasından hello hello birincil anahtar kutusunda Azure portal alabilir, birincil anahtar budur.</span><span class="sxs-lookup"><span data-stu-id="da5c3-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="da5c3-138">Merhaba Kopyala düğmesini hello sol tarafında hello kutusu toocopy hello değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="da5c3-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="da5c3-139">connectionPool</span></span>|<span data-ttu-id="da5c3-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="da5c3-140">{enableSsl: true}</span></span>|<span data-ttu-id="da5c3-141">SSL için bağlantı havuzu ayarınız.</span><span class="sxs-lookup"><span data-stu-id="da5c3-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="da5c3-142">serializer</span><span class="sxs-lookup"><span data-stu-id="da5c3-142">serializer</span></span>|<span data-ttu-id="da5c3-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="da5c3-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="da5c3-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="da5c3-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="da5c3-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="da5c3-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="da5c3-146">Toothis değeri ayarlayın ve silmek `\n` hello değerinde yapıştırılırken satır sonlarında.</span><span class="sxs-lookup"><span data-stu-id="da5c3-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="da5c3-147">Merhaba Hello konakları değerini kopyalayın **Gremlin URI** başlangıç değerinden **genel bakış** sayfa: ![hello Azure portal'hello genel bakış sayfasında görüntüleme ve kopyalama hello Gremlin URI değeri](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="da5c3-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="da5c3-148">Merhaba Hello parola değerini kopyalayın **birincil anahtar** hello gelen **anahtarları** sayfa: ![görüntüleme ve kopyalama birincil anahtarınızı hello Azure portal, anahtarları sayfası](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="da5c3-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="da5c3-149">Terminalinizde Çalıştır `bin/gremlin.bat` veya `bin/gremlin.sh` toostart hello [Gremlin konsol](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="da5c3-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="da5c3-150">Terminalinizde Çalıştır `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="da5c3-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="da5c3-151">Merhaba hata alırsanız `No appenders could be found for logger` 2. adımda açıklandığı gibi hello uzaktan secure.yaml dosyasındaki hello seri hale getirici değer güncelleştirilmiş emin olun.</span><span class="sxs-lookup"><span data-stu-id="da5c3-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="da5c3-152">Harika!</span><span class="sxs-lookup"><span data-stu-id="da5c3-152">Great!</span></span> <span data-ttu-id="da5c3-153">Biz hello Kurulumu tamamladığımıza göre bazı Konsolu komutları çalıştıran başlayalım.</span><span class="sxs-lookup"><span data-stu-id="da5c3-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="da5c3-154">Basit bir count() komutunu deneyelim.</span><span class="sxs-lookup"><span data-stu-id="da5c3-154">Let's try a simple count() command.</span></span> <span data-ttu-id="da5c3-155">Merhaba konsoluna hello isteminde Hello aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="da5c3-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="da5c3-156">Bildirim hello `:>` hello önündeki `g.V().count()` metin?</span><span class="sxs-lookup"><span data-stu-id="da5c3-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="da5c3-157">Bu hello komuta tootype ihtiyacınız bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="da5c3-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="da5c3-158">Merhaba Gremlin konsolu, Azure Cosmos DB ile kullanıldığında önemlidir.</span><span class="sxs-lookup"><span data-stu-id="da5c3-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="da5c3-159">Bu atlama `:>` önek bildirir hello konsol tooexecute hello komutu yerel olarak genellikle bir bellek içi grafik karşı.</span><span class="sxs-lookup"><span data-stu-id="da5c3-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="da5c3-160">Bu kullanarak `:>` hello konsol tooexecute uzak komutu bu durumda Cosmos DB karşı söyler (ya da hello localhost öykünücü veya bir > Azure örneği).</span><span class="sxs-lookup"><span data-stu-id="da5c3-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="da5c3-161">Köşe ve kenar oluşturma</span><span class="sxs-lookup"><span data-stu-id="da5c3-161">Create vertices and edges</span></span>

<span data-ttu-id="da5c3-162">İlk olarak *Thomas*, *Mary Kay*, *Robin*, *Ben* ve *Jack* için beş kişi köşesi ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="da5c3-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="da5c3-163">Giriş (Thomas):</span><span class="sxs-lookup"><span data-stu-id="da5c3-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="da5c3-164">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="da5c3-165">Giriş (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="da5c3-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="da5c3-166">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="da5c3-167">Giriş (Robin):</span><span class="sxs-lookup"><span data-stu-id="da5c3-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="da5c3-168">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="da5c3-169">Giriş (Ben):</span><span class="sxs-lookup"><span data-stu-id="da5c3-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="da5c3-170">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="da5c3-171">Giriş (Jack):</span><span class="sxs-lookup"><span data-stu-id="da5c3-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="da5c3-172">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="da5c3-173">Ardından, kişilerimiz arasındaki ilişkiler için kenarlar ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="da5c3-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="da5c3-174">Giriş (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="da5c3-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="da5c3-175">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="da5c3-176">Giriş (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="da5c3-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="da5c3-177">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="da5c3-178">Giriş (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="da5c3-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="da5c3-179">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="da5c3-180">Köşe güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="da5c3-180">Update a vertex</span></span>

<span data-ttu-id="da5c3-181">Şimdi hello güncelleştirme *Thomas* köşe yeni yaşını ile *45*.</span><span class="sxs-lookup"><span data-stu-id="da5c3-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="da5c3-182">Giriş:</span><span class="sxs-lookup"><span data-stu-id="da5c3-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="da5c3-183">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="da5c3-184">Grafiğinizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="da5c3-184">Query your graph</span></span>

<span data-ttu-id="da5c3-185">Şimdi de grafiğinize karşı çeşitli sorgular çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="da5c3-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="da5c3-186">İlk olarak, bir sorgu kişilerle eski 40 yıldan daha eski bir filtre tooreturn yalnızca deneyelim.</span><span class="sxs-lookup"><span data-stu-id="da5c3-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="da5c3-187">Giriş (filtre sorgusu):</span><span class="sxs-lookup"><span data-stu-id="da5c3-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="da5c3-188">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="da5c3-189">Daha sonra şirketinizdeki eski 40 yıldan daha eski hello kişiler için hello ad proje.</span><span class="sxs-lookup"><span data-stu-id="da5c3-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="da5c3-190">Giriş (filtre + planlama sorgusu):</span><span class="sxs-lookup"><span data-stu-id="da5c3-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="da5c3-191">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="da5c3-192">Grafiğinizi çapraz geçirme</span><span class="sxs-lookup"><span data-stu-id="da5c3-192">Traverse your graph</span></span>

<span data-ttu-id="da5c3-193">Şimdi hello grafik tooreturn çapraz tüm Thomas'ın arkadaş.</span><span class="sxs-lookup"><span data-stu-id="da5c3-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="da5c3-194">Giriş (Thomas’ın arkadaşları):</span><span class="sxs-lookup"><span data-stu-id="da5c3-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="da5c3-195">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="da5c3-196">Ardından, şimdi hello sonraki katmanı köşeleri, alın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="da5c3-197">Hello grafik tooreturn Thomas'ın arkadaş tüm hello arkadaş çapraz geçiş yapamaz.</span><span class="sxs-lookup"><span data-stu-id="da5c3-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="da5c3-198">Giriş (Thomas’ın arkadaşlarının arkadaşları):</span><span class="sxs-lookup"><span data-stu-id="da5c3-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="da5c3-199">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="da5c3-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="da5c3-200">Köşe bırakma</span><span class="sxs-lookup"><span data-stu-id="da5c3-200">Drop a vertex</span></span>

<span data-ttu-id="da5c3-201">Şimdi şimdi bir köşe hello grafik veritabanından silin.</span><span class="sxs-lookup"><span data-stu-id="da5c3-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="da5c3-202">Giriş (Jack köşesini bırakın):</span><span class="sxs-lookup"><span data-stu-id="da5c3-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="da5c3-203">Grafiğinizi temizleme</span><span class="sxs-lookup"><span data-stu-id="da5c3-203">Clear your graph</span></span>

<span data-ttu-id="da5c3-204">Son olarak, tüm köşeleri ve kenarları hello veritabanı şimdi temizleyin.</span><span class="sxs-lookup"><span data-stu-id="da5c3-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="da5c3-205">Giriş:</span><span class="sxs-lookup"><span data-stu-id="da5c3-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="da5c3-206">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="da5c3-206">Congratulations!</span></span> <span data-ttu-id="da5c3-207">Bu Azure Cosmos DB: Grafik API’si öğreticisini tamamladınız!</span><span class="sxs-lookup"><span data-stu-id="da5c3-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="da5c3-208">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="da5c3-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="da5c3-209">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="da5c3-209">Clean up resources</span></span>

<span data-ttu-id="da5c3-210">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="da5c3-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="da5c3-211">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="da5c3-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="da5c3-212">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="da5c3-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da5c3-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da5c3-213">Next steps</span></span>

<span data-ttu-id="da5c3-214">Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir grafik oluşturmak, köşe ve kenarları oluşturun ve hello Gremlin konsolunu kullanarak, grafik çapraz öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="da5c3-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="da5c3-215">Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da5c3-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="da5c3-216">Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="da5c3-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
