---
title: "Windows güvenliği kullanarak Windows üzerinde çalışan küme a aaaSecure | Microsoft Docs"
description: "Tek başına bir tooconfigure düğümü düğümü ve istemci düğüm güvenlik nasıl küme Windows güvenliği kullanarak Windows üzerinde çalışan öğrenin."
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
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a><span data-ttu-id="63418-103">Windows tek başına bir kümede Windows güvenliği kullanarak güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="63418-103">Secure a standalone cluster on Windows by using Windows security</span></span>
<span data-ttu-id="63418-104">erişim tooa Service Fabric kümesi tooprevent yetkisiz, hello küme güvenlik altına almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63418-104">tooprevent unauthorized access tooa Service Fabric cluster, you must secure hello cluster.</span></span> <span data-ttu-id="63418-105">Merhaba küme üretim iş yükleri çalıştığında güvenlik özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="63418-105">Security is especially important when hello cluster runs production workloads.</span></span> <span data-ttu-id="63418-106">Bu makalede nasıl hello Windows güvenliği kullanarak tooconfigure düğümü düğümü ve istemci düğüm güvenlik *ClusterConfig.JSON* dosya.</span><span class="sxs-lookup"><span data-stu-id="63418-106">This article describes how tooconfigure node-to-node and client-to-node security by using Windows security in hello *ClusterConfig.JSON* file.</span></span>  <span data-ttu-id="63418-107">Merhaba işleme toohello karşılık gelen güvenlik adımında yapılandırma [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="63418-107">hello process corresponds toohello configure security step of [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span> <span data-ttu-id="63418-108">Service Fabric Windows güvenliği nasıl kullandığı hakkında daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="63418-108">For more information about how Service Fabric uses Windows security, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

> [!NOTE]
> <span data-ttu-id="63418-109">Bir güvenlik seçim tooanother'den hiçbir Küme yükseltme olduğundan hello seçimi düğümü düğümü güvenlik dikkatle düşünmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="63418-109">You should consider hello selection of node-to-node security carefully because there is no cluster upgrade from one security choice tooanother.</span></span> <span data-ttu-id="63418-110">toochange hello güvenlik seçimi toorebuild hello tam küme sahip.</span><span class="sxs-lookup"><span data-stu-id="63418-110">toochange hello security selection, you have toorebuild hello full cluster.</span></span>
>
>

## <a name="configure-windows-security-using-gmsa"></a><span data-ttu-id="63418-111">GMSA kullanarak Windows güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="63418-111">Configure Windows security using gMSA</span></span>  
<span data-ttu-id="63418-112">Merhaba örnek *ClusterConfig.gMSA.Windows.MultiMachine.JSON* yapılandırma dosyasını karşıdan ile Merhaba [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi içeren Windows güvenliği kullanarak yapılandırmak için bir şablon [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span><span class="sxs-lookup"><span data-stu-id="63418-112">hello sample *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security using [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):</span></span>  

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
  
| <span data-ttu-id="63418-113">**Yapılandırma ayarı**</span><span class="sxs-lookup"><span data-stu-id="63418-113">**Configuration Setting**</span></span> | <span data-ttu-id="63418-114">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="63418-114">**Description**</span></span> |  
| --- | --- |  
| <span data-ttu-id="63418-115">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="63418-115">WindowsIdentities</span></span> |<span data-ttu-id="63418-116">Merhaba küme ve istemci kimliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="63418-116">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="63418-117">ClustergMSAIdentity</span><span class="sxs-lookup"><span data-stu-id="63418-117">ClustergMSAIdentity</span></span> |<span data-ttu-id="63418-118">Düğümü düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="63418-118">Configures node-to-node security.</span></span> <span data-ttu-id="63418-119">Bir grup yönetilen hizmet hesabı.</span><span class="sxs-lookup"><span data-stu-id="63418-119">A group managed service account.</span></span> |  
| <span data-ttu-id="63418-120">ClusterSPN</span><span class="sxs-lookup"><span data-stu-id="63418-120">ClusterSPN</span></span> |<span data-ttu-id="63418-121">GMSA hesabının tam olarak nitelenmiş etki alanı SPN</span><span class="sxs-lookup"><span data-stu-id="63418-121">Fully qualified domain SPN for gMSA account</span></span>|  
| <span data-ttu-id="63418-122">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="63418-122">ClientIdentities</span></span> |<span data-ttu-id="63418-123">İstemcisi düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="63418-123">Configures client-to-node security.</span></span> <span data-ttu-id="63418-124">İstemci kullanıcı hesapları dizisi.</span><span class="sxs-lookup"><span data-stu-id="63418-124">An array of client user accounts.</span></span> |  
| <span data-ttu-id="63418-125">Kimlik</span><span class="sxs-lookup"><span data-stu-id="63418-125">Identity</span></span> |<span data-ttu-id="63418-126">Merhaba istemci kimliği, bir etki alanı kullanıcısı.</span><span class="sxs-lookup"><span data-stu-id="63418-126">hello client identity, a domain user.</span></span> |  
| <span data-ttu-id="63418-127">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="63418-127">IsAdmin</span></span> |<span data-ttu-id="63418-128">TRUE, hello etki alanı kullanıcısı yönetici istemci erişimi, kullanıcı istemci erişimi için false belirtir.</span><span class="sxs-lookup"><span data-stu-id="63418-128">True specifies that hello domain user has administrator client access, false for user client access.</span></span> |  
  
<span data-ttu-id="63418-129">[Düğüm toonode güvenlik](service-fabric-cluster-security.md#node-to-node-security) ayarlayarak yapılandırılmış **ClustergMSAIdentity** toorun gMSA altında service fabric gerektiği zaman.</span><span class="sxs-lookup"><span data-stu-id="63418-129">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting **ClustergMSAIdentity** when service fabric needs toorun under gMSA.</span></span> <span data-ttu-id="63418-130">Sipariş toobuild güven ilişkilerini düğümler arasında bunlar birbirinden haberdar olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63418-130">In order toobuild trust relationships between nodes, they must be made aware of each other.</span></span> <span data-ttu-id="63418-131">Bu iki farklı yolla gerçekleştirilebilir: hello hello kümedeki tüm düğümleri içeren Grup yönetilen hizmet hesabı veya hello kümedeki tüm düğümleri içerir hello etki alanı makine grubu belirtin.</span><span class="sxs-lookup"><span data-stu-id="63418-131">This can be accomplished in two different ways: Specify hello Group Managed Service Account that includes all nodes in hello cluster or Specify hello domain machine group that includes all nodes in hello cluster.</span></span> <span data-ttu-id="63418-132">Hello kullanarak önerilir [Grup yönetilen hizmet hesabı (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) yaklaşım, özellikle büyük kümeler (10'dan fazla düğüm) veya büyük olasılıkla toogrow ya da küçültmek kümeleri.</span><span class="sxs-lookup"><span data-stu-id="63418-132">We strongly recommend using hello [Group Managed Service Account (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) approach, particularly for larger clusters (more than 10 nodes) or for clusters that are likely toogrow or shrink.</span></span>  
<span data-ttu-id="63418-133">Bu yaklaşım, kendisi için küme yöneticileri erişim hakları tooadd verilmiş ve üye kaldırma bir etki alanı grubu hello oluşturulmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="63418-133">This approach does not require hello creation of a domain group for which cluster administrators have been granted access rights tooadd and remove members.</span></span> <span data-ttu-id="63418-134">Bu hesaplar, otomatik parola yönetimi için de yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="63418-134">These accounts are also useful for automatic password management.</span></span> <span data-ttu-id="63418-135">Daha fazla bilgi için bkz: [Grup yönetilen hizmet hesapları ile çalışmaya başlama](http://technet.microsoft.com/library/jj128431.aspx).</span><span class="sxs-lookup"><span data-stu-id="63418-135">For more information, see [Getting Started with Group Managed Service Accounts](http://technet.microsoft.com/library/jj128431.aspx).</span></span>  
 
<span data-ttu-id="63418-136">[İstemci toonode güvenlik](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılmış **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="63418-136">[Client toonode security](service-fabric-cluster-security.md#client-to-node-security) is configured using **ClientIdentities**.</span></span> <span data-ttu-id="63418-137">Bir istemci ve hello kümesi arasında sipariş tooestablish güven içinde güven hangi istemci kimlikleri hello küme tooknow yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63418-137">In order tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow which client identities that it can trust.</span></span> <span data-ttu-id="63418-138">Bu iki farklı şekillerde yapılabilir: bağlanmak veya belirtmek hello etki alanı grubu kullanıcıları hello bağlanabilmesi için etki alanı düğümü kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="63418-138">This can be done in two different ways: Specify hello domain group users that can connect or specify hello domain node users that can connect.</span></span> <span data-ttu-id="63418-139">Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="63418-139">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="63418-140">Erişim denetimi Küme Yöneticisi toolimit erişim toocertain türü küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için hello hello yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="63418-140">Access control provides hello ability for hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, making hello cluster more secure.</span></span>  <span data-ttu-id="63418-141">Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="63418-141">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="63418-142">Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="63418-142">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span> <span data-ttu-id="63418-143">Erişim denetimleri hakkında daha fazla bilgi için bkz: [Service Fabric istemciler için rol tabanlı erişim denetimi](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="63418-143">For more information on access controls, see [Role based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>  
 
<span data-ttu-id="63418-144">Örnek Hello **güvenlik** bölüm Windows güvenliği kullanarak gMSA yapılandırır ve bu hello makineleri belirtir *ServiceFabric.clusterA.contoso.com* gMSA hello küme ve, parçası olan *CONTOSO\usera* yönetici istemci erişimi vardır:</span><span class="sxs-lookup"><span data-stu-id="63418-144">hello following example **security** section configures Windows security using gMSA and specifies that hello machines in *ServiceFabric.clusterA.contoso.com* gMSA are part of hello cluster and that *CONTOSO\usera* has admin client access:</span></span>  
  
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
  
## <a name="configure-windows-security-using-a-machine-group"></a><span data-ttu-id="63418-145">Makine grubu kullanarak Windows güvenliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="63418-145">Configure Windows security using a machine group</span></span>  
<span data-ttu-id="63418-146">Merhaba örnek *ClusterConfig.Windows.MultiMachine.JSON* yapılandırma dosyasını karşıdan ile Merhaba [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. zip](http://go.microsoft.com/fwlink/?LinkId=730690) tek başına küme paketi, Windows güvenliği yapılandırmak için bir şablonu içerir.</span><span class="sxs-lookup"><span data-stu-id="63418-146">hello sample *ClusterConfig.Windows.MultiMachine.JSON* configuration file downloaded with hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>.zip](http://go.microsoft.com/fwlink/?LinkId=730690) standalone cluster package contains a template for configuring Windows security.</span></span>  <span data-ttu-id="63418-147">Windows güvenliği hello yapılandırılmış **özellikleri** bölümü:</span><span class="sxs-lookup"><span data-stu-id="63418-147">Windows security is configured in hello **Properties** section:</span></span> 

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

| <span data-ttu-id="63418-148">**Yapılandırma ayarı**</span><span class="sxs-lookup"><span data-stu-id="63418-148">**Configuration setting**</span></span> | <span data-ttu-id="63418-149">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="63418-149">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="63418-150">ClusterCredentialType</span><span class="sxs-lookup"><span data-stu-id="63418-150">ClusterCredentialType</span></span> |<span data-ttu-id="63418-151">**ClusterCredentialType** çok ayarlanır*Windows* ClusterIdentity bir Active Directory makine grubu adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="63418-151">**ClusterCredentialType** is set too*Windows* if ClusterIdentity specifies an Active Directory Machine Group Name.</span></span> |  
| <span data-ttu-id="63418-152">ServerCredentialType</span><span class="sxs-lookup"><span data-stu-id="63418-152">ServerCredentialType</span></span> |<span data-ttu-id="63418-153">Çok ayarlamak*Windows* tooenable istemciler için Windows Güvenlik.</span><span class="sxs-lookup"><span data-stu-id="63418-153">Set too*Windows* tooenable Windows security for clients.</span></span><br /><br /><span data-ttu-id="63418-154">Bu, hello istemcileri hello küme hello kümenin kendisi ve bir Active Directory etki alanı içinde çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="63418-154">This indicates that hello clients of hello cluster and hello cluster itself are running within an Active Directory domain.</span></span> |  
| <span data-ttu-id="63418-155">WindowsIdentities</span><span class="sxs-lookup"><span data-stu-id="63418-155">WindowsIdentities</span></span> |<span data-ttu-id="63418-156">Merhaba küme ve istemci kimliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="63418-156">Contains hello cluster and client identities.</span></span> |  
| <span data-ttu-id="63418-157">ClusterIdentity</span><span class="sxs-lookup"><span data-stu-id="63418-157">ClusterIdentity</span></span> |<span data-ttu-id="63418-158">Makine grubu adı, domain\machinegroup, tooconfigure düğümü düğümü güvenlik kullanın.</span><span class="sxs-lookup"><span data-stu-id="63418-158">Use a machine group name, domain\machinegroup, tooconfigure node-to-node security.</span></span> |  
| <span data-ttu-id="63418-159">ClientIdentities</span><span class="sxs-lookup"><span data-stu-id="63418-159">ClientIdentities</span></span> |<span data-ttu-id="63418-160">İstemcisi düğümü güvenliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="63418-160">Configures client-to-node security.</span></span> <span data-ttu-id="63418-161">İstemci kullanıcı hesapları dizisi.</span><span class="sxs-lookup"><span data-stu-id="63418-161">An array of client user accounts.</span></span> |  
| <span data-ttu-id="63418-162">Kimlik</span><span class="sxs-lookup"><span data-stu-id="63418-162">Identity</span></span> |<span data-ttu-id="63418-163">Merhaba etki alanı kullanıcısı, hello istemci kimliği için etki alanı\kullanıcı adı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63418-163">Add hello domain user, domain\username, for hello client identity.</span></span> |  
| <span data-ttu-id="63418-164">IsAdmin</span><span class="sxs-lookup"><span data-stu-id="63418-164">IsAdmin</span></span> |<span data-ttu-id="63418-165">Etki alanı kullanıcısı hello kümesi tootrue toospecify yönetici istemci erişimi ya da kullanıcı istemci erişimi için yanlış sahiptir.</span><span class="sxs-lookup"><span data-stu-id="63418-165">Set tootrue toospecify that hello domain user has administrator client access or false for user client access.</span></span> |  

<span data-ttu-id="63418-166">[Düğüm toonode güvenlik](service-fabric-cluster-security.md#node-to-node-security) ayarı kullanılarak yapılandırılır **ClusterIdentity** toouse bir Active Directory etki alanı içindeki bir makine grubun istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="63418-166">[Node toonode security](service-fabric-cluster-security.md#node-to-node-security) is configured by setting using **ClusterIdentity** if you want toouse a machine group within an Active Directory Domain.</span></span> <span data-ttu-id="63418-167">Daha fazla bilgi için bkz: [Active Directory'de bir makine grubu oluştur](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span><span class="sxs-lookup"><span data-stu-id="63418-167">For more information, see [Create a Machine Group in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).</span></span>

<span data-ttu-id="63418-168">[İstemcisi düğümü güvenlik](service-fabric-cluster-security.md#client-to-node-security) kullanılarak yapılandırılan **ClientIdentities**.</span><span class="sxs-lookup"><span data-stu-id="63418-168">[Client-to-node security](service-fabric-cluster-security.md#client-to-node-security) is configured by using **ClientIdentities**.</span></span> <span data-ttu-id="63418-169">tooestablish güven bir istemci ve hello kümesi arasında küme hello kimlikleri güvenebileceği hello küme tooknow hello istemci yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63418-169">tooestablish trust between a client and hello cluster, you must configure hello cluster tooknow hello client identities that hello cluster can trust.</span></span> <span data-ttu-id="63418-170">İki farklı yolla güven kurabilir:</span><span class="sxs-lookup"><span data-stu-id="63418-170">You can establish trust in two different ways:</span></span>

- <span data-ttu-id="63418-171">Bağlanabilir hello etki alanı grubu kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="63418-171">Specify hello domain group users that can connect.</span></span>
- <span data-ttu-id="63418-172">Bağlanabilir hello etki alanı düğümü kullanıcıları belirtin.</span><span class="sxs-lookup"><span data-stu-id="63418-172">Specify hello domain node users that can connect.</span></span>

<span data-ttu-id="63418-173">Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="63418-173">Service Fabric supports two different access control types for clients that are connected tooa Service Fabric cluster: administrator and user.</span></span> <span data-ttu-id="63418-174">Erişim denetimi, hangi hello küme daha güvenli hale getirir hello küme yönetici toolimit erişim toocertain türleri için farklı kullanıcı grupları, küme işlemlerinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="63418-174">Access control enables hello cluster administrator toolimit access toocertain types of cluster operations for different groups of users, which makes hello cluster more secure.</span></span>  <span data-ttu-id="63418-175">Yöneticiler tam erişim toomanagement özellikleri (okuma/yazma özellikleri dahil) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="63418-175">Administrators have full access toomanagement capabilities (including read/write capabilities).</span></span> <span data-ttu-id="63418-176">Kullanıcıların varsayılan olarak, yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve hizmetleri vardır.</span><span class="sxs-lookup"><span data-stu-id="63418-176">Users, by default, have only read access toomanagement capabilities (for example, query capabilities), and hello ability tooresolve applications and services.</span></span>  

<span data-ttu-id="63418-177">Örnek Hello **güvenlik** bölüm Windows güvenliği yapılandırır, o hello makineleri belirtir *ServiceFabric/clusterA.contoso.com* hello kümesinin parçası olan ve bu belirtir *CONTOSO\usera* yönetici istemci erişimi vardır:</span><span class="sxs-lookup"><span data-stu-id="63418-177">hello following example **security** section configures Windows security, specifies that hello machines in *ServiceFabric/clusterA.contoso.com* are part of hello cluster, and specifies that *CONTOSO\usera* has admin client access:</span></span>

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
> <span data-ttu-id="63418-178">Service Fabric bir etki alanı denetleyicisinde dağıtılmalıdır değil.</span><span class="sxs-lookup"><span data-stu-id="63418-178">Service Fabric should not be deployed on a domain controller.</span></span> <span data-ttu-id="63418-179">ClusterConfig.json başlangıç IP adresi hello etki alanı denetleyicisinin makine grubu kullanırken içermez ve Grup yönetilen hizmet hesabı (gMSA) olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="63418-179">Make sure that ClusterConfig.json does not include hello IP address of hello domain controller when using a machine group or group Managed Service Account (gMSA).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="63418-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63418-180">Next steps</span></span>
<span data-ttu-id="63418-181">Windows güvenliği hello yapılandırdıktan sonra *ClusterConfig.JSON* dosya, hello küme oluşturma işlemine devam [Windows üzerinde çalışan tek başına küme oluşturmak](service-fabric-cluster-creation-for-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="63418-181">After configuring Windows security in hello *ClusterConfig.JSON* file, resume hello cluster creation process in [Create a standalone cluster running on Windows](service-fabric-cluster-creation-for-windows-server.md).</span></span>

<span data-ttu-id="63418-182">Düğümü düğümü nasıl güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi, bkz: hakkında daha fazla bilgi için [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="63418-182">For more information about how node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

<span data-ttu-id="63418-183">Bkz: [Bağlan tooa güvenli küme](service-fabric-connect-to-secure-cluster.md) PowerShell veya FabricClient kullanarak bağlanma örnekler.</span><span class="sxs-lookup"><span data-stu-id="63418-183">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for examples of connecting by using PowerShell or FabricClient.</span></span>
