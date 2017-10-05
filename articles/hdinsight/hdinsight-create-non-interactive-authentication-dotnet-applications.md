---
title: "Etkileşimli olmayan kimlik doğrulama .NET Hdınsight applciations - Azure oluşturun | Microsoft Docs"
description: "Etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamalarının nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="a4d93-103">Etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4d93-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="a4d93-104">.NET Azure Hdınsight uygulamanızı ya da uygulamanın kendi kimliğini (etkileşimli olmayan) (etkileşimli) uygulamasının oturum açmış kullanıcının kimliğini altında ya da çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d93-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="a4d93-105">Etkileşimli uygulama örnek için bkz: [Azure Hdınsight Bağlan](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="a4d93-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="a4d93-106">Bu makalede Azure bağlanmak ve Hdınsight yönetmek için etkileşimli olmayan kimlik doğrulama .NET uygulamasının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4d93-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="a4d93-107">Etkileşimli olmayan .NET uygulamanızdan, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4d93-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="a4d93-108">Azure aboneliği Kiracı Kimliğinizi (A.K.A dizin kimliği).</span><span class="sxs-lookup"><span data-stu-id="a4d93-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="a4d93-109">Bkz: [alma Kiracı kimliği](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="a4d93-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="a4d93-110">Azure Active Directory Uygulama istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="a4d93-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="a4d93-111">Bkz: [Azure Active Directory Uygulama oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), ve [bir uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="a4d93-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="a4d93-112">Azure Active Directory Uygulama gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="a4d93-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="a4d93-113">Bkz: [Get uygulama kimlik doğrulama anahtarı](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="a4d93-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4d93-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a4d93-114">Prerequisites</span></span>
* <span data-ttu-id="a4d93-115">Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="a4d93-115">HDInsight cluster.</span></span> <span data-ttu-id="a4d93-116">Bkz: [başlama Öğreticisi](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="a4d93-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="a4d93-117">Azure AD uygulama rolü atayın</span><span class="sxs-lookup"><span data-stu-id="a4d93-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="a4d93-118">Uygulamaya atamalısınız bir [rol](../active-directory/role-based-access-built-in-roles.md) eylemleri gerçekleştirmek için izinleri vermek için.</span><span class="sxs-lookup"><span data-stu-id="a4d93-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="a4d93-119">Abonelik, kaynak grubu ya da kaynak düzeyinde kapsamı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d93-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="a4d93-120">Daha düşük düzeyde kapsam (örneğin, kaynak grubu okuyabilmesi için bir kaynak grubu için okuyucu rolüne uygulamaya anlamına gelir ekleme ve içerdiği tüm kaynaklar) devralınan izinleri.</span><span class="sxs-lookup"><span data-stu-id="a4d93-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="a4d93-121">Bu öğreticide kaynak grubu düzeyinde kapsamı ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="a4d93-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="a4d93-122">Daha fazla bilgi için bkz: [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a4d93-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="a4d93-123">**Azure AD uygulama sahip rolünü eklemek için**</span><span class="sxs-lookup"><span data-stu-id="a4d93-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="a4d93-124">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a4d93-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a4d93-125">Tıklatın **kaynak grubu** sol bölmeden.</span><span class="sxs-lookup"><span data-stu-id="a4d93-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="a4d93-126">Daha sonra Bu öğreticide, Hive sorgunuzu çalıştırılacağı Hdınsight kümesi içeren kaynak grubunu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a4d93-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="a4d93-127">Çok fazla kaynak grupları varsa, filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d93-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="a4d93-128">Tıklatın **erişim denetimi (IAM)** kaynak grubu menüsünde.</span><span class="sxs-lookup"><span data-stu-id="a4d93-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="a4d93-129">Tıklatın **Ekle** gelen **kullanıcılar** dikey.</span><span class="sxs-lookup"><span data-stu-id="a4d93-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="a4d93-130">Eklemek için yönergeleri izleyin **sahibi** Azure AD uygulaması rolüne son yordamda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="a4d93-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="a4d93-131">Başarıyla tamamladıktan sonra kullanıcılar dikey penceresi sahip rolünü ile listelenen uygulama göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a4d93-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="a4d93-132">Hdınsight istemci uygulaması geliştirme</span><span class="sxs-lookup"><span data-stu-id="a4d93-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="a4d93-133">Bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4d93-133">Create a C# console application.</span></span>
2. <span data-ttu-id="a4d93-134">Aşağıdaki Nuget paketleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a4d93-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="a4d93-135">Aşağıdaki kod örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="a4d93-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="a4d93-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4d93-136">Next steps</span></span>
* [<span data-ttu-id="a4d93-137">Azure Active Directory uygulaması ve hizmet sorumlusu portal kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4d93-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="a4d93-138">Hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a4d93-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="a4d93-139">Azure rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="a4d93-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
