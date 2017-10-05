---
title: "REST API'yi kullanarak Data Lake Analytics ile çalışmaya başlama| Microsoft Belgeleri"
description: "Data Lake Analytics üzerinde işlem yapmak için WebHDFS REST API'lerini kullanma"
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
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="02e06-103">REST API’lerini kullanarak Azure Data Lake Analytics ile çalışmaya başlama | Azure</span><span class="sxs-lookup"><span data-stu-id="02e06-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="02e06-104">Data Lake Analytics hesaplarını, işlerini ve kataloğunu yönetmek için WebHDFS REST API’lerini ve Data Lake Analytics REST API’lerini nasıl kullanacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="02e06-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="02e06-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="02e06-105">Prerequisites</span></span>
* <span data-ttu-id="02e06-106">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="02e06-106">**An Azure subscription**.</span></span> <span data-ttu-id="02e06-107">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02e06-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="02e06-108">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="02e06-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="02e06-109">Data Lake Analytics uygulamasında Azure AD ile kimlik doğrulaması yapmak için Azure AD uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="02e06-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="02e06-110">Azure AD kimlik doğrulaması için **son kullanıcı kimlik doğrulaması** veya **hizmetten hizmete kimlik doğrulama** gibi farklı yaklaşımlar bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="02e06-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="02e06-111">Kimlik doğrulaması hakkında yönergeler ve daha fazla bilgi için bkz. [Azure Active Directory kullanarak Data Lake Analytics kimlik doğrulaması yapma](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="02e06-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="02e06-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="02e06-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="02e06-113">Bu makalede, bir Data Lake Analytics hesabına yönelik olarak REST API çağrılarının nasıl yapılacağını göstermek üzere cURL kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="02e06-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="02e06-114">Azure Active Directory ile kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="02e06-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="02e06-115">Azure Active Directory ile kimlik doğrulama gerçekleştirmek için kullanılabilecek iki yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="02e06-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="02e06-116">Son kullanıcı kimlik doğrulaması (etkileşimli)</span><span class="sxs-lookup"><span data-stu-id="02e06-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="02e06-117">Bu yöntemi kullanarak, uygulama kullanıcıdan oturum açmasını ister ve tüm işlemler, kullanıcı bağlamında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="02e06-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="02e06-118">Etkileşimli kimlik doğrulaması için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="02e06-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="02e06-119">Uygulamanızı kullanarak kullanıcıyı şu URL'ye yönlendirin:</span><span class="sxs-lookup"><span data-stu-id="02e06-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="02e06-120">\<REDIRECT-URI>, bir URL içinde kullanılmak üzere kodlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="02e06-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="02e06-121">Bu nedenle, https://localhost için `https%3A%2F%2Flocalhost` kullanılır)</span><span class="sxs-lookup"><span data-stu-id="02e06-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="02e06-122">Bu öğreticinin amaçları doğrultusunda, yukarıdaki URL'deki yer tutucu değerlerini değiştirebilir ve bir web tarayıcısının adres çubuğuna yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02e06-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="02e06-123">Azure oturum açma bilgilerinizi kullanarak kimlik doğrulaması gerçekleştirmeye yönlendirileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="02e06-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="02e06-124">Başarıyla oturum açmanızın ardından yanıt, tarayıcının adres çubuğunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="02e06-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="02e06-125">Yanıt şu biçimde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="02e06-126">Yanıttaki yetki kodunu alın.</span><span class="sxs-lookup"><span data-stu-id="02e06-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="02e06-127">Bu öğretici için, web tarayıcısının adres çubuğundan yetki kodunu kopyalayabilir ve belirteç uç noktasını istemek için aşağıda gösterildiği gibi POST isteğinde geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="02e06-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="02e06-128">Bu durumda, \<REDIRECT-URI> öğesinin kodlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="02e06-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="02e06-129">Yanıt, bir erişim belirteci içeren bir JSON nesnesi (ör. `"access_token": "<ACCESS_TOKEN>"`) ve bir yenileme belirtecidir (ör. `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="02e06-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="02e06-130">Uygulamanız Azure Data Lake Store'a erişmek için erişim belirtecini ve bir erişim belirtecinin süresi olduğunda başka bir erişim belirteci almak için yenileme belirtecini kullanır.</span><span class="sxs-lookup"><span data-stu-id="02e06-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="02e06-131">Erişim belirtecinin süresi dolduğunda, aşağıda gösterildiği gibi yenileme belirtecini kullanarak yeni bir erişim belirteci isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="02e06-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="02e06-132">Etkileşimli kullanıcı kimlik doğrulaması hakkında daha fazla bilgi için bkz. [Yetki kodu izin akışı](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="02e06-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="02e06-133">Hizmetten hizmete kimlik doğrulaması (etkileşimli olmayan)</span><span class="sxs-lookup"><span data-stu-id="02e06-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="02e06-134">Bu yöntemi kullanarak uygulama, işlemleri gerçekleştirmek için kendi kimlik bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="02e06-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="02e06-135">Bunun için aşağıda gösterilene benzer bir POST isteği yayımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="02e06-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="02e06-136">Bu isteğin çıktısı, sonrasında REST API çağrılarınızla geçireceğiniz bir yetki belirteci (aşağıdaki çıktıda `access-token` ile belirtilmiştir) içerir.</span><span class="sxs-lookup"><span data-stu-id="02e06-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="02e06-137">Bu kimlik doğrulama belirtecini bir metin dosyasına kaydedin; belirteç, bu makalenin ilerleyen bölümlerinde gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="02e06-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="02e06-138">Bu makalede, **etkileşimli olmayan** yaklaşım kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="02e06-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="02e06-139">Etkileşimli olmayan seçeneği (hizmet-hizmet çağrıları) hakkında daha fazla bilgi için bkz. [Kimlik bilgilerini kullanarak gerçekleştirilen hizmet-hizmet çağrıları](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="02e06-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="02e06-140">Data Lake Analytics hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="02e06-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="02e06-141">Data Lake Analytics hesabı oluşturabilmek için Azure kaynak grubu ve Data Lake Store hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="02e06-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="02e06-142">Bkz. [Data Lake Store hesabı oluşturma](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="02e06-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="02e06-143">Aşağıdaki Curl komutu nasıl hesap oluşturulacağını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="02e06-144">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`AzureSubscriptionID`\> yerine abonelik kimliğinizi, \<`AzureResourceGroupName`\> yerine var olan Azure kaynak grubu adını ve \<`NewAzureDataLakeAnalyticsAccountName`\> yerine yeni Data Lake Analytics hesabı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="02e06-145">Bu komuta yönelik istek yükü, yukarıdaki `-d` parametresi için sağlanan **CreateDatalakeAnalyticsAccountRequest.json** dosyasına dahildir.</span><span class="sxs-lookup"><span data-stu-id="02e06-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="02e06-146">Söz konusu input.json dosyasının içeriği şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="02e06-146">The contents of the input.json file resemble the following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="02e06-147">Bir abonelikteki Data Lake Analytics hesaplarını listeleme</span><span class="sxs-lookup"><span data-stu-id="02e06-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="02e06-148">Aşağıdaki Curl komutu bir abonelikteki hesapların nasıl listeleneceğini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="02e06-149">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`AzureSubscriptionID`\> yerine de abonelik kimliğinizi yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="02e06-150">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-150">The output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="02e06-151">Bir Data Lake Analytics hesabı hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="02e06-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="02e06-152">Aşağıdaki Curl komutu hesap bilgilerinin nasıl alınacağını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="02e06-153">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`AzureSubscriptionID`\> yerine abonelik kimliğinizi, \<`AzureResourceGroupName`\> yerine var olan Azure kaynak grubu adını ve \<`DataLakeAnalyticsAccountName`\> yerine var olan Data Lake Analytics hesabını yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="02e06-154">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-154">The output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="02e06-155">Bir Data Lake Analytics hesabının Data Lake Store bilgilerini listeleme</span><span class="sxs-lookup"><span data-stu-id="02e06-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="02e06-156">Aşağıdaki Curl komutu bir hesaptaki Data Lake Store bilgilerinin nasıl listeleneceğini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="02e06-157">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`AzureSubscriptionID`\> yerine abonelik kimliğinizi, \<`AzureResourceGroupName`\> yerine var olan Azure kaynak grubu adını ve \<`DataLakeAnalyticsAccountName`\> yerine var olan Data Lake Analytics hesabını yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="02e06-158">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-158">The output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="02e06-159">U-SQL işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="02e06-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="02e06-160">Aşağıdaki Curl komutu bir U-SQL işinin nasıl gönderileceğini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="02e06-161">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`DataLakeAnalyticsAccountName`\> yerine de var olan Data Lake Analytics hesabının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="02e06-162">Bu komuta yönelik istek yükü, yukarıdaki `-d` parametresi için sağlanan **SubmitADLAJob.json** dosyasına dahildir.</span><span class="sxs-lookup"><span data-stu-id="02e06-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="02e06-163">Söz konusu input.json dosyasının içeriği şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="02e06-163">The contents of the input.json file resemble the following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="02e06-164">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-164">The output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="02e06-165">U-SQL işlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="02e06-165">List U-SQL jobs</span></span>
<span data-ttu-id="02e06-166">Aşağıdaki Curl komutu bir U-SQL işinin nasıl listeleneceğini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="02e06-167">\<`REDACTED`\> yerine yetkilendirme belirtecini, \<`DataLakeAnalyticsAccountName`\> yerine de var olan Data Lake Analytics hesabının adını yazın.</span><span class="sxs-lookup"><span data-stu-id="02e06-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="02e06-168">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-168">The output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="02e06-169">Katalog öğelerini alma</span><span class="sxs-lookup"><span data-stu-id="02e06-169">Get catalog items</span></span>
<span data-ttu-id="02e06-170">Aşağıdaki Curl komutu katalogdan veritabanlarının nasıl alınacağını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="02e06-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="02e06-171">Çıktı şuna benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="02e06-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="02e06-172">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="02e06-172">See also</span></span>
* <span data-ttu-id="02e06-173">Daha karmaşık bir sorgu görmek için [Azure Data Lake Analytics'i kullanarak Web sitesi günlüklerini çözümleme](data-lake-analytics-analyze-weblogs.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="02e06-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="02e06-174">U-SQL uygulamalarını geliştirmeye başlamak için bkz. [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="02e06-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="02e06-175">U-SQL öğrenmek için bkz. [Azure Data Lake Analytics U-SQL dili ile çalışmaya başlama](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="02e06-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="02e06-176">Yönetim görevleri için bkz. [Azure portalı kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="02e06-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="02e06-177">Data Lake Analytics'e yönelik bir genel bakış için bkz. [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02e06-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="02e06-178">Aynı öğreticiyi diğer araçları kullanarak görmek için sayfanın üst kısmındaki sekme seçicilerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="02e06-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

