---
title: "aaaCreate etkileşimli olmayan kimlik doğrulama .NET Hdınsight applciations - Azure | Microsoft Docs"
description: "Bilgi nasıl toocreate .NET Hdınsight uygulamaları etkileşimli olmayan kimlik doğrulaması."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="e91d8-103">Etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91d8-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="e91d8-104">.NET Azure Hdınsight uygulamanızı ya da uygulamanın kendi kimliğini (etkileşimli olmayan) hello oturum açmış kullanıcının (etkileşimli) hello uygulamasının hello kimliğini altında ya da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91d8-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="e91d8-105">Merhaba etkileşimli uygulaması örnek için bkz: [tooAzure Hdınsight bağlanmak](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="e91d8-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="e91d8-106">Bu makale size nasıl gösterir toocreate etkileşimli olmayan kimlik doğrulama .NET uygulama tooconnect tooAzure ve Hdınsight yönetin.</span><span class="sxs-lookup"><span data-stu-id="e91d8-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="e91d8-107">Etkileşimli olmayan .NET uygulamanızdan, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="e91d8-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="e91d8-108">Azure aboneliği Kiracı Kimliğinizi (A.K.A dizin kimliği).</span><span class="sxs-lookup"><span data-stu-id="e91d8-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="e91d8-109">Bkz: [alma Kiracı kimliği](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="e91d8-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="e91d8-110">Hello Azure Active Directory Uygulama istemci kimliği</span><span class="sxs-lookup"><span data-stu-id="e91d8-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="e91d8-111">Bkz: [Azure Active Directory Uygulama oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), ve [bir uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="e91d8-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="e91d8-112">Hello Azure Active Directory Uygulama gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="e91d8-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="e91d8-113">Bkz: [Get uygulama kimlik doğrulama anahtarı](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="e91d8-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e91d8-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e91d8-114">Prerequisites</span></span>
* <span data-ttu-id="e91d8-115">Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="e91d8-115">HDInsight cluster.</span></span> <span data-ttu-id="e91d8-116">Bkz: [başlama Öğreticisi](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="e91d8-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="e91d8-117">Azure AD uygulama toorole atayın</span><span class="sxs-lookup"><span data-stu-id="e91d8-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="e91d8-118">Merhaba uygulama tooa atamalısınız [rol](../active-directory/role-based-access-built-in-roles.md) toogrant bu eylemleri gerçekleştirmek için izinler.</span><span class="sxs-lookup"><span data-stu-id="e91d8-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="e91d8-119">Merhaba kapsam hello abonelik, kaynak grubu ya da kaynak hello düzeyinde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91d8-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="e91d8-120">Merhaba, kapsam (örneğin, bir kaynak grubu için bir uygulama toohello okuyucu rolüne hello kaynak grubu okuyabilir anlamına gelir ekleme ve içerdiği tüm kaynaklar) devralınan toolower düzeyleri izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="e91d8-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="e91d8-121">Bu öğreticide, hello kaynak grubu düzeyinde hello kapsam ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="e91d8-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="e91d8-122">Daha fazla bilgi için bkz: [rol atamalarını toomanage erişim tooyour Azure aboneliği kaynakları kullanın](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="e91d8-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="e91d8-123">**tooadd hello sahibi rolü toohello Azure AD uygulama**</span><span class="sxs-lookup"><span data-stu-id="e91d8-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="e91d8-124">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e91d8-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e91d8-125">Tıklatın **kaynak grubu** hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="e91d8-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="e91d8-126">Daha sonra Bu öğreticide, Hive sorgunuzu çalıştırılacağı hello Hdınsight kümesi içeren hello kaynak grubunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e91d8-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="e91d8-127">Çok fazla kaynak grupları varsa, hello filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e91d8-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="e91d8-128">Tıklatın **erişim denetimi (IAM)** hello kaynak grubu menüsünde.</span><span class="sxs-lookup"><span data-stu-id="e91d8-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="e91d8-129">Tıklatın **Ekle** hello gelen **kullanıcılar** dikey.</span><span class="sxs-lookup"><span data-stu-id="e91d8-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="e91d8-130">Merhaba yönerge tooadd hello izleyin **sahibi** rol toohello Azure AD uygulaması hello son yordamda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="e91d8-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="e91d8-131">Başarıyla tamamladıktan sonra hello kullanıcılar dikey penceresinde hello sahibi rolüyle listelenen Merhaba uygulaması göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e91d8-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="e91d8-132">Hdınsight istemci uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="e91d8-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="e91d8-133">Bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e91d8-133">Create a C# console application.</span></span>
2. <span data-ttu-id="e91d8-134">Nuget paketleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e91d8-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="e91d8-135">Aşağıdaki kod örneği hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e91d8-135">Use hello following code sample:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a><span data-ttu-id="e91d8-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e91d8-136">Next steps</span></span>
* [<span data-ttu-id="e91d8-137">Azure Active Directory uygulaması ve hizmet sorumlusu portal kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="e91d8-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="e91d8-138">Hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="e91d8-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="e91d8-139">Azure rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="e91d8-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
