---
title: "aaaC ++ Azure Cosmos DB Öğreticisi | Microsoft Docs"
description: "C++ için Azure Cosmos DB onaylı bir SDK’yı kullanarak bir C++ veritabanı ve konsol uygulaması oluşturan öğretici. Azure Cosmos DB, çok büyük ölçekli bir veritabanı hizmetidir."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a><span data-ttu-id="7c57a-104">Azure Cosmos DB: Merhaba DocumentDB API C++ konsol uygulaması Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="7c57a-104">Azure Cosmos DB: C++ console application tutorial for hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c57a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7c57a-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="7c57a-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7c57a-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="7c57a-107">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="7c57a-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="7c57a-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="7c57a-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="7c57a-109">Java</span><span class="sxs-lookup"><span data-stu-id="7c57a-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="7c57a-110">C++</span><span class="sxs-lookup"><span data-stu-id="7c57a-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="7c57a-111">Hoş Geldiniz toohello C++ öğretici hello Azure Cosmos DB DocumentDB API için C++ için SDK Destekli!</span><span class="sxs-lookup"><span data-stu-id="7c57a-111">Welcome toohello C++ tutorial for hello Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="7c57a-112">Bu öğreticiden yararlandıktan sonra, bir C++ veritabanı dahil olmak üzere Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c57a-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="7c57a-113">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="7c57a-113">We'll cover:</span></span>

* <span data-ttu-id="7c57a-114">Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="7c57a-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="7c57a-115">Uygulamanızı kurma</span><span class="sxs-lookup"><span data-stu-id="7c57a-115">Setting up your application</span></span>
* <span data-ttu-id="7c57a-116">C++ Azure Cosmos DB veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="7c57a-117">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-117">Creating a collection</span></span>
* <span data-ttu-id="7c57a-118">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-118">Creating JSON documents</span></span>
* <span data-ttu-id="7c57a-119">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c57a-119">Querying hello collection</span></span>
* <span data-ttu-id="7c57a-120">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="7c57a-120">Replacing a document</span></span>
* <span data-ttu-id="7c57a-121">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="7c57a-121">Deleting a document</span></span>
* <span data-ttu-id="7c57a-122">Merhaba C++ Azure Cosmos DB veritabanı siliniyor</span><span class="sxs-lookup"><span data-stu-id="7c57a-122">Deleting hello C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="7c57a-123">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="7c57a-123">Don't have time?</span></span> <span data-ttu-id="7c57a-124">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="7c57a-124">Don't worry!</span></span> <span data-ttu-id="7c57a-125">Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span><span class="sxs-lookup"><span data-stu-id="7c57a-125">hello complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="7c57a-126">Bkz: [alma hello eksiksiz bir çözüm](#GetSolution) hızlı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7c57a-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="7c57a-127">Merhaba C++ öğreticiyi tamamladıktan sonra lütfen hello kullan oylama hello bu sayfa toogive sonunda bize geri bildirim düğmeler.</span><span class="sxs-lookup"><span data-stu-id="7c57a-127">After you've completed hello C++ tutorial, please use hello voting buttons at hello bottom of this page toogive us feedback.</span></span> 

<span data-ttu-id="7c57a-128">Bize istiyorsanız toocontact doğrudan düşündüğünüz ücretsiz tooinclude e-posta adresi, yorumlarınızı veya [toous burada ulaşmak](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="7c57a-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments or [reach out toous here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="7c57a-129">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="7c57a-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-c-tutorial"></a><span data-ttu-id="7c57a-130">Merhaba C++ öğreticisi için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7c57a-130">Prerequisites for hello C++ tutorial</span></span>
<span data-ttu-id="7c57a-131">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="7c57a-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="7c57a-132">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7c57a-132">An active Azure account.</span></span> <span data-ttu-id="7c57a-133">Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7c57a-134">[Visual Studio](https://www.visualstudio.com/downloads/), hello C++ dil bileşenlerinin yüklü ile.</span><span class="sxs-lookup"><span data-stu-id="7c57a-134">[Visual Studio](https://www.visualstudio.com/downloads/), with hello C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="7c57a-135">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="7c57a-136">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="7c57a-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="7c57a-137">Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[C++ uygulamanızı kurma](#SetupNode).</span><span class="sxs-lookup"><span data-stu-id="7c57a-137">If you already have an account you want toouse, you can skip ahead too[Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="7c57a-138"><a id="SetupC++"></a>2. Adım: C++ uygulamanızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7c57a-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="7c57a-139">Visual Studio'yu açın ve ardından hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-139">Open Visual Studio, and then on hello **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="7c57a-140">Merhaba, **yeni proje** penceresinde hello **yüklü** bölmesinde genişletin **Visual C++**, tıklatın **Win32**ve ardından  **Win32 konsol uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-140">In hello **New Project** window, in hello **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="7c57a-141">Merhaba proje hellodocumentdb olarak adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-141">Name hello project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Merhaba Yeni Proje Sihirbazı ekran görüntüsü](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="7c57a-143">Win32 Uygulama Sihirbazı'nı Hello başladığında tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-143">When hello Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="7c57a-144">Merhaba Proje oluşturulduktan sonra hello NuGet Paket Yöneticisi hello sağ tıklayarak açın **hellodocumentdb** proje **Çözüm Gezgini** tıklatıp **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-144">Once hello project has been created, open hello NuGet package manager by right-clicking hello **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![NuGet paketini Yönet hello Proje menüsünde gösteren ekran görüntüsü](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="7c57a-146">Merhaba, **NuGet: hellodocumentdb** sekmesini tıklatın, **Gözat**, arayın ve sonra *documentdbcpp*.</span><span class="sxs-lookup"><span data-stu-id="7c57a-146">In hello **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="7c57a-147">Merhaba sonuçlarında DocumentDbCPP, hello ekran aşağıdaki gösterildiği gibi seçin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-147">In hello results, select DocumentDbCPP, as shown in hello following screenshot.</span></span> <span data-ttu-id="7c57a-148">Bu paketi başvuruları tooC ++ REST SDK hello DocumentDbCPP için bağımlılık olduğu yükler.</span><span class="sxs-lookup"><span data-stu-id="7c57a-148">This package installs references tooC++ REST SDK, which is a dependency for hello DocumentDbCPP.</span></span>  
   
    ![Vurgulanan gösteren ekran görüntüsü hello DocumentDbCpp paketi](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="7c57a-150">Merhaba paketleri tooyour proje eklendikten sonra tüm kümesi toostart biraz kod yazmaya duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-150">Once hello packages have been added tooyour project, we are all set toostart writing some code.</span></span>   

## <span data-ttu-id="7c57a-151"><a id="Config"></a>3. Adım: Azure Cosmos DB veritabanınıza yönelik bağlantı ayrıntılarını Azure portaldan kopyalama</span><span class="sxs-lookup"><span data-stu-id="7c57a-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="7c57a-152">Ortaya çıkarmak [Azure portal](https://portal.azure.com) ve çapraz oluşturduğunuz toohello Azure Cosmos DB veritabanı hesabı.</span><span class="sxs-lookup"><span data-stu-id="7c57a-152">Bring up [Azure portal](https://portal.azure.com) and traverse toohello Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="7c57a-153">Bizim C++ kod parçacığını biz hello URI ve hello sonraki adım tooestablish bağlantı Azure portalından hello birincil anahtar gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-153">We will need hello URI and hello primary key from Azure portal in hello next step tooestablish a connection from our C++ code snippet.</span></span> 

![Azure Cosmos DB URI ve anahtarları'hello Azure portalı](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="7c57a-155"><a id="Connect"></a>4. adım: tooan Azure Cosmos DB hesap bağlanma</span><span class="sxs-lookup"><span data-stu-id="7c57a-155"><a id="Connect"></a>Step 4: Connect tooan Azure Cosmos DB account</span></span>
1. <span data-ttu-id="7c57a-156">Üstbilgiler ve ad alanlarını tooyour kaynak kodu, sonra aşağıdaki hello eklemek `#include "stdafx.h"`.</span><span class="sxs-lookup"><span data-stu-id="7c57a-156">Add hello following headers and namespaces tooyour source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="7c57a-157">Sonraki hello aşağıdaki kod tooyour main işlevi ve hello hesabı yapılandırması birincil anahtar toomatch 3. adımındaki Azure Cosmos DB ayarlarınızı değiştirip ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-157">Next add hello following code tooyour main function and replace hello account configuration and primary key toomatch your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="7c57a-158">Merhaba kod tooinitialize hello documentdb istemci sahip olduğunuza göre Azure Cosmos DB kaynaklarla çalışmak bir bakalım.</span><span class="sxs-lookup"><span data-stu-id="7c57a-158">Now that you have hello code tooinitialize hello documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="7c57a-159"><a id="CreateDBColl"></a>5. Adım: C++ veritabanı ve koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="7c57a-160">Biz bu adımı gerçekleştirmeden önce nasıl bir veritabanı, koleksiyon ve belgeler için olanlar da yeni tooAzure Cosmos DB olan etkileşim üzerinden edelim.</span><span class="sxs-lookup"><span data-stu-id="7c57a-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new tooAzure Cosmos DB.</span></span> <span data-ttu-id="7c57a-161">[Veritabanı](documentdb-resources.md#databases), koleksiyonlar genelinde bölümlenmiş belge depolama alanının mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="7c57a-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="7c57a-162">A [koleksiyonu](documentdb-resources.md#collections) hello ilişkili JavaScript uygulama mantığının ve JSON belgelerinin bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7c57a-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and hello associated JavaScript application logic.</span></span> <span data-ttu-id="7c57a-163">Hello Azure Cosmos DB hiyerarşik kaynak modeli ve konuları hakkında daha fazla bilgi edinmek [Azure Cosmos DB hiyerarşik kaynak modeli ve kavramları](documentdb-resources.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-163">You can learn more about hello Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="7c57a-164">Veritabanı bir toocreate ve karşılık gelen koleksiyon kod toohello ana işlevinizi sonuna aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-164">toocreate a database and a corresponding collection add hello following code toohello end of your main function.</span></span> <span data-ttu-id="7c57a-165">Bu, 'FamilyRegistry' ve 'hello önceki adımda bildirilen hello İstemci Yapılandırması'nı kullanarak FamilyCollection' adlı bir koleksiyon adı verilen bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7c57a-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using hello client configuration you declared in hello previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="7c57a-166"><a id="CreateDoc"></a>6. Adım: Belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c57a-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="7c57a-167">[Belgeler](documentdb-resources.md#documents), kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="7c57a-168">Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="7c57a-169">Bir belge hello main işlevi hello sonuna koddan hello kopyalayarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-169">You can create a document by copying hello following code into hello end of hello main function.</span></span> 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

<span data-ttu-id="7c57a-170">toosummarize, bu kod bir Azure Cosmos DB veritabanı, koleksiyon ve belge Gezgini Azure portalında sorgulayabilirsiniz belgeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7c57a-170">toosummarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++ Öğreticisi - hello hello hesabı, hello veritabanı, hello koleksiyonu ve hello belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="7c57a-172"><a id="QueryDB"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="7c57a-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="7c57a-173">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="7c57a-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="7c57a-174">Merhaba aşağıdaki örnek kod hello önceki adımda oluşturduğumuz hello belgeleri karşı çalıştırabilirsiniz SQL söz dizimi kullanılarak yapılan bir sorguyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-174">hello following sample code shows a query made using SQL syntax that you can run against hello documents we created in hello previous step.</span></span>

<span data-ttu-id="7c57a-175">benzersiz tanımlayıcı veya kaynak kimliği hello veritabanı ve hello belge istemci birlikte hello koleksiyonu için bağımsız değişkenler hello gibi hello işlevi alır.</span><span class="sxs-lookup"><span data-stu-id="7c57a-175">hello function takes in as arguments hello unique identifier or resource id for hello database and hello collection along with hello document client.</span></span> <span data-ttu-id="7c57a-176">Bu kodu ana işlevden önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-176">Add this code before main function.</span></span>

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="7c57a-177"><a id="Replace"></a>8. Adım: Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="7c57a-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="7c57a-178">Azure Cosmos DB hello kod aşağıdaki gösterildiği gibi JSON belgelerini değiştirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="7c57a-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in hello following code.</span></span> <span data-ttu-id="7c57a-179">Merhaba executesimplequery işlevi sonra bu kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-179">Add this code after hello executesimplequery function.</span></span>

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <span data-ttu-id="7c57a-180"><a id="Delete"></a>9. Adım: Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="7c57a-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="7c57a-181">JSON belgeleri silmeyi azure Cosmos DB destekler, kopyalama ve yapıştırma hello koddan sonra hello replacedocument işlevi tarafından bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting hello following code after hello replacedocument function.</span></span> 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="7c57a-182"><a id="DeleteDB"></a>10. Adım: Bir veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="7c57a-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="7c57a-183">Oluşturulan hello veritabanı siliniyor hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7c57a-183">Deleting hello created database removes hello database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="7c57a-184">Kod parçacığını (işlevi temizleme) hello deletedocument işlevi tooremove hello veritabanı ve tüm hello alt kaynakları sonra aşağıdaki hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="7c57a-184">Copy and paste hello following code snippet (function cleanup) after hello deletedocument function tooremove hello database and all hello child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="7c57a-185"><a id="Run"></a>11. Adım: C++ uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="7c57a-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="7c57a-186">Biz kod toocreate artık eklemiş olduğunuz, sorgu, değiştirmek ve farklı Azure Cosmos DB kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="7c57a-186">We have now added code toocreate, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="7c57a-187">Bize şimdi bu yukarı bizim main işlevi hellodocumentdb.cpp bazı tanılama iletileri ile birlikte gelen çağrıları toothese farklı işlevler ekleyerek bağlayın.</span><span class="sxs-lookup"><span data-stu-id="7c57a-187">Let us now wire this up by adding calls toothese different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="7c57a-188">Merhaba main işlevi, uygulamanızın koddan hello ile değiştirerek bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c57a-188">You can do so by replacing hello main function of your application with hello following code.</span></span> <span data-ttu-id="7c57a-189">Bu yazma hello account_configuration_uri ve 3. adımında, hello koda kopyaladığınız primary_key üzerinden şekilde kaydedin bu satırı ya da kopyalama hello değer yeniden hello portalından.</span><span class="sxs-lookup"><span data-stu-id="7c57a-189">This writes over hello account_configuration_uri and primary_key you copied into hello code in Step 3, so save that line or copy hello values in again from hello portal.</span></span> 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

<span data-ttu-id="7c57a-190">Artık mümkün toobuild olması ve F5 tuşuna basarak Visual Studio'da kodunuzu çalıştırmak veya gerekir alternatif olarak hello uygulama bulma ve çalıştırarak terminal penceresinde hello yürütülebilir hello.</span><span class="sxs-lookup"><span data-stu-id="7c57a-190">You should now be able toobuild and run your code in Visual Studio by pressing F5 or alternatively in hello terminal window by locating hello application and running hello executable.</span></span> 

<span data-ttu-id="7c57a-191">Merhaba Başlarken uygulamanızın çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-191">You should see hello output of your get started app.</span></span> <span data-ttu-id="7c57a-192">Merhaba çıkış ekran aşağıdaki hello eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-192">hello output should match hello following screenshot.</span></span>

![Azure Cosmos DB C++ uygulama çıktısı](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="7c57a-194">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="7c57a-194">Congratulations!</span></span> <span data-ttu-id="7c57a-195">Merhaba C++ öğreticisini tamamladınız ve İlk Azure Cosmos DB konsol uygulamanız sahip!</span><span class="sxs-lookup"><span data-stu-id="7c57a-195">You've completed hello C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="7c57a-196"><a id="GetSolution"></a>Merhaba tam C++ Öğreticisi çözümünü edinme</span><span class="sxs-lookup"><span data-stu-id="7c57a-196"><a id="GetSolution"></a>Get hello complete C++ tutorial solution</span></span>
<span data-ttu-id="7c57a-197">Bu makaledeki tüm hello örnekleri içeren toobuild hello GetStarted çözümünü hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c57a-197">toobuild hello GetStarted solution that contains all hello samples in this article, you need hello following:</span></span>

* <span data-ttu-id="7c57a-198">[Azure Cosmos DB hesabı][create-account].</span><span class="sxs-lookup"><span data-stu-id="7c57a-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="7c57a-199">Merhaba [GetStarted](https://github.com/stalker314314/DocumentDBCpp) çözüm Github'da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c57a-199">hello [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c57a-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c57a-200">Next steps</span></span>
* <span data-ttu-id="7c57a-201">Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-201">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="7c57a-202">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="7c57a-202">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="7c57a-203">Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="7c57a-203">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


