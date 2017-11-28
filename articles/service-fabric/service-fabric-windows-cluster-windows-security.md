---
title: "Windows güvenliği kullanarak Windows çalıştıran bir kümeye güvenli | Microsoft Docs"
description: "Windows güvenliği kullanarak Windows üzerinde çalışan tek başına kümedeki düğüm düğümü ve istemci düğümü güvenlik yapılandırmayı öğrenin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: e093a631b0cf81195981a8e3d345504ebce02723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="b378b-103">Windows tek başına bir kümede Windows güvenliği kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="b378b-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="b378b-104">Bir Service Fabric kümesi yetkisiz erişimi önlemek için küme güvenlik altına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b378b-104">To prevent unauthorized access to a Service Fabric cluster, you must secure the cluster.</span></span> <span data-ttu-id="b378b-105">Küme üretim iş yükleri çalıştığında güvenlik özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b378b-105">Security is especially important when the cluster runs production workloads.</span></span> <span data-ttu-id="b378b-106">Bu makalede Windows güvenliği kullanarak düğümü düğümü ve istemci düğümü güvenliği yapılandırmak nasıl *ClusterConfig.JSON* dosya.</span><span class="sxs-lookup"><span data-stu-id="b378b-106">This article describes how to configure node-to-node and client-to-node security by using Windows security in the *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="b378b-107">İşleme için yapılandırma güvenlik adımı, karşılık gelen [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="b378b-107">The process corresponds to the configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="b378b-108">Service Fabric Windows güvenliği nasıl kullandığı hakkında daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="b378b-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b378b-109">Bir güvenlik seçim diğerine hiçbir Küme yükseltme olduğundan düğümü düğümü güvenlik seçimini dikkatle düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b378b-109">You should consider the selection of node-to-node security carefully because there is no cluster upgrade from one security choice to another.</span></span> <span data-ttu-id="b378b-110">Güvenlik seçimini değiştirmek için tam küme yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="b378b-110">To change the security selection, you have to rebuild the full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="b378b-111">GMSA kullanarak Windows güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b378b-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="b378b-112">Örnek *ClusterConfig.gMSA.Windows.MultiMachine.JSON* yapılandırma dosyası ile indirilen [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi içeren Windows güvenliği kullanarak yapılandırmak için bir şablon [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="b378b-112">The sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| <span data-ttu-id="b378b-113">**Yapılandırma ayarı**</span><span class="sxs-lookup"><span data-stu-id="b378b-113">**Configuration Setting**</span></span> | <span data-ttu-id="b378b-114">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b378b-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="b378b-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="b378b-115">WindowsIdentities</span></span> |<span data-ttu-id="b378b-116">Küme ve istemci kimliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b378b-116">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="b378b-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="b378b-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="b378b-118">Düğümü düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b378b-118">Configures node-to-node security.</span></span> <span data-ttu-id="b378b-119">Bir grup yönetilen hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="b378b-119">A group managed service account.</span></span> |  
| <span data-ttu-id="b378b-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="b378b-120">ClusterSPN</span></span> |<span data-ttu-id="b378b-121">GMSA hesabının tam olarak nitelenmiş etki alanı SPN</span><span class="sxs-lookup"><span data-stu-id="b378b-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="b378b-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="b378b-122">ClientIdentities</span></span> |<span data-ttu-id="b378b-123">İstemcisi düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b378b-123">Configures client-to-node security.</span></span> <span data-ttu-id="b378b-124">İstemci kullanıcı hesapları dizisi.</span><span class="sxs-lookup"><span data-stu-id="b378b-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="b378b-125">Kimlik</span><span class="sxs-lookup"><span data-stu-id="b378b-125">Identity</span></span> |<span data-ttu-id="b378b-126">İstemci kimliği, bir etki alanı kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="b378b-126">The client identity, a domain user.</span></span> |  
| <span data-ttu-id="b378b-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="b378b-127">IsAdmin</span></span> |<span data-ttu-id="b378b-128">TRUE, etki alanı kullanıcısı yönetici istemci erişimi, kullanıcı istemci erişimi için yanlış olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b378b-128">True specifies that the domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="b378b-129">[Düğüm güvenlik düğüme](service-fabric-cluster-security.md#node-to-node-security) ayarlayarak yapılandırılmış **ClustergMSAIdentity** service fabric gerektiği zaman gMSA altında çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="b378b-129">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs to run under gMSA.</span></span> <span data-ttu-id="b378b-130">Düğümler arasındaki güven ilişkileri oluşturmak için bunlar birbirinden haberdar olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b378b-130">In order to build trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="b378b-131">Bu iki farklı yolla gerçekleştirilebilir: Grup yönetilen hizmet kümedeki tüm düğümleri içeren hesabı veya kümedeki tüm düğümleri içeren etki alanı makine grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b378b-131">This can be accomplished in two different ways: Specify the Group Managed Service Account that includes all nodes in the cluster or Specify the domain machine group that includes all nodes in the cluster.</span></span> <span data-ttu-id="b378b-132">Kullanmanızı öneririz [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) yaklaşım, özellikle büyük kümeler (10'dan fazla düğüm) veya büyütür veya küçültür olasılığı kümeleri.</span><span class="sxs-lookup"><span data-stu-id="b378b-132">We strongly recommend using the [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely to grow or shrink.</span></span>  
<span data-ttu-id="b378b-133">Bu yaklaşım eklemek ve üyeleri kaldırmak için erişim haklarını küme yöneticileri verilmiş bir etki alanı grubu oluşturulmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="b378b-133">This approach does not require the creation of a domain group for which cluster administrators have been granted access rights to add and remove members.</span></span> <span data-ttu-id="b378b-134">Bu hesaplar, otomatik parola yönetimi için de yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b378b-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="b378b-135">Daha fazla bilgi için bkz: [Grup yönetilen hizmet hesapları ile çalışmaya başlama](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="b378b-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="b378b-136">[Düğüm güvenlik istemciye](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılmış **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="b378b-136">[Client to node security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="b378b-137">Bir istemci ve küme arasında güven sağlamak için hangi istemci, güvenilir kimlikleri bilmeniz küme yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b378b-137">In order to establish trust between a client and the cluster, you must configure the cluster to know which client identities that it can trust.</span></span> <span data-ttu-id="b378b-138">Bu iki farklı şekillerde yapılabilir: bağlanın veya bağlanabilmesi için etki alanı düğümü kullanıcıları belirtmek etki alanı grubu kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="b378b-138">This can be done in two different ways: Specify the domain group users that can connect or specify the domain node users that can connect.</span></span> <span data-ttu-id="b378b-139">Service Fabric Service Fabric kümeye bağlı istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="b378b-139">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="b378b-140">Erişim denetimi, belirli türde bir küme işlemleri farklı küme daha güvenli hale getirme kullanıcı grupları için erişimi sınırlamak Küme Yöneticisi yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="b378b-140">Access control provides the ability for the cluster administrator to limit access to certain types of cluster operations for different groups of users, making the cluster more secure.</span></span>  <span data-ttu-id="b378b-141">Yöneticiler için yönetim özellikleri (okuma/yazma özellikleri dahil) tam erişime sahip.</span><span class="sxs-lookup"><span data-stu-id="b378b-141">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="b378b-142">Kullanıcıların varsayılan olarak, yalnızca yönetim özellikleri (örneğin, sorgu özellikleri) okuma erişimi ve uygulamaları ve Hizmetleri çözümleme olanağı vardır.</span><span class="sxs-lookup"><span data-stu-id="b378b-142">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span> <span data-ttu-id="b378b-143">Erişim denetimleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b378b-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="b378b-144">Aşağıdaki örnek **güvenlik** bölüm Windows güvenliği kullanarak gMSA yapılandırır ve belirten makinelerinizde *ServiceFabric.clusterA.contoso.com* gMSA küme ve o parçasıolan *CONTOSO\usera* yönetici istemci erişimi vardır:</span><span class="sxs-lookup"><span data-stu-id="b378b-144">The following example **security** section configures Windows security using gMSA and specifies that the machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of the cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="b378b-145">Makine grubu kullanarak Windows güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b378b-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="b378b-146">Örnek *ClusterConfig.Windows.MultiMachine.JSON* yapılandırma dosyası ile indirilen [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi, Windows güvenliği yapılandırmak için bir şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="b378b-146">The sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with the [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="b378b-147">Windows güvenliği yapılandırılmıştır **özellikleri** bölümü:</span><span class="sxs-lookup"><span data-stu-id="b378b-147">Windows security is configured in the **Properties** section:</span></span> 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| <span data-ttu-id="b378b-148">**Yapılandırma ayarı**</span><span class="sxs-lookup"><span data-stu-id="b378b-148">**Configuration setting**</span></span> | <span data-ttu-id="b378b-149">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="b378b-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="b378b-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="b378b-150">ClusterCredentialType</span></span> |<span data-ttu-id="b378b-151">**ClusterCredentialType** ayarlanır *Windows* ClusterIdentity bir Active Directory makine grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b378b-151">**ClusterCredentialType** is set to *Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="b378b-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="b378b-152">ServerCredentialType</span></span> |<span data-ttu-id="b378b-153">Kümesine *Windows* istemcilerde Windows güvenliği etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="b378b-153">Set to *Windows* to enable Windows security for clients.</span></span><br /><br /><span data-ttu-id="b378b-154">Bu, küme ve küme istemcilerinin bir Active Directory etki alanı içinde çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b378b-154">This indicates that the clients of the cluster and the cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="b378b-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="b378b-155">WindowsIdentities</span></span> |<span data-ttu-id="b378b-156">Küme ve istemci kimliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="b378b-156">Contains the cluster and client identities.</span></span> |  
| <span data-ttu-id="b378b-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="b378b-157">ClusterIdentity</span></span> |<span data-ttu-id="b378b-158">Makine grubu adı, domain\machinegroup, düğümü düğümü güvenlik yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b378b-158">Use a machine group name, domain\machinegroup, to configure node-to-node security.</span></span> |  
| <span data-ttu-id="b378b-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="b378b-159">ClientIdentities</span></span> |<span data-ttu-id="b378b-160">İstemcisi düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b378b-160">Configures client-to-node security.</span></span> <span data-ttu-id="b378b-161">İstemci kullanıcı hesapları dizisi.</span><span class="sxs-lookup"><span data-stu-id="b378b-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="b378b-162">Kimlik</span><span class="sxs-lookup"><span data-stu-id="b378b-162">Identity</span></span> |<span data-ttu-id="b378b-163">Etki alanı kullanıcısı, istemci kimliği için etki alanı\kullanıcı adı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b378b-163">Add the domain user, domain\username, for the client identity.</span></span> |  
| <span data-ttu-id="b378b-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="b378b-164">IsAdmin</span></span> |<span data-ttu-id="b378b-165">Etki alanı kullanıcısı yönetici istemci erişimi ya da kullanıcı istemci erişimi için yanlış olduğunu belirtmek için true olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b378b-165">Set to true to specify that the domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="b378b-166">[Düğüm güvenlik düğüme](service-fabric-cluster-security.md#node-to-node-security) ayarı kullanılarak yapılandırılır **ClusterIdentity** bir Active Directory etki alanı içinde bir makine grubu kullanmak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b378b-166">[Node to node security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want to use a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="b378b-167">Daha fazla bilgi için bkz: [Active Directory'de bir makine grubu oluştur](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="b378b-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="b378b-168">[İstemcisi düğümü güvenlik](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılan **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="b378b-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="b378b-169">Bir istemci ve küme arasında güven sağlamak için kümenin küme güvenebileceği kimlikleri istemci bilmeniz için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b378b-169">To establish trust between a client and the cluster, you must configure the cluster to know the client identities that the cluster can trust.</span></span> <span data-ttu-id="b378b-170">İki farklı yolla güven kurabilir:</span><span class="sxs-lookup"><span data-stu-id="b378b-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="b378b-171">Bağlanabilmesi için etki alanı grubu kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="b378b-171">Specify the domain group users that can connect.</span></span>
- <span data-ttu-id="b378b-172">Bağlanabilmesi için etki alanı düğümü kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="b378b-172">Specify the domain node users that can connect.</span></span>

<span data-ttu-id="b378b-173">Service Fabric Service Fabric kümeye bağlı istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="b378b-173">Service Fabric supports two different access control types for clients that are connected to a Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="b378b-174">Erişim denetimi, belirli türde bir küme işlemleri için farklı kullanıcı grupları, küme daha güvenli kılan erişimi sınırlamak Küme Yöneticisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b378b-174">Access control enables the cluster administrator to limit access to certain types of cluster operations for different groups of users, which makes the cluster more secure.</span></span>  <span data-ttu-id="b378b-175">Yöneticiler için yönetim özellikleri (okuma/yazma özellikleri dahil) tam erişime sahip.</span><span class="sxs-lookup"><span data-stu-id="b378b-175">Administrators have full access to management capabilities (including read/write capabilities).</span></span> <span data-ttu-id="b378b-176">Kullanıcıların varsayılan olarak, yalnızca yönetim özellikleri (örneğin, sorgu özellikleri) okuma erişimi ve uygulamaları ve Hizmetleri çözümleme olanağı vardır.</span><span class="sxs-lookup"><span data-stu-id="b378b-176">Users, by default, have only read access to management capabilities (for example, query capabilities), and the ability to resolve applications and services.</span></span>  

<span data-ttu-id="b378b-177">Aşağıdaki örnek **güvenlik** bölüm Windows güvenliği yapılandırır, belirleyen makinelerinizde *ServiceFabric/clusterA.contoso.com* kümesinin parçası olan ve bu belirtir*CONTOSO\usera* yönetici istemci erişimi vardır:</span><span class="sxs-lookup"><span data-stu-id="b378b-177">The following example **security** section configures Windows security, specifies that the machines in *ServiceFabric/clusterA.contoso.com* are part of the cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> <span data-ttu-id="b378b-178">Service Fabric bir etki alanı denetleyicisinde dağıtılmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="b378b-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="b378b-179">ClusterConfig.json etki alanı denetleyicisinin IP adresine bir makine grubu kullanırken içermez ve Grup yönetilen hizmet hesabı (gMSA) olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b378b-179">Make sure that ClusterConfig.json does not include the IP address of the domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="b378b-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b378b-180">Next steps</span></span>
<span data-ttu-id="b378b-181">Windows Güvenlik yapılandırdıktan sonra *ClusterConfig.JSON* dosya, küme oluşturma işlemine devam [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="b378b-181">After configuring Windows security in the *ClusterConfig.JSON* file, resume the cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="b378b-182">Düğümü düğümü nasıl güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi, bkz: hakkında daha fazla bilgi için [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="b378b-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="b378b-183">Bkz: [güvenli kümeye Bağlan](service-fabric-connect-to-secure-cluster.md) PowerShell veya FabricClient kullanarak bağlanma örnekler.</span><span class="sxs-lookup"><span data-stu-id="b378b-183">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
