---
title: "aaaImplement Oracle Golden kapısı Azure Linux VM'de | Microsoft Docs"
description: "Hızla bir Oracle Golden kapısı yukarı ve Azure ortamınızda çalışan alın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="058b9-103">Bir Azure Linux VM'de Oracle Golden kapısı uygulama</span><span class="sxs-lookup"><span data-stu-id="058b9-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="058b9-104">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="058b9-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="058b9-105">Bu kılavuzu nasıl toouse hello Azure CLI toodeploy 12 c bir Oracle veritabanı hello Azure Market galeri görüntüsünden ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="058b9-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="058b9-106">Bu belge size adım adım gösterir nasıl toocreate, yükleyin ve Oracle Golden kapısı Azure VM temelinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="058b9-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="058b9-107">Başlamadan önce Azure CLI yüklenmiş bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="058b9-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="058b9-108">Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="058b9-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="058b9-109">Merhaba ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="058b9-109">Prepare hello environment</span></span>

<span data-ttu-id="058b9-110">tooperform hello Oracle Golden kapısı yükleme, gereksinim duyduğunuz hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="058b9-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="058b9-111">Merhaba Market görüntü toocreate hello VM'ler kullandığınız **Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="058b9-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="058b9-112">Ayrıca toobe UNIX Düzenleyicisi VI aşina gerekir ve x11 (X Windows), temel bilgilere sahipsiniz.</span><span class="sxs-lookup"><span data-stu-id="058b9-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="058b9-113">Merhaba, hello ortamı yapılandırmasının özeti aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="058b9-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="058b9-114">**Birincil site**</span><span class="sxs-lookup"><span data-stu-id="058b9-114">**Primary site**</span></span> | <span data-ttu-id="058b9-115">**Çoğaltma sitesi**</span><span class="sxs-lookup"><span data-stu-id="058b9-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="058b9-116">**Oracle Sürüm**</span><span class="sxs-lookup"><span data-stu-id="058b9-116">**Oracle release**</span></span> |<span data-ttu-id="058b9-117">Oracle 12c sürüm 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="058b9-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="058b9-118">Oracle 12c sürüm 2 – (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="058b9-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="058b9-119">**Makine adı**</span><span class="sxs-lookup"><span data-stu-id="058b9-119">**Machine name**</span></span> |<span data-ttu-id="058b9-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="058b9-120">myVM1</span></span> |<span data-ttu-id="058b9-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="058b9-121">myVM2</span></span> |
> | <span data-ttu-id="058b9-122">**İşletim Sistemi**</span><span class="sxs-lookup"><span data-stu-id="058b9-122">**Operating system**</span></span> |<span data-ttu-id="058b9-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="058b9-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="058b9-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="058b9-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="058b9-125">**Oracle SID**</span><span class="sxs-lookup"><span data-stu-id="058b9-125">**Oracle SID**</span></span> |<span data-ttu-id="058b9-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="058b9-126">CDB1</span></span> |<span data-ttu-id="058b9-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="058b9-127">CDB1</span></span> |
> | <span data-ttu-id="058b9-128">**Çoğaltma şeması**</span><span class="sxs-lookup"><span data-stu-id="058b9-128">**Replication schema**</span></span> |<span data-ttu-id="058b9-129">TEST</span><span class="sxs-lookup"><span data-stu-id="058b9-129">TEST</span></span>|<span data-ttu-id="058b9-130">TEST</span><span class="sxs-lookup"><span data-stu-id="058b9-130">TEST</span></span> |
> | <span data-ttu-id="058b9-131">**Golden kapısı sahibi/çoğaltılır**</span><span class="sxs-lookup"><span data-stu-id="058b9-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="058b9-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="058b9-132">C##GGADMIN</span></span> |<span data-ttu-id="058b9-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="058b9-133">REPUSER</span></span> |
> | <span data-ttu-id="058b9-134">**Golden kapısı işlemi**</span><span class="sxs-lookup"><span data-stu-id="058b9-134">**Golden Gate process**</span></span> |<span data-ttu-id="058b9-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="058b9-135">EXTORA</span></span> |<span data-ttu-id="058b9-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="058b9-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="058b9-137">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="058b9-137">Sign in tooAzure</span></span> 

<span data-ttu-id="058b9-138">Oturum açma tooyour hello Azure aboneliğinizle [az oturum açma](/cli/azure/#login) komutu.</span><span class="sxs-lookup"><span data-stu-id="058b9-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="058b9-139">Ardından hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="058b9-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="058b9-140">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="058b9-140">Create a resource group</span></span>

<span data-ttu-id="058b9-141">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="058b9-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="058b9-142">Bir Azure kaynak grubu bir mantıksal hangi Azure kaynaklarını dağıtılan içine ve hangi bunlar yönetilebilir bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="058b9-143">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="058b9-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="058b9-144">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="058b9-144">Create an availability set</span></span>

<span data-ttu-id="058b9-145">adımı aşağıdaki hello isteğe bağlıdır ancak önerilir.</span><span class="sxs-lookup"><span data-stu-id="058b9-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="058b9-146">Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="058b9-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="058b9-147">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="058b9-147">Create a virtual machine</span></span>

<span data-ttu-id="058b9-148">Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="058b9-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="058b9-149">Merhaba aşağıdaki örnek adlı iki VM'ler oluşturur `myVM1` ve `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="058b9-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="058b9-150">Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="058b9-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="058b9-151">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="058b9-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="058b9-152">MyVM1 (birincil) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="058b9-153">Hello VM oluşturulduktan sonra aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir.</span><span class="sxs-lookup"><span data-stu-id="058b9-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="058b9-154">(Merhaba not edin `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="058b9-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="058b9-155">Bu kullanılan tooaccess hello VM adresidir.)</span><span class="sxs-lookup"><span data-stu-id="058b9-155">This address is used tooaccess hello VM.)</span></span>

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="058b9-156">MyVM2 oluşturun (Çoğaltma):</span><span class="sxs-lookup"><span data-stu-id="058b9-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="058b9-157">Merhaba not edin `publicIpAddress` de oluşturulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="058b9-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="058b9-158">Bağlantı için Hello TCP bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="058b9-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="058b9-159">Merhaba sonraki tooaccess hello Oracle veritabanı'ı uzaktan etkinleştirme tooconfigure dış uç adımdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="058b9-160">tooconfigure dış uç noktalar Merhaba, hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="058b9-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="058b9-161">MyVM1 açık hello bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="058b9-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="058b9-162">Merhaba sonuçları benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="058b9-162">hello results should look similar toohello following response:</span></span>

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="058b9-163">MyVM2 açık hello bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="058b9-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="058b9-164">Toohello sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="058b9-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="058b9-165">Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu.</span><span class="sxs-lookup"><span data-stu-id="058b9-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="058b9-166">Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makinenizin.</span><span class="sxs-lookup"><span data-stu-id="058b9-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="058b9-167">Merhaba veritabanı üzerinde myVM1 (birincil) oluşturma</span><span class="sxs-lookup"><span data-stu-id="058b9-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="058b9-168">Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="058b9-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="058b9-169">Merhaba yazılım hello 'oracle' süper kullanıcı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="058b9-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="058b9-170">Merhaba veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-170">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="058b9-171">Çıkış benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="058b9-171">Outputs should look similar toohello following response:</span></span>

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="058b9-172">Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="058b9-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="058b9-173">İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar gelecekteki oturum açma işlemleri için kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="058b9-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="058b9-174">Oracle dinleyicisini başlatmak</span><span class="sxs-lookup"><span data-stu-id="058b9-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="058b9-175">Merhaba veritabanı üzerinde myVM2 oluşturun (Çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="058b9-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="058b9-176">Merhaba veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-176">Create hello database:</span></span>

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
<span data-ttu-id="058b9-177">Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="058b9-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="058b9-178">İsteğe bağlı olarak, böylece bu ayarlar gelecekteki oturum açma işlemleri için kaydedilir eklenen ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="058b9-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="058b9-179">Oracle dinleyicisini başlatmak</span><span class="sxs-lookup"><span data-stu-id="058b9-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="058b9-180">Golden kapısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="058b9-180">Configure Golden Gate</span></span> 
<span data-ttu-id="058b9-181">Bu bölümde hello adımları uygulamanız tooconfigure Golden kapısı.</span><span class="sxs-lookup"><span data-stu-id="058b9-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="058b9-182">MyVM1 (birincil) arşiv günlük modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="058b9-182">Enable archive log mode on myVM1 (primary)</span></span>

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
<span data-ttu-id="058b9-183">Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="058b9-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="058b9-184">Golden kapısı yazılımları indirme</span><span class="sxs-lookup"><span data-stu-id="058b9-184">Download Golden Gate software</span></span>
<span data-ttu-id="058b9-185">toodownload ve hello Oracle Golden kapısı yazılım, aşağıdaki adımları tam hello hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="058b9-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="058b9-186">Merhaba karşıdan **fbo_ggs_Linux_x64_shiphome.zip** hello dosyasından [Oracle Golden kapısı indirme sayfası](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="058b9-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="058b9-187">Başlık altında Hello karşıdan **Oracle Linux x86-64 için Oracle GoldenGate 12.x.x.x**, .zip dosyalarını toodownload bir dizi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="058b9-188">Merhaba .zip dosyaları tooyour istemci bilgisayara indirdikten sonra güvenli kopyalama Protokolü (SCP) toocopy hello dosyaları tooyour VM kullanın:</span><span class="sxs-lookup"><span data-stu-id="058b9-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="058b9-189">Merhaba .zip dosyalarını toohello taşıma **/ opt** klasör.</span><span class="sxs-lookup"><span data-stu-id="058b9-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="058b9-190">Hello sahibi hello dosyaları, aşağıda gösterildiği gibi değiştirmek:</span><span class="sxs-lookup"><span data-stu-id="058b9-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="058b9-191">(Yükleme hello Linux sıkıştırmasını yardımcı programı henüz yüklü değilse) hello dosyaları sıkıştırmasını açın:</span><span class="sxs-lookup"><span data-stu-id="058b9-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="058b9-192">Değiştirme izni:</span><span class="sxs-lookup"><span data-stu-id="058b9-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="058b9-193">Merhaba istemci ve VM toorun x11 (yalnızca Windows istemcileri için) hazırlama</span><span class="sxs-lookup"><span data-stu-id="058b9-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="058b9-194">Bu isteğe bağlı bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-194">This is an optional step.</span></span> <span data-ttu-id="058b9-195">Bir Linux istemcisi kullanarak veya x11 zaten varsa bu adımı atlayabilirsiniz kurulumu.</span><span class="sxs-lookup"><span data-stu-id="058b9-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="058b9-196">PuTTY ve Xming tooyour Windows bilgisayarda indirin:</span><span class="sxs-lookup"><span data-stu-id="058b9-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="058b9-197">PuTTY indirin</span><span class="sxs-lookup"><span data-stu-id="058b9-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="058b9-198">Xming indirin</span><span class="sxs-lookup"><span data-stu-id="058b9-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="058b9-199">PuTTY yükledikten sonra PuTTY klasörünü (örneğin, C:\Program Files\PuTTY) Merhaba, puttygen.exe (PuTTY anahtar Oluşturucu) çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="058b9-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="058b9-200">PuTTY anahtar oluşturma Aracı'nda:</span><span class="sxs-lookup"><span data-stu-id="058b9-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="058b9-201">toogenerate anahtar, select hello **Generate** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="058b9-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="058b9-202">Başlangıç anahtarı Hello içeriğini kopyalayın (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="058b9-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="058b9-203">Select hello **özel anahtarı Kaydet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="058b9-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="058b9-204">Görünür ve ardından hello uyarıyı göz ardı **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="058b9-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Merhaba PuTTY anahtarı Oluşturucu sayfasının ekran görüntüsü](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="058b9-206">VM'nizi, şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="058b9-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="058b9-207">Adlı bir dosya oluşturun **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="058b9-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="058b9-208">Bu dosyada hello anahtar Hello içeriğini yapıştırın ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="058b9-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="058b9-209">başlangıç anahtarı hello dize içermelidir `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="058b9-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="058b9-210">Ayrıca, başlangıç anahtarı Merhaba içeriğine tek satırlık metin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="058b9-211">PuTTY’yi başlatın.</span><span class="sxs-lookup"><span data-stu-id="058b9-211">Start PuTTY.</span></span> <span data-ttu-id="058b9-212">Merhaba, **kategori** bölmesinde, **bağlantı** > **SSH** > **Auth**. Merhaba, **kimlik doğrulama için özel anahtar dosyası** kutusunda, daha önce oluşturulan toohello anahtarı göz atın.</span><span class="sxs-lookup"><span data-stu-id="058b9-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Merhaba özel anahtarı ayarlama sayfasının ekran görüntüsü](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="058b9-214">Merhaba, **kategori** bölmesinde, **bağlantı** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="058b9-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="058b9-215">Merhaba seçip **X11 Enable iletimi** kutusu.</span><span class="sxs-lookup"><span data-stu-id="058b9-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Merhaba etkinleştir X11 sayfasının ekran görüntüsü](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="058b9-217">Merhaba, **kategori** bölmesinde çok Git**oturum**.</span><span class="sxs-lookup"><span data-stu-id="058b9-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="058b9-218">Merhaba ana bilgisayar bilgilerini girin ve ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="058b9-218">Enter hello host information, and then select **Open**.</span></span>

  ![Merhaba oturum sayfasının ekran görüntüsü](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="058b9-220">Golden kapısı yazılımı yükleyin</span><span class="sxs-lookup"><span data-stu-id="058b9-220">Install Golden Gate software</span></span>

<span data-ttu-id="058b9-221">tooinstall Oracle Golden ağ geçidi, şu adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="058b9-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="058b9-222">Oracle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="058b9-222">Sign in as oracle.</span></span> <span data-ttu-id="058b9-223">(İçin bir parola istenmesini olmadan mümkün toosign olmalıdır.) Merhaba yüklemeye başlamadan önce Xming çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="058b9-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="058b9-224">'Oracle veritabanı 12 c için Oracle GoldenGate' seçin.</span><span class="sxs-lookup"><span data-stu-id="058b9-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="058b9-225">Ardından **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="058b9-225">Then select **Next** toocontinue.</span></span>

  ![Merhaba yükleyici seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="058b9-227">Merhaba yazılım konumunu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="058b9-227">Change hello software location.</span></span> <span data-ttu-id="058b9-228">Merhaba seçip **Yöneticisi'ni başlatın** kutusunda ve hello veritabanı konumu girin.</span><span class="sxs-lookup"><span data-stu-id="058b9-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="058b9-229">Seçin **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="058b9-229">Select **Next** toocontinue.</span></span>

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="058b9-231">Hello stok dizini değiştirin ve ardından **sonraki** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="058b9-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="058b9-233">Merhaba üzerinde **Özet** ekran, select **yükleme** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="058b9-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Merhaba yükleyici seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="058b9-235">İstendiğinde toorun bir komut dosyası 'kök olarak' olabilir.</span><span class="sxs-lookup"><span data-stu-id="058b9-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="058b9-236">Bu durumda, ayrı bir oturum ssh toohello VM, sudo tooroot açın ve hello betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="058b9-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="058b9-237">Seçin **Tamam** devam edin.</span><span class="sxs-lookup"><span data-stu-id="058b9-237">Select **OK** continue.</span></span>

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="058b9-239">Merhaba yükleme tamamlandığında seçin **Kapat** toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="058b9-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="058b9-241">MyVM1 hizmette (birincil) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="058b9-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="058b9-242">Oluşturma veya hello tnsnames.ora dosyasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="058b9-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="058b9-243">Merhaba Golden kapısı sahip ve kullanıcı hesapları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="058b9-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="058b9-244">Merhaba sahip hesabı C ## önekine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="058b9-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="058b9-245">Merhaba Golden kapısı test kullanıcı hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="058b9-246">Merhaba extract parametre dosyası yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="058b9-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="058b9-247">Merhaba altın kapısı komut satırı arabirimi (ggsci) başlatın:</span><span class="sxs-lookup"><span data-stu-id="058b9-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="058b9-248">Merhaba (VI komutlarını kullanarak) aşağıdaki toohello EXTRACT parametre dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="058b9-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="058b9-249">Esc tuşuna basın, ': wq!'</span><span class="sxs-lookup"><span data-stu-id="058b9-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="058b9-250">toosave dosyası.</span><span class="sxs-lookup"><span data-stu-id="058b9-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="058b9-251">YAZMAÇ ayıklayın--tümleşik Ayıkla:</span><span class="sxs-lookup"><span data-stu-id="058b9-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="058b9-252">Extract denetim noktaları ayarlama ve gerçek zamanlı extract başlatın:</span><span class="sxs-lookup"><span data-stu-id="058b9-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="058b9-253">Bu adımda, daha sonra farklı bir bölümde kullanılacak SCN başlangıç hello bulur:</span><span class="sxs-lookup"><span data-stu-id="058b9-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="058b9-254">MyVM2 hizmette ayarlayın (Çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="058b9-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="058b9-255">Oluşturma veya hello tnsnames.ora dosyasını güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="058b9-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="058b9-256">Bir çoğaltma hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="058b9-257">Bir Golden kapısı test kullanıcı hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="058b9-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="058b9-258">REPLICAT parametre dosyası tooreplicate değişiklikler:</span><span class="sxs-lookup"><span data-stu-id="058b9-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="058b9-259">REPORA parametresi dosyasının içeriği:</span><span class="sxs-lookup"><span data-stu-id="058b9-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="058b9-260">Replicat denetim noktası ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="058b9-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="058b9-261">(MyVM1 ve myVM2) Hello çoğaltmayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="058b9-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="058b9-262">1. MyVM2 hello çoğaltmayı ayarlayın (Çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="058b9-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="058b9-263">Merhaba dosyasını hello aşağıdakilerle güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="058b9-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="058b9-264">Hello Yöneticisi hizmetini durdurup yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="058b9-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="058b9-265">2. MyVM1 hello çoğaltmayı (birincil) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="058b9-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="058b9-266">Merhaba ilk yükleme ve hatalar için onay başlatın:</span><span class="sxs-lookup"><span data-stu-id="058b9-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="058b9-267">3. MyVM2 hello çoğaltmayı ayarlayın (Çoğaltma)</span><span class="sxs-lookup"><span data-stu-id="058b9-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="058b9-268">Önce aldığınız hello hello numarası SCN numarasıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="058b9-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="058b9-269">Merhaba çoğaltma başladıktan ve yeni kayıtlar tooTEST tablolar ekleyerek test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="058b9-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="058b9-270">İş durumunu görüntüleme ve sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="058b9-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="058b9-271">Raporları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="058b9-271">View reports</span></span>
<span data-ttu-id="058b9-272">tooview hello aşağıdaki komutları çalıştırın myVM1 üzerinde raporları:</span><span class="sxs-lookup"><span data-stu-id="058b9-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="058b9-273">tooview hello aşağıdaki komutları çalıştırın myVM2 üzerinde raporları:</span><span class="sxs-lookup"><span data-stu-id="058b9-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="058b9-274">Görünüm durumu ve geçmişi</span><span class="sxs-lookup"><span data-stu-id="058b9-274">View status and history</span></span>
<span data-ttu-id="058b9-275">tooview durumunu ve geçmişini myVM1, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="058b9-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="058b9-276">tooview durumunu ve geçmişini myVM2, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="058b9-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="058b9-277">Bu, hello yükleme ve Oracle linux üzerinde Golden kapısı yapılandırmasını tamamlar.</span><span class="sxs-lookup"><span data-stu-id="058b9-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="058b9-278">Merhaba sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="058b9-278">Delete hello virtual machine</span></span>

<span data-ttu-id="058b9-279">Artık gerekli olmadığında, komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="058b9-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="058b9-280">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="058b9-280">Next steps</span></span>

[<span data-ttu-id="058b9-281">Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi</span><span class="sxs-lookup"><span data-stu-id="058b9-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="058b9-282">VM dağıtımı CLI örneklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="058b9-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
