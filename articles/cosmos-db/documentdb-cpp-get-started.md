---
title: "Azure Cosmos DB için C++ öğreticisi | Microsoft Docs"
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
ms.openlocfilehash: 7d8de973765830ccd7983182bc1bb19b1e01e505
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-the-documentdb-api"></a><span data-ttu-id="4c9c3-104">Azure Cosmos DB: DocumentDB API’si için C++ konsol uygulaması öğreticisi</span><span class="sxs-lookup"><span data-stu-id="4c9c3-104">Azure Cosmos DB: C++ console application tutorial for the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c9c3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4c9c3-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="4c9c3-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4c9c3-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="4c9c3-107">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="4c9c3-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="4c9c3-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="4c9c3-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="4c9c3-109">Java</span><span class="sxs-lookup"><span data-stu-id="4c9c3-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="4c9c3-110">C++</span><span class="sxs-lookup"><span data-stu-id="4c9c3-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 
 

<span data-ttu-id="4c9c3-111">C++ için Azure Cosmos DB DocumentDB API’si onaylı SDK için C++ öğreticisine hoş geldiniz!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-111">Welcome to the C++ tutorial for the Azure Cosmos DB DocumentDB API endorsed SDK for C++!</span></span> <span data-ttu-id="4c9c3-112">Bu öğreticiden yararlandıktan sonra, bir C++ veritabanı dahil olmak üzere Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources, including a C++ database.</span></span>

<span data-ttu-id="4c9c3-113">Şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="4c9c3-113">We'll cover:</span></span>

* <span data-ttu-id="4c9c3-114">Azure Cosmos DB hesabı oluşturma ve hesaba bağlanma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="4c9c3-115">Uygulamanızı kurma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-115">Setting up your application</span></span>
* <span data-ttu-id="4c9c3-116">C++ Azure Cosmos DB veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-116">Creating a C++ Azure Cosmos DB database</span></span>
* <span data-ttu-id="4c9c3-117">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-117">Creating a collection</span></span>
* <span data-ttu-id="4c9c3-118">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-118">Creating JSON documents</span></span>
* <span data-ttu-id="4c9c3-119">Koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="4c9c3-119">Querying the collection</span></span>
* <span data-ttu-id="4c9c3-120">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-120">Replacing a document</span></span>
* <span data-ttu-id="4c9c3-121">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-121">Deleting a document</span></span>
* <span data-ttu-id="4c9c3-122">C++ Azure Cosmos DB veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-122">Deleting the C++ Azure Cosmos DB database</span></span>

<span data-ttu-id="4c9c3-123">Zamanınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="4c9c3-123">Don't have time?</span></span> <span data-ttu-id="4c9c3-124">Endişelenmeyin!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-124">Don't worry!</span></span> <span data-ttu-id="4c9c3-125">Eksiksiz çözümü [GitHub](https://github.com/stalker314314/DocumentDBCpp)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-125">The complete solution is available on [GitHub](https://github.com/stalker314314/DocumentDBCpp).</span></span> <span data-ttu-id="4c9c3-126">Hızlı yönergeler için bkz. [Eksiksiz çözüm edinme](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="4c9c3-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="4c9c3-127">C++ öğreticisini tamamladıktan sonra, bize geri bildirim sağlamak için lütfen bu sayfanın alt kısmındaki oylama düğmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-127">After you've completed the C++ tutorial, please use the voting buttons at the bottom of this page to give us feedback.</span></span> 

<span data-ttu-id="4c9c3-128">Doğrudan sizinle iletişim kurmamızı isterseniz yorumlarınıza e-posta adresinizi ekleyin veya [buradan bize ulaşın](https://www.research.net/r/8BKRJ3Z).</span><span class="sxs-lookup"><span data-stu-id="4c9c3-128">If you'd like us to contact you directly, feel free to include your email address in your comments or [reach out to us here](https://www.research.net/r/8BKRJ3Z).</span></span> 

<span data-ttu-id="4c9c3-129">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-c-tutorial"></a><span data-ttu-id="4c9c3-130">C++ öğreticisi için önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4c9c3-130">Prerequisites for the C++ tutorial</span></span>
<span data-ttu-id="4c9c3-131">Lütfen aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="4c9c3-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="4c9c3-132">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-132">An active Azure account.</span></span> <span data-ttu-id="4c9c3-133">Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4c9c3-134">C++ dil bileşenleri yüklü [Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4c9c3-134">[Visual Studio](https://www.visualstudio.com/downloads/), with the C++ language components installed.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="4c9c3-135">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="4c9c3-136">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="4c9c3-137">Kullanmak istediğiniz bir hesap zaten varsa [C++ uygulamanızı kurma](#SetupNode)'ya atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-137">If you already have an account you want to use, you can skip ahead to [Setup your C++ application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="4c9c3-138"><a id="SetupC++"></a>2. Adım: C++ uygulamanızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="4c9c3-138"><a id="SetupC++"></a>Step 2: Set up your C++ application</span></span>
1. <span data-ttu-id="4c9c3-139">Visual Studio’yu açın ve **Dosya** menüsünde **Yeni**’ye, ardından **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-139">Open Visual Studio, and then on the **File** menu, click **New**, and then click **Project**.</span></span> 
2. <span data-ttu-id="4c9c3-140">**Yeni Proje** penceresindeki **Yüklü** bölmesinde **Visual C++** seçeneğini genişletin, **Win32**’ye ve ardından **Win32 Konsol Uygulaması**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-140">In the **New Project** window, in the **Installed** pane, expand **Visual C++**, click **Win32**, and then click **Win32 Console Application**.</span></span> <span data-ttu-id="4c9c3-141">Projeyi hellodocumentdb olarak adlandırıp **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-141">Name the project hellodocumentdb and then click **OK**.</span></span> 
   
    ![Yeni proje sihirbazının ekran görüntüsü](media/documentdb-cpp-get-started/hello.png)
3. <span data-ttu-id="4c9c3-143">Win32 Uygulama Sihirbazı başlatıldığında **Son**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-143">When the Win32 Application Wizard starts, click **Finish**.</span></span>
4. <span data-ttu-id="4c9c3-144">Proje oluşturulduktan sonra **Çözüm Gezgini**’nde **hellodocumentdb** projesine sağ tıklayıp **NuGet Paketlerini Yönet**’e tıklayarak NuGet paket yöneticisini açın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-144">Once the project has been created, open the NuGet package manager by right-clicking the **hellodocumentdb** project in **Solution Explorer** and clicking **Manage NuGet Packages**.</span></span> 
   
    ![Proje menüsündeki NuGet Paketlerini Yönet seçeneğini gösteren ekran görüntüsü](media/documentdb-cpp-get-started/nuget.png)
5. <span data-ttu-id="4c9c3-146">**NuGet: hellodocumentdb** sekmesinde **Gözat**’a tıklayın ve *documentdbcpp* öğesini aratın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-146">In the **NuGet: hellodocumentdb** tab, click **Browse**, and then search for *documentdbcpp*.</span></span> <span data-ttu-id="4c9c3-147">Aşağıdaki ekran görüntüsünde gösterildiği gibi, sonuçlardan DocumentDbCPP’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-147">In the results, select DocumentDbCPP, as shown in the following screenshot.</span></span> <span data-ttu-id="4c9c3-148">Bu paket, DocumentDbCPP için bir bağımlılık olan C++ REST SDK başvurularını yükler.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-148">This package installs references to C++ REST SDK, which is a dependency for the DocumentDbCPP.</span></span>  
   
    ![DocumentDbCpp paketini vurgulanmış halde gösteren ekran görüntüsü](media/documentdb-cpp-get-started/cpp.png)
   
    <span data-ttu-id="4c9c3-150">Paketler projenize eklendikten sonra biraz kod yazmaya hazırız demektir.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-150">Once the packages have been added to your project, we are all set to start writing some code.</span></span>   

## <span data-ttu-id="4c9c3-151"><a id="Config"></a>3. Adım: Azure Cosmos DB veritabanınıza yönelik bağlantı ayrıntılarını Azure portaldan kopyalama</span><span class="sxs-lookup"><span data-stu-id="4c9c3-151"><a id="Config"></a>Step 3: Copy connection details from Azure portal for your Azure Cosmos DB database</span></span>
<span data-ttu-id="4c9c3-152">[Azure portalını](https://portal.azure.com) açın ve oluşturduğunuz Azure Cosmos DB veritabanı hesabına gidin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-152">Bring up [Azure portal](https://portal.azure.com) and traverse to the Azure Cosmos DB database account you created.</span></span> <span data-ttu-id="4c9c3-153">C++ kod parçacığımızdan bir bağlantı oluşturmak için bir sonraki adımda Azure portalından alınan URI ve birincil anahtara ihtiyacımız olacak.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-153">We will need the URI and the primary key from Azure portal in the next step to establish a connection from our C++ code snippet.</span></span> 

![Azure portalında Azure Cosmos DB URI’si ve anahtarlar](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <span data-ttu-id="4c9c3-155"><a id="Connect"></a>4. Adım: Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-155"><a id="Connect"></a>Step 4: Connect to an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="4c9c3-156">Aşağıdaki üst bilgileri ve ad alanlarını kaynak kodunuza `#include "stdafx.h"` ifadesinden sonra gelecek şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-156">Add the following headers and namespaces to your source code, after `#include "stdafx.h"`.</span></span>
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. <span data-ttu-id="4c9c3-157">Ardından, aşağıdaki kodu ana işlevinize ekleyin ve hesap yapılandırması ile birincil anahtarı 3. adımdaki Azure Cosmos DB ayarlarınızla eşleşecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-157">Next add the following code to your main function and replace the account configuration and primary key to match your Azure Cosmos DB settings from step 3.</span></span> 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    <span data-ttu-id="4c9c3-158">Artık documentdb istemcisini başlatmaya yarayacak koda sahip olduğunuza göre, Azure Cosmos DB kaynaklarıyla çalışmaya bakalım.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-158">Now that you have the code to initialize the documentdb client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <span data-ttu-id="4c9c3-159"><a id="CreateDBColl"></a>5. Adım: C++ veritabanı ve koleksiyonu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-159"><a id="CreateDBColl"></a>Step 5: Create a C++ database and collection</span></span>
<span data-ttu-id="4c9c3-160">Bu adımı gerçekleştirmeden önce, Azure Cosmos DB konusunda acemi olanlar için veritabanı, koleksiyon ve belgelerin nasıl etkileşimde bulunduğundan bahsedelim.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-160">Before we perform this step, let's go over how a database, collection and documents interact for those of you who are new to Azure Cosmos DB.</span></span> <span data-ttu-id="4c9c3-161">[Veritabanı](documentdb-resources.md#databases), koleksiyonlar genelinde bölümlenmiş belge depolama alanının mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-161">A [database](documentdb-resources.md#databases) is a logical container of document storage portioned across collections.</span></span> <span data-ttu-id="4c9c3-162">[Koleksiyon](documentdb-resources.md#collections), JSON belgeleri ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-162">A [collection](documentdb-resources.md#collections) is a container of JSON documents and the associated JavaScript application logic.</span></span> <span data-ttu-id="4c9c3-163">[Azure Cosmos DB hiyerarşik kaynak modeli ve kavramları](documentdb-resources.md) konusundan Azure Cosmos DB hiyerarşik kaynak modeli ve kavramları hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-163">You can learn more about the Azure Cosmos DB hierarchical resource model and concepts in [Azure Cosmos DB hierarchical resource model and concepts](documentdb-resources.md).</span></span>

<span data-ttu-id="4c9c3-164">Bir veritabanı ve ona karşılık gelen bir koleksiyon oluşturmak için aşağıdaki kodu ana işlevinizin sonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-164">To create a database and a corresponding collection add the following code to the end of your main function.</span></span> <span data-ttu-id="4c9c3-165">Bunu yaptığınızda, önceki adımda belirttiğiniz istemci yapılandırması kullanılarak 'FamilyRegistry’ adlı bir veritabanı ve ‘FamilyCollection’ adlı bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-165">This creates a database called 'FamilyRegistry’ and a collection called ‘FamilyCollection’ using the client configuration you declared in the previous step.</span></span>

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <span data-ttu-id="4c9c3-166"><a id="CreateDoc"></a>6. Adım: Belge oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c9c3-166"><a id="CreateDoc"></a>Step 6: Create a document</span></span>
<span data-ttu-id="4c9c3-167">[Belgeler](documentdb-resources.md#documents), kullanıcı tanımlı (rastgele) JSON içeriğidir.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-167">[Documents](documentdb-resources.md#documents) are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="4c9c3-168">Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-168">You can now insert a document into Azure Cosmos DB.</span></span> <span data-ttu-id="4c9c3-169">Aşağıdaki kodu ana işlevin sonuna kopyalayarak bir belge oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-169">You can create a document by copying the following code into the end of the main function.</span></span> 

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

<span data-ttu-id="4c9c3-170">Özetlemek gerekirse, bu kod bir Azure Cosmos DB veritabanı, koleksiyonu ve belgeleri oluşturur ve bunları Azure portalındaki Belge Gezgini’nde sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-170">To summarize, this code creates an Azure Cosmos DB database, collection, and documents, which you can query in Document Explorer in Azure portal.</span></span> 

![C++ öğreticisi - Hesap, veritabanı, koleksiyon ve belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram](media/documentdb-cpp-get-started/docs.png)

## <span data-ttu-id="4c9c3-172"><a id="QueryDB"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="4c9c3-172"><a id="QueryDB"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="4c9c3-173">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-173">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="4c9c3-174">Aşağıdaki örnek kod, önceki adımda oluşturduğumuz belgelerde SQL söz dizimi kullanarak gerçekleştirebileceğimiz bir sorguyu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-174">The following sample code shows a query made using SQL syntax that you can run against the documents we created in the previous step.</span></span>

<span data-ttu-id="4c9c3-175">Bu işlev, veritabanı ve koleksiyonun yanı sıra belge istemcisinin benzersiz tanımlayıcısı ve kaynak kimliğini bağımsız değişkenler olarak alır.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-175">The function takes in as arguments the unique identifier or resource id for the database and the collection along with the document client.</span></span> <span data-ttu-id="4c9c3-176">Bu kodu ana işlevden önce ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-176">Add this code before main function.</span></span>

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

## <span data-ttu-id="4c9c3-177"><a id="Replace"></a>8. Adım: Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-177"><a id="Replace"></a>Step 8: Replace a document</span></span>
<span data-ttu-id="4c9c3-178">Azure Cosmos DB, aşağıdaki kodda gösterildiği gibi JSON belgelerinin değiştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-178">Azure Cosmos DB supports replacing JSON documents, as demonstrated in the following code.</span></span> <span data-ttu-id="4c9c3-179">Bu kodu executesimplequery işlevinden sonra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-179">Add this code after the executesimplequery function.</span></span>

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

## <span data-ttu-id="4c9c3-180"><a id="Delete"></a>9. Adım: Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-180"><a id="Delete"></a>Step 9: Delete a document</span></span>
<span data-ttu-id="4c9c3-181">Azure Cosmos DB JSON belgelerinin silinmesini destekler; aşağıdaki kodu kopyalayıp replacedocument işlevinden sonra yapıştırarak bunu gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-181">Azure Cosmos DB supports deleting JSON documents, you can do so by copy and pasting the following code after the replacedocument function.</span></span> 

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

## <span data-ttu-id="4c9c3-182"><a id="DeleteDB"></a>10. Adım: Bir veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="4c9c3-182"><a id="DeleteDB"></a>Step 10: Delete a database</span></span>
<span data-ttu-id="4c9c3-183">Oluşturulan veritabanı silindiğinde, veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler vb.) kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-183">Deleting the created database removes the database and all child resources (collections, documents, etc.).</span></span>

<span data-ttu-id="4c9c3-184">Veritabanını ve tüm alt kaynaklarını kaldırmak için aşağıdaki kod parçacığını (cleanup işlevi) kopyalayıp deletedocument işlevinden sonra yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-184">Copy and paste the following code snippet (function cleanup) after the deletedocument function to remove the database and all the child resources.</span></span>

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <span data-ttu-id="4c9c3-185"><a id="Run"></a>11. Adım: C++ uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-185"><a id="Run"></a>Step 11: Run your C++ application all together!</span></span>
<span data-ttu-id="4c9c3-186">Farklı Azure Cosmos DB kaynaklarını oluşturmak, sorgulamak, değiştirmek ve silmek için kod ekledik.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-186">We have now added code to create, query, modify, and delete different Azure Cosmos DB resources.</span></span>  <span data-ttu-id="4c9c3-187">Şimdi de bu farklı işlevlere hellodocumentdb.cpp’deki ana işlevimizden çağrıların yanı sıra bazı tanılama iletileri ekleyerek bağlantıları tamamlayalım.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-187">Let us now wire this up by adding calls to these different functions from our main function in hellodocumentdb.cpp along with some diagnostic messages.</span></span>

<span data-ttu-id="4c9c3-188">Bunu, uygulamanızın ana işlevini aşağıdaki kodla değiştirerek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-188">You can do so by replacing the main function of your application with the following code.</span></span> <span data-ttu-id="4c9c3-189">Bu işlem 3. adımda koda kopyaladığınız account_configuration_uri ve primary_key değerlerinin üzerine yazacağından, bu satırı kaydedin veya değerleri yeniden portaldan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-189">This writes over the account_configuration_uri and primary_key you copied into the code in Step 3, so save that line or copy the values in again from the portal.</span></span> 

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

<span data-ttu-id="4c9c3-190">Artık F5’e basarak veya alternatif olarak terminal penceresinden uygulamayı bulup yürütülebilir dosyayı çalıştırarak Visual Studio’da kendi kodunuzu derleyip çalıştırabilmeniz gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-190">You should now be able to build and run your code in Visual Studio by pressing F5 or alternatively in the terminal window by locating the application and running the executable.</span></span> 

<span data-ttu-id="4c9c3-191">Başlarken uygulamanızın çıktısını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-191">You should see the output of your get started app.</span></span> <span data-ttu-id="4c9c3-192">Çıkışın aşağıdaki görüntüyle eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-192">The output should match the following screenshot.</span></span>

![Azure Cosmos DB C++ uygulama çıktısı](media/documentdb-cpp-get-started/console.png)

<span data-ttu-id="4c9c3-194">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-194">Congratulations!</span></span> <span data-ttu-id="4c9c3-195">C++ öğreticisini tamamladınız ve ilk Azure Cosmos DB konsol uygulamanızı oluşturdunuz!</span><span class="sxs-lookup"><span data-stu-id="4c9c3-195">You've completed the C++ tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="4c9c3-196"><a id="GetSolution"></a>Tam C++ öğreticisi çözümünü edinin</span><span class="sxs-lookup"><span data-stu-id="4c9c3-196"><a id="GetSolution"></a>Get the complete C++ tutorial solution</span></span>
<span data-ttu-id="4c9c3-197">Bu makaledeki tüm örnekleri içeren GetStarted çözümünü derlemek için aşağıdakilere ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="4c9c3-197">To build the GetStarted solution that contains all the samples in this article, you need the following:</span></span>

* <span data-ttu-id="4c9c3-198">[Azure Cosmos DB hesabı][create-account].</span><span class="sxs-lookup"><span data-stu-id="4c9c3-198">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="4c9c3-199">GitHub'da bulunan [GetStarted](https://github.com/stalker314314/DocumentDBCpp) çözümü.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-199">The [GetStarted](https://github.com/stalker314314/DocumentDBCpp) solution available on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c9c3-200">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c9c3-200">Next steps</span></span>
* <span data-ttu-id="4c9c3-201">[Azure Cosmos DB hesabını nasıl izleyebileceğinizi](monitor-accounts.md) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-201">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="4c9c3-202">[Query Playground](https://www.documentdb.com/sql/demo)'daki örnek veri kümelerimizde sorgular çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-202">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="4c9c3-203">[Azure Cosmos DB belgeleri sayfasının](https://azure.microsoft.com/documentation/services/documentdb/) Geliştirme bölümünde programlama modeli hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="4c9c3-203">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account


