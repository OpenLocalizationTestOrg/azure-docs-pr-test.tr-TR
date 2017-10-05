---
title: "Azure Cosmos DB kullanarak Java uygulaması geliştirme öğreticisi | Microsoft Docs"
description: "Bu Java web uygulaması Öğreticisi Azure Web Siteleri'nde barındırılan bir Java uygulaması erişim verileri ve Azure Cosmos DB ve DocumentDB API depolamak için nasıl kullanılacağını gösterir."
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
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="8826d-104">Azure Cosmos DB ve DocumentDB API kullanarak bir Java web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8826d-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8826d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="8826d-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="8826d-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8826d-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="8826d-107">Java</span><span class="sxs-lookup"><span data-stu-id="8826d-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="8826d-108">Python</span><span class="sxs-lookup"><span data-stu-id="8826d-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="8826d-109">Bu Java web uygulaması Öğreticisi nasıl kullanılacağını gösterir [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) depolamak ve Azure App Service Web Apps üzerinde barındırılan bir Java uygulamasında verilere erişmek için hizmet.</span><span class="sxs-lookup"><span data-stu-id="8826d-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="8826d-110">Bu konu başlığında şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="8826d-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="8826d-111">Eclipse'te temel bir JavaServer sayfaları (JSP) uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8826d-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="8826d-112">[Azure Cosmos DB Java SDK’sı](https://github.com/Azure/azure-documentdb-java) kullanılarak Azure Cosmos DB hizmetiyle çalışma.</span><span class="sxs-lookup"><span data-stu-id="8826d-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="8826d-113">Bu Java uygulaması öğreticisi görevleri oluşturmanızı, almanızı ve aşağıdaki görüntüde gösterilen şekilde tamamlandı olarak işaretlemenizi sağlayan bir web tabanlı görev yönetimi uygulamasını nasıl oluşturacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8826d-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="8826d-114">Yapılacaklar listesindeki görevlerin her biri, Azure Cosmos DB'de JSON belgeleri olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="8826d-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Yapılacaklar Listesi Java uygulamam](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="8826d-116">Bu uygulama geliştirme öğreticisi, Java kullanımına ilişkin deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8826d-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="8826d-117">Java veya [önkoşul araçlarında](#Prerequisites) yeniyseniz GitHub'dan [yapılacaklar](https://github.com/Azure-Samples/documentdb-java-todo-app) projesinin tamamını indirmenizi ve [bu makalenin sonundaki yönergeleri](#GetProject) kullanarak projeyi oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8826d-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="8826d-118">Oluşturduktan sonra, proje bağlamında kodu daha iyi kavramak için makaleyi inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8826d-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="8826d-119"><a id="Prerequisites"></a>Bu Java web uygulaması öğreticisi için önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8826d-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="8826d-120">Bu uygulama geliştirme öğreticisine başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8826d-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="8826d-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="8826d-121">An active Azure account.</span></span> <span data-ttu-id="8826d-122">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8826d-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="8826d-123">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="8826d-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="8826d-124">OR</span><span class="sxs-lookup"><span data-stu-id="8826d-124">OR</span></span>

    <span data-ttu-id="8826d-125">Yerel bir [Azure Cosmos DB Öykünücüsü](local-emulator.md) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="8826d-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="8826d-126">[Java Geliştirme Seti (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="8826d-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="8826d-127">Java EE Geliştiricileri için Eclipse IDE.</span><span class="sxs-lookup"><span data-stu-id="8826d-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="8826d-128">Etkin bir Java Çalışma zamanı ortamı (ör. Tomcat veya Jetty) sahip bir Azure Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="8826d-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="8826d-129">Bu araçları ilk kez yüklüyorsanız coreservlets.com adresindeki [Öğretici: TomCat7'yi yükleme ve Eclipse ile kullanma](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) makalesinin Hızlı Başlangıç bölümünde yükleme işlem için bir adım adım kılavuz mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="8826d-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="8826d-130"><a id="CreateDB"></a>1. adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8826d-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="8826d-131">İlk olarak bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="8826d-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="8826d-132">Zaten bir hesabınız varsa veya bu öğretici için Azure Cosmos DB Öykünücüsü’nü kullanıyorsanız [2. Adım: Java JSP uygulaması oluşturma](#CreateJSP) adımına atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8826d-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="8826d-133"><a id="CreateJSP"></a>2. Adım: Java JSP uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="8826d-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="8826d-134">JSP uygulaması oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="8826d-134">To create the JSP application:</span></span>

1. <span data-ttu-id="8826d-135">İlk olarak, bir Java projesi oluşturarak başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="8826d-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="8826d-136">Eclipse'i başlatın, ardından **Dosya**'ya tıklayın, **Yeni**'ye tıklayın ve ardından **Dinamik Web Projesi**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="8826d-137">Kullanılabilir bir proje olarak **Dinamik Web Projesi**'ni listelenmiş şekilde görmüyorsanız şunu yapın: **Dosya**'ya tıklayın, **Yeni**'ye tıklayın, **Proje**… seçeneğine tıklayın, **Web**'i genişletin, **Dinamik Web Projesi**'ne tıklayın ve **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java Uygulaması Geliştirme](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="8826d-139">**Proje adı** kutusuna bir proje adı girin ve **Hedef Çalışma Zamanı** açılan menüsünde isteğe bağlı olarak bir değer seçin (ör. Apache Tomcat v7.0) ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="8826d-140">Bir hedef çalışma zamanının seçilmesi, projenizi Eclipse aracılığıyla yerel olarak çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8826d-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="8826d-141">Eclipse'te Proje Gezgini görünümünde projenizi genişletin.</span><span class="sxs-lookup"><span data-stu-id="8826d-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="8826d-142">**WebContent**'e sağ tıklayın, **Yeni**'ye tıklayın ve ardından **JSP Dosyası**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="8826d-143">**Yeni JSP Dosyası** iletişim kutusunda dosyaya **index.jsp** adını verin.</span><span class="sxs-lookup"><span data-stu-id="8826d-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="8826d-144">Üst klasörü aşağıdaki resimde gösterildiği gibi **WebContent** olarak tutun ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Yeni bir JSP Dosyası Oluşturma - Java Web Uygulaması Öğreticisi](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="8826d-146">**Select JSP Template (JSP Şablon Seçme)** iletişim kutusunda bu öğreticinin amacı doğrultusunda **New JSP File (html) (Yeni JSP Dosyası (html))** seçeneğini belirleyin ve ardından **Finish (Son)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="8826d-147">index.jsp dosyası Eclipse'te açıldığında, var olan **öğesinin içinde**</span><span class="sxs-lookup"><span data-stu-id="8826d-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="8826d-148"><body>Hello World! (Merhaba Dünya!) ifadesinin görüntülenmesi için metni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8826d-148">within the existing <body> element.</span></span> <span data-ttu-id="8826d-149">Güncelleştirilmiş <body> içeriğiniz aşağıdaki kod gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="8826d-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="8826d-150">index.jsp dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8826d-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="8826d-151">2 adımda bir hedef çalışma zamanı ayarlarsanız **Proje**'ye ve ardından **Çalıştır**'a tıklayıp JSP uygulamanızı yerel olarak çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8826d-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World - Java Uygulaması Öğreticisi](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="8826d-153"><a id="InstallSDK"></a>3. Adım: DocumentDB Java SDK'sını yükleme</span><span class="sxs-lookup"><span data-stu-id="8826d-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="8826d-154">[Apache Maven](http://maven.apache.org/), DocumentDB Java SDK'sını ve bağımlılıklarını çekmenin en kolay yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="8826d-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="8826d-155">Bunu yapmak için aşağıdaki adımları tamamlayarak projenizi bir Maven projesine dönüştürmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="8826d-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="8826d-156">Proje Gezgini'nde projenize sağ tıklayın, **Yapılandır**'a tıklayın, **Maven Projesine Dönüştür**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="8826d-157">**Yeni POM oluştur** penceresinde varsayılanları kabul edin ve **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="8826d-158">**Proje Gezgini**'nde pom.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="8826d-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="8826d-159">**Bağımlılıklar** sekmesindeki **Bağımlılıklar** bölmesinde **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="8826d-160">**Bağımlılık Seç** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8826d-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="8826d-161">İçinde **Grup Kimliği** kutusuna, com.microsoft.azure girin.</span><span class="sxs-lookup"><span data-stu-id="8826d-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="8826d-162">İçinde **Artifact ID** kutusuna, azure-documentdb girin.</span><span class="sxs-lookup"><span data-stu-id="8826d-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="8826d-163">İçinde **sürüm** kutusuna, 1.5.1 girin.</span><span class="sxs-lookup"><span data-stu-id="8826d-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java Uygulaması SDK'sını yükleme](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="8826d-165">Veya bağımlılık XML'sini grup kimliği ve yapı kimliği için doğrudan bir metin düzenleyicisi aracılığıyla pom.XML'ye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8826d-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="8826d-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="8826d-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="8826d-167">Tıklatın **Tamam** ve Maven DocumentDB Java SDK'sını yükler.</span><span class="sxs-lookup"><span data-stu-id="8826d-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="8826d-168">Pom.xml dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8826d-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="8826d-169"><a id="UseService"></a>4. Adım: Azure Cosmos DB hizmetini bir Java uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="8826d-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="8826d-170">İlk olarak, Todoıtem nesnesini TodoItem.java içinde şimdi tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="8826d-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="8826d-171">Bu projede oluşturucuyu, alıcıları ve ayarlayıcıları oluşturmak için [Project Lombok](http://projectlombok.org/)'u kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="8826d-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="8826d-172">Alternatif olarak, bu kodu el ile yazabilir veya IDE'nin oluşturmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8826d-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="8826d-173">Azure Cosmos DB hizmetini çağırmak için yeni bir **DocumentClient** örneği oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8826d-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="8826d-174">Genel olarak, sonraki her istek için yeni bir istemci oluşturmak yerine **DocumentClient**'ı tekrar kullanmak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="8826d-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="8826d-175">İstemciyi bir **DocumentClientFactory**'ye sarmalayarak tekrar kullanabiliriz.</span><span class="sxs-lookup"><span data-stu-id="8826d-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="8826d-176">DocumentClientFactory.java içinde kaydettiğiniz panonuza URI ve birincil anahtar değeri yapıştırmanız gereken [1. adım](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="8826d-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="8826d-177">[YOUR\_ENDPOINT\_HERE] yerine URI'nizi ve [YOUR\_KEY\_HERE] yerine BİRİNCİL ANAHTARINIZI girin.</span><span class="sxs-lookup"><span data-stu-id="8826d-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="8826d-178">Şimdi Yapılacaklar öğelerimizi Azure Cosmos DB'de kalıcı hale getirmeyi özetlemek için bir Veri Erişim Nesnesi (DAO) oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="8826d-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="8826d-179">Yapılacaklar öğelerini bir koleksiyona kaydetmek için, istemcinin hangi veritabanı ve koleksiyona kalıcı hale getireceğini (kendine bağlantılar tarafından başvurulduğu üzere) bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8826d-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="8826d-180">Genel olarak, veritabanına ek gidiş gelişleri önlemek için veritabanı ve koleksiyonu mümkün olduğunda ön belleğe almak en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="8826d-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="8826d-181">Aşağıdaki kod, veritabanımızın ve koleksiyonumuzun varsa nasıl alınacağını veya yoksa yenisinin nasıl oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="8826d-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="8826d-182">Sonraki adım, TodoItems öğelerini koleksiyonda kalıcı hale getirmek için biraz kod yazmaktır.</span><span class="sxs-lookup"><span data-stu-id="8826d-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="8826d-183">Bu örnekte TodoItem Eski Basit Java Nesnelerini (POJO'lar) JSON belgelerine seri hale getirmek ve seri durumdan çıkarmak için [Gson](https://code.google.com/p/google-gson/)'u kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="8826d-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="8826d-184">Azure Cosmos DB veritabanları ve koleksiyonlarına benzer şekilde belgelere de kendine bağlantılar tarafından başvurulur.</span><span class="sxs-lookup"><span data-stu-id="8826d-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="8826d-185">Aşağıdaki yardımcı işlevi, belgeleri kendine bağlantı yerine başka bir öznitelik (ör. "id") aracılığıyla almamızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="8826d-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
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
6. <span data-ttu-id="8826d-186">Id ile bir TodoItem JSON belgesini alıp ardından bunu bir POJO'ya seri durumdan çıkarmak için 5. adımdaki yardımcı yöntemi kullanabiliriz:</span><span class="sxs-lookup"><span data-stu-id="8826d-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="8826d-187">DocumentDB SQL kullanarak bir koleksiyonu veya TodoItems listesini almak için DocumentClient'ı da kullanabiliriz:</span><span class="sxs-lookup"><span data-stu-id="8826d-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="8826d-188">DocumentClient ile bir belgeyi güncelleştirmenin birçok yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="8826d-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="8826d-189">Yapılacaklar listesi uygulamamızda bir TodoItem'ın tamamlandı ve tamamlanmadı durumları arasında geçiş yapabilmek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8826d-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="8826d-190">Belgenin içinde "tamamlandı" özniteliğini güncelleştirerek bunu yapabiliriz:</span><span class="sxs-lookup"><span data-stu-id="8826d-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="8826d-191">Son olarak, listemizden bir TodoItem'ı silebilmek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="8826d-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="8826d-192">Bunu yapmak için daha önce yazmış olduğumuz yardımcı yöntemi kullanarak kendine bağlantıyı alıp ardından istemciye bunu silmesini söyleyebiliriz:</span><span class="sxs-lookup"><span data-stu-id="8826d-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="8826d-193"><a id="Wire"></a>5. Adım: Java uygulaması geliştirme projesinin geriye kalan kısmını bağlama</span><span class="sxs-lookup"><span data-stu-id="8826d-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="8826d-194">Biz eğlenceli kısımları tamamladığımıza göre şimdi - kalan tüm bittir Hızlı kullanıcı arabirimi oluşturma ve bunu dao'muza.</span><span class="sxs-lookup"><span data-stu-id="8826d-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="8826d-195">İlk olarak, DAO'muzu çağırmak için bir denetleyici oluşturmakla başlayalım:</span><span class="sxs-lookup"><span data-stu-id="8826d-195">First, let's start with building a controller to call our DAO:</span></span>
   
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
   
    <span data-ttu-id="8826d-196">Karmaşık bir uygulamada, denetleyici DAO'nun üstünde karmaşık bir iş mantığı barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="8826d-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="8826d-197">Ardından, HTTP isteklerini denetleyiciye yönlendirmek için bir servlet oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="8826d-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
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
3. <span data-ttu-id="8826d-198">Kullanıcıya görüntülenecek web kullanıcı arabirimi ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="8826d-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="8826d-199">Daha önce oluşturduğumuz index.jsp'yi yeniden yazalım:</span><span class="sxs-lookup"><span data-stu-id="8826d-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
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
   
            <!-- The ToDo List -->
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
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="8826d-200">Ve son olarak, web kullanıcı arabirimi ile servlet'i birbirine bağlamak için bazı istemci tarafı JavaScript'i yazın:</span><span class="sxs-lookup"><span data-stu-id="8826d-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
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
   
              // Call api to update todo items.
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
           * Install the TodoApp
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
5. <span data-ttu-id="8826d-201">Harika!</span><span class="sxs-lookup"><span data-stu-id="8826d-201">Awesome!</span></span> <span data-ttu-id="8826d-202">Şimdi geriye yalnızca uygulamayı test etmek kaldı.</span><span class="sxs-lookup"><span data-stu-id="8826d-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="8826d-203">Uygulamayı yerel olarak çalıştırın, ardından öğe adı ve kategoriyi doldurarak ve **Görev Ekle**'ye tıklayarak birkaç Yapılacaklar öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8826d-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="8826d-204">Öğe göründükten sonra, onay kutusundaki işareti değiştirip **Görevleri Güncelleştir**'e tıklayarak öğeyi tamamlandı veya tamamlanmadı olarak güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8826d-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="8826d-205"><a id="Deploy"></a>6. adım: Java uygulamanızı Azure Web siteleri için dağıtma</span><span class="sxs-lookup"><span data-stu-id="8826d-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="8826d-206">Uygulamanızı bir WAR dosyası olarak dışarı aktarma ve ya da kaynak denetimi (ör. Gıt) veya FTP aracılığıyla karşıya kadar basit Java uygulamalarını dağıtma azure Web siteleri yapar.</span><span class="sxs-lookup"><span data-stu-id="8826d-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="8826d-207">Uygulamanızı bir WAR dosyası olarak dışarı aktarmak için projenize sağ tıklayın **Proje Gezgini**, tıklatın **verme**ve ardından **WAR dosyasını**.</span><span class="sxs-lookup"><span data-stu-id="8826d-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="8826d-208">**WAR Dışarı Aktar** penceresinde aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8826d-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="8826d-209">Web projesi kutusuna azure-documentdb-java-sample metnini girin.</span><span class="sxs-lookup"><span data-stu-id="8826d-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="8826d-210">Hedef kutusunda WAR dosyasını kaydetmek için bir hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="8826d-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="8826d-211">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-211">Click **Finish**.</span></span>
3. <span data-ttu-id="8826d-212">Eldeki elinizde bir WAR dosyası, yalnızca bunu Azure Web sitenizin için yükleyebilirsiniz **webapps** dizin.</span><span class="sxs-lookup"><span data-stu-id="8826d-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="8826d-213">Dosyayı karşıya yükleme ile ilgili yönergeler için bkz: [Azure App Service Web Apps bir Java uygulama eklemek](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="8826d-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="8826d-214">WAR dosyası webapps dizinine yüklendikten sonra, çalışma zamanı ortamı bunu eklemiş olduğunuzu algılar ve otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="8826d-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="8826d-215">Tamamlanmış ürününüzü görmek için http://YOUR için gidin\_SITE\_NAME.azurewebsites.net/azure-java-sample/ ve görevlerinizi eklemeye başlayın!</span><span class="sxs-lookup"><span data-stu-id="8826d-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="8826d-216"><a id="GetProject"></a>Projeyi GitHub'dan alma</span><span class="sxs-lookup"><span data-stu-id="8826d-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="8826d-217">Bu öğreticideki tüm örnekler GitHub'daki [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projesinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="8826d-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="8826d-218">todo projesini Eclipse'e aktarmak için [Önkoşullar](#Prerequisites) bölümünde listelenen yazılım ve kaynaklara sahip olduğunuzdan emin olun ve ardından aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="8826d-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="8826d-219">[Proje Lombok](http://projectlombok.org/)'u yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8826d-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="8826d-220">Lombok projede oluşturucular, alıcılar ve ayarlayıcılar oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8826d-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="8826d-221">Lombok.jar dosyasını indirdikten sonra, yüklemek için buna çift tıklayın veya komut satırından yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8826d-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="8826d-222">Eclipse açıksa kapatın ve Lombok'u yüklemek için yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="8826d-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="8826d-223">Eclipse'te **Dosya** menüsünde **İçeri Aktar**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="8826d-224">**İçeri Aktar** penceresinde **Git**'e tıklayın, **Git Projeleri**'ne tıklayın ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="8826d-225">**Depo Kaynağı Seçin** ekranında **URI'yi kopyalama**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="8826d-226">Üzerinde **kaynak Git deposu** ekranında **URI** kutusuna https://github.com/Azure-Samples/java-todo-app.git girin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="8826d-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="8826d-227">**Dal Seçimi** ekranında **master**'ın seçili olduğundan emin olun ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="8826d-228">**Yerel Hedef** ekranında deponun kopyalanabileceği bir klasör seçmek için **Gözat**'a tıklayın ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="8826d-229">**Projeleri içeri aktarmada kullanmak için sihirbaz seçin** ekranında **Var olan projeleri içeri aktar**'ın seçili olduğundan emin olun ve ardından **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="8826d-230">**Projeleri İçeri Aktar** ekranında **DocumentDB** projesinin seçimini kaldırın ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="8826d-231">DocumentDB projesi Azure Cosmos DB Java biz bağımlılık olarak ekleyeceğimiz SDK içerir.</span><span class="sxs-lookup"><span data-stu-id="8826d-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="8826d-232">İçinde **Proje Gezgini**, azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java için gidin ve HOST ve MASTER_KEY değerlerini URI ve birincil anahtar yerine, Azure Cosmos DB hesap ve ardından dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8826d-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="8826d-233">Daha fazla bilgi için bkz. [1. Adım. Bir Azure Cosmos DB veritabanı hesabı oluşturma](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="8826d-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="8826d-234">**Proje Gezgini**'nde **azure-documentdb-java-sample**'a sağ tıklayın, **Yapı Yolu**'na tıklayın ve ardından **Oluşturma Yolunu Yapılandır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="8826d-235">**Java Oluşturma Yolu** ekranında sağ bölmedeki **Kitaplıklar** sekmesini seçin ve ardından **Dış JAR'lar Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="8826d-236">Lombok.jar dosyasının konumuna gidin, **Aç**'a tıklayın ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="8826d-237">**Özellikler** penceresini tekrar açmak için 12. adımı kullanın ve ardından sol bölmedeki **Hedeflenen Çalışma Zamanları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="8826d-238">**Hedeflenen Çalışma Zamanları** ekranında **Yeni**'ye tıklayın, **Apache Tomcat v7.0**'ı seçin ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="8826d-239">**Özellikler** penceresini tekrar açmak için 12. adımı kullanın ve ardından sol bölmedeki **Proje Modelleri**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="8826d-240">**Proje Modelleri** ekranında **Dinamik Web Modülü**'nü ve **Java**'yı seçin ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="8826d-241">Ekranın en altındaki **Sunucular** sekmesinde **Localhost'ta Tomcat v7.0 Sunucusu**'na sağ tıklayın ve ardından **Ekle ve Kaldır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="8826d-242">**Ekle ve Kaldır** penceresinde **azure-documentdb-java-sample**'ı **Yapılandırılmış** kutusuna taşıyın ve ardından **Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="8826d-243">İçinde **sunucuları** sekmesinde, sağ **Server localhost'ta Tomcat v7.0**ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="8826d-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="8826d-244">Bir tarayıcıda http://localhost:8080/azure-documentdb-java-sample/ adresine gidin ve görev listenize eklemeye başlayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="8826d-245">Varsayılan bağlantı noktası değerlerinizi değiştirdiyseniz 8080'i seçtiğiniz değere değiştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8826d-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="8826d-246">Projenizi bir Azure web sitesine dağıtmak için bkz. [6. Adım. Uygulamanızı Azure Web siteleri için dağıtmak](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="8826d-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
