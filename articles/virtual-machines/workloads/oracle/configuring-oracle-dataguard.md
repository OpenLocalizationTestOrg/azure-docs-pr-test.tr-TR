---
title: aaaImplement Oracle Data Guard Azure Linux VM'de | Microsoft Docs
description: "Hızla bir Oracle Data Guard yukarı ve Azure ortamınızda çalışan alın."
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="5f4d2-103">Azure Linux VM'de Oracle veri koruma uygulama</span><span class="sxs-lookup"><span data-stu-id="5f4d2-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="5f4d2-104">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="5f4d2-105">Hello Azure CLI toodeploy bir Oracle hello Market galeri görüntüsü 12 C'den veritabanı kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="5f4d2-106">Merhaba Oracle veritabanı oluşturulduktan sonra bu belgede, gösterir adım adım nasıl tooinstall ve veri koruma Azure VM yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="5f4d2-107">Başlamadan önce Azure CLI yüklenmiş bu hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="5f4d2-108">Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5f4d2-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="5f4d2-109">Merhaba ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="5f4d2-110">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="5f4d2-110">Assumptions</span></span>

<span data-ttu-id="5f4d2-111">tooperform hello, Oracle Data Guard yüklemek ihtiyacınız hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="5f4d2-112">Merhaba Market görüntü toocreate hello VM'ler kullandığınız "Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="5f4d2-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="5f4d2-113">Merhaba birincil VM (myVM1) çalışan bir Oracle örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="5f4d2-114">Merhaba hello Oracle yazılımı yalnızca yüklü bekleme VM (myVM2) sahip.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5f4d2-115">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="5f4d2-115">Log in tooAzure</span></span> 

<span data-ttu-id="5f4d2-116">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="5f4d2-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-117">Create a resource group</span></span>

<span data-ttu-id="5f4d2-118">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5f4d2-119">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="5f4d2-120">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="5f4d2-121">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-121">Create availability set</span></span>

<span data-ttu-id="5f4d2-122">Bu adım isteğe bağlıdır ancak önerilir.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="5f4d2-123">bkz: [Azure kullanılabilirlik kümeleri Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="5f4d2-124">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-124">Create virtual machine</span></span>

<span data-ttu-id="5f4d2-125">Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="5f4d2-126">Merhaba aşağıdaki örnek adlı 2 VM'ler oluşturur `myVM1` ve `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="5f4d2-127">Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="5f4d2-128">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="5f4d2-129">MyVM1 (birincil) oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-129">Create myVM1 (primary)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="5f4d2-130">VM oluşturulan hello, bir örnek aşağıdaki bilgileri benzer toohello hello Azure CLI kez gösterir: hello Al Not `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="5f4d2-131">Kullanılan tooaccess hello VM adresidir.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="5f4d2-132">MyVM2 oluşturun (bekleme)</span><span class="sxs-lookup"><span data-stu-id="5f4d2-132">Create myVM2 (standby)</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="5f4d2-133">Merhaba not edin `publicIpAddress` oluşturulduktan sonra da.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="5f4d2-134">Bağlantı için Hello TCP bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="5f4d2-135">Hello adım tooconfigure dış uç noktalar, Oracle DB hello uzaktan erişmesini sağlayan, hello aşağıdaki komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="5f4d2-136">MyVM1 için açık bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="5f4d2-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="5f4d2-137">Sonuç benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5f4d2-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="5f4d2-138">MyVM2 için açık bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="5f4d2-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="5f4d2-139">Toovirtual makineyi bağlayın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-139">Connect toovirtual machine</span></span>

<span data-ttu-id="5f4d2-140">Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="5f4d2-141">Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makinenizin.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="5f4d2-142">MyVM1 üzerinde veritabanı oluşturma (birincil)</span><span class="sxs-lookup"><span data-stu-id="5f4d2-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="5f4d2-143">Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="5f4d2-144">Merhaba ilk adımı hello 'oracle' süper kullanıcı çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="5f4d2-145">Merhaba veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="5f4d2-145">create hello database:</span></span>

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
<span data-ttu-id="5f4d2-146">Çıkış benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="5f4d2-146">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="5f4d2-147">Merhaba ORACLE_SID ve ORACLE_HOME değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="5f4d2-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="5f4d2-148">İsteğe bağlı olarak, böylece bu ayarlar sonraki oturumlar için kaydedilir eklenen ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="5f4d2-149">Veri koruma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="5f4d2-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="5f4d2-150">MyVM1 (birincil) arşiv günlük modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="5f4d2-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="5f4d2-151">Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="5f4d2-152">Bekleme Yinele günlükleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="5f4d2-153">(Hangi hello kurtarma çok daha önce yaptığınız) Flashback açın ve STANDBY_FILE_MANAGEMENT tooauto ayarlayın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="5f4d2-154">MyVM1 (birincil) üzerinde hizmeti Kurulumu</span><span class="sxs-lookup"><span data-stu-id="5f4d2-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="5f4d2-155">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello tnsnames.ora dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5f4d2-156">Girdileri aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-156">Add hello following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="5f4d2-157">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello listener.ora dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5f4d2-158">Girdileri aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-158">Add hello following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="5f4d2-159">Merhaba dinleyicisini başlatmak</span><span class="sxs-lookup"><span data-stu-id="5f4d2-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="5f4d2-160">Hizmeti Kurulumu myVM2 üzerinde (bekleme)</span><span class="sxs-lookup"><span data-stu-id="5f4d2-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="5f4d2-161">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello tnsnames.ora dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5f4d2-162">Girdileri aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-162">Add hello following entries</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="5f4d2-163">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello listener.ora dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="5f4d2-164">Girdileri aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-164">Add hello following entries</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="5f4d2-165">Merhaba dinleyicisini başlatmak</span><span class="sxs-lookup"><span data-stu-id="5f4d2-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="5f4d2-166">Veri koruma Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="5f4d2-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="5f4d2-167">Veritabanı toomyVM2 geri yükleme (bekleme)</span><span class="sxs-lookup"><span data-stu-id="5f4d2-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="5f4d2-168">Bir parametre dosyası oluştur ' / tmp/initcdb1_stby.ora' hello aşağıdakilere içeriğiyle</span><span class="sxs-lookup"><span data-stu-id="5f4d2-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="5f4d2-169">Klasör Oluştur</span><span class="sxs-lookup"><span data-stu-id="5f4d2-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="5f4d2-170">Parola dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="5f4d2-171">Veritabanı myVM2 üzerinde Başlat</span><span class="sxs-lookup"><span data-stu-id="5f4d2-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="5f4d2-172">RMAN yardımcı programını kullanarak veritabanını geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="5f4d2-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="5f4d2-173">RMAN komutlarda aşağıdaki hello yürütme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="5f4d2-174">Veri koruma Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="5f4d2-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="5f4d2-175">Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5f4d2-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="5f4d2-176">Merhaba veri koruma Yöneticisi'ni ve oturum açma SYS ve parolası (OS kimlik doğrulaması kullanmayan yapın) kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="5f4d2-177">Merhaba aşağıdakilere gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="5f4d2-177">Perform hello followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="5f4d2-178">Merhaba yapılandırmayı gözden geçir</span><span class="sxs-lookup"><span data-stu-id="5f4d2-178">Review hello configuration</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="5f4d2-179">Merhaba Oracle Data Guard Kurulum tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="5f4d2-180">Merhaba sonraki bölümde, nasıl tootest hello bağlantısı ve geçişi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="5f4d2-181">İstemci makineden veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-181">Connect database from client machine</span></span>

<span data-ttu-id="5f4d2-182">Güncelleştirme veya genellikle $ORACLE_HOME\network\admin bulunur, istemci makinenizde hello tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="5f4d2-183">Merhaba IP ile değiştirmek, `publicIpAddress` myVM1 ve myVM2 için</span><span class="sxs-lookup"><span data-stu-id="5f4d2-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="5f4d2-184">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="5f4d2-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="5f4d2-185">Test veri koruma yapılandırması</span><span class="sxs-lookup"><span data-stu-id="5f4d2-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="5f4d2-186">Veritabanı geçiş myVM1 (birincil) üzerinde</span><span class="sxs-lookup"><span data-stu-id="5f4d2-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="5f4d2-187">Birincil toostandby (cdb1 toocdb1_stby) gelen tooswitch</span><span class="sxs-lookup"><span data-stu-id="5f4d2-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="5f4d2-188">Artık mümkün tooconnect toohello bekleme veritabanı olmalıdır</span><span class="sxs-lookup"><span data-stu-id="5f4d2-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="5f4d2-189">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="5f4d2-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="5f4d2-190">Veritabanı anahtarda geri myVM2 (bekleme)</span><span class="sxs-lookup"><span data-stu-id="5f4d2-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="5f4d2-191">geri tooswitch üzerinde myVM2 hello aşağıdakilere çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5f4d2-191">tooswitch back, run hello followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="5f4d2-192">Bir kez daha, artık mümkün tooconnect toohello birincil veritabanı olması gerekir</span><span class="sxs-lookup"><span data-stu-id="5f4d2-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="5f4d2-193">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="5f4d2-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="5f4d2-194">Bu hello yüklemesi ve Oracle linux üzerinde veri koruma yapılandırması tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="5f4d2-195">Sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="5f4d2-195">Delete virtual machine</span></span>

<span data-ttu-id="5f4d2-196">Artık gerekli olduğunda, komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, VM olabilir ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5f4d2-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="5f4d2-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f4d2-197">Next steps</span></span>

[<span data-ttu-id="5f4d2-198">Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi</span><span class="sxs-lookup"><span data-stu-id="5f4d2-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="5f4d2-199">VM dağıtımı CLI örneklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="5f4d2-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
