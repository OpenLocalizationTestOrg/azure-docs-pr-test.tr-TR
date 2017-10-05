---
title: "Azure Data Lake Store’da uygulama geliştirmek için Java SDK'sını kullanma | Microsoft Docs"
description: "Bir Data Lake Store hesabı oluşturmak ve Data Lake Store'da temel işlemleri gerçekleştirmek için Azure Data Lake Store Java SDK’sını kullanma"
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
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="514d1-103">Java'yı kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="514d1-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="514d1-104">Portal</span><span class="sxs-lookup"><span data-stu-id="514d1-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="514d1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="514d1-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="514d1-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="514d1-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="514d1-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="514d1-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="514d1-108">REST API</span><span class="sxs-lookup"><span data-stu-id="514d1-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="514d1-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="514d1-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="514d1-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="514d1-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="514d1-111">Python</span><span class="sxs-lookup"><span data-stu-id="514d1-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="514d1-112">Klasör oluşturma, veri dosyalarını karşıya yükleme ve indirme gibi temel işlemleri gerçekleştirmek için Azure Data Lake Store Java SDK’sını kullanma hakkında bilgi edinin. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="514d1-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="514d1-113">Azure Data Lake Store için Java SDK API belgelerine, [Azure Data Lake Store Java API belgelerinden](https://azure.github.io/azure-data-lake-store-java/javadoc/) erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514d1-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="514d1-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="514d1-114">Prerequisites</span></span>
* <span data-ttu-id="514d1-115">Java Development Kit (Java sürüm 1.7 veya üzerini kullanan JDK 7 ya da üzeri)</span><span class="sxs-lookup"><span data-stu-id="514d1-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="514d1-116">Azure Data Lake Store hesabı.</span><span class="sxs-lookup"><span data-stu-id="514d1-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="514d1-117">[Azure Portal'ı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md) bölümündeki yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="514d1-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="514d1-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="514d1-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="514d1-119">Bu eğiticide, yapı ve proje bağımlılıkları için Maven kullanılır.</span><span class="sxs-lookup"><span data-stu-id="514d1-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="514d1-120">Maven veya Gradle gibi bir yapı sistemi olmadan derleme yapmak mümkün olsa da bu sistemler bağımlılıkların yönetilmesini çok daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="514d1-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="514d1-121">(İsteğe bağlı) [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) vb. bir IDE.</span><span class="sxs-lookup"><span data-stu-id="514d1-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="514d1-122">Azure Active Directory'yi kullanarak nasıl kimlik doğrulaması gerçekleştiririm?</span><span class="sxs-lookup"><span data-stu-id="514d1-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="514d1-123">Bu eğiticide, Azure Active Directory belirteci (hizmetten hizmete kimlik doğrulama) almak için Azure AD uygulamasının istemci gizli anahtarını kullanırız.</span><span class="sxs-lookup"><span data-stu-id="514d1-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="514d1-124">Bu belirteci kullanarak işlem dosyasını ve dizin işlemlerini gerçekleştirmek için Data Lake Store istemci nesnesi oluştururuz.</span><span class="sxs-lookup"><span data-stu-id="514d1-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="514d1-125">İstemci gizli anahtarı kullanarak Azure Data Lake Store’da kimlik doğrulamaya ilişkin yönergeler için aşağıdaki üst düzey adımları gerçekleştiririz:</span><span class="sxs-lookup"><span data-stu-id="514d1-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="514d1-126">Azure AD web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="514d1-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="514d1-127">Azure AD web uygulaması için istemci kimliğini, istemci gizli anahtarını ve belirteç uç noktasını alın.</span><span class="sxs-lookup"><span data-stu-id="514d1-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="514d1-128">Oluşturduğunuz Java uygulamasından erişmek istediğiniz Data Lake Store dosyasında/klasöründe Azure AD web uygulaması için erişimi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="514d1-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="514d1-129">Bu adımların nasıl gerçekleştirileceğine ilişkin yönergeler için bkz. [Active Directory uygulaması oluşturma](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="514d1-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="514d1-130">Azure Active Directory, belirteç almak için başka seçenekler de sunar.</span><span class="sxs-lookup"><span data-stu-id="514d1-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="514d1-131">Tarayıcınızda çalışan bir uygulama, masaüstü uygulaması olarak dağıtılan bir uygulama ya da şirket içinde veya Azure sanal makinesinde çalışan sunucu uygulaması gibi farklı kimlik doğrulama mekanizmaları arasından senaryonuza en uygun olanını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514d1-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="514d1-132">Parolalar, sertifikalar, 2 öğeli kimlik doğrulaması vb. farklı kimlik bilgileri arasından da seçim yapabilirsiniz. Ayrıca Azure Active Directory, şirket içi Active Directory kullanıcılarınızı bulutla eşitlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="514d1-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="514d1-133">Ayrıntılar için bkz. [Azure Active Directory için Kimlik Doğrulama Senaryoları](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="514d1-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="514d1-134">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="514d1-134">Create a Java application</span></span>
<span data-ttu-id="514d1-135">[GitHub’da](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) bulunan kod örneği, depoda dosya oluşturma, dosyaları birleştirme, dosya indirme ve depodaki bazı dosyaları silme işlemlerinde size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="514d1-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="514d1-136">Makalenin bu bölümü, kodun ana bölümlerinde sizi yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="514d1-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="514d1-137">Komut satırından [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) veya bir IDE kullanarak Maven projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="514d1-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="514d1-138">IntelliJ kullanarak Java projesi oluşturma yönergeleri için [buraya](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html) bakın.</span><span class="sxs-lookup"><span data-stu-id="514d1-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="514d1-139">Eclipse kullanarak proje oluşturma yönergeleri için [buraya](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm) bakın.</span><span class="sxs-lookup"><span data-stu-id="514d1-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="514d1-140">Maven **pom.xml** dosyanıza aşağıdaki bağımlılıkları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="514d1-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="514d1-141">Metnin şu kod parçacığını **\</version>** etiketi ile **\</project>** etiketi arasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="514d1-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="514d1-142">İlk bağımlılık, maven deposundan Data Lake Store SDK’sını (`azure-data-lake-store-sdk`) kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="514d1-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="514d1-143">İkinci bağımlılık (`slf4j-nop`), bu uygulama için hangi günlük altyapısının kullanılacağını belirtmektir.</span><span class="sxs-lookup"><span data-stu-id="514d1-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="514d1-144">Data Lake Store SDK’sı; log4j, Java günlük kaydı, logback gibi birçok popüler günlük altyapısından birini seçmenizi veya günlük kaydı seçmemenizi sağlayan [slf4j](http://www.slf4j.org/) günlük cephesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="514d1-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="514d1-145">Bu örnekte, günlük kaydını devre dışı bırakacak ve dolayısıyla **slf4j-nop** bağlamasını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="514d1-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="514d1-146">Uygulamanızda diğer günlük seçeneklerini kullanmak için [buraya](http://www.slf4j.org/manual.html#projectDep) bakın.</span><span class="sxs-lookup"><span data-stu-id="514d1-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="514d1-147">Uygulama kodunu ekleme</span><span class="sxs-lookup"><span data-stu-id="514d1-147">Add the application code</span></span>
<span data-ttu-id="514d1-148">Kodun üç ana bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="514d1-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="514d1-149">Azure Active Directory belirtecini edinme</span><span class="sxs-lookup"><span data-stu-id="514d1-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="514d1-150">Data Lake Store istemcisi oluşturmak için belirteci kullanın.</span><span class="sxs-lookup"><span data-stu-id="514d1-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="514d1-151">İşlemleri gerçekleştirmek için Data Lake Store istemcisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="514d1-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="514d1-152">1. Adım: Azure Active Directory belirteci edinin.</span><span class="sxs-lookup"><span data-stu-id="514d1-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="514d1-153">Data Lake Store SDK’sı, Data Lake Store hesabıyla iletişim kurmak için gereken güvenlik belirteçlerini yönetmenizi sağlayacak kullanışlı yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="514d1-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="514d1-154">Bununla birlikte, SDK yalnızca bu yöntemlerin kullanılmasını zorunlu kılmaz.</span><span class="sxs-lookup"><span data-stu-id="514d1-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="514d1-155">[Azure Active Directory SDK’sını](https://github.com/AzureAD/azure-activedirectory-library-for-java) veya kendi özel kodunuzu kullanma gibi diğer belirteç edinme yöntemlerinden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514d1-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="514d1-156">Daha önce oluşturduğunuz Active Directory Web uygulaması için belirteci edinmek üzere Data Lake Store SDK’sını kullanmak için `AccessTokenProvider` alt sınıflarından birini kullanın (aşağıdaki örnekte `ClientCredsTokenProvider` kullanılmaktadır).</span><span class="sxs-lookup"><span data-stu-id="514d1-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="514d1-157">Belirteç sağlayıcısı, bellekteki belirteci almak için kullanılan kimlik bilgilerini önbelleğe alır ve süre sonu yaklaştığında belirteci otomatik olarak yeniler.</span><span class="sxs-lookup"><span data-stu-id="514d1-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="514d1-158">Kendi `AccessTokenProvider` alt sınıflarınızı oluşturabilir, böylece belirteçlerin müşteri kodunuza göre alınmasını sağlayabilirsiniz; ancak şimdilik yalnızca SDK’da verileni kullanalım.</span><span class="sxs-lookup"><span data-stu-id="514d1-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="514d1-159">**BURAYI DOLDURUN** alanını, Azure Active Directory Web uygulaması için gerçek değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="514d1-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="514d1-160">2. Adım: Azure Data Lake Store istemci (ADLStoreClient) nesnesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="514d1-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="514d1-161">[ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) nesnesi oluşturmak için Data Lake Store hesap adını ve son adımda oluşturduğunuz belirteç sağlayıcısını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="514d1-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="514d1-162">Data Lake Store hesap adının tam etki alanı adı olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="514d1-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="514d1-163">Örneğin, **BURAYI DOLDURUN** alanını **mydatalakestore.azuredatalakestore.net** gibi bir etki alanı adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="514d1-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="514d1-164">3. Adım: Dosya ve dizin işlemlerini gerçekleştirmek için ADLStoreClient’ı kullanın</span><span class="sxs-lookup"><span data-stu-id="514d1-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="514d1-165">Aşağıdaki kod, bazı yaygın işlemlerin kod parçacıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="514d1-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="514d1-166">Diğer işlemleri görmek için **ADLStoreClient** nesnesinin tüm [Data Lake Store Java SDK API belgelerine](https://azure.github.io/azure-data-lake-store-java/javadoc/) bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514d1-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="514d1-167">Dosyalar, standart Java akışları kullanılarak okunur ve yazılır.</span><span class="sxs-lookup"><span data-stu-id="514d1-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="514d1-168">Bu, standart Java işlevlerinden (ör. biçimlendirilmiş çıkış için Yazdırma akışları ya da en üstteki ek işlevler için herhangi bir sıkıştırma veya şifreleme akışı vb.) yararlanmak için Java akışlarından herhangi birini Data Lake Store akışlarının üzerine katmanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="514d1-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
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

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="514d1-169">4. Adım: Uygulamayı derleme ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="514d1-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="514d1-170">Bir IDE içinden çalıştırmak için **Çalıştır** düğmesini bulup basın.</span><span class="sxs-lookup"><span data-stu-id="514d1-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="514d1-171">Maven’den çalıştırmak [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html)’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="514d1-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="514d1-172">Komut satırından çalıştırabileceğiniz tek başına bir jar oluşturmak için jar’ı [Maven derleme eklentisini](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html) kullanarak dahil edilen tüm bağımlılıklarla birlikte derleyin.</span><span class="sxs-lookup"><span data-stu-id="514d1-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="514d1-173">[Github’daki örnek kaynak kodda](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) bulunan pom.xml, bunun nasıl yapılacağını gösteren bir örnek içerir.</span><span class="sxs-lookup"><span data-stu-id="514d1-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="514d1-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="514d1-174">Next steps</span></span>
* [<span data-ttu-id="514d1-175">Java SDK için JavaDoc’u keşfedin</span><span class="sxs-lookup"><span data-stu-id="514d1-175">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="514d1-176">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="514d1-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="514d1-177">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="514d1-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="514d1-178">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="514d1-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

