---
title: "Java ile Azure Cosmos DB grafik veritabanı oluşturma | Microsoft Docs | Microsoft Docs'"
description: "Gremlin kullanarak Azure Cosmos DB'ye bağlanmak ve içindeki grafik verilerini sorgulamak için kullanabileceğiniz bir Java kodu örneği sunar."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 0273072c7c10e219ab8d6c85eb252badafc17147
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-the-azure-portal"></a><span data-ttu-id="ac8fb-103">Azure Cosmos DB: Java ve Azure portalını kullanarak bir grafik veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac8fb-103">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>

<span data-ttu-id="ac8fb-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ac8fb-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ac8fb-106">Bu hızlı başlangıç Azure Cosmos DB için Azure portal araçlarını kullanarak bir grafik veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-106">This quickstart creates a graph database using the Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="ac8fb-107">Bu hızlı başlangıçta ayrıca bir Java konsol uygulamasını [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) sürücüsü kullanan bir grafik veritabanını kullanarak nasıl hızlı bir şekilde oluşturabileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-107">This quickstart also shows you how to quickly create a Java console app using a graph database using the OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="ac8fb-108">Bu hızlı başlangıçtaki yönergeler Java çalıştırabilen tüm işletim sistemlerinde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-108">The instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="ac8fb-109">Bu hızlı başlangıcı tamamladığınızda tercihinize bağlı olarak Kullanıcı Arabiriminde veya programlama arabiriminde grafik kaynaklarını oluşturma ve değiştirme hakkında bilgi sahibi olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-109">This quickstart familiarizes you with creating and modifying graph resources in either the UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ac8fb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-110">Prerequisites</span></span>

* [<span data-ttu-id="ac8fb-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="ac8fb-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="ac8fb-112">Ubuntu’da JDK’yi yüklemek için `apt-get install default-jdk` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-112">On Ubuntu, run `apt-get install default-jdk` to install the JDK.</span></span>
    * <span data-ttu-id="ac8fb-113">JAVA_HOME ortam değişkenini JDK’nin yüklü olduğu klasöre işaret edecek şekilde ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-113">Be sure to set the JAVA_HOME environment variable to point to the folder where the JDK is installed.</span></span>
* <span data-ttu-id="ac8fb-114">Bir [Maven](http://maven.apache.org/) ikili arşivi [indirin](http://maven.apache.org/download.cgi) ve [yükleyin](http://maven.apache.org/install.html)</span><span class="sxs-lookup"><span data-stu-id="ac8fb-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="ac8fb-115">Ubuntu’da Maven’i yüklemek için `apt-get install maven` komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-115">On Ubuntu, you can run `apt-get install maven` to install Maven.</span></span>
* [<span data-ttu-id="ac8fb-116">Git</span><span class="sxs-lookup"><span data-stu-id="ac8fb-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="ac8fb-117">Ubuntu’da Git’i yüklemek için `sudo apt-get install git` komutunu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-117">On Ubuntu, you can run `sudo apt-get install git` to install Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="ac8fb-118">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ac8fb-118">Create a database account</span></span>

<span data-ttu-id="ac8fb-119">Bir grafik veritabanı oluşturmadan önce Azure Cosmos DB ile bir Gremlin (Graf) veritabanı hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-119">Before you can create a graph database, you need to create a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="ac8fb-120">Grafik ekleme</span><span class="sxs-lookup"><span data-stu-id="ac8fb-120">Add a graph</span></span>

<span data-ttu-id="ac8fb-121">Şimdi bir grafik veritabanı oluşturmak için Azure portalında Veri Gezgini aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-121">You can now use the Data Explorer tool in the Azure portal to create a graph database.</span></span> 

1. <span data-ttu-id="ac8fb-122">Azure portalının solundaki gezinti menüsünde **Veri Gezgini (Önizleme)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-122">In the Azure portal, in the left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="ac8fb-123">**Veri Gezgini (Önizleme)** dikey penceresinde **Yeni Grafik**'e tıklayın ve aşağıdaki bilgileri kullanarak sayfayı doldurun:</span><span class="sxs-lookup"><span data-stu-id="ac8fb-123">In the **Data Explorer (Preview)** blade, click **New Graph**, then fill in the page using the following information:</span></span>

    ![Azure portalında Veri Gezgini](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="ac8fb-125">Ayar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-125">Setting</span></span>|<span data-ttu-id="ac8fb-126">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="ac8fb-126">Suggested value</span></span>|<span data-ttu-id="ac8fb-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ac8fb-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="ac8fb-128">Veritabanı Kimliği</span><span class="sxs-lookup"><span data-stu-id="ac8fb-128">Database ID</span></span>|<span data-ttu-id="ac8fb-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="ac8fb-129">sample-database</span></span>|<span data-ttu-id="ac8fb-130">Yeni veritabanınızın kimliği.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-130">The ID for your new database.</span></span> <span data-ttu-id="ac8fb-131">Veritabanı adı 1 ile 255 karakter arasında olmalı, `/ \ # ?` içermemeli ve boşlukla bitmemelidir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="ac8fb-132">Grafik Kimliği</span><span class="sxs-lookup"><span data-stu-id="ac8fb-132">Graph ID</span></span>|<span data-ttu-id="ac8fb-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="ac8fb-133">sample-graph</span></span>|<span data-ttu-id="ac8fb-134">Yeni grafiğinizin kimliği.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-134">The ID for your new graph.</span></span> <span data-ttu-id="ac8fb-135">Grafik adı karakter gereksinimleri, veritabanı kimliklerine ilişkin karakter gereksinimleri ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-135">Graph names have the same character requirements as database ids.</span></span>
    <span data-ttu-id="ac8fb-136">Depolama Kapasitesi</span><span class="sxs-lookup"><span data-stu-id="ac8fb-136">Storage Capacity</span></span>| <span data-ttu-id="ac8fb-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="ac8fb-137">10 GB</span></span>|<span data-ttu-id="ac8fb-138">Varsayılan değeri değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-138">Leave the default value.</span></span> <span data-ttu-id="ac8fb-139">Bu, veritabanının depolama kapasitesidir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-139">This is the storage capacity of the database.</span></span>
    <span data-ttu-id="ac8fb-140">Aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="ac8fb-140">Throughput</span></span>|<span data-ttu-id="ac8fb-141">400 RU</span><span class="sxs-lookup"><span data-stu-id="ac8fb-141">400 RUs</span></span>|<span data-ttu-id="ac8fb-142">Varsayılan değeri değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-142">Leave the default value.</span></span> <span data-ttu-id="ac8fb-143">Daha sonra gecikme süresini azaltmak isterseniz, aktarım hızının ölçeğini artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-143">You can scale up the throughput later if you want to reduce latency.</span></span>
    <span data-ttu-id="ac8fb-144">Bölüm anahtarı</span><span class="sxs-lookup"><span data-stu-id="ac8fb-144">Partition key</span></span>|<span data-ttu-id="ac8fb-145">Boş bırakın</span><span class="sxs-lookup"><span data-stu-id="ac8fb-145">Leave blank</span></span>|<span data-ttu-id="ac8fb-146">Bu hızlı başlangıç için bölüm anahtarını boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-146">For the purpose of this quickstart, leave the partition key blank.</span></span>

3. <span data-ttu-id="ac8fb-147">Formu doldurduktan sonra **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-147">Once the form is filled out, click **OK**.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="ac8fb-148">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="ac8fb-148">Clone the sample application</span></span>

<span data-ttu-id="ac8fb-149">Şimdi github'dan bir grafik uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-149">Now let's clone a graph app from github, set the connection string, and run it.</span></span> <span data-ttu-id="ac8fb-150">Verilerle programlı bir şekilde çalışmanın ne kadar kolay olduğunu görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-150">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="ac8fb-151">Git bash gibi bir git terminal penceresi açın ve `cd` ile çalışma dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-151">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="ac8fb-152">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-152">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-the-code"></a><span data-ttu-id="ac8fb-153">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="ac8fb-153">Review the code</span></span>

<span data-ttu-id="ac8fb-154">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-154">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="ac8fb-155">\src\GetStarted klasöründen `Program.java` dosyasını açın ve bu kod satırlarını bulun.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-155">Open the `Program.java` file from the \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="ac8fb-156">Gremlin `Client`, `src/remote.yaml` içinde bulunan yapılandırmadan başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-156">The Gremlin `Client` is initialized from the configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="ac8fb-157">Bir dizi Gremlin adımı `client.submit` yöntemi kullanılarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-157">A series of Gremlin steps are executed using the `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="ac8fb-158">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ac8fb-158">Update your connection string</span></span>

1. <span data-ttu-id="ac8fb-159">src/remote.yaml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-159">Open the src/remote.yaml file.</span></span> 

3. <span data-ttu-id="ac8fb-160">src/remote.yaml dosyasında *hosts*, *username* ve *password* değerlerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-160">Fill in your *hosts*, *username*, and *password* values in the src/remote.yaml file.</span></span> <span data-ttu-id="ac8fb-161">Ayarların geri kalanının değiştirilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-161">The rest of the settings do not need to be changed.</span></span>

    <span data-ttu-id="ac8fb-162">Ayar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-162">Setting</span></span>|<span data-ttu-id="ac8fb-163">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="ac8fb-163">Suggested value</span></span>|<span data-ttu-id="ac8fb-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ac8fb-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="ac8fb-165">Ana bilgisayarlar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-165">Hosts</span></span>|<span data-ttu-id="ac8fb-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="ac8fb-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="ac8fb-167">Bu tablodan sonraki ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-167">See the screenshot following this table.</span></span> <span data-ttu-id="ac8fb-168">Bu değer, Azure portalının Genel Bakış sayfasında bulunan, köşeli ayraç içindeki, sonundan :443/ bölümü çıkartılmış Gremlin URI değeridir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-168">This value is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="ac8fb-169">Bu değer, Anahtarlar sekmesinde bulunan URI değeri kullanılıp https:// bölümü çıkarılarak ve belgeleri grafiklere dönüştürüp sondaki :443/ bölümü çıkarılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-169">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="ac8fb-170">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ac8fb-170">Username</span></span>|<span data-ttu-id="ac8fb-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="ac8fb-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="ac8fb-172">`/dbs/<db>/colls/<coll>` formunun kaynağı; burada `<db>` mevcut veritabanı adınız ve `<coll>` mevcut koleksiyon adınızdır.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-172">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="ac8fb-173">Parola</span><span class="sxs-lookup"><span data-stu-id="ac8fb-173">Password</span></span>|<span data-ttu-id="ac8fb-174">*Birincil ana anahtarınız*</span><span class="sxs-lookup"><span data-stu-id="ac8fb-174">*Your primary master key*</span></span>|<span data-ttu-id="ac8fb-175">Bu tablodan sonraki ikinci ekran görüntüsüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-175">See the second screenshot following this table.</span></span> <span data-ttu-id="ac8fb-176">Bu değer sizin birincil anahtarınızdır, bu anahtarı Azure portalının Anahtarlar sayfasındaki Birincil Anahtar kutusunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-176">This value is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="ac8fb-177">Değeri kopyalamak için kutunun sağındaki kopyala düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-177">Copy the value using the copy button on the right side of the box.</span></span>

    <span data-ttu-id="ac8fb-178">Hosts değeri için **Genel Bakış** sayfasındaki **Gremlin URI** değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-178">For the Hosts value, copy the **Gremlin URI** value from the **Overview** page.</span></span> <span data-ttu-id="ac8fb-179">Boşsa, anahtarlar dikey penceresinden Gremlin URI’si oluşturma hakkındaki önceki tablonun Hosts satırındaki yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-179">If it's empty, see the instructions in the Hosts row in the preceding table about creating the Gremlin URI from the Keys blade.</span></span>
<span data-ttu-id="ac8fb-180">![Azure Portalı'ndaki Genel Bakış sayfasında Gremlin URI değerini görüntüleme ve kopyalama](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="ac8fb-180">![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="ac8fb-181">Parola değeri için, **Anahtarlar** dikey penceresindeki **Birincil Anahtar**’ı kopyalayın: ![Azure portalındaki Anahtarlar sayfasında bulunan birincil anahtarı görüntüleme ve kopyalama](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="ac8fb-181">For the Password value, copy the **Primary key** from the **Keys** blade: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-the-console-app"></a><span data-ttu-id="ac8fb-182">Konsol uygulamasını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ac8fb-182">Run the console app</span></span>

1. <span data-ttu-id="ac8fb-183">Git terminal penceresinde `cd` komutuyla azure-cosmos-db-graph-java-getting-started klasörüne ulaşın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-183">In the git terminal window, `cd` to the azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="ac8fb-184">Git terminal penceresinde `mvn package` yazarak gerekli Java paketlerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-184">In the git terminal window, type `mvn package` to install the required Java packages.</span></span>

3. <span data-ttu-id="ac8fb-185">Git terminal penceresinde Java uygulamanızı başlatmak için terminal penceresinde `mvn exec:java -D exec.mainClass=GetStarted.Program` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-185">In the git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in the terminal window to start your Java application.</span></span>

<span data-ttu-id="ac8fb-186">Terminal penceresinde grafiğe eklenmekte olan köşeler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-186">The terminal window displays the vertices being added to the graph.</span></span> <span data-ttu-id="ac8fb-187">Program tamamlandıktan sonra geri İnternet tarayıcınızdaki Azure Portalı'na geçin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-187">Once the program completes, switch back to the Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="ac8fb-188">Örnek verileri inceleme ve ekleme</span><span class="sxs-lookup"><span data-stu-id="ac8fb-188">Review and add sample data</span></span>

<span data-ttu-id="ac8fb-189">Şimdi Veri Gezgini’ne dönüp grafiğe eklenen köşeleri görebilir ve ek veri noktaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-189">You can now go back to Data Explorer and see the vertices added to the graph, and add additional data points.</span></span>

1. <span data-ttu-id="ac8fb-190">Veri Gezgini'nde **sample-database**/**sample-graph** seçeneğini genişletin, **Graf** ve ardından **Filtre Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-190">In Data Explorer, expand the **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Azure portalındaki Veri Gezgini'nde yeni belge oluşturma](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="ac8fb-192">**Sonuç listesinde**, grafiğe yeni kullanıcıların eklendiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-192">In the **Results** list, notice the new users added to the graph.</span></span> <span data-ttu-id="ac8fb-193">**Ben**’i seçin, robin ile bağlantılı olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-193">Select **ben** and notice that he's connected to robin.</span></span> <span data-ttu-id="ac8fb-194">Grafik gezgininde köşeleri taşıyabilir, yakınlaştırma ve uzaklaştırma yapabilir, grafik gezgininin yüzey boyutunu genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-194">You can move the vertices around on the graph explorer, zoom in and out, and expand the size of the graph explorer surface.</span></span> 

   ![Azure portalında Veri Gezgini'ndeki grafikte yeni köşeler](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="ac8fb-196">Veri Gezgini'ni kullanarak grafiğe birkaç yeni kullanıcı ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-196">Let's add a few new users to the graph using the Data Explorer.</span></span> <span data-ttu-id="ac8fb-197">Grafiğe veri eklemek için **yeni köşe** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-197">Click the **New Vertex** button to add data to your graph.</span></span>

   ![Azure portalındaki Veri Gezgini'nde yeni belge oluşturma](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="ac8fb-199">*kişi* etiketini girin ve ardından grafikte ilk köşeyi oluşturmak için aşağıdaki anahtarları ve değerleri girin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-199">Enter a label of *person* then enter the following keys and values to create the first vertex in the graph.</span></span> <span data-ttu-id="ac8fb-200">Grafikteki her kişi için benzersiz özellikler oluşturabileceğinizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="ac8fb-201">Yalnızca kimliği anahtarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-201">Only the id key is required.</span></span>

    <span data-ttu-id="ac8fb-202">anahtar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-202">key</span></span>|<span data-ttu-id="ac8fb-203">değer</span><span class="sxs-lookup"><span data-stu-id="ac8fb-203">value</span></span>|<span data-ttu-id="ac8fb-204">Notlar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="ac8fb-205">id</span><span class="sxs-lookup"><span data-stu-id="ac8fb-205">id</span></span>|<span data-ttu-id="ac8fb-206">ashley</span><span class="sxs-lookup"><span data-stu-id="ac8fb-206">ashley</span></span>|<span data-ttu-id="ac8fb-207">Köşe için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-207">The unique identifier for the vertex.</span></span> <span data-ttu-id="ac8fb-208">Kimlik belirtmezseniz, bir kimlik otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="ac8fb-209">cinsiyet</span><span class="sxs-lookup"><span data-stu-id="ac8fb-209">gender</span></span>|<span data-ttu-id="ac8fb-210">kadın</span><span class="sxs-lookup"><span data-stu-id="ac8fb-210">female</span></span>| 
    <span data-ttu-id="ac8fb-211">teknoloji</span><span class="sxs-lookup"><span data-stu-id="ac8fb-211">tech</span></span> | <span data-ttu-id="ac8fb-212">java</span><span class="sxs-lookup"><span data-stu-id="ac8fb-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="ac8fb-213">Bu hızlı başlangıçta bölümlenmemiş bir koleksiyon oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="ac8fb-214">Ancak koleksiyon oluşturma sırasında bir bölüm anahtarı belirterek bölümlendirilmiş bir koleksiyon oluşturursanız, daha sonra bölüm anahtarını her yeni köşede anahtar olarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-214">However, if you create a partitioned collection by specifying a partition key during the collection creation, then you need to include the partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="ac8fb-215">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-215">Click **OK**.</span></span> <span data-ttu-id="ac8fb-216">Ekranın en altındaki **Tamam** seçeneğini görmek için ekranınızı genişletmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-216">You may need to expand your screen to see **OK** on the bottom of the screen.</span></span>

6. <span data-ttu-id="ac8fb-217">Tekrar **Yeni Köşe**’ye tıklayın ve ek yeni kullanıcıyı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="ac8fb-218">*Kişi* etiketini ve ardından aşağıdaki anahtarları ve değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="ac8fb-218">Enter a label of *person* then enter the following keys and values:</span></span>

    <span data-ttu-id="ac8fb-219">anahtar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-219">key</span></span>|<span data-ttu-id="ac8fb-220">değer</span><span class="sxs-lookup"><span data-stu-id="ac8fb-220">value</span></span>|<span data-ttu-id="ac8fb-221">Notlar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="ac8fb-222">id</span><span class="sxs-lookup"><span data-stu-id="ac8fb-222">id</span></span>|<span data-ttu-id="ac8fb-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="ac8fb-223">rakesh</span></span>|<span data-ttu-id="ac8fb-224">Köşe için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-224">The unique identifier for the vertex.</span></span> <span data-ttu-id="ac8fb-225">Kimlik belirtmezseniz, bir kimlik otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="ac8fb-226">cinsiyet</span><span class="sxs-lookup"><span data-stu-id="ac8fb-226">gender</span></span>|<span data-ttu-id="ac8fb-227">erkek</span><span class="sxs-lookup"><span data-stu-id="ac8fb-227">male</span></span>| 
    <span data-ttu-id="ac8fb-228">okul</span><span class="sxs-lookup"><span data-stu-id="ac8fb-228">school</span></span>|<span data-ttu-id="ac8fb-229">MIT</span><span class="sxs-lookup"><span data-stu-id="ac8fb-229">MIT</span></span>| 

7. <span data-ttu-id="ac8fb-230">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-230">Click **OK**.</span></span> 

8. <span data-ttu-id="ac8fb-231">Varsayılan `g.V()` filtresiyle **Filtre Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-231">Click **Apply Filter** with the default `g.V()` filter.</span></span> <span data-ttu-id="ac8fb-232">Tüm kullanıcılar **Sonuç listesinde** gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-232">All of the users now show in the **Results** list.</span></span> <span data-ttu-id="ac8fb-233">Daha fazla veri ekledikçe sonuçlarınızı sınırlamak için filtreleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-233">As you add more data, you can use filters to limit your results.</span></span> <span data-ttu-id="ac8fb-234">Varsayılan olarak, Veri Gezgini bir grafikteki tüm köşeleri almak için `g.V()` kullanır, ancak grafikteki tüm köşelerin sayısını JSON biçiminde döndürmek isterseniz bunu `g.V().count()` gibi farklı bir [grafik sorgusuyla](tutorial-query-graph.md) değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-234">By default, Data Explorer uses `g.V()` to retrieve all vertices in a graph, but you can change that to a different [graph query](tutorial-query-graph.md), such as `g.V().count()`, to return a count of all the vertices in the graph in JSON format.</span></span>

9. <span data-ttu-id="ac8fb-235">Artık rakesh ve ashley arasında bağlantı kurabiliriz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="ac8fb-236">**Sonuç listesinde** **ashley**’in seçili olduğundan emin olun ve ardından sağ alttaki **Hedefler**’in yanında bulunan Düzenle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-236">Ensure **ashley** in selected in the **Results** list, then click the edit button next to **Targets** on lower right side.</span></span> <span data-ttu-id="ac8fb-237">**Özellikler** alanını görmek için pencerenizi genişletmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-237">You may need to widen your window to see the **Properties** area.</span></span>

   ![Hedef grafikteki bir köşeyi değiştirme](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="ac8fb-239">**Hedef** kutusunda *rakesh* yazın, **Kenar etiketi** kutusunda *tanıyor* yazın ve ardından onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-239">In the **Target** box type *rakesh*, and in the **Edge label** box type *knows*, and then click the check box.</span></span>

   ![Veri Gezgininde ashley ve rakesh arasında bir bağlantı ekleyin](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="ac8fb-241">Sonuç listesinden **rakesh**’i seçin, ashley ve rakesh’in bağlantılı olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-241">Now select **rakesh** from the results list and see that ashley and rakesh are connected.</span></span> 

   ![Veri Gezgini'nde bağlı iki köşe](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="ac8fb-243">Veri Gezgini'ni kullanarak ayrıca saklı yordamlar, UDF'ler ve tetikleyiciler oluşturabilir, bu sayede sunucu tarafı iş mantığını gerçekleştirebilir ve aktarım hızını ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-243">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="ac8fb-244">Veri Gezgini, API'lerdeki tüm yerleşik programlı veri erişimini açığa çıkarır ancak Azure portalındaki verilerinize kolayca erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-244">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>



## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="ac8fb-245">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="ac8fb-245">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="ac8fb-246">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="ac8fb-246">Clean up resources</span></span>

<span data-ttu-id="ac8fb-247">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu hızlı başlangıç tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="ac8fb-247">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span> 

1. <span data-ttu-id="ac8fb-248">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-248">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="ac8fb-249">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-249">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac8fb-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac8fb-250">Next steps</span></span>

<span data-ttu-id="ac8fb-251">Bu hızlı başlangıçta Azure Cosmos DB hesabı oluşturmayı, Veri Gezgini'ni kullanarak grafik oluşturmayı ve bir uygulamayı çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-251">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, and run an app.</span></span> <span data-ttu-id="ac8fb-252">Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ac8fb-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ac8fb-253">Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="ac8fb-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

