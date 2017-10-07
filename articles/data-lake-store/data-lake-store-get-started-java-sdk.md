---
title: "aaaUse hello Azure Data Lake Store Java SDK'sı toodevelop uygulamaları | Microsoft Docs"
description: "Azure Data Lake Store Java SDK toocreate bir Data Lake Store hesabı kullanıp hello Data Lake Store temel işlemleri"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="08eea-103">Java'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="08eea-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="08eea-104">Portal</span><span class="sxs-lookup"><span data-stu-id="08eea-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="08eea-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08eea-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="08eea-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="08eea-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="08eea-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="08eea-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="08eea-108">REST API</span><span class="sxs-lookup"><span data-stu-id="08eea-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="08eea-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="08eea-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="08eea-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="08eea-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="08eea-111">Python</span><span class="sxs-lookup"><span data-stu-id="08eea-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="08eea-112">Toouse hello Azure Data Lake Store Java SDK tooperform temel işlemleri gibi klasörleri oluşturmak nasıl öğrenin, karşıya yükleme ve indirme vb. veri dosyaları. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08eea-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="08eea-113">Hello Azure Data Lake Store için Java SDK API belgeleri erişebilirsiniz [Azure Data Lake Store Java API belgeleri](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="08eea-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08eea-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="08eea-114">Prerequisites</span></span>
* <span data-ttu-id="08eea-115">Java Development Kit (Java sürüm 1.7 veya üzerini kullanan JDK 7 ya da üzeri)</span><span class="sxs-lookup"><span data-stu-id="08eea-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="08eea-116">Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="08eea-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="08eea-117">Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="08eea-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="08eea-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="08eea-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="08eea-119">Bu eğiticide, yapı ve proje bağımlılıkları için Maven kullanılır.</span><span class="sxs-lookup"><span data-stu-id="08eea-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="08eea-120">Derleme Sistemi Maven veya Gradle gibi kullanmadan olası toobuild olmasına karşın, çok daha kolay toomanage bağımlılıkları olduğundan bu sistemler olun.</span><span class="sxs-lookup"><span data-stu-id="08eea-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="08eea-121">(İsteğe bağlı) [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) vb. bir IDE.</span><span class="sxs-lookup"><span data-stu-id="08eea-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="08eea-122">Azure Active Directory'yi kullanarak nasıl kimlik doğrulaması gerçekleştiririm?</span><span class="sxs-lookup"><span data-stu-id="08eea-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="08eea-123">Bu öğreticide bir Azure AD uygulama istemci gizli tooretrieve bir Azure Active Directory token (hizmet kimlik doğrulaması) kullanın.</span><span class="sxs-lookup"><span data-stu-id="08eea-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="08eea-124">Bu belirteç toocreate bir Data Lake Store istemcisi nesnesi tooperform işlemleri dosya ve dizin işlemlerini kullanırız.</span><span class="sxs-lookup"><span data-stu-id="08eea-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="08eea-125">Nasıl kullanarak Azure Data Lake Store ile tooauthenticate hello istemci parolası ile ilgili yönergeler için aşağıdaki üst düzey adımları hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="08eea-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="08eea-126">Azure AD web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="08eea-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="08eea-127">Merhaba istemci kimliği, gizli ve hello Azure AD web uygulaması için belirteç uç noktası alamadı.</span><span class="sxs-lookup"><span data-stu-id="08eea-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="08eea-128">Merhaba tooaccess hello oluşturmakta olduğunuz Java uygulaması'ndan istediğiniz Data Lake Store dosya/klasör hello Azure AD web uygulamasına erişimi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="08eea-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="08eea-129">Yönergeler için nasıl tooperform bu adımları görmek [Active Directory Uygulama oluşturma](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="08eea-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="08eea-130">Azure Active Directory, diğer de tooretrieve bir belirteç seçenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="08eea-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="08eea-131">Farklı kimlik doğrulama mekanizmaları toosuit arasında bir sayı senaryonuz, örneğin, bir tarayıcı, bir masaüstü uygulaması olarak dağıtılmış bir uygulama ya da şirket içi çalıştıran bir sunucu uygulaması veya bir Azure sanal çalışan bir uygulama seçin Makine.</span><span class="sxs-lookup"><span data-stu-id="08eea-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="08eea-132">Parolalar, sertifikalar, 2 öğeli kimlik doğrulaması vb. farklı kimlik bilgileri arasından da seçim yapabilirsiniz. Ayrıca, Azure Active Directory toosynchronize sayesinde şirket içi Active Directory kullanıcılarınıza hello bulut.</span><span class="sxs-lookup"><span data-stu-id="08eea-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="08eea-133">Ayrıntılar için bkz. [Azure Active Directory için Kimlik Doğrulama Senaryoları](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="08eea-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="08eea-134">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="08eea-134">Create a Java application</span></span>
<span data-ttu-id="08eea-135">Merhaba kod örneği [github'da](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) hello depoda dosya oluşturma, dosyaları birleştirme, dosya indirme ve hello deposundaki bazı dosyaları silin hello işleminde size yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="08eea-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="08eea-136">Bu bölümde hello makalenin hello ana hello kod parçalarını size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="08eea-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="08eea-137">Kullanarak bir Maven projesi oluşturun [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) gelen hello komut satırı veya bir IDE kullanma.</span><span class="sxs-lookup"><span data-stu-id="08eea-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="08eea-138">Nasıl toocreate bir Java projesi Intellij kullanma ile ilgili yönergeler için bkz: [burada](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="08eea-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="08eea-139">Yönergeler için Eclipse, kullanarak proje a toocreate bkz [burada](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="08eea-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="08eea-140">Bağımlılıklar tooyour Maven aşağıdaki hello eklemek **pom.xml** dosya.</span><span class="sxs-lookup"><span data-stu-id="08eea-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="08eea-141">Merhaba arasında metin parçacığını aşağıdaki hello eklemek  **\</VERSION >** etiketini ve hello  **\</project >** etiketi:</span><span class="sxs-lookup"><span data-stu-id="08eea-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="08eea-142">Merhaba ilk bağımlılık olan toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) hello maven depodan.</span><span class="sxs-lookup"><span data-stu-id="08eea-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="08eea-143">İkinci bağımlılık hello (`slf4j-nop`) bu uygulama için hangi günlük framework toouse toospecify olduğu.</span><span class="sxs-lookup"><span data-stu-id="08eea-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="08eea-144">Merhaba Data Lake Store SDK kullanan [slf4j](http://www.slf4j.org/) log4j gibi popüler günlük çerçevelerinden sayısından günlüğü, logback, vb. Java seçmenize olanak tanır günlük cephesi veya günlük yok.</span><span class="sxs-lookup"><span data-stu-id="08eea-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="08eea-145">Bu örneğin biz günlüğü devre dışı bırakır, bu nedenle hello kullanırız **slf4j nop** bağlama.</span><span class="sxs-lookup"><span data-stu-id="08eea-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="08eea-146">toouse, uygulamanızda diğer günlüğe kaydetme seçeneklerini görmek [burada](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="08eea-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="08eea-147">Merhaba uygulama kodu ekleyin</span><span class="sxs-lookup"><span data-stu-id="08eea-147">Add hello application code</span></span>
<span data-ttu-id="08eea-148">Toohello kod üç ana bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="08eea-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="08eea-149">Hello Azure Active Directory belirteç edinme</span><span class="sxs-lookup"><span data-stu-id="08eea-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="08eea-150">Merhaba belirteci toocreate bir Data Lake Store istemcisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="08eea-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="08eea-151">Merhaba Data Lake Store istemcisi tooperform işlemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="08eea-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="08eea-152">1. Adım: Azure Active Directory belirteci edinin.</span><span class="sxs-lookup"><span data-stu-id="08eea-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="08eea-153">Merhaba Data Lake Store SDK hello güvenlik belirteçleri yönetmenize olanak sağlayan kullanışlı yöntemler tootalk toohello Data Lake Store hesabı gerekli sağlar.</span><span class="sxs-lookup"><span data-stu-id="08eea-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="08eea-154">Ancak, hello SDK yalnızca bu yöntemleri kullanılmasını zorunlu kılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="08eea-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="08eea-155">Belirteç de hello kullanarak gibi almanın başka bir yöntemle kullanabilirsiniz [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), ya da kendi özel kod.</span><span class="sxs-lookup"><span data-stu-id="08eea-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="08eea-156">toouse hello daha önce oluşturduğunuz Merhaba Active Directory Web uygulaması için Data Lake Store SDK tooobtain belirteci hello alt sınıflarının birini kullanın `AccessTokenProvider` (Merhaba örneği kullanır `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="08eea-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="08eea-157">Merhaba belirteç sağlayıcısı önbellekleri hello kimlik bilgileri tooobtain hello belirteci kullanılan bellek ve tooexpire hakkında ise hello belirteci otomatik olarak yeniler.</span><span class="sxs-lookup"><span data-stu-id="08eea-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="08eea-158">Kendi alt sınıflarının olası toocreate olan `AccessTokenProvider` belirteçleri müşteri kodunuz tarafından elde edilir, ancak şu an için şimdi yalnızca kullanım hello bir hello SDK sağlanan şekilde.</span><span class="sxs-lookup"><span data-stu-id="08eea-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="08eea-159">Değiştir **burada doldurma** hello Azure Active Directory Web uygulaması için hello gerçek değerlerle.</span><span class="sxs-lookup"><span data-stu-id="08eea-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="08eea-160">2. Adım: Azure Data Lake Store istemci (ADLStoreClient) nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="08eea-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="08eea-161">Oluşturma bir [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) nesnesi hello son adımda oluşturulan toospecify hello Data Lake Store hesabı adı ve hello belirteç sağlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="08eea-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="08eea-162">Bu hello Data Lake Store hesabı adı toobe bir tam etki alanı adı gerekiyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="08eea-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="08eea-163">Örneğin, **BURAYI DOLDURUN** alanını **mydatalakestore.azuredatalakestore.net** gibi bir etki alanı adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="08eea-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="08eea-164">3. adım: Merhaba, ADLStoreClient tooperform dosya ve dizin işlemleri kullanın</span><span class="sxs-lookup"><span data-stu-id="08eea-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="08eea-165">Merhaba kodunu aşağıdaki örnek kod parçacıkları bazı ortak işlemlerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="08eea-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="08eea-166">Merhaba tam bakabilirsiniz [veri Gölü deposu Java SDK API belgeleri](https://azure.github.io/azure-data-lake-store-java/javadoc/) Merhaba, **ADLStoreClient** toosee diğer işlemleri nesne.</span><span class="sxs-lookup"><span data-stu-id="08eea-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="08eea-167">Dosyalar, standart Java akışları kullanılarak okunur ve yazılır.</span><span class="sxs-lookup"><span data-stu-id="08eea-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="08eea-168">Bu standart Java işlevleri (örneğin, yazdırma akışları biçimlendirilmiş çıkışı ya da herhangi bir üzerinde ek işlevsellik için hello sıkıştırma veya şifreleme akışlar için gelen toobenefit Data Lake Store akışları hello Java akışları hello üstünde hiçbirini katman anlamına gelir. Top, vs.).</span><span class="sxs-lookup"><span data-stu-id="08eea-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="08eea-169">4. adım: Derleme ve Merhaba uygulaması çalıştırma</span><span class="sxs-lookup"><span data-stu-id="08eea-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="08eea-170">gelen toorun bir IDE içinde bulun ve basın hello **çalıştırmak** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="08eea-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="08eea-171">Maven, kullanım gelen toorun [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="08eea-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="08eea-172">tooproduce hello kullanarak komut satırı derleme hello jar dahil, tüm bağımlılıklarıyla çalıştırabileceğiniz bir tek başına jar [Maven derlemesi eklenti](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="08eea-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="08eea-173">Merhaba pom.XML hello [örnek kaynak kodu github'da](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) nasıl bir örneği olan toodo bu.</span><span class="sxs-lookup"><span data-stu-id="08eea-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08eea-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="08eea-174">Next steps</span></span>
* [<span data-ttu-id="08eea-175">Merhaba Java SDK'sı JavaDoc keşfedin</span><span class="sxs-lookup"><span data-stu-id="08eea-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="08eea-176">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="08eea-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="08eea-177">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="08eea-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="08eea-178">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="08eea-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

