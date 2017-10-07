---
title: "aaaGet REST API'sini kullanarak Data Lake Analytics ile çalışmaya | Microsoft Docs"
description: "Data Lake Analytics WebHDFS REST API'lerini tooperform işlemleri kullanın"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="6564b-103">REST API’lerini kullanarak Azure Data Lake Analytics ile çalışmaya başlama | Azure</span><span class="sxs-lookup"><span data-stu-id="6564b-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="6564b-104">Nasıl toouse WebHDFS REST API'lerini ve Data Lake Analytics REST API'leri toomanage Data Lake Analytics hesaplarını, işlerini ve Katalog öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6564b-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6564b-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6564b-105">Prerequisites</span></span>
* <span data-ttu-id="6564b-106">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="6564b-106">**An Azure subscription**.</span></span> <span data-ttu-id="6564b-107">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6564b-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6564b-108">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6564b-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="6564b-109">Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Analytics uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="6564b-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="6564b-110">Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="6564b-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="6564b-111">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [Azure Active Directory kullanarak Data Lake Analytics ile kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="6564b-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="6564b-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="6564b-113">Bu makalede, nasıl bir Data Lake Analytics hesabı karşı toomake REST API çağrıları cURL toodemonstrate kullanır.</span><span class="sxs-lookup"><span data-stu-id="6564b-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="6564b-114">Azure Active Directory ile kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="6564b-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="6564b-115">Azure Active Directory ile kimlik doğrulama gerçekleştirmek için kullanılabilecek iki yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="6564b-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="6564b-116">Son kullanıcı kimlik doğrulaması (etkileşimli)</span><span class="sxs-lookup"><span data-stu-id="6564b-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="6564b-117">Bu yöntemi kullanarak, uygulama hello kullanıcı toolog ister ve tüm hello işlemler hello hello kullanıcı bağlamında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6564b-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="6564b-118">Etkileşimli kimlik doğrulaması için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6564b-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="6564b-119">Uygulamanızı kullanarak URL aşağıdaki hello kullanıcı toohello yönlendir:</span><span class="sxs-lookup"><span data-stu-id="6564b-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="6564b-120">\<Yeniden yönlendirme URI'si > kullanılmak üzere bir URL kodlanmış toobe gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6564b-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="6564b-121">Bu nedenle, https://localhost için `https%3A%2F%2Flocalhost` kullanılır)</span><span class="sxs-lookup"><span data-stu-id="6564b-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="6564b-122">Bu öğretici Hello amaçla hello URL'de hello yer tutucu değerlerini değiştirin ve bir web tarayıcısının Adres çubuğuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6564b-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="6564b-123">Azure oturum açma bilgilerinizi kullanarak yeniden yönlendirilen tooauthenticate olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6564b-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="6564b-124">Başarıyla oturum açmanızın sonra hello yanıt hello tarayıcının adres çubuğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6564b-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="6564b-125">Merhaba yanıt biçimi aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6564b-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="6564b-126">Merhaba yanıt Hello yetkilendirme kodundan yakalayın.</span><span class="sxs-lookup"><span data-stu-id="6564b-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="6564b-127">Bu öğretici için hello web tarayıcınızın adres çubuğunda hello hello yetkilendirme kodu kopyalayın ve aşağıda gösterildiği gibi hello POST isteği toohello belirteç uç noktasında geçirin:</span><span class="sxs-lookup"><span data-stu-id="6564b-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="6564b-128">Bu durumda, hello \<REDIRECT-URI > öğesinin kodlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6564b-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="6564b-129">Merhaba yanıt olan bir erişim belirteci içeren bir JSON nesnesi (örn., `"access_token": "<ACCESS_TOKEN>"`) ve bir yenileme belirteci (örn., `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="6564b-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="6564b-130">Bir erişim belirtecinin süresi dolduğunda, uygulamanızın hello erişim belirteci Azure Data Lake Store ve hello yenileme belirteci tooget erişirken başka bir erişim belirteci kullanır.</span><span class="sxs-lookup"><span data-stu-id="6564b-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="6564b-131">Merhaba erişim belirtecinin süresi dolduğunda, aşağıda gösterildiği gibi hello yenileme belirtecini kullanarak yeni bir erişim belirteci isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6564b-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="6564b-132">Etkileşimli kullanıcı kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Yetki kodu izin akışı](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="6564b-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="6564b-133">Hizmetten hizmete kimlik doğrulaması (etkileşimli olmayan)</span><span class="sxs-lookup"><span data-stu-id="6564b-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="6564b-134">Bu yöntemi kullanarak, uygulama kendi kimlik bilgilerini tooperform hello işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="6564b-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="6564b-135">Bunun için aşağıda gösterilene hello gibi bir POST isteği yayımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="6564b-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="6564b-136">Merhaba bu isteğin çıktısı, bir yetki belirteci içerir (belirtilmiştir `access-token` hello çıkışı aşağıdaki), REST API çağrıları ile sonradan geçecek.</span><span class="sxs-lookup"><span data-stu-id="6564b-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="6564b-137">Bu kimlik doğrulama belirtecini bir metin dosyasına kaydedin; belirteç, bu makalenin ilerleyen bölümlerinde gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6564b-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="6564b-138">Bu makalede hello kullanan **etkileşimli olmayan** yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="6564b-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="6564b-139">Etkileşimli olmayan (hizmet-hizmet çağrıları) hakkında daha fazla bilgi için bkz: [hizmet kimlik bilgilerini kullanarak tooservice çağrıları](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="6564b-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="6564b-140">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6564b-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="6564b-141">Data Lake Analytics hesabı oluşturabilmek için Azure kaynak grubu ve Data Lake Store hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6564b-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="6564b-142">Bkz. [Data Lake Store hesabı oluşturma](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="6564b-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="6564b-143">Curl komutunu gösterir nasıl aşağıdaki hello toocreate bir hesap:</span><span class="sxs-lookup"><span data-stu-id="6564b-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="6564b-144">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `NewAzureDataLakeAnalyticsAccountName` \> ile yeni bir Data Lake Analytics hesap adı.</span><span class="sxs-lookup"><span data-stu-id="6564b-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="6564b-145">Bu komut için başlangıç istek yükü hello bulunan **CreateDatalakeAnalyticsAccountRequest.json** hello için sağlanan dosya `-d` yukarıdaki parametresini.</span><span class="sxs-lookup"><span data-stu-id="6564b-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="6564b-146">hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-146">hello contents of hello input.json file resemble hello following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="6564b-147">Bir abonelikteki Data Lake Analytics hesaplarını listeleme</span><span class="sxs-lookup"><span data-stu-id="6564b-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="6564b-148">Aşağıdaki Curl komutunu hello nasıl toolist bir abonelikte hesapları gösterir:</span><span class="sxs-lookup"><span data-stu-id="6564b-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="6564b-149">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> abonelik kimliğinizi içeren</span><span class="sxs-lookup"><span data-stu-id="6564b-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="6564b-150">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-150">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="6564b-151">Bir Data Lake Analytics hesabı hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="6564b-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="6564b-152">Curl komutunu gösterir nasıl aşağıdaki hello tooget bir hesap bilgileri:</span><span class="sxs-lookup"><span data-stu-id="6564b-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="6564b-153">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="6564b-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="6564b-154">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-154">hello output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="6564b-155">Bir Data Lake Analytics hesabının Data Lake Store bilgilerini listeleme</span><span class="sxs-lookup"><span data-stu-id="6564b-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="6564b-156">Aşağıdaki Curl komutunu hello nasıl toolist Data Lake bir hesabı depoladığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="6564b-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="6564b-157">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `AzureSubscriptionID` \> değerini abonelik kimliğinizle \< `AzureResourceGroupName` \> mevcut bir Azure kaynağı ile Grup adı ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="6564b-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="6564b-158">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-158">hello output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="6564b-159">U-SQL işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="6564b-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="6564b-160">Curl komutunu gösterir nasıl aşağıdaki hello toosubmit U-SQL işi:</span><span class="sxs-lookup"><span data-stu-id="6564b-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="6564b-161">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="6564b-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="6564b-162">Bu komut için başlangıç istek yükü hello bulunan **SubmitADLAJob.json** hello için sağlanan dosya `-d` yukarıdaki parametresini.</span><span class="sxs-lookup"><span data-stu-id="6564b-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="6564b-163">hello input.json dosyasının Merhaba içeriğine hello aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-163">hello contents of hello input.json file resemble hello following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="6564b-164">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-164">hello output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="6564b-165">U-SQL işlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="6564b-165">List U-SQL jobs</span></span>
<span data-ttu-id="6564b-166">Curl komutunu gösterir nasıl aşağıdaki hello toolist U-SQL işleri:</span><span class="sxs-lookup"><span data-stu-id="6564b-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="6564b-167">Değiştir \< `REDACTED` \> hello yetkilendirme belirteci ile ve \< `DataLakeAnalyticsAccountName` \> varolan bir Data Lake Analytics hesabı hello adı.</span><span class="sxs-lookup"><span data-stu-id="6564b-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="6564b-168">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-168">hello output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="6564b-169">Katalog öğelerini alma</span><span class="sxs-lookup"><span data-stu-id="6564b-169">Get catalog items</span></span>
<span data-ttu-id="6564b-170">Aşağıdaki Curl komutunu hello nasıl tooget hello veritabanlarından katalog hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="6564b-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="6564b-171">Merhaba çıkış benzer:</span><span class="sxs-lookup"><span data-stu-id="6564b-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="6564b-172">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6564b-172">See also</span></span>
* <span data-ttu-id="6564b-173">toosee daha karmaşık bir sorgu görmek [Web sitesi günlüklerini çözümleme Azure Data Lake Analytics'i kullanarak](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="6564b-174">U-SQL uygulamalarını geliştirmeye başlatılan tooget bkz [Visual Studio için Data Lake Araçları'nı kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="6564b-175">U-SQL, toolearn bkz [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="6564b-176">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="6564b-177">bir Data Lake Analytics özetini tooget bkz [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6564b-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="6564b-178">toosee hello aynı öğreticiyi diğer araçları kullanarak, hello sekmesini seçiciler hello sayfasının hello üstte'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6564b-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

