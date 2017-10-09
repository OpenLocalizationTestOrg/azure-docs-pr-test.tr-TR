---
title: "Java'da Azure Search ile çalışmaya aaaGet | Microsoft Docs"
description: "Nasıl toobuild barındırılan bir bulut uygulama programlama diliniz olarak Java kullanarak Azure üzerinde arayın."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="e1010-103">Java'da Azure Search kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e1010-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1010-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e1010-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="e1010-105">.NET</span><span class="sxs-lookup"><span data-stu-id="e1010-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="e1010-106">Nasıl toobuild özel bir Java arama arama deneyimi için Azure Search kullanan uygulamayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e1010-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="e1010-107">Bu öğretici hello kullanır [Azure Search Hizmeti REST API'si](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello nesneleri ve bu alıştırmada kullanılan işlemleri.</span><span class="sxs-lookup"><span data-stu-id="e1010-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="e1010-108">toorun hello için kaydolabilirsiniz bir Azure Search hizmeti bu örnek olmalıdır [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1010-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="e1010-109">Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="e1010-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="e1010-110">Biz yazılım toobuild aşağıdaki hello kullanılan ve bu örnek test edin:</span><span class="sxs-lookup"><span data-stu-id="e1010-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="e1010-111">[Java EE Geliştiricileri için Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="e1010-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="e1010-112">Toodownload hello EE sürümünü emin olun.</span><span class="sxs-lookup"><span data-stu-id="e1010-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="e1010-113">Hello doğrulama adımlardan biri, yalnızca bu sürümde bulunan bir özelliği gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1010-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="e1010-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="e1010-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="e1010-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="e1010-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="e1010-116">Merhaba veri hakkında</span><span class="sxs-lookup"><span data-stu-id="e1010-116">About hello data</span></span>
<span data-ttu-id="e1010-117">Bu örnek uygulama hello verileri kullanan [Birleşik Devletler Jeoloji Hizmetleri (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrelenmiş hello Rhode Island eyaleti tooreduce hello veri kümesi boyutu.</span><span class="sxs-lookup"><span data-stu-id="e1010-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="e1010-118">Bu veri toobuild akışlar, Göller ve zirveler gibi jeolojik özelliklerin yanı sıra hastaneler ve okullar gibi önemli binaları döndüren bir arama uygulaması kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e1010-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="e1010-119">Bu uygulamada hello **SearchServlet.java** programı oluşturup yükleri hello dizini kullanarak bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/dn798918.aspx) hello alma yapısı, filtrelenmiş USGS veri kümesini ortak bir Azure SQL veritabanından.</span><span class="sxs-lookup"><span data-stu-id="e1010-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="e1010-120">Önceden tanımlanmış kimlik bilgileri ve bağlantı bilgileri toohello çevrimiçi veri kaynağı hello program kodu içinde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e1010-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="e1010-121">Veri erişimi açısından ek yapılandırma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e1010-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="e1010-122">Bu veri kümesi toostay hello 10.000 belge limiti hello ücretsiz fiyatlandırma katmanı altında üzerinde bir filtre uygulanmış.</span><span class="sxs-lookup"><span data-stu-id="e1010-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="e1010-123">Merhaba standart katmanı kullanırsanız bu limit uygulanmaz ve bu kodu toouse büyük bir veri kümesini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e1010-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="e1010-124">Her fiyatlandırma katmanının kapasitesi hakkında ayrıntılı bilgi için bkz: [Limitler ve kısıtlamalar](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="e1010-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="e1010-125">Merhaba program dosyaları hakkında</span><span class="sxs-lookup"><span data-stu-id="e1010-125">About hello program files</span></span>
<span data-ttu-id="e1010-126">Merhaba aşağıdaki listede ilgili toothis örnek hello dosyaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e1010-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="e1010-127">Search.jsp: hello kullanıcı arabirimi sağlar</span><span class="sxs-lookup"><span data-stu-id="e1010-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="e1010-128">SearchServlet.java: yöntemler (benzer tooa denetleyicisi MVC) sağlar</span><span class="sxs-lookup"><span data-stu-id="e1010-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="e1010-129">SearchServiceClient.java: HTTP isteklerini işler</span><span class="sxs-lookup"><span data-stu-id="e1010-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="e1010-130">SearchServiceHelper.java: Statik yöntemler sağlayan bir yardımcı sınıfı</span><span class="sxs-lookup"><span data-stu-id="e1010-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="e1010-131">Document.Java: hello veri modeli sağlar</span><span class="sxs-lookup"><span data-stu-id="e1010-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="e1010-132">Config.Properties: hello Search Hizmeti URL'sini ve api anahtarını ayarlar</span><span class="sxs-lookup"><span data-stu-id="e1010-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="e1010-133">Pom.xml: Maven bağımlılığı</span><span class="sxs-lookup"><span data-stu-id="e1010-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="e1010-134">Merhaba hizmet adı ve Azure Search hizmetinizin api anahtarını bulma</span><span class="sxs-lookup"><span data-stu-id="e1010-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="e1010-135">Azure Search tüm REST API çağrıları hello hizmet URL'sini ve api anahtarı sağlamanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1010-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="e1010-136">İçinde toohello oturum [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e1010-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e1010-137">Merhaba atlama çubuğunda, **Search Hizmeti** aboneliğiniz için sağlanan tüm hello Azure arama hizmetleri toolist.</span><span class="sxs-lookup"><span data-stu-id="e1010-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="e1010-138">Toouse istediğiniz hello hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="e1010-139">Merhaba hizmet panosunda yanı sıra hello yönetici anahtarlarına erişim için anahtar simgesine hello önemli bilgiler için kutucuklar görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e1010-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="e1010-140">Merhaba hizmet URL'sini ve bir yönetici anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="e1010-141">Toohello eklediğinizde, bunları daha sonra gerekecektir **config.properties** dosya.</span><span class="sxs-lookup"><span data-stu-id="e1010-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="e1010-142">Merhaba örnek dosyalarını indirme</span><span class="sxs-lookup"><span data-stu-id="e1010-142">Download hello sample files</span></span>
1. <span data-ttu-id="e1010-143">Çok Git[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) github'da.</span><span class="sxs-lookup"><span data-stu-id="e1010-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="e1010-144">Tıklatın **ZIP'i indir**hello .zip dosyası toodisk kaydedin ve ardından içerdiği tüm hello dosyaları ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="e1010-145">Ayıklamayı göz önünde bulundurun hello dosyalarının, Java Çalışma toomake daha kolay toofind hello proje daha sonra.</span><span class="sxs-lookup"><span data-stu-id="e1010-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="e1010-146">Merhaba örnek dosyaları salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="e1010-146">hello sample files are read-only.</span></span> <span data-ttu-id="e1010-147">Klasör özelliklerini ve Temizle hello salt okunur özniteliğini sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e1010-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="e1010-148">Sonraki tüm dosya değişiklikleri ve çalıştırma deyimleri bu klasördeki dosyalara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="e1010-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="e1010-149">Projeyi içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="e1010-149">Import project</span></span>
1. <span data-ttu-id="e1010-150">Eclipse'te, **File (Dosya)** > **Import (İçeri Aktar)** > **General (Genel)** > **Existing Projects into Workspace (Var olan Projeleri Çalışma Alanına)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e1010-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="e1010-151">İçinde **Select kök dizini**, örnek dosyaları içeren toohello klasörüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="e1010-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="e1010-152">Merhaba proje klasörünü içeren hello klasörü seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="e1010-153">Merhaba proje hello görünmelidir **projeleri** seçili öğe olarak listesi.</span><span class="sxs-lookup"><span data-stu-id="e1010-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="e1010-154">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-154">Click **Finish**.</span></span>
4. <span data-ttu-id="e1010-155">Kullanım **Proje Gezgini** tooview ve düzenleme hello dosyaları.</span><span class="sxs-lookup"><span data-stu-id="e1010-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="e1010-156">Zaten açık değilse, tıklatın **penceresi** > **görünümü göster** > **Proje Gezgini** veya hello kısayol tooopen kullanın.</span><span class="sxs-lookup"><span data-stu-id="e1010-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="e1010-157">Merhaba hizmet URL'si ve api anahtarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e1010-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="e1010-158">İçinde **Proje Gezgini**, çift **config.properties** hello sunucu adını ve api anahtarını içeren tooedit hello yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="e1010-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="e1010-159">Burada bulunan hello hizmet URL'sini ve api anahtarını hello daha önce bu makalede toohello adımları başvurun [Azure Portal](https://portal.azure.com), tooget hello değerleri şimdi girdiğiniz içine **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="e1010-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="e1010-160">İçinde **config.properties**, "Api anahtarı" Merhaba hizmetinizin api anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e1010-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="e1010-161">Ardından, hizmet adı (Merhaba URL http://servicename.search.windows.net hello ilk bileşeni) "hizmet adı" hello yerine geçer aynı dosya.</span><span class="sxs-lookup"><span data-stu-id="e1010-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="e1010-162">Merhaba proje, derleme ve çalışma zamanı ortamları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e1010-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="e1010-163">Eclipse'te, proje Gezgini'nde hello projesine sağ tıklayın > **özellikleri** > **proje modelleri**.</span><span class="sxs-lookup"><span data-stu-id="e1010-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="e1010-164">**Dynamic Web Module (Dinamik Web Modülü)** öğesini, **Java**'yı ve **JavaScript**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="e1010-165">**Apply (Uygula)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-165">Click **Apply**.</span></span>
4. <span data-ttu-id="e1010-166">**Window (Pencere)** > **Preferences (Tercihler)** > **Server (Sunucu)** > **Runtime Environments (Çalışma Zamanı Ortamları)** > **Add... (Ekle...)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="e1010-167">Apache genişletin ve daha önce yüklediğiniz hello Apache Tomcat sunucusunu hello sürümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="e1010-168">Sistemimizde sürüm 8 yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="e1010-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="e1010-169">Merhaba sonraki sayfada hello Tomcat yükleme dizinini belirtin.</span><span class="sxs-lookup"><span data-stu-id="e1010-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="e1010-170">Windows bilgisayarda, bu büyük olasılıkla C:\Program Files\Apache Software Foundation\Tomcat *sürüm* olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e1010-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="e1010-171">**Finish (Son)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-171">Click **Finish**.</span></span>
8. <span data-ttu-id="e1010-172">**Window (Pencere)** > **Preferences (Tercihler)** > **Java** > **Installed JREs (Yüklü JRE'ler)** > **Add (Ekle)** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e1010-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="e1010-173">**Add JRE (JRE Ekle)** bölümünde **Standard VM (Standart VM)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="e1010-174">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-174">Click **Next**.</span></span>
11. <span data-ttu-id="e1010-175">JRE Tanımı'nda, JRE giriş alanında **Directory (Dizin)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="e1010-176">Çok gidin**Program Files** > **Java** ve hello daha önce yüklediğiniz JDK seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="e1010-177">Bu önemli tooselect hello JDK hello JRE gösterir.</span><span class="sxs-lookup"><span data-stu-id="e1010-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="e1010-178">Yüklü Jre'ler içinde hello seçin **JDK**.</span><span class="sxs-lookup"><span data-stu-id="e1010-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="e1010-179">Ayarlarınız aşağıdaki ekran görüntüsüne benzer toohello görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="e1010-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="e1010-180">İsteğe bağlı olarak, seçin **penceresi** > **Web tarayıcısı** > **Internet Explorer** tooopen Merhaba uygulaması bir dış tarayıcı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="e1010-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="e1010-181">Dış tarayıcı kullanmanız daha iyi bir Web uygulaması deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e1010-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="e1010-182">Merhaba yapılandırma görevlerini tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="e1010-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="e1010-183">Ardından, yapı ve Merhaba projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e1010-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="e1010-184">Merhaba projeyi derleme</span><span class="sxs-lookup"><span data-stu-id="e1010-184">Build hello project</span></span>
1. <span data-ttu-id="e1010-185">Proje Gezgini'nde hello proje adına sağ tıklayın ve seçin **Çalıştır** > **Maven build...**  tooconfigure hello projesi.</span><span class="sxs-lookup"><span data-stu-id="e1010-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="e1010-186">Edit Configuration (Yapılandırmayı Düzenle) alanında Targets (Hedefler) için "clean install" ("temiz yükleme") yazın ve ardından **Run (Çalıştır)** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="e1010-187">Durum iletileri çıktı toohello konsol penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="e1010-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="e1010-188">Yapı Başarısı hatasız yerleşik belirten hello proje görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1010-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="e1010-189">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e1010-189">Run hello app</span></span>
<span data-ttu-id="e1010-190">Bu son adımda, bir yerel sunucu çalışma zamanı ortamında hello uygulama çalışacaktır.</span><span class="sxs-lookup"><span data-stu-id="e1010-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="e1010-191">Eclipse'te henüz bir sunucu çalışma zamanı ortamı belirtmediyseniz öncelikle toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1010-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="e1010-192">Proje Gezgini'nde **WebContent**'i genişletin.</span><span class="sxs-lookup"><span data-stu-id="e1010-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="e1010-193">**Search.jsp** > **Run As (Farklı Çalıştır)** > **Run on Server (Sunucuda Çalıştır)** öğesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="e1010-194">Merhaba Apache Tomcat sunucusunu seçin ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="e1010-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="e1010-195">Varsayılan olmayan çalışma toostore projenizi kullandıysanız, toomodify gerekir **yapılandırma Çalıştır** toopoint toohello proje konumu tooavoid sunucu başlangıç hatasını.</span><span class="sxs-lookup"><span data-stu-id="e1010-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="e1010-196">Proje Gezgini'nde **Search.jsp** > **Run As (Farklı Çalıştır)** > **Run Configurations (Yapılandırmaları Çalıştır)** öğesine sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="e1010-197">Merhaba Apache Tomcat sunucusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1010-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="e1010-198">**Arguments (Bağımsız Değişkenler)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e1010-198">Click **Arguments**.</span></span> <span data-ttu-id="e1010-199">Tıklatın **çalışma** veya **dosya sistemi** Merhaba projeyi içeren tooset hello klasör.</span><span class="sxs-lookup"><span data-stu-id="e1010-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="e1010-200">Merhaba uygulamayı çalıştırdığınızda, koşulları girmeniz için bir arama kutusu sağlayan bir tarayıcı penceresi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e1010-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="e1010-201">Seçeneğine tıklamadan önce yaklaşık bir dakika bekleyin **arama** toogive hello hizmeti zaman toocreate ve yük başlangıç dizini.</span><span class="sxs-lookup"><span data-stu-id="e1010-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="e1010-202">HTTP 404 hatası alırsanız yeniden denemeden önce biraz daha uzun toowait yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="e1010-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="e1010-203">USGS verilerinde arama</span><span class="sxs-lookup"><span data-stu-id="e1010-203">Search on USGS data</span></span>
<span data-ttu-id="e1010-204">Merhaba USGS veri kümesini ilgili toohello Rhode Island eyaleti kayıtları içerir.</span><span class="sxs-lookup"><span data-stu-id="e1010-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="e1010-205">Tıklatırsanız **arama** bir boş arama kutusunda hello varsayılan olduğu hello ilk 50 girişi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e1010-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="e1010-206">Bir arama terimi girerek hello arama motoru bir şey toogo üzerinde verecektir.</span><span class="sxs-lookup"><span data-stu-id="e1010-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="e1010-207">Bölgesel bir ad girmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="e1010-207">Try entering a regional name.</span></span> <span data-ttu-id="e1010-208">"Roger Williams", Rhode Island hello ilk İdarecisi oluştu.</span><span class="sxs-lookup"><span data-stu-id="e1010-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="e1010-209">Çok sayıda parka, binaya ve okula onun adı verildi.</span><span class="sxs-lookup"><span data-stu-id="e1010-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="e1010-210">Ayrıca, bu terimlerden herhangi birini de deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e1010-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="e1010-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="e1010-211">Pawtucket</span></span>
* <span data-ttu-id="e1010-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="e1010-212">Pembroke</span></span>
* <span data-ttu-id="e1010-213">kaz + şapka</span><span class="sxs-lookup"><span data-stu-id="e1010-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1010-214">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e1010-214">Next steps</span></span>
<span data-ttu-id="e1010-215">Bu Java ve USGS veri kümesini hello hello ilk Azure Search öğreticisidir.</span><span class="sxs-lookup"><span data-stu-id="e1010-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="e1010-216">Zaman içinde biz özel çözümlerinizde toouse isteyebilirsiniz ek arama özellikleri Bu öğretici toodemonstrate genişletmeniz.</span><span class="sxs-lookup"><span data-stu-id="e1010-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="e1010-217">Bazı arka plan Azure Search'te zaten varsa, bu örneği dayanak olarak daha fazla deneyim için hello kullanabilirsiniz [arama sayfası](search-pagination-page-layout.md), veya uygulama [modellenmiş bir gezinmede](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="e1010-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="e1010-218">Ayrıca, numaralar ekleyerek ve böylece kullanıcılar hello sonuçları belgeleri toplu işleme hello arama sonuçları sayfasını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="e1010-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="e1010-219">Yeni tooAzure arama?</span><span class="sxs-lookup"><span data-stu-id="e1010-219">New tooAzure Search?</span></span> <span data-ttu-id="e1010-220">Diğer öğreticiler toodevelop bir neler yapabileceğinizi anlamak çalışırken öneririz.</span><span class="sxs-lookup"><span data-stu-id="e1010-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="e1010-221">Ziyaret bizim [belge sayfasının](https://azure.microsoft.com/documentation/services/search/) toofind daha fazla kaynak.</span><span class="sxs-lookup"><span data-stu-id="e1010-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="e1010-222">Merhaba bağlantılar da görüntüleyebilirsiniz bizim [Video ve öğretici listemiz](search-video-demo-tutorial-list.md) tooaccess daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="e1010-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
