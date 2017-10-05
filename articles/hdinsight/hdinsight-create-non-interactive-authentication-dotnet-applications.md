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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma
.NET Azure Hdınsight uygulamanızı ya da uygulamanın kendi kimliğini (etkileşimli olmayan) (etkileşimli) uygulamasının oturum açmış kullanıcının kimliğini altında ya da çalıştırabilirsiniz. Etkileşimli uygulama örnek için bkz: [Azure Hdınsight Bağlan](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Bu makalede Azure bağlanmak ve Hdınsight yönetmek için etkileşimli olmayan kimlik doğrulama .NET uygulamasının nasıl oluşturulacağını gösterir.

Etkileşimli olmayan .NET uygulamanızdan, aşağıdakiler gerekir:

* Azure aboneliği Kiracı Kimliğinizi (A.K.A dizin kimliği). Bkz: [alma Kiracı kimliği](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Azure Active Directory Uygulama istemci kimliği. Bkz: [Azure Active Directory Uygulama oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), ve [bir uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* Azure Active Directory Uygulama gizli anahtarı. Bkz: [Get uygulama kimlik doğrulama anahtarı](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Ön koşullar
* Hdınsight kümesi. Bkz: [başlama Öğreticisi](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-to-role"></a>Azure AD uygulama rolü atayın
Uygulamaya atamalısınız bir [rol](../active-directory/role-based-access-built-in-roles.md) eylemleri gerçekleştirmek için izinleri vermek için. Abonelik, kaynak grubu ya da kaynak düzeyinde kapsamı ayarlayabilirsiniz. Daha düşük düzeyde kapsam (örneğin, kaynak grubu okuyabilmesi için bir kaynak grubu için okuyucu rolüne uygulamaya anlamına gelir ekleme ve içerdiği tüm kaynaklar) devralınan izinleri. Bu öğreticide kaynak grubu düzeyinde kapsamı ayarlarsınız. Daha fazla bilgi için bkz: [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](../active-directory/role-based-access-control-configure.md)

**Azure AD uygulama sahip rolünü eklemek için**

1. [Azure Portal](https://portal.azure.com) oturum açın.
2. Tıklatın **kaynak grubu** sol bölmeden.
3. Daha sonra Bu öğreticide, Hive sorgunuzu çalıştırılacağı Hdınsight kümesi içeren kaynak grubunu tıklatın. Çok fazla kaynak grupları varsa, filtresini kullanabilirsiniz.
4. Tıklatın **erişim denetimi (IAM)** kaynak grubu menüsünde.
5. Tıklatın **Ekle** gelen **kullanıcılar** dikey.
6. Eklemek için yönergeleri izleyin **sahibi** Azure AD uygulaması rolüne son yordamda oluşturduğunuz. Başarıyla tamamladıktan sonra kullanıcılar dikey penceresi sahip rolünü ile listelenen uygulama göreceksiniz.

## <a name="develop-hdinsight-client-application"></a>Hdınsight istemci uygulaması geliştirme

1. Bir C# konsol uygulaması oluşturun.
2. Aşağıdaki Nuget paketleri ekleyin:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Aşağıdaki kod örneği kullanın:

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

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Active Directory uygulaması ve hizmet sorumlusu portal kullanarak oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)
