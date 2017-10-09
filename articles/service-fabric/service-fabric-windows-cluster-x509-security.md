---
title: "aaaSecure Azure Service Fabric kümesi sertifikaları kullanarak Windows üzerinde | Microsoft Docs"
description: "Bu makalede nasıl toosecure iletişimi hello tek başına veya özel küme de istemcileri ve hello küme arasında açıklanmaktadır."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="928f7-103">X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli</span><span class="sxs-lookup"><span data-stu-id="928f7-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="928f7-104">Bu makalede nasıl toosecure hello iletişimine hello çeşitli, tek başına Windows küme düğümlerinin de nasıl toothis küme bağlanan tooauthenticate istemcileri X.509 sertifikaları kullanma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="928f7-104">This article describes how toosecure hello communication between hello various nodes of your standalone Windows cluster, as well as how tooauthenticate clients connecting toothis cluster, using X.509 certificates.</span></span> <span data-ttu-id="928f7-105">Bu, yalnızca yetkili kullanıcılar hello küme erişebilir dağıtılan uygulamalar hello ve yönetim görevlerini gerçekleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="928f7-105">This ensures that only authorized users can access hello cluster, hello deployed applications and perform management tasks.</span></span>  <span data-ttu-id="928f7-106">Merhaba küme oluşturulduğunda sertifika güvenliği hello kümede etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="928f7-106">Certificate security should be enabled on hello cluster when hello cluster is created.</span></span>  

<span data-ttu-id="928f7-107">Düğümü düğümü güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi gibi küme güvenlik üzerinde daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="928f7-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="928f7-108">Hangi sertifikaların ihtiyacınız olacak?</span><span class="sxs-lookup"><span data-stu-id="928f7-108">Which certificates will you need?</span></span>
<span data-ttu-id="928f7-109">ile toostart [hello tek başına küme paketini indirin](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) kümenizdeki hello düğümlerinin tooone.</span><span class="sxs-lookup"><span data-stu-id="928f7-109">toostart with, [download hello standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone of hello nodes in your cluster.</span></span> <span data-ttu-id="928f7-110">Size Hello paket, karşıdan bir **ClusterConfig.X509.MultiMachine.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="928f7-110">In hello downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="928f7-111">Merhaba dosyasını açın ve hello bölümünü gözden **güvenlik** hello altında **özellikleri** bölümü:</span><span class="sxs-lookup"><span data-stu-id="928f7-111">Open hello file and review hello section for **security** under hello **properties** section:</span></span>

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

<span data-ttu-id="928f7-112">Bu bölümde, tek başına Windows kümeniz güvenliğini sağlamak için gereksinim duyduğunuz hello sertifikaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="928f7-112">This section describes hello certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="928f7-113">Bir küme sertifika belirtiyorsanız hello değerini ayarlamak **ClusterCredentialType** too_**X509**_. Dış bağlantıları için sunucu sertifikası belirtiyorsanız hello ayarlamak **ServerCredentialType** çok_**X509**_. Zorunlu değil, ancak her iki bu sertifikaların düzgün bir şekilde güvenli bir küme için toohave öneririz. Bu değerleri çok ayarlarsanız*X509* sonra karşılık gelen sertifikaları hello veya Service Fabric bir özel durum oluşturur belirtmeniz gerekir. Bazı senaryolarda, yalnızca toospecify hello isteyebilirsiniz _ClientCertificateThumbprints_ veya _ReverseProxyCertificate_. Bu senaryolarda, ayarlanmamış _ClusterCredentialType_ veya _ServerCredentialType_ too_X509_.</span><span class="sxs-lookup"><span data-stu-id="928f7-113">If you are specifying a cluster certificate, set hello value of **ClusterCredentialType** too_**X509**_. If you are specifying server certificate for outside connections, set hello **ServerCredentialType** too_**X509**_. Although not mandatory, we recommend toohave both these certificates for a properly secured cluster. If you set these values too*X509* then you must also specify hello corresponding certificates or Service Fabric will throw an exception. In some scenarios, you may only want toospecify hello _ClientCertificateThumbprints_ or _ReverseProxyCertificate_. In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ too_X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="928f7-114">A [parmak izi](https://en.wikipedia.org/wiki/Public_key_fingerprint) hello birincil bir sertifika kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="928f7-114">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is hello primary identity of a certificate.</span></span> <span data-ttu-id="928f7-115">Okuma [nasıl tooretrieve bir sertifikanın parmak izini](https://msdn.microsoft.com/library/ms734695.aspx) toofind hello parmak izi oluşturduğunuz hello sertifikaların çıkışı.</span><span class="sxs-lookup"><span data-stu-id="928f7-115">Read [How tooretrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) toofind out hello thumbprint of hello certificates that you create.</span></span>
> 
> 

<span data-ttu-id="928f7-116">Merhaba aşağıdaki tabloda, Küme kurulumu gerekir hello sertifikaları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="928f7-116">hello following table lists hello certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="928f7-117">**CertificateInformation ayarı**</span><span class="sxs-lookup"><span data-stu-id="928f7-117">**CertificateInformation Setting**</span></span> | <span data-ttu-id="928f7-118">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="928f7-118">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="928f7-119">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="928f7-119">ClusterCertificate</span></span> |<span data-ttu-id="928f7-120">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-120">Recommended for test environment.</span></span> <span data-ttu-id="928f7-121">Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok.</span><span class="sxs-lookup"><span data-stu-id="928f7-121">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="928f7-122">İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-122">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="928f7-123">Merhaba sertifikanın parmak izini hello birincil hello ayarlamak **parmak izi** bölümü ve, hello hello ikincil **ThumbprintSecondary** değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="928f7-123">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="928f7-124">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="928f7-124">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="928f7-125">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-125">Recommended for production environment.</span></span> <span data-ttu-id="928f7-126">Bu sertifika bir kümede hello düğümler arasında gerekli toosecure hello iletişim yok.</span><span class="sxs-lookup"><span data-stu-id="928f7-126">This certificate is required toosecure hello communication between hello nodes on a cluster.</span></span> <span data-ttu-id="928f7-127">Bir veya iki küme sertifika ortak adları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-127">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="928f7-128">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="928f7-128">ServerCertificate</span></span> |<span data-ttu-id="928f7-129">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-129">Recommended for test environment.</span></span> <span data-ttu-id="928f7-130">Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur.</span><span class="sxs-lookup"><span data-stu-id="928f7-130">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="928f7-131">Toouse seçebileceğiniz kolaylık sağlamak için aynı sertifika için hello *ClusterCertificate* ve *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="928f7-131">For convenience, you can choose toouse hello same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="928f7-132">İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-132">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="928f7-133">Merhaba sertifikanın parmak izini hello birincil hello ayarlamak **parmak izi** bölümü ve, hello hello ikincil **ThumbprintSecondary** değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="928f7-133">Set hello thumbprint of hello primary certificate in hello **Thumbprint** section and that of hello secondary in hello **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="928f7-134">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="928f7-134">ServerCertificateCommonNames</span></span> |<span data-ttu-id="928f7-135">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-135">Recommended for production environment.</span></span> <span data-ttu-id="928f7-136">Tooconnect toothis küme çalıştığında bu sertifikayı toohello istemci sunulur.</span><span class="sxs-lookup"><span data-stu-id="928f7-136">This certificate is presented toohello client when it tries tooconnect toothis cluster.</span></span> <span data-ttu-id="928f7-137">Toouse seçebileceğiniz kolaylık sağlamak için aynı sertifika için hello *ClusterCertificateCommonNames* ve *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="928f7-137">For convenience, you can choose toouse hello same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="928f7-138">Bir veya iki sunucu sertifika ortak adları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-138">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="928f7-139">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="928f7-139">ClientCertificateThumbprints</span></span> |<span data-ttu-id="928f7-140">Kimliği doğrulanmış hello istemcilerde tooinstall istediğiniz sertifikaları kümesidir.</span><span class="sxs-lookup"><span data-stu-id="928f7-140">This is a set of certificates that you want tooinstall on hello authenticated clients.</span></span> <span data-ttu-id="928f7-141">Bir dizi farklı istemci sertifikalarını tooallow erişim toohello küme istediğiniz hello makinelerde yüklü olabilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-141">You can have a number of different client certificates installed on hello machines that you want tooallow access toohello cluster.</span></span> <span data-ttu-id="928f7-142">Merhaba sertifikanın parmak izini her hello ayarlamak **CertificateThumbprint** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="928f7-142">Set hello thumbprint of each certificate in hello **CertificateThumbprint** variable.</span></span> <span data-ttu-id="928f7-143">Merhaba ayarlarsanız **IsAdmin** çok*doğru*, sonra hello istemci yüklü bu sertifikayla yönetici hello küme yönetimi etkinliklerini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-143">If you set hello **IsAdmin** too*true*, then hello client with this certificate installed on it can do administrator management activities on hello cluster.</span></span> <span data-ttu-id="928f7-144">Merhaba, **IsAdmin** olan *yanlış*, bu sertifikayla hello istemci yalnızca kullanıcı erişim haklarını, salt okunur genellikle izin hello eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="928f7-144">If hello **IsAdmin** is *false*, hello client with this certificate can only perform hello actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="928f7-145">Rolleri hakkında daha fazla bilgi için okumaya devam [rol tabanlı erişim denetimi (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="928f7-145">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="928f7-146">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="928f7-146">ClientCertificateCommonNames</span></span> |<span data-ttu-id="928f7-147">Set hello ortak adı hello ilk istemci sertifikası hello için **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="928f7-147">Set hello common name of hello first client certificate for hello **CertificateCommonName**.</span></span> <span data-ttu-id="928f7-148">Merhaba **CertificateIssuerThumbprint** hello için bu sertifikayı veren hello parmak izi olan.</span><span class="sxs-lookup"><span data-stu-id="928f7-148">hello **CertificateIssuerThumbprint** is hello thumbprint for hello issuer of this certificate.</span></span> <span data-ttu-id="928f7-149">Okuma [sertifikalarla çalışma](https://msdn.microsoft.com/library/ms731899.aspx) tooknow ortak adları ve hello veren hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="928f7-149">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) tooknow more about common names and hello issuer.</span></span> |
| <span data-ttu-id="928f7-150">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="928f7-150">ReverseProxyCertificate</span></span> |<span data-ttu-id="928f7-151">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-151">Recommended for test environment.</span></span> <span data-ttu-id="928f7-152">Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="928f7-152">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="928f7-153">Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="928f7-153">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="928f7-154">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="928f7-154">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="928f7-155">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="928f7-155">Recommended for production environment.</span></span> <span data-ttu-id="928f7-156">Bu, olabilir, isteğe bağlı bir sertifikadır toosecure isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="928f7-156">This is an optional certificate that can be specified if you want toosecure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="928f7-157">Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="928f7-157">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="928f7-158">Burada hello küme, sunucu ve istemci sertifikaları sağlanan örnek küme yapılandırması İşte.</span><span class="sxs-lookup"><span data-stu-id="928f7-158">Here is example cluster configuration where hello Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="928f7-159">Küme için lütfen unutmayın / sunucu / reverseProxy sertifikalar, parmak izi ve ortak ad verilmez toobe yapılandırılmış birlikte hello için aynı sertifika türü.</span><span class="sxs-lookup"><span data-stu-id="928f7-159">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed toobe configured together for hello same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a><span data-ttu-id="928f7-160">Sertifika geçir</span><span class="sxs-lookup"><span data-stu-id="928f7-160">Certificate roll over</span></span>
<span data-ttu-id="928f7-161">Sertifika ortak adı yerine parmak izi kullanırken, sertifika alma üzerinden küme yapılandırması yükseltme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="928f7-161">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="928f7-162">Sertifika alma üzerinden veren içeriyorsa, UTC'ye, lütfen hello eski veren sertifika hello sertifika deposunda hello yeni sertifikayı veren sertifika yükledikten sonra en az 2 saat tutmak.</span><span class="sxs-lookup"><span data-stu-id="928f7-162">If certificate roll over involves issuer roll over, please keep hello old issuer cert in hello cert store at least 2 hours after installing hello new issuer cert.</span></span>

## <a name="acquire-hello-x509-certificates"></a><span data-ttu-id="928f7-163">Merhaba X.509 sertifikaları alma</span><span class="sxs-lookup"><span data-stu-id="928f7-163">Acquire hello X.509 certificates</span></span>
<span data-ttu-id="928f7-164">Merhaba küme içinde toosecure iletişimi, küme düğümleri için tooobtain X.509 sertifikalarını ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="928f7-164">toosecure communication within hello cluster, you will first need tooobtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="928f7-165">Ayrıca, toolimit bağlantı toothis tooauthorized makineleri/kullanıcılar küme, tooobtain ihtiyacınız ve hello istemci makineleri için sertifikaları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="928f7-165">Additionally, toolimit connection toothis cluster tooauthorized machines/users, you will need tooobtain and install certificates for hello client machines.</span></span>

<span data-ttu-id="928f7-166">Üretim iş yükleri çalıştıran kümeler için kullanmanız gereken bir [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority) X.509 sertifikası toosecure hello küme imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="928f7-166">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate toosecure hello cluster.</span></span> <span data-ttu-id="928f7-167">Bu sertifikaları edinme hakkında ayrıntılı bilgi için çok gidin[nasıl yapılır: bir sertifika edinin](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="928f7-167">For details on obtaining these certificates, go too[How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="928f7-168">Test amaçları için kullandığınız kümeler için otomatik olarak imzalanan bir sertifika toouse seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-168">For clusters that you use for test purposes, you can choose toouse a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="928f7-169">İsteğe bağlı: otomatik olarak imzalanan bir sertifika oluşturun</span><span class="sxs-lookup"><span data-stu-id="928f7-169">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="928f7-170">Tek yönlü toocreate doğru şekilde güvenli hale getirilebilir otomatik olarak imzalanan bir sertifika olduğundan toouse hello *CertSetup.ps1* hello dizin hello Service Fabric SDK klasöründe betik *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*.</span><span class="sxs-lookup"><span data-stu-id="928f7-170">One way toocreate a self-signed cert that can be secured correctly is toouse hello *CertSetup.ps1* script in hello Service Fabric SDK folder in hello directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="928f7-171">Bu dosya toochange hello varsayılan adını hello sertifika Düzenle (Merhaba değeri Ara *CN ServiceFabricDevClusterCert =*).</span><span class="sxs-lookup"><span data-stu-id="928f7-171">Edit this file toochange hello default name of hello certificate (look for hello value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="928f7-172">Bu komut dosyası olarak çalıştıracak `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="928f7-172">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="928f7-173">Şimdi hello sertifika tooa PFX dosyasını korumalı bir parolayla dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="928f7-173">Now export hello certificate tooa PFX file with a protected password.</span></span> <span data-ttu-id="928f7-174">İlk hello sertifikanın parmak izini hello alın.</span><span class="sxs-lookup"><span data-stu-id="928f7-174">First get hello thumbprint of hello certificate.</span></span> <span data-ttu-id="928f7-175">Merhaba gelen *Başlat* hello çalıştırmak menüsünde *bilgisayar sertifikalarını yönetmek*.</span><span class="sxs-lookup"><span data-stu-id="928f7-175">From hello *Start* menu, run hello *Manage computer certificates*.</span></span> <span data-ttu-id="928f7-176">Toohello gidin **yerel Bilgisayar\Kişisel** klasörü ve hello sertifika, yalnızca Bul oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="928f7-176">Navigate toohello **Local Computer\Personal** folder and find hello certificate you just created.</span></span> <span data-ttu-id="928f7-177">Merhaba sertifika tooopen çift tıklayın, select hello *ayrıntıları* sekmesi ve toohello aşağı kaydırın *parmak izi* alan.</span><span class="sxs-lookup"><span data-stu-id="928f7-177">Double-click hello certificate tooopen it, select hello *Details* tab and scroll down toohello *Thumbprint* field.</span></span> <span data-ttu-id="928f7-178">Merhaba, aşağıdaki PowerShell komutunu hello alanları kaldırdıktan sonra Hello parmak izi değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="928f7-178">Copy hello thumbprint value into hello PowerShell command below, after removing hello spaces.</span></span>  <span data-ttu-id="928f7-179">Değişiklik hello `String` tooa uygun güvenli parola tooprotect ve PowerShell içinde aşağıdaki çalışma başlangıç değeri:</span><span class="sxs-lookup"><span data-stu-id="928f7-179">Change hello `String` value tooa suitable secure password tooprotect it and run hello following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="928f7-180">toosee hello hello üzerinde yüklü bir sertifika ayrıntılarını makine hello aşağıdaki PowerShell komutunu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="928f7-180">toosee hello details of a certificate installed on hello machine you can run hello following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="928f7-181">Alternatif olarak, bir Azure aboneliğiniz varsa, hello bölümü izleyin [sertifikaları tooKey kasası eklemek](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="928f7-181">Alternatively, if you have an Azure subscription, follow hello section [Add certificates tooKey Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-hello-certificates"></a><span data-ttu-id="928f7-182">Merhaba sertifikaları yükleyin</span><span class="sxs-lookup"><span data-stu-id="928f7-182">Install hello certificates</span></span>
<span data-ttu-id="928f7-183">Sertifikaları olduktan sonra bunları hello küme düğümlerinde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-183">Once you have certificate(s), you can install them on hello cluster nodes.</span></span> <span data-ttu-id="928f7-184">Düğümleriniz toohave gereken en son Windows PowerShell hello 3.x yüklü.</span><span class="sxs-lookup"><span data-stu-id="928f7-184">Your nodes need toohave hello latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="928f7-185">Küme ve sunucu sertifikaları ve tüm ikincil sertifikaları için her bir düğümde aşağıdaki adımları toorepeat ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="928f7-185">You will need toorepeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="928f7-186">Merhaba .pfx dosyaları toohello düğümü kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="928f7-186">Copy hello .pfx file(s) toohello node.</span></span>
2. <span data-ttu-id="928f7-187">Bir yönetici olarak bir PowerShell penceresi açın ve aşağıdaki komutları hello girin.</span><span class="sxs-lookup"><span data-stu-id="928f7-187">Open a PowerShell window as an administrator and enter hello following commands.</span></span> <span data-ttu-id="928f7-188">Hello yerine *$pswd* Bu sertifika toocreate kullanılan hello parolayla.</span><span class="sxs-lookup"><span data-stu-id="928f7-188">Replace hello *$pswd* with hello password that you used toocreate this certificate.</span></span> <span data-ttu-id="928f7-189">Hello yerine *$PfxFilePath* hello .pfx kopyalanan toothis düğümünün hello tam yoluna sahip.</span><span class="sxs-lookup"><span data-stu-id="928f7-189">Replace hello *$PfxFilePath* with hello full path of hello .pfx copied toothis node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="928f7-190">Şimdi hello Network Service hesabı altında çalışır, hello Service Fabric işlem, komut dosyası izleyen hello çalıştırarak kullanabilmesi için bu sertifikayı hello erişim denetimini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="928f7-190">Now set hello access control on this certificate so that hello Service Fabric process, which runs under hello Network Service account, can use it by running hello following script.</span></span> <span data-ttu-id="928f7-191">Merhaba sertifika ve hello hizmet hesabı için "NETWORK SERVICE" Merhaba parmak izi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="928f7-191">Provide hello thumbprint of hello certificate and "NETWORK SERVICE" for hello service account.</span></span> <span data-ttu-id="928f7-192">Bu ' % s'hello ACL'ler hello sertifikanın doğru hello sertifikada açarak denetleyebilirsiniz *Başlat* > *bilgisayar sertifikalarını yönetmek* ve bakarak *tüm görevler*  >  *Özel anahtarları Yönet*.</span><span class="sxs-lookup"><span data-stu-id="928f7-192">You can check that hello ACLs on hello certificate are correct by opening hello certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="928f7-193">Her sunucu sertifikası için yukarıdaki Hello adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="928f7-193">Repeat hello steps above for each server certificate.</span></span> <span data-ttu-id="928f7-194">Tooallow erişim toohello küme istediğiniz bu adımları tooinstall hello istemci sertifikalarını hello makinelerde de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-194">You can also use these steps tooinstall hello client certificates on hello machines that you want tooallow access toohello cluster.</span></span>

## <a name="create-hello-secure-cluster"></a><span data-ttu-id="928f7-195">Merhaba güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="928f7-195">Create hello secure cluster</span></span>
<span data-ttu-id="928f7-196">Merhaba yapılandırdıktan sonra **güvenlik** hello bölümünü **ClusterConfig.X509.MultiMachine.json** dosyası devam çok[kümenizi oluşturduktan](service-fabric-cluster-creation-for-windows-server.md#createcluster) bölüm tooconfigure düğümleri hello ve hello tek başına bir küme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="928f7-196">After configuring hello **security** section of hello **ClusterConfig.X509.MultiMachine.json** file, you can proceed too[Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section tooconfigure hello nodes and create hello standalone cluster.</span></span> <span data-ttu-id="928f7-197">Toouse hello unutmayın **ClusterConfig.X509.MultiMachine.json** hello küme oluşturma sırasında dosya.</span><span class="sxs-lookup"><span data-stu-id="928f7-197">Remember toouse hello **ClusterConfig.X509.MultiMachine.json** file while creating hello cluster.</span></span> <span data-ttu-id="928f7-198">Örneğin, komutunuzu hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="928f7-198">For example, your command might look like hello following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="928f7-199">Merhaba güvenli olduktan sonra tek başına Windows başarıyla çalışan küme ve kimliği doğrulanmış istemciler tooconnect tooit Merhaba, hello bölümü izleyin kurulumun [Bağlan tooa güvenli küme PowerShell kullanarak](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="928f7-199">Once you have hello secure standalone Windows cluster successfully running, and have setup hello authenticated clients tooconnect tooit, follow hello section [Connect tooa secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit.</span></span> <span data-ttu-id="928f7-200">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="928f7-200">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="928f7-201">Bu gibi durumlarda, diğer PowerShell komutları toowork sonra Bu kümeyle çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="928f7-201">You can then run other PowerShell commands toowork with this cluster.</span></span> <span data-ttu-id="928f7-202">Örneğin, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow bu güvenli küme düğümlerinde listesi.</span><span class="sxs-lookup"><span data-stu-id="928f7-202">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="928f7-203">tooremove hello küme hello Service Fabric paketi indirdiğiniz hello kümesinde toohello düğümüne bağlanmak, bir komut satırı açın ve toohello paket klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="928f7-203">tooremove hello cluster, connect toohello node on hello cluster where you downloaded hello Service Fabric package, open a command line and navigate toohello package folder.</span></span> <span data-ttu-id="928f7-204">Şimdi hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="928f7-204">Now run hello following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="928f7-205">Yanlış sertifika yapılandırması hello Küme dağıtımı sırasında yaklaşan engellemek.</span><span class="sxs-lookup"><span data-stu-id="928f7-205">Incorrect certificate configuration may prevent hello cluster from coming up during deployment.</span></span> <span data-ttu-id="928f7-206">tooself-güvenlik sorunları tanılamak, lütfen Olay Görüntüleyicisi'ni grubunda bakın *uygulama ve hizmet günlükleri* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="928f7-206">tooself-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

