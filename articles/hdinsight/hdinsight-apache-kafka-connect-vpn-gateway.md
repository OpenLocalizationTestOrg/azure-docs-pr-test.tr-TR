---
title: "Sanal ağları - Azure Hdınsight kullanarak aaaConnect tooKafka | Microsoft Docs"
description: "Nasıl toodirectly bağlanmak tooKafka hdınsight'ta bir Azure sanal ağı bilgi edinin. Bir VPN ağ geçidi kullanarak geliştirme istemcilerden ya da şirket içi istemcilerden tooconnect tooKafka nasıl ağ VPN ağ geçidi aygıtı kullanarak öğrenin."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.custom: hdinsightactive
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/01/2017
ms.author: larryfr
ms.openlocfilehash: 03542fe14b9a1d010dffa22a8f8d96b098a1576e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tookafka-on-hdinsight-preview-through-an-azure-virtual-network"></a><span data-ttu-id="5e791-104">Bir Azure sanal ağı (Önizleme) hdınsight'ta tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="5e791-104">Connect tooKafka on HDInsight (preview) through an Azure Virtual Network</span></span>

<span data-ttu-id="5e791-105">Toodirectly tooKafka Azure sanal ağları kullanarak hdınsight'ta nasıl bağlanacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5e791-105">Learn how toodirectly connect tooKafka on HDInsight using Azure Virtual Networks.</span></span> <span data-ttu-id="5e791-106">Bu belgede, yapılandırmaları aşağıdaki hello kullanarak tooKafka bağlanmaya ilişkin bilgiler sağlanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5e791-106">This document provides information on connecting tooKafka using hello following configurations:</span></span>

* <span data-ttu-id="5e791-107">Bir şirket ağında kaynaklardan.</span><span class="sxs-lookup"><span data-stu-id="5e791-107">From resources in an on-premises network.</span></span> <span data-ttu-id="5e791-108">Bu bağlantı, yerel ağınızda bir VPN cihazı (yazılım veya donanım) kullanılarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5e791-108">This connection is established by using a VPN device (software or hardware) on your local network.</span></span>
* <span data-ttu-id="5e791-109">Geliştirme ortamından bir VPN yazılımı istemcisi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5e791-109">From a development environment using a VPN software client.</span></span>

## <a name="architecture-and-planning"></a><span data-ttu-id="5e791-110">Mimari ve planlama</span><span class="sxs-lookup"><span data-stu-id="5e791-110">Architecture and planning</span></span>

<span data-ttu-id="5e791-111">Hdınsight doğrudan bağlantı tooKafka hello izin vermiyor genel internet.</span><span class="sxs-lookup"><span data-stu-id="5e791-111">HDInsight does not allow direct connection tooKafka over hello public internet.</span></span> <span data-ttu-id="5e791-112">Bunun yerine, Kafka istemcileri (üreticileri ve tüketicileri) bağlantı yöntemleri aşağıdaki hello birini kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5e791-112">Instead, Kafka clients (producers and consumers) must use one of hello following connection methods:</span></span>

* <span data-ttu-id="5e791-113">Hello Hello istemcisini çalıştıran hdınsight'ta Kafka aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="5e791-113">Run hello client in hello same virtual network as Kafka on HDInsight.</span></span> <span data-ttu-id="5e791-114">Bu yapılandırma hello kullanılır [Hdınsight üzerinde Apache Kafka (Önizleme) ile başlar](hdinsight-apache-kafka-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="5e791-114">This configuration is used in hello [Start with Apache Kafka (preview) on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span> <span data-ttu-id="5e791-115">Merhaba doğrudan istemci çalışır hello üzerinde Hdınsight küme düğümü veya başka bir sanal makinede aynı hello ağ.</span><span class="sxs-lookup"><span data-stu-id="5e791-115">hello client runs directly on hello HDInsight cluster nodes or on another virtual machine in hello same network.</span></span>

* <span data-ttu-id="5e791-116">Şirket içi ağınıza toohello sanal ağ gibi özel bir ağa bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5e791-116">Connect a private network, such as your on-premises network, toohello virtual network.</span></span> <span data-ttu-id="5e791-117">Bu yapılandırma istemcileri Kafka ile şirket içi ağ toodirectly çalışmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e791-117">This configuration allows clients in your on-premises network toodirectly work with Kafka.</span></span> <span data-ttu-id="5e791-118">tooenable bu yapılandırma, hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5e791-118">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="5e791-119">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e791-119">Create a virtual network.</span></span>
    2. <span data-ttu-id="5e791-120">Siteden siteye yapılandırmasını kullanan bir VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e791-120">Create a VPN gateway that uses a site-to-site configuration.</span></span> <span data-ttu-id="5e791-121">Bu belgede kullanılan hello yapılandırma tooa VPN ağ geçidi aygıtı, şirket içi ağınıza bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5e791-121">hello configuration used in this document connects tooa VPN gateway device in your on-premises network.</span></span>
    3. <span data-ttu-id="5e791-122">Bir DNS sunucusu hello sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e791-122">Create a DNS server in hello virtual network.</span></span>
    4. <span data-ttu-id="5e791-123">Her ağ hello DNS sunucusu arasında iletim yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5e791-123">Configure forwarding between hello DNS server in each network.</span></span>
    5. <span data-ttu-id="5e791-124">Kafka Hdınsight'ta hello sanal ağınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5e791-124">Install Kafka on HDInsight into hello virtual network.</span></span>

    <span data-ttu-id="5e791-125">Merhaba daha fazla bilgi için bkz: [tooKafka bir şirket içi ağ üzerinden bağlanma](#on-premises) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5e791-125">For more information, see hello [Connect tooKafka from an on-premises network](#on-premises) section.</span></span> 

* <span data-ttu-id="5e791-126">Makineleri tek tek toohello sanal ağ VPN ağ geçidi ve VPN istemcisi kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5e791-126">Connect individual machines toohello virtual network using a VPN gateway and VPN client.</span></span> <span data-ttu-id="5e791-127">tooenable bu yapılandırma, hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="5e791-127">tooenable this configuration, perform hello following tasks:</span></span>

    1. <span data-ttu-id="5e791-128">Bir sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e791-128">Create a virtual network.</span></span>
    2. <span data-ttu-id="5e791-129">Bir noktadan siteye yapılandırması kullanan bir VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5e791-129">Create a VPN gateway that uses a point-to-site configuration.</span></span> <span data-ttu-id="5e791-130">Bu yapılandırma Windows istemcilerinde yüklü bir VPN istemcisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e791-130">This configuration provides a VPN client that can be installed on Windows clients.</span></span>
    3. <span data-ttu-id="5e791-131">Kafka Hdınsight'ta hello sanal ağınıza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5e791-131">Install Kafka on HDInsight into hello virtual network.</span></span>
    4. <span data-ttu-id="5e791-132">Kafka IP reklam için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5e791-132">Configure Kafka for IP advertising.</span></span> <span data-ttu-id="5e791-133">Bu yapılandırma, IP adresi yerine etki alanı adlarını kullanarak hello istemci tooconnect sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e791-133">This configuration allows hello client tooconnect using IP addressing instead of domain names.</span></span>
    5. <span data-ttu-id="5e791-134">İndirin ve hello geliştirme sisteminde hello VPN İstemcisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e791-134">Download and use hello VPN client on hello development system.</span></span>

    <span data-ttu-id="5e791-135">Merhaba daha fazla bilgi için bkz: [tooKafka bir VPN istemcisi ile bağlantı](#vpnclient) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5e791-135">For more information, see hello [Connect tooKafka with a VPN client](#vpnclient) section.</span></span>

    > [!WARNING]
    > <span data-ttu-id="5e791-136">Bu yapılandırma, yalnızca Geliştirme amaçlı sınırlamalar aşağıdaki hello nedeniyle önerilir:</span><span class="sxs-lookup"><span data-stu-id="5e791-136">This configuration is only recommended for development purposes because of hello following limitations:</span></span>
    >
    > * <span data-ttu-id="5e791-137">Her bir istemci bir VPN yazılımı istemcisi kullanarak bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e791-137">Each client must connect using a VPN software client.</span></span> <span data-ttu-id="5e791-138">Azure yalnızca Windows tabanlı bir istemci sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e791-138">Azure only provides a Windows-based client.</span></span>
    > * <span data-ttu-id="5e791-139">IP ile Kafka toocommunicate adresleme kullanmalısınız hello istemci ad çözümleme istekleri toohello sanal ağ, geçmez.</span><span class="sxs-lookup"><span data-stu-id="5e791-139">hello client does not pass name resolution requests toohello virtual network, so you must use IP addressing toocommunicate with Kafka.</span></span> <span data-ttu-id="5e791-140">IP iletişimi hello Kafka küme üzerinde ek yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5e791-140">IP communication requires additional configuration on hello Kafka cluster.</span></span>

<span data-ttu-id="5e791-141">Sanal bir ağa Hdınsight kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure sanal ağları kullanarak Hdınsight](./hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="5e791-141">For more information on using HDInsight in a virtual network, see [Extend HDInsight by using Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).</span></span>

## <span data-ttu-id="5e791-142"><a id="on-premises"></a>Bir şirket içi ağdan tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="5e791-142"><a id="on-premises"></a> Connect tooKafka from an on-premises network</span></span>

<span data-ttu-id="5e791-143">toocreate şirket içi ağınız ile iletişim kuran Kafka küme hello hello adımlarını izleyin [bağlanmak Hdınsight tooyour şirket içi ağ](./connect-on-premises-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="5e791-143">toocreate a Kafka cluster that communicates with your on-premises network, follow hello steps in hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e791-144">Merhaba Hdınsight kümesi oluştururken, hello seçin __Kafka__ küme türü.</span><span class="sxs-lookup"><span data-stu-id="5e791-144">When creating hello HDInsight cluster, select hello __Kafka__ cluster type.</span></span>

<span data-ttu-id="5e791-145">Bu adımları yapılandırma aşağıdaki hello oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5e791-145">These steps create hello following configuration:</span></span>

* <span data-ttu-id="5e791-146">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="5e791-146">Azure Virtual Network</span></span>
* <span data-ttu-id="5e791-147">Siteden siteye VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="5e791-147">Site-to-site VPN gateway</span></span>
* <span data-ttu-id="5e791-148">Azure depolama hesabı (Hdınsight tarafından kullanılır)</span><span class="sxs-lookup"><span data-stu-id="5e791-148">Azure Storage account (used by HDInsight)</span></span>
* <span data-ttu-id="5e791-149">Hdınsight üzerinde Kafka</span><span class="sxs-lookup"><span data-stu-id="5e791-149">Kafka on HDInsight</span></span>

<span data-ttu-id="5e791-150">Şirket içi, kullanım hello hello adımlarda Kafka istemcisi toohello küme bağlanabilir tooverify [örnek: Python istemci](#python-client) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5e791-150">tooverify that a Kafka client can connect toohello cluster from on-premises, use hello steps in hello [Example: Python client](#python-client) section.</span></span>

## <span data-ttu-id="5e791-151"><a id="vpnclient"></a>Bir VPN istemcisiyle tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="5e791-151"><a id="vpnclient"></a> Connect tooKafka with a VPN client</span></span>

<span data-ttu-id="5e791-152">Bu bölümde toocreate hello yapılandırma aşağıdaki Hello adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="5e791-152">Use hello steps in this section toocreate hello following configuration:</span></span>

* <span data-ttu-id="5e791-153">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="5e791-153">Azure Virtual Network</span></span>
* <span data-ttu-id="5e791-154">Noktadan siteye VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="5e791-154">Point-to-site VPN gateway</span></span>
* <span data-ttu-id="5e791-155">Azure depolama hesabı (Hdınsight tarafından kullanılır)</span><span class="sxs-lookup"><span data-stu-id="5e791-155">Azure Storage Account (used by HDInsight)</span></span>
* <span data-ttu-id="5e791-156">Hdınsight üzerinde Kafka</span><span class="sxs-lookup"><span data-stu-id="5e791-156">Kafka on HDInsight</span></span>

1. <span data-ttu-id="5e791-157">Merhaba Hello adımları [noktadan siteye bağlantıları için otomatik olarak imzalanan sertifikalar ile çalışma](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) belge.</span><span class="sxs-lookup"><span data-stu-id="5e791-157">Follow hello steps in hello [Working with self-signed certificates for Point-to-site connections](../vpn-gateway/vpn-gateway-certificates-point-to-site.md) document.</span></span> <span data-ttu-id="5e791-158">Bu belge hello ağ geçidi için gereken hello sertifikaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5e791-158">This document creates hello certificates needed for hello gateway.</span></span>

2. <span data-ttu-id="5e791-159">PowerShell komut istemini açın ve aşağıdaki kodu toolog tooyour Azure aboneliği içindeki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="5e791-159">Open a PowerShell prompt and use hello following code toolog in tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureRmAccount
    # If you have multiple subscriptions, uncomment tooset hello subscription
    #Select-AzureRmSubscription -SubscriptionName "name of your subscription"
    ```

3. <span data-ttu-id="5e791-160">Yapılandırma bilgilerini içeren kod toocreate değişkenler aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5e791-160">Use hello following code toocreate variables that contain configuration information:</span></span>

    ```powershell
    # Prompt for generic information
    $resourceGroupName = Read-Host "What is hello resource group name?"
    $baseName = Read-Host "What is hello base name? It is used toocreate names for resources, such as 'net-basename' and 'kafka-basename':"
    $location = Read-Host "What Azure Region do you want toocreate hello resources in?"
    $rootCert = Read-Host "What is hello file path toohello root certificate? It is used toosecure hello VPN gateway."

    # Prompt for HDInsight credentials
    $adminCreds = Get-Credential -Message "Enter hello HTTPS user name and password for hello HDInsight cluster" -UserName "admin"
    $sshCreds = Get-Credential -Message "Enter hello SSH user name and password for hello HDInsight cluster" -UserName "sshuser"

    # Names for Azure resources
    $networkName = "net-$baseName"
    $clusterName = "kafka-$baseName"
    $storageName = "store$baseName" # Can't use dashes in storage names
    $defaultContainerName = $clusterName
    $defaultSubnetName = "default"
    $gatewaySubnetName = "GatewaySubnet"
    $gatewayPublicIpName = "GatewayIp"
    $gatewayIpConfigName = "GatewayConfig"
    $vpnRootCertName = "rootcert"
    $vpnName = "VPNGateway"

    # Network settings
    $networkAddressPrefix = "10.0.0.0/16"
    $defaultSubnetPrefix = "10.0.0.0/24"
    $gatewaySubnetPrefix = "10.0.1.0/24"
    $vpnClientAddressPool = "172.16.201.0/24"

    # HDInsight settings
    $HdiWorkerNodes = 4
    $hdiVersion = "3.5"
    $hdiType = "Kafka"
    ```

4. <span data-ttu-id="5e791-161">Kullanım hello aşağıdaki kod toocreate hello Azure kaynak grubu ve sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="5e791-161">Use hello following code toocreate hello Azure resource group and virtual network:</span></span>

    ```powershell
    # Create hello resource group that contains everything
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello subnet configuration
    $defaultSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -AddressPrefix $defaultSubnetPrefix
    $gatewaySubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -AddressPrefix $gatewaySubnetPrefix

    # Create hello subnet
    New-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AddressPrefix $networkAddressPrefix `
        -Subnet $defaultSubnetConfig, $gatewaySubnetConfig

    # Get hello network & subnet that were created
    $network = Get-AzureRmVirtualNetwork -Name $networkName `
        -ResourceGroupName $resourceGroupName
    $gatewaySubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $gatewaySubnetName `
        -VirtualNetwork $network
    $defaultSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $defaultSubnetName `
        -VirtualNetwork $network

    # Set a dynamic public IP address for hello gateway subnet
    $gatewayPublicIp = New-AzureRmPublicIpAddress -Name $gatewayPublicIpName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -AllocationMethod Dynamic
    $gatewayIpConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $gatewayIpConfigName `
        -Subnet $gatewaySubnet `
        -PublicIpAddress $gatewayPublicIp

    # Get hello certificate info
    # Get hello full path in case a relative path was passed
    $rootCertFile = Get-ChildItem $rootCert
    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($rootCertFile)
    $certBase64 = [System.Convert]::ToBase64String($cert.RawData)
    $p2sRootCert = New-AzureRmVpnClientRootCertificate -Name $vpnRootCertName `
        -PublicCertData $certBase64

    # Create hello VPN gateway
    New-AzureRmVirtualNetworkGateway -Name $vpnName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -IpConfigurations $gatewayIpConfig `
        -GatewayType Vpn `
        -VpnType RouteBased `
        -EnableBgp $false `
        -GatewaySku Standard `
        -VpnClientAddressPool $vpnClientAddressPool `
        -VpnClientRootCertificates $p2sRootCert
    ```

    > [!WARNING]
    > <span data-ttu-id="5e791-162">Bu işlem toocomplete için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5e791-162">It can take several minutes for this process toocomplete.</span></span>

5. <span data-ttu-id="5e791-163">Aşağıdaki kod, toocreate hello Azure depolama hesabı ve blob kapsayıcı hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5e791-163">Use hello following code toocreate hello Azure Storage Account and blob container:</span></span>

    ```powershell
    # Create hello storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $storageName `
        -Type Standard_GRS `
        -Location $location

    # Get hello storage account keys and create a context
    $defaultStorageKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName `
        -Name $storageName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageName `
        -StorageAccountKey $defaultStorageKey

    # Create hello default storage container
    New-AzureStorageContainer -Name $defaultContainerName `
        -Context $storageContext
    ```

6. <span data-ttu-id="5e791-164">Aşağıdaki kod toocreate hello Hdınsight kümesi hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5e791-164">Use hello following code toocreate hello HDInsight cluster:</span></span>

    ```powershell
    # Create hello HDInsight cluster
    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $hdiWorkerNodes `
        -ClusterType $hdiType `
        -OSType Linux `
        -Version $hdiVersion `
        -HttpCredential $adminCreds `
        -SshCredential $sshCreds `
        -DefaultStorageAccountName "$storageName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageKey `
        -DefaultStorageContainer $defaultContainerName `
        -VirtualNetworkId $network.Id `
        -SubnetName $defaultSubnet.Id
    ```

  > [!WARNING]
  > <span data-ttu-id="5e791-165">Bu işlem yaklaşık 20 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="5e791-165">This process takes around 20 minutes toocomplete.</span></span>

8. <span data-ttu-id="5e791-166">Cmdlet tooretrieve hello URL hello sanal ağ için hello Windows VPN istemcisi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5e791-166">Use hello following cmdlet tooretrieve hello URL for hello Windows VPN client for hello virtual network:</span></span>

    ```powershell
    Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName `
        -VirtualNetworkGatewayName $vpnName `
        -ProcessorArchitecture Amd64
    ```

    <span data-ttu-id="5e791-167">toodownload hello Windows VPN istemcisi, kullanım hello web tarayıcınızda URİ'si döndürüldü.</span><span class="sxs-lookup"><span data-stu-id="5e791-167">toodownload hello Windows VPN client, use hello returned URI in your web browser.</span></span>

### <a name="configure-kafka-for-ip-advertising"></a><span data-ttu-id="5e791-168">Kafka IP reklam için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e791-168">Configure Kafka for IP advertising</span></span>

<span data-ttu-id="5e791-169">Varsayılan olarak, Zookeeper hello Kafka aracıların tooclients hello etki alanı adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e791-169">By default, Zookeeper returns hello domain name of hello Kafka brokers tooclients.</span></span> <span data-ttu-id="5e791-170">Bu yapılandırma tarafından ad çözümlemesi hello sanal ağ içindeki varlıklar için kullanılamaz olarak VPN yazılımı istemci hello ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="5e791-170">This configuration does not work with hello VPN software client, as it cannot use name resolution for entities in hello virtual network.</span></span> <span data-ttu-id="5e791-171">Bu yapılandırma için hello aşağıdaki kullanın adımları tooconfigure Kafka tooadvertise IP adresleri yerine etki alanı adları:</span><span class="sxs-lookup"><span data-stu-id="5e791-171">For this configuration, use hello following steps tooconfigure Kafka tooadvertise IP addresses instead of domain names:</span></span>

1. <span data-ttu-id="5e791-172">Bir web tarayıcısı kullanarak toohttps://CLUSTERNAME.azurehdinsight.net gidin.</span><span class="sxs-lookup"><span data-stu-id="5e791-172">Using a web browser, go toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5e791-173">Değiştir __CLUSTERNAME__ hello Kafka Hdınsight kümesinde hello adı.</span><span class="sxs-lookup"><span data-stu-id="5e791-173">Replace __CLUSTERNAME__ with hello name of hello Kafka on HDInsight cluster.</span></span>

    <span data-ttu-id="5e791-174">İstendiğinde, hello HTTPS kullanıcı adı ve parola hello küme için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e791-174">When prompted, use hello HTTPS user name and password for hello cluster.</span></span> <span data-ttu-id="5e791-175">Merhaba küme Merhaba Ambari Web kullanıcı Arabirimi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5e791-175">hello Ambari Web UI for hello cluster is displayed.</span></span>

2. <span data-ttu-id="5e791-176">Kafka, tooview bilgi seçin __Kafka__ hello soldaki hello listeden.</span><span class="sxs-lookup"><span data-stu-id="5e791-176">tooview information on Kafka, select __Kafka__ from hello list on hello left.</span></span>

    ![Hizmet listesi Kafka ile vurgulanan](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-service.png)

3. <span data-ttu-id="5e791-178">tooview Kafka yapılandırma seçin __yapılandırmalar__ hello üst orta gelen.</span><span class="sxs-lookup"><span data-stu-id="5e791-178">tooview Kafka configuration, select __Configs__ from hello top middle.</span></span>

    ![Kafka için yapılandırmalar bağlantıları](./media/hdinsight-apache-kafka-connect-vpn-gateway/select-kafka-config.png)

4. <span data-ttu-id="5e791-180">toofind hello __kafka env__ yapılandırması girin `kafka-env` hello içinde __filtre__ hello üst köşedeki alan.</span><span class="sxs-lookup"><span data-stu-id="5e791-180">toofind hello __kafka-env__ configuration, enter `kafka-env` in hello __Filter__ field on hello upper right.</span></span>

    ![Kafka env için Kafka yapılandırma](./media/hdinsight-apache-kafka-connect-vpn-gateway/search-for-kafka-env.png)

5. <span data-ttu-id="5e791-182">tooconfigure Kafka tooadvertise IP adresleri, metin toohello hello sonuna aşağıdaki hello eklemek __kafka env şablonu__ alan:</span><span class="sxs-lookup"><span data-stu-id="5e791-182">tooconfigure Kafka tooadvertise IP addresses, add hello following text toohello bottom of hello __kafka-env-template__ field:</span></span>

    ```
    # Configure Kafka tooadvertise IP addresses instead of FQDN
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

6. <span data-ttu-id="5e791-183">Kafka dinlediği tooconfigure hello arabirimine `listeners` hello içinde __filtre__ hello üst köşedeki alan.</span><span class="sxs-lookup"><span data-stu-id="5e791-183">tooconfigure hello interface that Kafka listens on, enter `listeners` in hello __Filter__ field on hello upper right.</span></span>

7. <span data-ttu-id="5e791-184">tüm ağ arabirimlerinde, değişiklik hello hello değerinde Kafka toolisten tooconfigure __dinleyicileri__ çok alan`PLAINTEXT://0.0.0.0:9092`.</span><span class="sxs-lookup"><span data-stu-id="5e791-184">tooconfigure Kafka toolisten on all network interfaces, change hello value in hello __listeners__ field too`PLAINTEXT://0.0.0.0:9092`.</span></span>

8. <span data-ttu-id="5e791-185">toosave hello yapılandırma değişikliklerini kullanmak hello __kaydetmek__ düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5e791-185">toosave hello configuration changes, use hello __Save__ button.</span></span> <span data-ttu-id="5e791-186">Merhaba değişiklikleri açıklayan bir metin iletisi girin.</span><span class="sxs-lookup"><span data-stu-id="5e791-186">Enter a text message describing hello changes.</span></span> <span data-ttu-id="5e791-187">Seçin __Tamam__ hello değişiklikler kaydedildikten sonra.</span><span class="sxs-lookup"><span data-stu-id="5e791-187">Select __OK__ once hello changes have been saved.</span></span>

    ![Kaydet Yapılandırma düğmesi](./media/hdinsight-apache-kafka-connect-vpn-gateway/save-button.png)

9. <span data-ttu-id="5e791-189">Kafka, yeniden başlatılırken tooprevent hatalarıyla hello __hizmet eylemleri__ düğmesine tıklayın ve ardından __kapatma üzerinde Bakım modu__.</span><span class="sxs-lookup"><span data-stu-id="5e791-189">tooprevent errors when restarting Kafka, use hello __Service Actions__ button and select __Turn On Maintenance Mode__.</span></span> <span data-ttu-id="5e791-190">Bu işlem Tamam toocomplete seçin.</span><span class="sxs-lookup"><span data-stu-id="5e791-190">Select OK toocomplete this operation.</span></span>

    ![Hizmet eylemlerle vurgulanmış bakım etkinleştirin](./media/hdinsight-apache-kafka-connect-vpn-gateway/turn-on-maintenance-mode.png)

10. <span data-ttu-id="5e791-192">toorestart Kafka, hello kullan __yeniden__ düğmesine tıklayın ve ardından __yeniden tüm etkilenen__.</span><span class="sxs-lookup"><span data-stu-id="5e791-192">toorestart Kafka, use hello __Restart__ button and select __Restart All Affected__.</span></span> <span data-ttu-id="5e791-193">Merhaba yeniden onaylayın ve ardından hello __Tamam__ hello işlemi tamamlandıktan sonra düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5e791-193">Confirm hello restart, and then use hello __OK__ button after hello operation has completed.</span></span>

    ![Etkilenen yeniden başlatma ile tüm düğmesi vurgulanmış yeniden başlatın](./media/hdinsight-apache-kafka-connect-vpn-gateway/restart-button.png)

11. <span data-ttu-id="5e791-195">toodisable Bakım modu, kullanım hello __hizmet eylemleri__ düğmesine tıklayın ve ardından __Bakım modu devre dışı bırakma__.</span><span class="sxs-lookup"><span data-stu-id="5e791-195">toodisable maintenance mode, use hello __Service Actions__ button and select __Turn Off Maintenance Mode__.</span></span> <span data-ttu-id="5e791-196">Seçin **Tamam** toocomplete bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="5e791-196">Select **OK** toocomplete this operation.</span></span>

### <a name="connect-toohello-vpn-gateway"></a><span data-ttu-id="5e791-197">Toohello VPN ağ geçidi Bağlan</span><span class="sxs-lookup"><span data-stu-id="5e791-197">Connect toohello VPN gateway</span></span>

<span data-ttu-id="5e791-198">tooconnect toohello VPN ağ geçidi bir __Windows İstemcisi__, hello kullan __tooAzure bağlanmak__ hello bölümünü [noktadan siteye bağlantı yapılandırma](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) belge.</span><span class="sxs-lookup"><span data-stu-id="5e791-198">tooconnect toohello VPN gateway from a __Windows client__, use hello __Connect tooAzure__ section of hello [Configure a Point-to-Site connection](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md#clientcertificate) document.</span></span>

## <span data-ttu-id="5e791-199"><a id="python-client"></a>Örnek: Python istemci</span><span class="sxs-lookup"><span data-stu-id="5e791-199"><a id="python-client"></a> Example: Python client</span></span>

<span data-ttu-id="5e791-200">toovalidate bağlantı tooKafka, aşağıdaki adımları toocreate hello kullanın ve Python üretici ve tüketici çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5e791-200">toovalidate connectivity tooKafka, use hello following steps toocreate and run a Python producer and consumer:</span></span>

1. <span data-ttu-id="5e791-201">Etki alanı adı (FQDN) ve IP adreslerini hello Kafka küme hello düğümler yöntemleri tooretrieve hello tam olarak aşağıdaki hello birini tam:</span><span class="sxs-lookup"><span data-stu-id="5e791-201">Use one of hello following methods tooretrieve hello fully qualified domain name (FQDN) and IP addresses of hello nodes in hello Kafka cluster:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="5e791-202">Bu komut dosyası varsayar `$resourceGroupName` hello sanal ağ içeren hello Azure kaynak grubu hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="5e791-202">This script assumes that `$resourceGroupName` is hello name of hello Azure resource group that contains hello virtual network.</span></span>

    <span data-ttu-id="5e791-203">Merhaba hello sonraki adımda döndürülen bilgilerini kullanmak için kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5e791-203">Save hello returned information for use in hello next steps.</span></span>

2. <span data-ttu-id="5e791-204">Kullanım hello tooinstall hello aşağıdaki [kafka python](http://kafka-python.readthedocs.io/) istemci:</span><span class="sxs-lookup"><span data-stu-id="5e791-204">Use hello following tooinstall hello [kafka-python](http://kafka-python.readthedocs.io/) client:</span></span>

        pip install kafka-python

3. <span data-ttu-id="5e791-205">toosend veri tooKafka, Python kodu aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="5e791-205">toosend data tooKafka, use hello following Python code:</span></span>

  ```python
  from kafka import KafkaProducer
  # Replace hello `ip_address` entries with hello IP address of your worker nodes
  # NOTE: you don't need hello full list of worker nodes, just one or two.
  producer = KafkaProducer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'])
  for _ in range(50):
      producer.send('testtopic', b'test message')
  ```

    <span data-ttu-id="5e791-206">Hello yerine `'kafka_broker'` girişleri hello adresleriyle döndürülen bu bölümdeki 1. adımdaki:</span><span class="sxs-lookup"><span data-stu-id="5e791-206">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="5e791-207">Kullanıyorsanız bir __yazılım VPN istemcisi__, hello yerine `kafka_broker` girişleri çalışan düğümlerinizin hello IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="5e791-207">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="5e791-208">Varsa __ad çözümlemesinin özel bir DNS sunucusu üzerinden etkin__, hello yerine `kafka_broker` girişleri hello hello çalışan düğümleri FQDN'si ile.</span><span class="sxs-lookup"><span data-stu-id="5e791-208">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5e791-209">Bu kod hello dizesi gönderir `test message` toohello konu `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="5e791-209">This code sends hello string `test message` toohello topic `testtopic`.</span></span> <span data-ttu-id="5e791-210">henüz yoksa hello varsayılan yapılandırmasını hdınsight'ta Kafka toocreate hello konudur.</span><span class="sxs-lookup"><span data-stu-id="5e791-210">hello default configuration of Kafka on HDInsight is toocreate hello topic if it does not exist.</span></span>

4. <span data-ttu-id="5e791-211">tooretrieve hello iletileri Kafka, Python kodu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="5e791-211">tooretrieve hello messages from Kafka, use hello following Python code:</span></span>

   ```python
   from kafka import KafkaConsumer
   # Replace hello `ip_address` entries with hello IP address of your worker nodes
   # Again, you only need one or two, not hello full list.
   # Note: auto_offset_reset='earliest' resets hello starting offset toohello beginning
   #       of hello topic
   consumer = KafkaConsumer(bootstrap_servers=['kafka_broker_1','kafka_broker_2'],auto_offset_reset='earliest')
   consumer.subscribe(['testtopic'])
   for msg in consumer:
     print (msg)
   ```

    <span data-ttu-id="5e791-212">Hello yerine `'kafka_broker'` girişleri hello adresleriyle döndürülen bu bölümdeki 1. adımdaki:</span><span class="sxs-lookup"><span data-stu-id="5e791-212">Replace hello `'kafka_broker'` entries with hello addresses returned from step 1 in this section:</span></span>

    * <span data-ttu-id="5e791-213">Kullanıyorsanız bir __yazılım VPN istemcisi__, hello yerine `kafka_broker` girişleri çalışan düğümlerinizin hello IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="5e791-213">If you are using a __Software VPN client__, replace hello `kafka_broker` entries with hello IP address of your worker nodes.</span></span>

    * <span data-ttu-id="5e791-214">Varsa __ad çözümlemesinin özel bir DNS sunucusu üzerinden etkin__, hello yerine `kafka_broker` girişleri hello hello çalışan düğümleri FQDN'si ile.</span><span class="sxs-lookup"><span data-stu-id="5e791-214">If you have __enabled name resolution through a custom DNS server__, replace hello `kafka_broker` entries with hello FQDN of hello worker nodes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e791-215">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e791-215">Next steps</span></span>

<span data-ttu-id="5e791-216">Merhaba Hdınsight bir sanal ağ ile kullanma hakkında daha fazla bilgi için bkz: [genişletmek Azure bir Azure sanal ağı kullanarak Hdınsight](hdinsight-extend-hadoop-virtual-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="5e791-216">For more information on using HDInsight with a virtual network, see hello [Extend Azure HDInsight using an Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

<span data-ttu-id="5e791-217">Noktadan siteye VPN ağ geçidi ile bir Azure sanal ağı oluşturma konusunda daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5e791-217">For more information on creating an Azure Virtual Network with Point-to-Site VPN gateway, see hello following documents:</span></span>

* [<span data-ttu-id="5e791-218">Hello Azure portal kullanarak bir noktadan siteye bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e791-218">Configure a Point-to-Site connection using hello Azure portal</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md)

* [<span data-ttu-id="5e791-219">Azure PowerShell kullanarak bir noktadan siteye bağlantı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5e791-219">Configure a Point-to-Site connection using Azure PowerShell</span></span>](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

<span data-ttu-id="5e791-220">Hdınsight'ta Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="5e791-220">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="5e791-221">HDInsight'ta Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5e791-221">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="5e791-222">Hdınsight üzerinde Kafka ile yansıtma kullanın</span><span class="sxs-lookup"><span data-stu-id="5e791-222">Use mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
