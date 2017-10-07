---
title: "aaaUse hello REST API tooget Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Data Lake Store üzerinde WebHDFS REST API'lerini tooperform işlemleri kullanın"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="96224-103">REST API'lerini kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="96224-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96224-104">Portal</span><span class="sxs-lookup"><span data-stu-id="96224-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="96224-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96224-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="96224-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="96224-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="96224-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="96224-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="96224-108">REST API</span><span class="sxs-lookup"><span data-stu-id="96224-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="96224-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="96224-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="96224-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="96224-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="96224-111">Python</span><span class="sxs-lookup"><span data-stu-id="96224-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="96224-112">Bu makalede, Azure Data Lake Store dosya sistemi işlemleri yanı sıra yönetim nasıl toouse WebHDFS REST API'lerini ve Data Lake Store REST API'lerini tooperform hesap öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="96224-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="96224-113">Azure Data Lake Store, hesap yönetimi işlemleri için kendi REST API'lerini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="96224-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="96224-114">Ancak Data Lake Store, HDFS ve Hadoop ekosistemi ile uyumlu olması nedeniyle, dosya sistemi işlemleri için WebHDFS REST API'lerini kullanarak destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="96224-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="96224-115">Hello Data Lake Store için REST API desteği hakkında ayrıntılı bilgi için bkz: [Azure Data Lake Store REST API Başvurusu](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="96224-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="96224-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96224-116">Prerequisites</span></span>
* <span data-ttu-id="96224-117">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="96224-117">**An Azure subscription**.</span></span> <span data-ttu-id="96224-118">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96224-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="96224-119">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="96224-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="96224-120">Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="96224-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="96224-121">Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="96224-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="96224-122">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="96224-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="96224-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="96224-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="96224-124">Bu makalede, nasıl bir Data Lake Store hesabı karşı toomake REST API çağrıları cURL toodemonstrate kullanır.</span><span class="sxs-lookup"><span data-stu-id="96224-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="96224-125">Azure Active Directory'yi kullanarak nasıl kimlik doğrulaması gerçekleştiririm?</span><span class="sxs-lookup"><span data-stu-id="96224-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="96224-126">Azure Active Directory'yi kullanarak iki yaklaşım tooauthenticate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96224-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="96224-127">Son kullanıcı kimlik doğrulaması (etkileşimli)</span><span class="sxs-lookup"><span data-stu-id="96224-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="96224-128">Bu senaryoda, Merhaba uygulaması hello kullanıcı toolog ister ve tüm hello işlemler hello hello kullanıcı bağlamında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="96224-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="96224-129">Etkileşimli kimlik doğrulaması için adımlara hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="96224-130">Uygulamanızı kullanarak URL aşağıdaki hello kullanıcı toohello yönlendir:</span><span class="sxs-lookup"><span data-stu-id="96224-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="96224-131">\<Yeniden yönlendirme URI'si > kullanılmak üzere bir URL kodlanmış toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="96224-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="96224-132">Bu nedenle, https://localhost için `https%3A%2F%2Flocalhost` kullanılır)</span><span class="sxs-lookup"><span data-stu-id="96224-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="96224-133">Bu öğretici Hello amaçla hello URL'de hello yer tutucu değerlerini değiştirin ve bir web tarayıcısının Adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="96224-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="96224-134">Azure oturum açma bilgilerinizi kullanarak yeniden yönlendirilen tooauthenticate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96224-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="96224-135">Başarıyla oturum açtığında hello yanıt hello tarayıcının adres çubuğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="96224-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="96224-136">Merhaba yanıt biçimi aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="96224-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="96224-137">Merhaba yanıt Hello yetkilendirme kodundan yakalayın.</span><span class="sxs-lookup"><span data-stu-id="96224-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="96224-138">Bu öğretici için hello web tarayıcınızın adres çubuğunda hello hello yetkilendirme kodu kopyalayın ve aşağıda gösterildiği gibi hello POST isteği toohello belirteç uç noktasında geçirin:</span><span class="sxs-lookup"><span data-stu-id="96224-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="96224-139">Bu durumda, hello \<REDIRECT-URI > öğesinin kodlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="96224-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="96224-140">Merhaba yanıt olan bir erişim belirteci içeren bir JSON nesnesi (örn., `"access_token": "<ACCESS_TOKEN>"`) ve bir yenileme belirteci (örn., `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="96224-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="96224-141">Bir erişim belirtecinin süresi dolduğunda, uygulamanızın hello erişim belirteci Azure Data Lake Store ve hello yenileme belirteci tooget erişirken başka bir erişim belirteci kullanır.</span><span class="sxs-lookup"><span data-stu-id="96224-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="96224-142">Merhaba erişim belirtecinin süresi dolduğunda, aşağıda gösterildiği gibi hello yenileme belirtecini kullanarak yeni bir erişim belirteci isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96224-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="96224-143">Etkileşimli kullanıcı kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Yetki kodu izin akışı](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="96224-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="96224-144">Hizmetten hizmete kimlik doğrulaması (etkileşimli olmayan)</span><span class="sxs-lookup"><span data-stu-id="96224-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="96224-145">Bu senaryoda, hello hello uygulama kendi kimlik bilgilerini tooperform hello işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="96224-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="96224-146">Bunun için aşağıda gösterilene hello gibi bir POST isteği yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96224-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="96224-147">Merhaba bu isteğin çıktısı, bir yetki belirteci içerir (belirtilmiştir `access-token` hello çıkışı aşağıdaki), REST API çağrıları ile sonradan geçecek.</span><span class="sxs-lookup"><span data-stu-id="96224-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="96224-148">Bu kimlik doğrulama belirtecini bir metin dosyasına kaydedin; belirteç, bu makalenin ilerleyen bölümlerinde gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="96224-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="96224-149">Bu makalede hello kullanan **etkileşimli olmayan** yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="96224-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="96224-150">Etkileşimli olmayan (hizmet-hizmet çağrıları) hakkında daha fazla bilgi için bkz: [hizmet kimlik bilgilerini kullanarak tooservice çağrıları](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="96224-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="96224-151">Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96224-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="96224-152">Bu işlem üzerinde tanımlı hello REST API çağrısı tabanlı [burada](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="96224-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="96224-153">Merhaba aşağıdaki cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96224-153">Use hello following cURL command.</span></span> <span data-ttu-id="96224-154">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="96224-155">Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız.</span><span class="sxs-lookup"><span data-stu-id="96224-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="96224-156">Bu komut için başlangıç istek yükü hello bulunan **input.json** hello için sağlanan dosya `-d` yukarıdaki parametresini.</span><span class="sxs-lookup"><span data-stu-id="96224-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="96224-157">hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="96224-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="96224-158">Data Lake Store hesabında klasör oluşturma</span><span class="sxs-lookup"><span data-stu-id="96224-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="96224-159">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="96224-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="96224-160">Merhaba aşağıdaki cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96224-160">Use hello following cURL command.</span></span> <span data-ttu-id="96224-161">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="96224-162">Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız.</span><span class="sxs-lookup"><span data-stu-id="96224-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="96224-163">Bu komut adlı bir dizin oluşturur **mytempdir** hello Data Lake Store hesabınızın kök klasörü altında.</span><span class="sxs-lookup"><span data-stu-id="96224-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="96224-164">Merhaba işlem başarıyla tamamlanırsa şuna benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="96224-165">Data Lake Store hesabındaki klasörleri listeleme</span><span class="sxs-lookup"><span data-stu-id="96224-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="96224-166">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="96224-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="96224-167">Merhaba aşağıdaki cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96224-167">Use hello following cURL command.</span></span> <span data-ttu-id="96224-168">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="96224-169">Komut yukarıda Hello yerine \< `REDACTED` \> hello yetki belirteciyle, daha önce aldığınız.</span><span class="sxs-lookup"><span data-stu-id="96224-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="96224-170">Merhaba işlem başarıyla tamamlanırsa şuna benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-170">You should see a response like this if hello operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="96224-171">Data Lake Store hesabına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="96224-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="96224-172">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="96224-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="96224-173">Merhaba aşağıdaki cURL komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96224-173">Use hello following cURL command.</span></span> <span data-ttu-id="96224-174">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="96224-175">Merhaba yukarıda söz dizimi içinde **-T** parametredir karşıya hello dosyasının başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="96224-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="96224-176">Merhaba çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="96224-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="96224-177">Data Lake Store hesabından veri okuma</span><span class="sxs-lookup"><span data-stu-id="96224-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="96224-178">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="96224-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="96224-179">Data Lake Store hesabından veri okuma, iki adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="96224-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="96224-180">İlk hello uç noktası bir GET isteği gönderme `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="96224-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="96224-181">Bu bir konum toosubmit hello sonraki GET isteğini döndürür.</span><span class="sxs-lookup"><span data-stu-id="96224-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="96224-182">Ardından hello endpoint hello GET isteğini göndermek `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="96224-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="96224-183">Bu hello hello dosyanın içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="96224-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="96224-184">Ancak, fark olduğundan hello giriş parametreleri hello arasında önce ve hello adım ikinci, hello kullanabilirsiniz `-L` parametresi toosubmit hello ilk istek.</span><span class="sxs-lookup"><span data-stu-id="96224-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="96224-185">`-L`seçeneği temelde iki isteği tek istekte birleştirir ve hello yeni konum hello isteğinde Yinele cURL hale getirir.</span><span class="sxs-lookup"><span data-stu-id="96224-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="96224-186">Son olarak, tüm hello istek çağrılarının çıktısı Merhaba, olduğu gibi görüntülenir aşağıda gösterilen.</span><span class="sxs-lookup"><span data-stu-id="96224-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="96224-187">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="96224-188">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="96224-189">Data Lake Store hesabındaki bir dosyayı yeniden adlandırma</span><span class="sxs-lookup"><span data-stu-id="96224-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="96224-190">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="96224-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="96224-191">Kullanım hello aşağıdaki komut toorename bir dosya cURL.</span><span class="sxs-lookup"><span data-stu-id="96224-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="96224-192">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="96224-193">Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="96224-194">Data Lake Store hesabından dosya silme</span><span class="sxs-lookup"><span data-stu-id="96224-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="96224-195">Bu işlem üzerinde tanımlı hello WebHDFS REST API çağrısı tabanlı [burada](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="96224-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="96224-196">Kullanım hello aşağıdaki komut toodelete bir dosya cURL.</span><span class="sxs-lookup"><span data-stu-id="96224-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="96224-197">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="96224-198">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="96224-199">Data Lake Store hesabını silme</span><span class="sxs-lookup"><span data-stu-id="96224-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="96224-200">Bu işlem üzerinde tanımlı hello REST API çağrısı tabanlı [burada](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="96224-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="96224-201">Kullanım hello aşağıdaki komut toodelete bir Data Lake Store hesabı cURL.</span><span class="sxs-lookup"><span data-stu-id="96224-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="96224-202">**\<yourstorename>** ifadesini, Data Lake Store adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="96224-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="96224-203">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="96224-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="96224-204">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="96224-204">See also</span></span>
* [<span data-ttu-id="96224-205">Azure Data Lake Store ile uyumlu Açık Kaynak Büyük Veri uygulamaları</span><span class="sxs-lookup"><span data-stu-id="96224-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

