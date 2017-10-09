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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma
.NET Azure Hdınsight uygulamanızı ya da uygulamanın kendi kimliğini (etkileşimli olmayan) hello oturum açmış kullanıcının (etkileşimli) hello uygulamasının hello kimliğini altında ya da çalıştırabilirsiniz. Merhaba etkileşimli uygulaması örnek için bkz: [tooAzure Hdınsight bağlanmak](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Bu makale size nasıl gösterir toocreate etkileşimli olmayan kimlik doğrulama .NET uygulama tooconnect tooAzure ve Hdınsight yönetin.

Etkileşimli olmayan .NET uygulamanızdan, aşağıdakiler gerekir:

* Azure aboneliği Kiracı Kimliğinizi (A.K.A dizin kimliği). Bkz: [alma Kiracı kimliği](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* Hello Azure Active Directory Uygulama istemci kimliği Bkz: [Azure Active Directory Uygulama oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), ve [bir uygulama kimliği alma](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* Hello Azure Active Directory Uygulama gizli anahtarı. Bkz: [Get uygulama kimlik doğrulama anahtarı](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)

## <a name="prerequisites"></a>Ön koşullar
* Hdınsight kümesi. Bkz: [başlama Öğreticisi](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Azure AD uygulama toorole atayın
Merhaba uygulama tooa atamalısınız [rol](../active-directory/role-based-access-built-in-roles.md) toogrant bu eylemleri gerçekleştirmek için izinler. Merhaba kapsam hello abonelik, kaynak grubu ya da kaynak hello düzeyinde ayarlayabilirsiniz. Merhaba, kapsam (örneğin, bir kaynak grubu için bir uygulama toohello okuyucu rolüne hello kaynak grubu okuyabilir anlamına gelir ekleme ve içerdiği tüm kaynaklar) devralınan toolower düzeyleri izinlerdir. Bu öğreticide, hello kaynak grubu düzeyinde hello kapsam ayarlarsınız. Daha fazla bilgi için bkz: [rol atamalarını toomanage erişim tooyour Azure aboneliği kaynakları kullanın](../active-directory/role-based-access-control-configure.md)

**tooadd hello sahibi rolü toohello Azure AD uygulama**

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **kaynak grubu** hello sol bölmesinden.
3. Daha sonra Bu öğreticide, Hive sorgunuzu çalıştırılacağı hello Hdınsight kümesi içeren hello kaynak grubunu tıklatın. Çok fazla kaynak grupları varsa, hello filtresini kullanabilirsiniz.
4. Tıklatın **erişim denetimi (IAM)** hello kaynak grubu menüsünde.
5. Tıklatın **Ekle** hello gelen **kullanıcılar** dikey.
6. Merhaba yönerge tooadd hello izleyin **sahibi** rol toohello Azure AD uygulaması hello son yordamda oluşturduğunuz. Başarıyla tamamladıktan sonra hello kullanıcılar dikey penceresinde hello sahibi rolüyle listelenen Merhaba uygulaması göreceksiniz.

## <a name="develop-hdinsight-client-application"></a>Hdınsight istemci uygulaması geliştirme

1. Bir C# konsol uygulaması oluşturun.
2. Nuget paketleri aşağıdaki hello ekleyin:

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Aşağıdaki kod örneği hello kullan:

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

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Active Directory uygulaması ve hizmet sorumlusu portal kullanarak oluşturma](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)
