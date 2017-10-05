---
title: "Sertifikaları kullanarak Windows Azure Service Fabric kümede güvenli | Microsoft Docs"
description: "Bu makalede, tek başına veya istemciler arasında iyi özel küme ve küme içinde iletişimin güvenliğini sağlamak açıklar."
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
ms.openlocfilehash: 71ece1e43cc3c4ac3350cd59633065de06672420
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a><span data-ttu-id="0ce55-103">X.509 sertifikaları kullanarak Windows'u bir tek başına kümede güvenli</span><span class="sxs-lookup"><span data-stu-id="0ce55-103">Secure a standalone cluster on Windows using X.509 certificates</span></span>
<span data-ttu-id="0ce55-104">Bu kümeye bağlanan istemciler X.509 kullanarak kimlik doğrulaması için sertifikaları nasıl bu makalede, tek başına Windows kümeniz çeşitli düğümleri arasındaki iletişimin güvenliğini sağlamak de açıklar.</span><span class="sxs-lookup"><span data-stu-id="0ce55-104">This article describes how to secure the communication between the various nodes of your standalone Windows cluster, as well as how to authenticate clients connecting to this cluster, using X.509 certificates.</span></span> <span data-ttu-id="0ce55-105">Bu, yalnızca yetkili kullanıcılar kümeye dağıtılan uygulamalar erişmek ve yönetim görevlerini gerçekleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ce55-105">This ensures that only authorized users can access the cluster, the deployed applications and perform management tasks.</span></span>  <span data-ttu-id="0ce55-106">Küme oluşturulduğunda sertifika güvenliği kümede etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-106">Certificate security should be enabled on the cluster when the cluster is created.</span></span>  

<span data-ttu-id="0ce55-107">Düğümü düğümü güvenlik, istemci düğümü güvenlik ve rol tabanlı erişim denetimi gibi küme güvenlik üzerinde daha fazla bilgi için bkz: [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="0ce55-107">For more information on cluster security such as node-to-node security, client-to-node security, and role-based access control, see [Cluster security scenarios](service-fabric-cluster-security.md).</span></span>

## <a name="which-certificates-will-you-need"></a><span data-ttu-id="0ce55-108">Hangi sertifikaların ihtiyacınız olacak?</span><span class="sxs-lookup"><span data-stu-id="0ce55-108">Which certificates will you need?</span></span>
<span data-ttu-id="0ce55-109">İle başlamak [tek başına küme paketini karşıdan](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) kümenizdeki düğümlerin birinde.</span><span class="sxs-lookup"><span data-stu-id="0ce55-109">To start with, [download the standalone cluster package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) to one of the nodes in your cluster.</span></span> <span data-ttu-id="0ce55-110">İndirilen paketteki, bulacaksınız bir **ClusterConfig.X509.MultiMachine.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="0ce55-110">In the downloaded package, you will find a **ClusterConfig.X509.MultiMachine.json** file.</span></span> <span data-ttu-id="0ce55-111">Dosyasını açın ve bölümünü gözden **güvenlik** altında **özellikleri** bölümü:</span><span class="sxs-lookup"><span data-stu-id="0ce55-111">Open the file and review the section for **security** under the **properties** section:</span></span>

```JSON
"security": {
    "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

<span data-ttu-id="0ce55-112">Bu bölümde, tek başına Windows kümeniz güvenliğini sağlamak için gereken sertifikaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0ce55-112">This section describes the certificates that you need for securing your standalone Windows cluster.</span></span> <span data-ttu-id="0ce55-113">Bir küme sertifika belirtiyorsanız değerini ayarlamak **ClusterCredentialType** için  _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="0ce55-113">If you are specifying a cluster certificate, set the value of **ClusterCredentialType** to _**X509**_.</span></span> <span data-ttu-id="0ce55-114">Dış bağlantıları için sunucu sertifikası belirtiyorsanız ayarlamak **ServerCredentialType** için  _**X509**_.</span><span class="sxs-lookup"><span data-stu-id="0ce55-114">If you are specifying server certificate for outside connections, set the **ServerCredentialType** to _**X509**_.</span></span> <span data-ttu-id="0ce55-115">Zorunlu değil, ancak düzgün güvenli bir küme için bu iki sertifikalara sahip olmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-115">Although not mandatory, we recommend to have both these certificates for a properly secured cluster.</span></span> <span data-ttu-id="0ce55-116">Bu değerleri ayarlamak, *X509* sonra da Service Fabric ve karşılık gelen sertifika bir özel durum oluşturur de belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-116">If you set these values to *X509* then you must also specify the corresponding certificates or Service Fabric will throw an exception.</span></span> <span data-ttu-id="0ce55-117">Bazı senaryolarda, yalnızca belirtmek isteyebilirsiniz _ClientCertificateThumbprints_ veya _ReverseProxyCertificate_.</span><span class="sxs-lookup"><span data-stu-id="0ce55-117">In some scenarios, you may only want to specify the _ClientCertificateThumbprints_ or _ReverseProxyCertificate_.</span></span> <span data-ttu-id="0ce55-118">Bu senaryolarda, ayarlanmamış _ClusterCredentialType_ veya _ServerCredentialType_ için _X509_.</span><span class="sxs-lookup"><span data-stu-id="0ce55-118">In those scenarios, you need not set _ClusterCredentialType_ or _ServerCredentialType_ to _X509_.</span></span>


> [!NOTE]
> <span data-ttu-id="0ce55-119">A [parmak izi](https://en.wikipedia.org/wiki/Public_key_fingerprint) bir sertifika birincil kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-119">A [thumbprint](https://en.wikipedia.org/wiki/Public_key_fingerprint) is the primary identity of a certificate.</span></span> <span data-ttu-id="0ce55-120">Okuma [bir sertifikanın parmak izini alma](https://msdn.microsoft.com/library/ms734695.aspx) oluşturduğunuz sertifika parmak izi bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="0ce55-120">Read [How to retrieve thumbprint of a certificate](https://msdn.microsoft.com/library/ms734695.aspx) to find out the thumbprint of the certificates that you create.</span></span>
> 
> 

<span data-ttu-id="0ce55-121">Aşağıdaki tabloda, Küme kurulumu gerekir sertifikaları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="0ce55-121">The following table lists the certificates that you will need on your cluster setup:</span></span>

| <span data-ttu-id="0ce55-122">**CertificateInformation ayarı**</span><span class="sxs-lookup"><span data-stu-id="0ce55-122">**CertificateInformation Setting**</span></span> | <span data-ttu-id="0ce55-123">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="0ce55-123">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="0ce55-124">ClusterCertificate</span><span class="sxs-lookup"><span data-stu-id="0ce55-124">ClusterCertificate</span></span> |<span data-ttu-id="0ce55-125">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-125">Recommended for test environment.</span></span> <span data-ttu-id="0ce55-126">Bu sertifika, bir küme düğümlerinde arasındaki iletişimin güvenliğini sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-126">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="0ce55-127">İki farklı sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-127">You can use two different certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="0ce55-128">Sertifikanın parmak izi birincil ayarlamak **parmak izi** bölümü ve, ikincil **ThumbprintSecondary** değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="0ce55-128">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="0ce55-129">ClusterCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0ce55-129">ClusterCertificateCommonNames</span></span> |<span data-ttu-id="0ce55-130">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-130">Recommended for production environment.</span></span> <span data-ttu-id="0ce55-131">Bu sertifika, bir küme düğümlerinde arasındaki iletişimin güvenliğini sağlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-131">This certificate is required to secure the communication between the nodes on a cluster.</span></span> <span data-ttu-id="0ce55-132">Bir veya iki küme sertifika ortak adları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-132">You can use one or two cluster certificate common names.</span></span> |
| <span data-ttu-id="0ce55-133">ServerCertificate</span><span class="sxs-lookup"><span data-stu-id="0ce55-133">ServerCertificate</span></span> |<span data-ttu-id="0ce55-134">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-134">Recommended for test environment.</span></span> <span data-ttu-id="0ce55-135">Bu kümeye bağlanmaya çalıştığında bu sertifikayı istemciye sunulur.</span><span class="sxs-lookup"><span data-stu-id="0ce55-135">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="0ce55-136">Kolaylık olması için için aynı sertifika kullanmayı tercih edebileceğiniz *ClusterCertificate* ve *ServerCertificate*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-136">For convenience, you can choose to use the same certificate for *ClusterCertificate* and *ServerCertificate*.</span></span> <span data-ttu-id="0ce55-137">İki farklı sunucu sertifikaları, birincil ve ikincil bir yükseltme için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-137">You can use two different server certificates, a primary and a secondary for upgrade.</span></span> <span data-ttu-id="0ce55-138">Sertifikanın parmak izi birincil ayarlamak **parmak izi** bölümü ve, ikincil **ThumbprintSecondary** değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="0ce55-138">Set the thumbprint of the primary certificate in the **Thumbprint** section and that of the secondary in the **ThumbprintSecondary** variables.</span></span> |
| <span data-ttu-id="0ce55-139">ServerCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0ce55-139">ServerCertificateCommonNames</span></span> |<span data-ttu-id="0ce55-140">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-140">Recommended for production environment.</span></span> <span data-ttu-id="0ce55-141">Bu kümeye bağlanmaya çalıştığında bu sertifikayı istemciye sunulur.</span><span class="sxs-lookup"><span data-stu-id="0ce55-141">This certificate is presented to the client when it tries to connect to this cluster.</span></span> <span data-ttu-id="0ce55-142">Kolaylık olması için için aynı sertifika kullanmayı tercih edebileceğiniz *ClusterCertificateCommonNames* ve *ServerCertificateCommonNames*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-142">For convenience, you can choose to use the same certificate for *ClusterCertificateCommonNames* and *ServerCertificateCommonNames*.</span></span> <span data-ttu-id="0ce55-143">Bir veya iki sunucu sertifika ortak adları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-143">You can use one or two server certificate common names.</span></span> |
| <span data-ttu-id="0ce55-144">ClientCertificateThumbprints</span><span class="sxs-lookup"><span data-stu-id="0ce55-144">ClientCertificateThumbprints</span></span> |<span data-ttu-id="0ce55-145">Kimliği doğrulanmış istemcilerde yüklemek istediğiniz sertifika kümesidir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-145">This is a set of certificates that you want to install on the authenticated clients.</span></span> <span data-ttu-id="0ce55-146">Bir dizi farklı istemci sertifikaları, küme erişmesine izin vermek istediğiniz makinelerde yüklü olabilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-146">You can have a number of different client certificates installed on the machines that you want to allow access to the cluster.</span></span> <span data-ttu-id="0ce55-147">Her sertifikanın parmak izini ayarlamak **CertificateThumbprint** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0ce55-147">Set the thumbprint of each certificate in the **CertificateThumbprint** variable.</span></span> <span data-ttu-id="0ce55-148">Ayarlarsanız **IsAdmin** için *doğru*, sonra istemcinin yüklü bu sertifikayla yönetici küme yönetimi etkinliklerini yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-148">If you set the **IsAdmin** to *true*, then the client with this certificate installed on it can do administrator management activities on the cluster.</span></span> <span data-ttu-id="0ce55-149">Varsa **IsAdmin** olan *yanlış*, istemcinin bu sertifikayla yalnızca kullanıcı erişim haklarını, salt okunur genellikle için izin verilen eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-149">If the **IsAdmin** is *false*, the client with this certificate can only perform the actions allowed for user access rights, typically read-only.</span></span> <span data-ttu-id="0ce55-150">Rolleri hakkında daha fazla bilgi için okumaya devam [rol tabanlı erişim denetimi (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span><span class="sxs-lookup"><span data-stu-id="0ce55-150">For more information on roles read [Role based access control (RBAC)](service-fabric-cluster-security.md#role-based-access-control-rbac)</span></span> |
| <span data-ttu-id="0ce55-151">ClientCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0ce55-151">ClientCertificateCommonNames</span></span> |<span data-ttu-id="0ce55-152">İlk istemci sertifikası için ortak adı ayarlama **CertificateCommonName**.</span><span class="sxs-lookup"><span data-stu-id="0ce55-152">Set the common name of the first client certificate for the **CertificateCommonName**.</span></span> <span data-ttu-id="0ce55-153">**CertificateIssuerThumbprint** bu sertifikayı verenin parmak izi olan.</span><span class="sxs-lookup"><span data-stu-id="0ce55-153">The **CertificateIssuerThumbprint** is the thumbprint for the issuer of this certificate.</span></span> <span data-ttu-id="0ce55-154">Okuma [sertifikalarla çalışma](https://msdn.microsoft.com/library/ms731899.aspx) ortak adları ve veren hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="0ce55-154">Read [Working with certificates](https://msdn.microsoft.com/library/ms731899.aspx) to know more about common names and the issuer.</span></span> |
| <span data-ttu-id="0ce55-155">ReverseProxyCertificate</span><span class="sxs-lookup"><span data-stu-id="0ce55-155">ReverseProxyCertificate</span></span> |<span data-ttu-id="0ce55-156">Test ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-156">Recommended for test environment.</span></span> <span data-ttu-id="0ce55-157">Bu, olabilir, isteğe bağlı bir sertifikadır güvenli isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="0ce55-157">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="0ce55-158">Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0ce55-158">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |
| <span data-ttu-id="0ce55-159">ReverseProxyCertificateCommonNames</span><span class="sxs-lookup"><span data-stu-id="0ce55-159">ReverseProxyCertificateCommonNames</span></span> |<span data-ttu-id="0ce55-160">Üretim ortamı için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-160">Recommended for production environment.</span></span> <span data-ttu-id="0ce55-161">Bu, olabilir, isteğe bağlı bir sertifikadır güvenli isteyip istemediğinizi belirtilen, [Ters Proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="0ce55-161">This is an optional certificate that can be specified if you want to secure your [Reverse Proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="0ce55-162">Bu sertifika kullanıyorsanız reverseProxyEndpointPort nodeTypes ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0ce55-162">Make sure reverseProxyEndpointPort is set in nodeTypes if you are using this certificate.</span></span> |

<span data-ttu-id="0ce55-163">Burada küme, sunucu ve istemci sertifikaları sağlanan örnek küme yapılandırması İşte.</span><span class="sxs-lookup"><span data-stu-id="0ce55-163">Here is example cluster configuration where the Cluster, Server, and Client certificates have been provided.</span></span> <span data-ttu-id="0ce55-164">Küme için lütfen unutmayın / sunucu / reverseProxy sertifikalar, parmak izi ve ortak adı için aynı sertifika türü birlikte yapılandırılması izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="0ce55-164">Please note that for cluster/ server/ reverseProxy certificates, thumbprint and common name are not allowed to be configured together for the same cert type.</span></span>

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace the localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace the localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "The Credential type X509 indicates this is cluster is secured using X509 Certificates. The thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
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

## <a name="certificate-roll-over"></a><span data-ttu-id="0ce55-165">Sertifika geçir</span><span class="sxs-lookup"><span data-stu-id="0ce55-165">Certificate roll over</span></span>
<span data-ttu-id="0ce55-166">Sertifika ortak adı yerine parmak izi kullanırken, sertifika alma üzerinden küme yapılandırması yükseltme gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="0ce55-166">When using certificate common name instead of thumbprint, certificate roll over doesn't require cluster configuration upgrade.</span></span>
<span data-ttu-id="0ce55-167">Sertifika alma üzerinden içeriyorsa veren geçir, lütfen tutma cert eski veren cert depolamak yeni sertifikayı veren sertifika yükledikten sonra en az 2 saat.</span><span class="sxs-lookup"><span data-stu-id="0ce55-167">If certificate roll over involves issuer roll over, please keep the old issuer cert in the cert store at least 2 hours after installing the new issuer cert.</span></span>

## <a name="acquire-the-x509-certificates"></a><span data-ttu-id="0ce55-168">X.509 sertifikaları alma</span><span class="sxs-lookup"><span data-stu-id="0ce55-168">Acquire the X.509 certificates</span></span>
<span data-ttu-id="0ce55-169">Küme içindeki iletişimin güvenliğini sağlamak için ilk X.509 sertifikaları için Küme düğümlerinizi edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-169">To secure communication within the cluster, you will first need to obtain X.509 certificates for your cluster nodes.</span></span> <span data-ttu-id="0ce55-170">Ayrıca, yetkili makineler/kullanıcıların bu kümeye bağlantı sınırlamak için elde edilir ve istemci makineleri için sertifikaları yüklemek gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="0ce55-170">Additionally, to limit connection to this cluster to authorized machines/users, you will need to obtain and install certificates for the client machines.</span></span>

<span data-ttu-id="0ce55-171">Üretim iş yükleri çalıştıran kümeler için kullanmanız gereken bir [sertifika yetkilisi (CA)](https://en.wikipedia.org/wiki/Certificate_authority) küme güvenli hale getirmek için X.509 sertifikası imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="0ce55-171">For clusters that are running production workloads, you should use a [Certificate Authority (CA)](https://en.wikipedia.org/wiki/Certificate_authority) signed X.509 certificate to secure the cluster.</span></span> <span data-ttu-id="0ce55-172">Bu sertifikaları edinme hakkında ayrıntılar için Git [nasıl yapılır: bir sertifika edinin](http://msdn.microsoft.com/library/aa702761.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ce55-172">For details on obtaining these certificates, go to [How to: Obtain a Certificate](http://msdn.microsoft.com/library/aa702761.aspx).</span></span>

<span data-ttu-id="0ce55-173">Test amaçları için kullandığınız kümeler için otomatik olarak imzalanan bir sertifika kullanmayı da tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-173">For clusters that you use for test purposes, you can choose to use a self-signed certificate.</span></span>

## <a name="optional-create-a-self-signed-certificate"></a><span data-ttu-id="0ce55-174">İsteğe bağlı: otomatik olarak imzalanan bir sertifika oluşturun</span><span class="sxs-lookup"><span data-stu-id="0ce55-174">Optional: Create a self-signed certificate</span></span>
<span data-ttu-id="0ce55-175">Doğru bir şekilde güvenli hale getirilebilir otomatik olarak imzalanan bir sertifika oluşturmak için bir yol kullanmaktır *CertSetup.ps1* betik dizinindeki Service Fabric SDK klasöründeki *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\ Güvenli*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-175">One way to create a self-signed cert that can be secured correctly is to use the *CertSetup.ps1* script in the Service Fabric SDK folder in the directory *C:\Program Files\Microsoft SDKs\Service Fabric\ClusterSetup\Secure*.</span></span> <span data-ttu-id="0ce55-176">Sertifikayı varsayılan adını değiştirmek için bu dosyayı düzenlemek (değeri Ara *CN ServiceFabricDevClusterCert =*).</span><span class="sxs-lookup"><span data-stu-id="0ce55-176">Edit this file to change the default name of the certificate (look for the value *CN=ServiceFabricDevClusterCert*).</span></span> <span data-ttu-id="0ce55-177">Bu komut dosyası olarak çalıştıracak `.\CertSetup.ps1 -Install`.</span><span class="sxs-lookup"><span data-stu-id="0ce55-177">Run this script as `.\CertSetup.ps1 -Install`.</span></span>

<span data-ttu-id="0ce55-178">Şimdi Sertifika PFX dosyasını korumalı bir parola ile dışa aktarın.</span><span class="sxs-lookup"><span data-stu-id="0ce55-178">Now export the certificate to a PFX file with a protected password.</span></span> <span data-ttu-id="0ce55-179">İlk sertifikanın parmak izini edinin.</span><span class="sxs-lookup"><span data-stu-id="0ce55-179">First get the thumbprint of the certificate.</span></span> <span data-ttu-id="0ce55-180">Gelen *Başlat* çalıştırmak menüsünde *bilgisayar sertifikalarını yönetmek*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-180">From the *Start* menu, run the *Manage computer certificates*.</span></span> <span data-ttu-id="0ce55-181">Gidin **yerel Bilgisayar\Kişisel** klasörü ve yeni sertifikayı oluşturan bulma.</span><span class="sxs-lookup"><span data-stu-id="0ce55-181">Navigate to the **Local Computer\Personal** folder and find the certificate you just created.</span></span> <span data-ttu-id="0ce55-182">Açmak için seçin sertifikayı çift tıklatın *ayrıntıları* sekmesinde ve ekranı aşağı kaydırarak *parmak izi* alan.</span><span class="sxs-lookup"><span data-stu-id="0ce55-182">Double-click the certificate to open it, select the *Details* tab and scroll down to the *Thumbprint* field.</span></span> <span data-ttu-id="0ce55-183">Parmak izi değeri, aşağıdaki PowerShell komutunu alanları kaldırdıktan sonra kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0ce55-183">Copy the thumbprint value into the PowerShell command below, after removing the spaces.</span></span>  <span data-ttu-id="0ce55-184">Değişiklik `String` koruyun ve PowerShell içinde aşağıdaki çalıştırmak için uygun bir güvenli parola değerine:</span><span class="sxs-lookup"><span data-stu-id="0ce55-184">Change the `String` value to a suitable secure password to protect it and run the following in PowerShell:</span></span>

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

<span data-ttu-id="0ce55-185">Makinede yüklü bir sertifika ayrıntılarını görmek için aşağıdaki PowerShell komutunu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0ce55-185">To see the details of a certificate installed on the machine you can run the following PowerShell command:</span></span>

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

<span data-ttu-id="0ce55-186">Alternatif olarak, bir Azure aboneliğiniz varsa, bölümü izleyin [sertifikaları anahtar Kasası'na eklemek](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span><span class="sxs-lookup"><span data-stu-id="0ce55-186">Alternatively, if you have an Azure subscription, follow the section [Add certificates to Key Vault](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault).</span></span>

## <a name="install-the-certificates"></a><span data-ttu-id="0ce55-187">Sertifika Yükleme</span><span class="sxs-lookup"><span data-stu-id="0ce55-187">Install the certificates</span></span>
<span data-ttu-id="0ce55-188">Sertifikaları olduktan sonra küme düğümleri üzerinde yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-188">Once you have certificate(s), you can install them on the cluster nodes.</span></span> <span data-ttu-id="0ce55-189">Düğümleriniz en son Windows PowerShell gerek 3.x yüklü.</span><span class="sxs-lookup"><span data-stu-id="0ce55-189">Your nodes need to have the latest Windows PowerShell 3.x installed on them.</span></span> <span data-ttu-id="0ce55-190">Küme ve sunucu sertifikaları ve tüm ikincil sertifikaları için her bir düğümde aşağıdaki adımları yinelemeniz gerekecek.</span><span class="sxs-lookup"><span data-stu-id="0ce55-190">You will need to repeat these steps on each node, for both Cluster and Server certificates and any secondary certificates.</span></span>

1. <span data-ttu-id="0ce55-191">.Pfx dosyaları düğüme kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0ce55-191">Copy the .pfx file(s) to the node.</span></span>
2. <span data-ttu-id="0ce55-192">Bir yönetici olarak bir PowerShell penceresi açın ve aşağıdaki komutları yazın.</span><span class="sxs-lookup"><span data-stu-id="0ce55-192">Open a PowerShell window as an administrator and enter the following commands.</span></span> <span data-ttu-id="0ce55-193">Değiştir *$pswd* bu sertifikayı oluşturmak için kullanılan parola ile.</span><span class="sxs-lookup"><span data-stu-id="0ce55-193">Replace the *$pswd* with the password that you used to create this certificate.</span></span> <span data-ttu-id="0ce55-194">Değiştir *$PfxFilePath* .pfx tam yoluna sahip bu düğüme kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="0ce55-194">Replace the *$PfxFilePath* with the full path of the .pfx copied to this node.</span></span>
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. <span data-ttu-id="0ce55-195">Şimdi ağ hizmeti hesabı altında çalışır, Service Fabric işlem, aşağıdaki komut dosyası çalıştırarak kullanabilmesi için bu sertifikaya erişim denetimini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0ce55-195">Now set the access control on this certificate so that the Service Fabric process, which runs under the Network Service account, can use it by running the following script.</span></span> <span data-ttu-id="0ce55-196">Hizmet hesabı "NETWORK SERVICE" ve sertifika parmak izini verin.</span><span class="sxs-lookup"><span data-stu-id="0ce55-196">Provide the thumbprint of the certificate and "NETWORK SERVICE" for the service account.</span></span> <span data-ttu-id="0ce55-197">Sertifikada açarak sertifika ACL'lerin doğru olduğundan emin olun *Başlat* > *bilgisayar sertifikalarını yönetmek* ve bakarak *tüm görevler*  >  *Özel anahtarları Yönet*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-197">You can check that the ACLs on the certificate are correct by opening the certificate in *Start* > *Manage computer certificates* and looking at *All Tasks* > *Manage Private Keys*.</span></span>
   
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
   
    # Specify the user, the permissions and the permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of the machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get the current acl of the private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add the new ace to the acl of the private key
    $acl.SetAccessRule($accessRule)
   
    # Write back the new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe the access rights currently assigned to this certificate.
    get-acl $keyFullPath| fl
    ```
4. <span data-ttu-id="0ce55-198">Her sunucu sertifikası için yukarıdaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0ce55-198">Repeat the steps above for each server certificate.</span></span> <span data-ttu-id="0ce55-199">Küme erişmesine izin vermek istediğiniz makinelere istemci sertifikalarını yüklemek için aşağıdaki adımları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-199">You can also use these steps to install the client certificates on the machines that you want to allow access to the cluster.</span></span>

## <a name="create-the-secure-cluster"></a><span data-ttu-id="0ce55-200">Güvenli küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ce55-200">Create the secure cluster</span></span>
<span data-ttu-id="0ce55-201">Yapılandırdıktan sonra **güvenlik** bölümünü **ClusterConfig.X509.MultiMachine.json** dosyası devam etmek için [kümenizi oluşturduktan](service-fabric-cluster-creation-for-windows-server.md#createcluster) düğümleri yapılandırma bölümü ve tek başına küme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0ce55-201">After configuring the **security** section of the **ClusterConfig.X509.MultiMachine.json** file, you can proceed to [Create your cluster](service-fabric-cluster-creation-for-windows-server.md#createcluster) section to configure the nodes and create the standalone cluster.</span></span> <span data-ttu-id="0ce55-202">Kullanmayı unutmayın **ClusterConfig.X509.MultiMachine.json** küme oluşturma sırasında dosya.</span><span class="sxs-lookup"><span data-stu-id="0ce55-202">Remember to use the **ClusterConfig.X509.MultiMachine.json** file while creating the cluster.</span></span> <span data-ttu-id="0ce55-203">Örneğin, komutunuzu aşağıdakine benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="0ce55-203">For example, your command might look like the following:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

<span data-ttu-id="0ce55-204">Güvenli tek başına Windows başarıyla çalışan küme ve buna bağlanmak için kimliği doğrulanmış istemciler ayarladıktan sonra bölümü izleyin [PowerShell kullanarak güvenli bir kümeye Bağlan](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="0ce55-204">Once you have the secure standalone Windows cluster successfully running, and have setup the authenticated clients to connect to it, follow the section [Connect to a secure cluster using PowerShell](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) to connect to it.</span></span> <span data-ttu-id="0ce55-205">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0ce55-205">For example:</span></span>

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

<span data-ttu-id="0ce55-206">Ardından, bu küme ile çalışmak için diğer PowerShell komutları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ce55-206">You can then run other PowerShell commands to work with this cluster.</span></span> <span data-ttu-id="0ce55-207">Örneğin, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) güvenli bu kümede düğümler listesi göstermek için.</span><span class="sxs-lookup"><span data-stu-id="0ce55-207">For example, [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) to show a list of nodes on this secure cluster.</span></span>


<span data-ttu-id="0ce55-208">Küme kaldırmak için Service Fabric paketi indirdiğiniz küme düğümünde bağlanmak, bir komut satırı açın ve paket klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="0ce55-208">To remove the cluster, connect to the node on the cluster where you downloaded the Service Fabric package, open a command line and navigate to the package folder.</span></span> <span data-ttu-id="0ce55-209">Şimdi aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0ce55-209">Now run the following command:</span></span>

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> <span data-ttu-id="0ce55-210">Yanlış sertifika yapılandırması Küme dağıtımı sırasında yaklaşan engellemek.</span><span class="sxs-lookup"><span data-stu-id="0ce55-210">Incorrect certificate configuration may prevent the cluster from coming up during deployment.</span></span> <span data-ttu-id="0ce55-211">Kendi kendine güvenlik sorunları tanılamak için lütfen Olay Görüntüleyicisi'ni grubunda bakın *uygulama ve hizmet günlükleri* > *Microsoft Service Fabric*.</span><span class="sxs-lookup"><span data-stu-id="0ce55-211">To self-diagnose security issues, please look in event viewer group *Applications and Services Logs* > *Microsoft-Service Fabric*.</span></span>
> 
> 

