---
title: "Azure Cosmos DB kullanarak aaaJava uygulaması geliştirme Öğreticisi | Microsoft Docs"
description: "Bu Java web uygulaması Öğreticisi nasıl toouse Azure Cosmos DB hello DocumentDB API toostore hello ve Azure Web Siteleri'nde barındırılan bir Java uygulamasında verilere gösterir."
keywords: "Uygulama geliştirme, veritabanı öğreticisi, java uygulaması, java web uygulaması öğreticisi, documentdb, Azure, Microsoft Azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="3efc4-104">Azure Cosmos DB ve hello DocumentDB API kullanarak bir Java web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3efc4-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3efc4-105">.NET</span><span class="sxs-lookup"><span data-stu-id="3efc4-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="3efc4-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="3efc4-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="3efc4-107">Java</span><span class="sxs-lookup"><span data-stu-id="3efc4-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="3efc4-108">Python</span><span class="sxs-lookup"><span data-stu-id="3efc4-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="3efc4-109">Bu Java web uygulaması Öğreticisi şunların nasıl yapıldığını gösterir toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hizmeti toostore ve erişim verilerini Azure App Service Web Apps üzerinde barındırılan bir Java uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="3efc4-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="3efc4-110">Bu konu başlığında şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="3efc4-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="3efc4-111">Nasıl toobuild eclipse'te temel bir JavaServer sayfaları (JSP) uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3efc4-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="3efc4-112">Toowork hello Azure Cosmos DB ile nasıl hizmet hello kullanarak [Azure Cosmos DB Java SDK'sı](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="3efc4-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="3efc4-113">Bu Java uygulaması Öğreticisi, toocreate, almak ve işareti etkinleştirir toocreate web tabanlı görev yönetimi uygulamasını nasıl görevler tamamlandı olarak hello görüntü aşağıdaki gösterildiği gibi gösterir.</span><span class="sxs-lookup"><span data-stu-id="3efc4-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="3efc4-114">Her bir hello görev hello Yapılacaklar listesinde Azure Cosmos DB JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="3efc4-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Yapılacaklar Listesi Java uygulamam](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="3efc4-116">Bu uygulama geliştirme öğreticisi, Java kullanımına ilişkin deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="3efc4-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="3efc4-117">Yeni tooJava veya hello ise [önkoşul araçlarında](#Prerequisites), hello tam indirme öneririz [Yapılacaklar](https://github.com/Azure-Samples/documentdb-java-todo-app) GitHub ve kullanarak proje [hello sonunda hello bu yönergeleri makale](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="3efc4-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="3efc4-118">Oluşturduktan sonra hello makale toogain Insight hello proje hello bağlamında hello kodu gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3efc4-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="3efc4-119"><a id="Prerequisites"></a>Bu Java web uygulaması öğreticisi için önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3efc4-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="3efc4-120">Bu uygulama geliştirme Öğreticisine başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3efc4-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="3efc4-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="3efc4-121">An active Azure account.</span></span> <span data-ttu-id="3efc4-122">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3efc4-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3efc4-123">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="3efc4-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="3efc4-124">OR</span><span class="sxs-lookup"><span data-stu-id="3efc4-124">OR</span></span>

    <span data-ttu-id="3efc4-125">Merhaba yerel yüklemesi [Azure Cosmos DB öykünücüsü](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="3efc4-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="3efc4-126">[Java Geliştirme Seti (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="3efc4-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="3efc4-127">Java EE Geliştiricileri için Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="3efc4-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="3efc4-128">Etkin bir Java Çalışma zamanı ortamı (ör. Tomcat veya Jetty) sahip bir Azure Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="3efc4-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="3efc4-129">Hello için bu araçları ilk kez yüklüyorsanız coreservlets.com hello hızlı başlangıç bölümünde hello yükleme işleminin bir kılavuz sağlar. kendi [öğretici: tomcat7'yi yükleme ve Eclipse ile kullanma](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) makalesi.</span><span class="sxs-lookup"><span data-stu-id="3efc4-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="3efc4-130"><a id="CreateDB"></a>1. adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3efc4-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="3efc4-131">İlk olarak bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3efc4-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="3efc4-132">Zaten bir hesabınız yok veya kullanıyorsanız bu öğretici için Azure Cosmos DB öykünücüsü hello kullanıyorsanız, çok atlayabilirsiniz[2. adım: hello Java JSP uygulaması oluşturma](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="3efc4-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="3efc4-133"><a id="CreateJSP"></a>2. adım: Merhaba Java JSP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3efc4-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="3efc4-134">toocreate hello JSP uygulaması:</span><span class="sxs-lookup"><span data-stu-id="3efc4-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="3efc4-135">İlk olarak, bir Java projesi oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="3efc4-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="3efc4-136">Eclipse'i başlatın, ardından **Dosya**'ya tıklayın, **Yeni**'ye tıklayın ve ardından **Dinamik Web Projesi**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="3efc4-137">Görmüyorsanız, **dinamik Web projesi** kullanılabilir bir proje listelenen, aşağıdaki hello: tıklatın **dosya**, tıklatın **yeni**,'ı tıklatın **proje**... genişletin **Web**, tıklatın **dinamik Web projesi**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java Uygulaması Geliştirme](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="3efc4-139">Hello proje adı girin **proje adı** kutusunda ve hello **hedef çalışma zamanı** açılan menüsünde isteğe bağlı olarak bir değer (örn. Apache Tomcat v7.0) seçin ve ardından **Son**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="3efc4-140">Bir hedef çalışma zamanı seçildiğinde, toorun projeniz yerel olarak Eclipse aracılığıyla etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3efc4-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="3efc4-141">Eclipse'te, hello Proje Gezgini görünümünde projenizi genişletin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="3efc4-142">**WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="3efc4-143">Merhaba, **yeni JSP dosyası** iletişim kutusu, ad hello dosyası **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="3efc4-144">Merhaba üst klasörünü olarak **WebContent**, aşağıdaki çizimde hello ve ardından gösterildiği gibi **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Yeni bir JSP Dosyası Oluşturma - Java Web Uygulaması Öğreticisi](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="3efc4-146">Merhaba, **JSP şablon seç** iletişim kutusunda, Bu öğretici seçimi hello amaçla **yeni JSP dosyası (html)**ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="3efc4-147">Merhaba index.jsp dosyası Eclipse'te açıldığında, metin toodisplay ekleme **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="3efc4-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="3efc4-148">Merhaba varolan içinde <body> öğesi.</span><span class="sxs-lookup"><span data-stu-id="3efc4-148">within hello existing <body> element.</span></span> <span data-ttu-id="3efc4-149">Güncelleştirilmiş <body> içerik hello kod aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="3efc4-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="3efc4-150">Merhaba index.jsp dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="3efc4-151">2. adımda bir hedef çalışma zamanı ayarlarsanız, tıklayabilirsiniz **proje** ve ardından **çalıştırmak** toorun JSP uygulamanızı yerel olarak:</span><span class="sxs-lookup"><span data-stu-id="3efc4-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World - Java Uygulaması Öğreticisi](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="3efc4-153"><a id="InstallSDK"></a>3. adım: Merhaba DocumentDB Java SDK'sını yükleme</span><span class="sxs-lookup"><span data-stu-id="3efc4-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="3efc4-154">Merhaba hello DocumentDB Java SDK'sını ve bağımlılıklarını en kolay yolu toopull aracılığıyladır [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="3efc4-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="3efc4-155">toodo bunu hello aşağıdaki adımları tamamlayarak proje tooa maven projenizi tooconvert gerekir:</span><span class="sxs-lookup"><span data-stu-id="3efc4-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="3efc4-156">Merhaba proje Gezgini'nde projenize sağ tıklayın, **yapılandırma**, tıklatın **tooMaven proje Dönüştür**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="3efc4-157">Merhaba, **yeni POM Oluştur** penceresinde hello Varsayılanları kabul edin ve tıklatın **son**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="3efc4-158">İçinde **Proje Gezgini**açın hello pom.xml dosyasını.</span><span class="sxs-lookup"><span data-stu-id="3efc4-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="3efc4-159">Merhaba üzerinde **bağımlılıkları** sekmede hello **bağımlılıkları** bölmesinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="3efc4-160">Merhaba, **bağımlılık Seç** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3efc4-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="3efc4-161">Merhaba, **Grup Kimliği** kutusuna, com.microsoft.azure girin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="3efc4-162">Merhaba, **Artifact ID** kutusuna, azure-documentdb girin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="3efc4-163">Merhaba, **sürüm** kutusuna, 1.5.1 girin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java Uygulaması SDK'sını yükleme](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="3efc4-165">Grup Kimliği ve yapı kimliği için hello bağımlılık XML ekleyin bir metin düzenleyicisi aracılığıyla doğrudan toohello pom.xml:</span><span class="sxs-lookup"><span data-stu-id="3efc4-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="3efc4-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="3efc4-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="3efc4-167">Tıklatın **Tamam** ve Maven hello DocumentDB Java SDK'sını yükler.</span><span class="sxs-lookup"><span data-stu-id="3efc4-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="3efc4-168">Merhaba pom.xml dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="3efc4-169"><a id="UseService"></a>4. adım: hello Azure Cosmos DB hizmeti bir Java uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="3efc4-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="3efc4-170">İlk olarak, şimdi hello Todoıtem nesnesini TodoItem.java içinde tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="3efc4-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="3efc4-171">Bu projede kullanıyoruz [Project Lombok](http://projectlombok.org/) toogenerate hello oluşturucusu, alıcılar, ayarlayıcılar ve oluşturucu.</span><span class="sxs-lookup"><span data-stu-id="3efc4-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="3efc4-172">Alternatif olarak, bu kodu el ile yazabilir veya sahip hello IDE oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3efc4-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="3efc4-173">tooinvoke hello Azure Cosmos DB hizmeti, gerekir örneği yeni bir **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="3efc4-174">Genel olarak, en iyi tooreuse hello olan **DocumentClient** - yerine sonraki her istek için yeni bir istemci oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="3efc4-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="3efc4-175">Biz hello istemci hello istemciyi yeniden bir **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="3efc4-176">DocumentClientFactory.java içinde tooyour Pano'da kaydettiğiniz toopaste hello URI ve birincil anahtar değerine ihtiyacı vardır [1. adım](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="3efc4-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="3efc4-177">[YOUR\_ENDPOINT\_HERE] yerine URI'nizi ve [YOUR\_KEY\_HERE] yerine BİRİNCİL ANAHTARINIZI girin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="3efc4-178">Şimdi bizim Yapılacaklar öğelerini tooAzure Cosmos DB kalıcı bir veri erişim nesnesi (DAO) tooabstract oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="3efc4-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="3efc4-179">İçinde toosave Yapılacaklar öğelerini tooa koleksiyonu sipariş, hello istemci tooknow çok hangi veritabanı ve koleksiyonu toopersist gerekir (tarafından başvurulduğu kendine bağlantılar).</span><span class="sxs-lookup"><span data-stu-id="3efc4-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="3efc4-180">Genel olarak, en iyi toocache hello veritabanı ve koleksiyonu mümkün olduğunda olduğu tooavoid ek gidiş dönüş toohello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="3efc4-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="3efc4-181">Merhaba aşağıdaki kod gösterir nasıl tooretrieve veritabanımızın ve koleksiyonumuzun var veya yoksa yeni bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3efc4-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="3efc4-182">Merhaba sonraki adım toowrite toohello koleksiyonundaki bazı kod toopersist hello Todoıtems olduğu.</span><span class="sxs-lookup"><span data-stu-id="3efc4-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="3efc4-183">Bu örnekte, kullanacağız [Gson](https://code.google.com/p/google-gson/) tooserialize ve seri durumundan Todoıtem eski basit Java nesnelerini (Pojo'lar) tooJSON belgeleri.</span><span class="sxs-lookup"><span data-stu-id="3efc4-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="3efc4-184">Azure Cosmos DB veritabanları ve koleksiyonlarına benzer şekilde belgelere de kendine bağlantılar tarafından başvurulur.</span><span class="sxs-lookup"><span data-stu-id="3efc4-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="3efc4-185">yardımcı işlevi sağlar bize alma belgeleri başka bir öznitelik (örneğin, "id") tarafından hello yerine kendi bağlantı:</span><span class="sxs-lookup"><span data-stu-id="3efc4-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="3efc4-186">Merhaba yardımcı yöntem kimliğine göre 5. adım tooretrieve bir Todoıtem JSON belgesini kullanın ve tooa POJO'ya seri durumdan:</span><span class="sxs-lookup"><span data-stu-id="3efc4-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="3efc4-187">Biz de hello DocumentClient tooget bir koleksiyonu veya Todoıtems DocumentDB SQL kullanarak listesini kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3efc4-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="3efc4-188">Merhaba DocumentClient ile bir belge birçok yolu tooupdate vardır.</span><span class="sxs-lookup"><span data-stu-id="3efc4-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="3efc4-189">Bizim Yapılacaklar listesi uygulaması Todoıtem tam olup toobe mümkün tootoggle istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3efc4-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="3efc4-190">Hello hello belge içinde "tamamlandı" özniteliğini güncelleştirerek bunu yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="3efc4-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="3efc4-191">Son olarak, hello özelliği toodelete Todoıtem listemizden istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="3efc4-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="3efc4-192">toodo Bu, daha önce yazdığımız hello yardımcı yöntemini kullanırız tooretrieve kendi bağlantı hello ve hello istemci toodelete söyleyin onu:</span><span class="sxs-lookup"><span data-stu-id="3efc4-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="3efc4-193"><a id="Wire"></a>5. adım: Java uygulaması geliştirme projesinin hello hello kalan birlikte bağlantı kabloları</span><span class="sxs-lookup"><span data-stu-id="3efc4-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="3efc4-194">Biz hello eğlenceli kısımları tamamladığımıza göre şimdi bitleri - kalan tüm toobuild bir hızlı kullanıcı arabirimi ve DAO tooour wire.</span><span class="sxs-lookup"><span data-stu-id="3efc4-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="3efc4-195">İlk olarak, bir denetleyici toocall bizim DAO oluşturmaya başlayalım:</span><span class="sxs-lookup"><span data-stu-id="3efc4-195">First, let's start with building a controller toocall our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="3efc4-196">Daha karmaşık bir uygulamada hello denetleyicisi hello DAO üstünde karmaşık iş mantığı barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="3efc4-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="3efc4-197">Ardından, bir servlet tooroute HTTP isteklerini toohello denetleyicisi oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="3efc4-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="3efc4-198">Bir web kullanıcı arabirimi toodisplay toohello kullanıcı ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="3efc4-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="3efc4-199">Merhaba index.jsp daha önce oluşturduğumuz yeniden yazalım:</span><span class="sxs-lookup"><span data-stu-id="3efc4-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="3efc4-200">Son olarak, bazı istemci tarafı JavaScript tootie hello web kullanıcı arabirimini yazmak ve servlet'i birbirine hello:</span><span class="sxs-lookup"><span data-stu-id="3efc4-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="3efc4-201">Harika!</span><span class="sxs-lookup"><span data-stu-id="3efc4-201">Awesome!</span></span> <span data-ttu-id="3efc4-202">Kalan tüm sunulmuştur tootest Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="3efc4-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="3efc4-203">Merhaba uygulamayı yerel olarak çalıştırın ve hello öğe adı ve kategoriyi doldurarak ve tıklayarak birkaç Yapılacaklar öğesi ekleyin **Görev Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="3efc4-204">Merhaba öğe göründükten sonra hello onay kutusu geçiş ve tıklayarak tamamlanmadan olarak güncelleştirebilirsiniz **güncelleştirme görevleri**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="3efc4-205"><a id="Deploy"></a>6. adım: Java uygulaması tooAzure Web siteleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="3efc4-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="3efc4-206">Uygulamanızı bir WAR dosyası olarak dışarı aktarma ve ya da kaynak denetimi (ör. Gıt) veya FTP aracılığıyla karşıya kadar basit Java uygulamalarını dağıtma azure Web siteleri yapar.</span><span class="sxs-lookup"><span data-stu-id="3efc4-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="3efc4-207">Uygulamanızı bir WAR dosyası olarak tooexport sağ tıklatın, projenizde üzerinde **Proje Gezgini**, tıklatın **verme**ve ardından **WAR dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="3efc4-208">Merhaba, **WAR dışarı** penceresinde, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3efc4-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="3efc4-209">Merhaba Web projesi kutusuna azure-documentdb-java-sample girin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="3efc4-210">Merhaba hedef kutusunda bir hedef toosave hello WAR dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="3efc4-211">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-211">Click **Finish**.</span></span>
3. <span data-ttu-id="3efc4-212">Eldeki elinizde bir WAR dosyası, yalnızca bu tooyour Azure Web sitesine ait yükleyebilirsiniz **webapps** dizin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="3efc4-213">Merhaba dosya karşıya yükleme ile ilgili yönergeler için bkz: [bir Java uygulaması tooAzure App Service Web Apps eklemek](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="3efc4-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="3efc4-214">Merhaba WAR dosyasını karşıya yüklenen toohello webapps dizinine eklendiğinde, hello çalışma zamanı ortamı bunu eklemiş ve otomatik olarak algılar.</span><span class="sxs-lookup"><span data-stu-id="3efc4-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="3efc4-215">tooview tamamlanmış ürününüzü toohttp://YOUR gidin\_SITE\_NAME.azurewebsites.net/azure-java-sample/ ve görevlerinizi eklemeye başlayın!</span><span class="sxs-lookup"><span data-stu-id="3efc4-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="3efc4-216"><a id="GetProject"></a>Merhaba projeyi Github'dan alma</span><span class="sxs-lookup"><span data-stu-id="3efc4-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="3efc4-217">Bu öğreticideki tüm hello örnekleri hello dahil edilen [Yapılacaklar](https://github.com/Azure-Samples/documentdb-java-todo-app) projeyi github'dan edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="3efc4-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="3efc4-218">tooimport hello Yapılacaklar Eclipse, projeye emin olun hello yazılım ve hello listelenen kaynakları [Önkoşullar](#Prerequisites) bölümünde, ardından aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="3efc4-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="3efc4-219">[Proje Lombok](http://projectlombok.org/)'u yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="3efc4-220">Lombok kullanılan toogenerate Oluşturucular, alıcılar ve ayarlayıcılar hello projesinde olur.</span><span class="sxs-lookup"><span data-stu-id="3efc4-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="3efc4-221">Merhaba lombok.jar dosyasını indirdikten sonra buna çift tıklayarak tooinstall onu veya hello komut satırından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3efc4-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="3efc4-222">Eclipse açıksa kapatın ve tooload Lombok yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="3efc4-223">Eclipse'te, hello **dosya** menüsünde tıklatın **alma**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="3efc4-224">Merhaba, **alma** penceresinde, tıklatın **Git**, tıklatın **Git projeleri**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="3efc4-225">Merhaba üzerinde **depo kaynağı seçin** ekranında **URI'yi kopyalama**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="3efc4-226">Merhaba üzerinde **kaynak Git deposu** ekranında hello **URI** kutusuna https://github.com/Azure-Samples/java-todo-app.git girin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="3efc4-227">Merhaba üzerinde **dal seçimi** ekranında, emin **ana** seçilir ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="3efc4-228">Merhaba üzerinde **yerel hedef** ekranında **Gözat** tooselect burada hello deposu kopyalanabilir ve ardından bir klasörü **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="3efc4-229">Merhaba üzerinde **projeleri İçeri Aktarma Sihirbazı'nı toouse seçin** ekranında, emin **var olan projeleri içeri aktar** seçilir ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="3efc4-230">Merhaba üzerinde **projeleri içeri aktar** ekran, Seçimi Kaldır hello **DocumentDB** proje ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="3efc4-231">Merhaba DocumentDB projesi hello Azure Cosmos DB Java biz bağımlılık olarak ekleyeceğimiz SDK içerir.</span><span class="sxs-lookup"><span data-stu-id="3efc4-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="3efc4-232">İçinde **Proje Gezgini**, tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java gidin ve hello URI ve birincil anahtar hello HOST ve MASTER_KEY değerlerini değiştirin Azure Cosmos DB hesabını tıklatın ve ardından Kaydet hello dosya.</span><span class="sxs-lookup"><span data-stu-id="3efc4-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="3efc4-233">Daha fazla bilgi için bkz. [1. Adım. Bir Azure Cosmos DB veritabanı hesabı oluşturma](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="3efc4-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="3efc4-234">İçinde **Proje Gezgini**, hello sağ tıklayın **azure-documentdb-java-sample**, tıklatın **yapı yolu**ve ardından **oluşturma yolunu Yapılandır**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="3efc4-235">Merhaba üzerinde **Java oluşturma yolu** , hello sağ bölmede, select Merhaba ekranında **kitaplıkları** sekmesini ve ardından **dış Jar'lar Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="3efc4-236">Merhaba lombok.jar dosyasının konumunu toohello gidin ve tıklayın **açık**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="3efc4-237">Kullanım 12. adımı tooopen hello **özellikleri** penceresini tekrar ve ardından hello sol bölmedeki tıklatın **hedeflenen çalışma zamanları**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="3efc4-238">Merhaba üzerinde **hedeflenen çalışma zamanları** ekranında **yeni**seçin **Apache Tomcat v7.0**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="3efc4-239">Kullanım 12. adımı tooopen hello **özellikleri** penceresini tekrar ve ardından hello sol bölmedeki tıklatın **proje modelleri**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="3efc4-240">Merhaba üzerinde **proje modelleri** ekran, select **dinamik Web Modülü** ve **Java**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="3efc4-241">Merhaba üzerinde **sunucuları** sekmesinde hello ekranın hello altında sağ **Server localhost'ta Tomcat v7.0** ve ardından **ekleme ve kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="3efc4-242">Merhaba üzerinde **ekleme ve kaldırma** penceresinde taşıma **azure-documentdb-java-sample** toohello **yapılandırıldı** kutusuna ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="3efc4-243">Merhaba, **sunucuları** sekmesinde, sağ **Server localhost'ta Tomcat v7.0**ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="3efc4-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="3efc4-244">Bir tarayıcıda toohttp://localhost:8080 gidin / azure-documentdb-java-sample / ve tooyour görev listesi eklemeye başlayın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="3efc4-245">Varsayılan bağlantı noktası değerlerini değiştirdiyseniz, seçtiğiniz 8080 toohello değerini değiştirin unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3efc4-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="3efc4-246">toodeploy, proje tooan Azure web sitesine bakın [adım 6. Uygulama tooAzure Web sitelerini dağıtmak](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="3efc4-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
