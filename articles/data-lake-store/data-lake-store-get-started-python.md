---
title: "aaaUse hello Python SDK tooget Azure Data Lake Store ile çalışmaya | Microsoft Docs"
description: "Nasıl toouse Python SDK toowork Data Lake Store hesapları ve hello dosya sistemi öğrenin."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="84f58-103">Python’u kullanarak Azure Data Lake Store ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84f58-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84f58-104">Portal</span><span class="sxs-lookup"><span data-stu-id="84f58-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="84f58-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f58-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="84f58-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="84f58-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="84f58-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="84f58-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="84f58-108">REST API</span><span class="sxs-lookup"><span data-stu-id="84f58-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="84f58-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="84f58-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="84f58-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="84f58-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="84f58-111">Python</span><span class="sxs-lookup"><span data-stu-id="84f58-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="84f58-112">Nasıl toouse hello Python SDK'sı Azure ve Azure Data Lake Store tooperform temel işlemleri gibi klasör oluşturma için karşıya yükleme ve indirme veri dosyaları, vb. öğrenin. Data Lake hakkında daha fazla bilgi için bkz. [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84f58-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84f58-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84f58-113">Prerequisites</span></span>

* <span data-ttu-id="84f58-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="84f58-114">**Python**.</span></span> <span data-ttu-id="84f58-115">Python’u [buradan](https://www.python.org/downloads/) indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f58-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="84f58-116">Bu makalede Python 3.5.2 kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="84f58-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="84f58-117">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="84f58-117">**An Azure subscription**.</span></span> <span data-ttu-id="84f58-118">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84f58-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="84f58-119">**Azure Active Directory Uygulaması oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="84f58-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="84f58-120">Azure AD ile hello Azure AD uygulama tooauthenticate hello Data Lake Store uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="84f58-121">Hangi Azure AD ile farklı yaklaşımlara tooauthenticate olan **son kullanıcı kimlik doğrulaması** veya **hizmeti için kimlik doğrulama**.</span><span class="sxs-lookup"><span data-stu-id="84f58-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="84f58-122">Yönergeler ve hakkında daha fazla bilgi için tooauthenticate, bkz: [son kullanıcı kimlik doğrulaması](data-lake-store-end-user-authenticate-using-active-directory.md) veya [hizmeti için kimlik doğrulama](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="84f58-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="84f58-123">Merhaba modüllerini yükleyin</span><span class="sxs-lookup"><span data-stu-id="84f58-123">Install hello modules</span></span>

<span data-ttu-id="84f58-124">toowork Python kullanarak Data Lake Store ile tooinstall üç modülleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f58-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="84f58-125">Merhaba `azure-mgmt-resource` modülü.</span><span class="sxs-lookup"><span data-stu-id="84f58-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="84f58-126">Bu, Active Directory gibi şeyler için Azure modüllerini içerir</span><span class="sxs-lookup"><span data-stu-id="84f58-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="84f58-127">Merhaba `azure-mgmt-datalake-store` modülü.</span><span class="sxs-lookup"><span data-stu-id="84f58-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="84f58-128">Bu hello Azure Data Lake Store hesabı yönetim işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="84f58-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="84f58-129">Bu modül hakkında daha fazla bilgi için bkz. [Azure Data Lake Store Yönetimi modül başvurusu](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="84f58-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="84f58-130">Merhaba `azure-datalake-store` modülü.</span><span class="sxs-lookup"><span data-stu-id="84f58-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="84f58-131">Bu hello Azure Data Lake Store dosya sistemi işlemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="84f58-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="84f58-132">Bu modül hakkında daha fazla bilgi için bkz. [Azure Data Lake Store Dosya Sistemi modül başvurusu](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="84f58-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="84f58-133">Aşağıdaki komutları tooinstall hello modülleri hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="84f58-134">Yeni Python uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f58-134">Create a new Python application</span></span>

1. <span data-ttu-id="84f58-135">Merhaba tercih ettiğiniz IDE Örneğin, yeni bir Python uygulaması oluşturma **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="84f58-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="84f58-136">Aşağıdaki satırları tooimport gerekli hello modülleri hello ekleme</span><span class="sxs-lookup"><span data-stu-id="84f58-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="84f58-137">Değişiklikleri toomysample.py kaydedin.</span><span class="sxs-lookup"><span data-stu-id="84f58-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="84f58-138">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-138">Authentication</span></span>

<span data-ttu-id="84f58-139">Bu bölümde, biz hello farklı şekillerde tooauthenticate Azure AD ile ilgili konuşun.</span><span class="sxs-lookup"><span data-stu-id="84f58-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="84f58-140">Başlangıç seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="84f58-140">hello options available are:</span></span>

* <span data-ttu-id="84f58-141">Son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-141">End-user authentication</span></span>
* <span data-ttu-id="84f58-142">Hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-142">Service-to-service authentication</span></span>
* <span data-ttu-id="84f58-143">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="84f58-143">Multi-factor authentication</span></span>

<span data-ttu-id="84f58-144">Bu kimlik doğrulama seçeneklerini hem hesap yönetimi hem de dosya sistemi yönetim modülleri için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f58-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="84f58-145">Hesap yönetimi için son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-145">End-user authentication for account management</span></span>

<span data-ttu-id="84f58-146">Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="84f58-147">Bir Azure AD kullanıcısının kullanıcı adını ve parolasını sağlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="84f58-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="84f58-148">Merhaba kullanıcının çok faktörlü kimlik doğrulaması için yapılandırılmamalıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="84f58-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="84f58-149">Dosya sistemi işlemleri için son kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="84f58-150">Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="84f58-151">Bunu mevcut bir Azure AD **yerel istemci** uygulaması ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="84f58-152">hello Azure AD kullanıcı kimlik bilgilerini sağlayın, çok faktörlü kimlik doğrulaması için yapılandırılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="84f58-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="84f58-153">Hesap yönetimi için gizli anahtarla hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="84f58-154">Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="84f58-155">Merhaba kod parçacığında kullanılan tooauthenticate uygulamanızı etkileşimsiz, hello gizli bir uygulama / hizmet sorumlusu için kullanılması olabilir.</span><span class="sxs-lookup"><span data-stu-id="84f58-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="84f58-156">Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="84f58-157">Dosya sistemi işlemleri için gizli anahtarla hizmetten hizmete kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="84f58-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="84f58-158">Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="84f58-159">Merhaba kod parçacığında kullanılan tooauthenticate uygulamanızı etkileşimsiz, hello gizli bir uygulama / hizmet sorumlusu için kullanılması olabilir.</span><span class="sxs-lookup"><span data-stu-id="84f58-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="84f58-160">Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="84f58-161">Hesap yönetimi için multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="84f58-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="84f58-162">Bu tooauthenticate (oluşturma/silme Data Lake Store hesabı, vs.) hesap yönetimi işlemleri için Azure AD ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="84f58-163">Merhaba aşağıdaki kod parçacığında olabilir çok faktörlü kimlik doğrulaması kullanarak uygulamanızı tooauthenticate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84f58-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="84f58-164">Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="84f58-165">Dosya sistemi yönetimi için multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="84f58-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="84f58-166">Dosya sistemi işlemleri (klasör, karşıya yükleme dosyasını oluşturun.) Azure AD ile bu tooauthenticate kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="84f58-167">Merhaba aşağıdaki kod parçacığında olabilir çok faktörlü kimlik doğrulaması kullanarak uygulamanızı tooauthenticate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84f58-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="84f58-168">Bunu mevcut Azure AD "Web App" uygulaması ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f58-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="84f58-169">Azure Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f58-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="84f58-170">Aşağıdaki kod parçacığını toocreate Azure kaynak grubu hello kullan:</span><span class="sxs-lookup"><span data-stu-id="84f58-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="84f58-171">İstemciler ve Data Lake Store hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f58-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="84f58-172">kod parçacığında önce aşağıdaki hello hello Data Lake Store hesabı istemci oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84f58-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="84f58-173">Merhaba istemci nesnesi toocreate Data Lake Store hesabını kullanır.</span><span class="sxs-lookup"><span data-stu-id="84f58-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="84f58-174">Son olarak, hello kod parçacığında, bir dosya sistemi istemci nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84f58-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="84f58-175">Merhaba Data Lake Store hesapları listeleme</span><span class="sxs-lookup"><span data-stu-id="84f58-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="84f58-176">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f58-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="84f58-177">Dosyayı karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="84f58-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="84f58-178">Dosya indirme</span><span class="sxs-lookup"><span data-stu-id="84f58-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="84f58-179">Bir dizini silme</span><span class="sxs-lookup"><span data-stu-id="84f58-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="84f58-180">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="84f58-180">See also</span></span>

- [<span data-ttu-id="84f58-181">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="84f58-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="84f58-182">Azure Data Lake Analytics'i Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="84f58-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="84f58-183">Azure HDInsight'ı Data Lake Store ile kullanma</span><span class="sxs-lookup"><span data-stu-id="84f58-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="84f58-184">Data Lake Store .NET SDK Başvurusu</span><span class="sxs-lookup"><span data-stu-id="84f58-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="84f58-185">Data Lake Store REST Başvurusu</span><span class="sxs-lookup"><span data-stu-id="84f58-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
