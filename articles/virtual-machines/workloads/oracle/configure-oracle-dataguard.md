---
title: "bir Azure Linux sanal makine üzerinde aaaImplement Oracle Data Guard | Microsoft Docs"
description: "Hızlı bir şekilde Oracle Data Guard ve Azure ortamınızda çalışan alın."
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
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="10c10-103">Bir Azure Linux sanal makinede Oracle veri koruma uygulama</span><span class="sxs-lookup"><span data-stu-id="10c10-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="10c10-104">Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="10c10-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="10c10-105">Bu makalede nasıl toouse Azure CLI toodeploy bir Oracle veritabanına 12 c veritabanı hello Azure Market görüntüsünden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="10c10-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="10c10-106">Bu makalede daha sonra adım adım nasıl gösterilmektedir tooinstall ve veri koruma Azure sanal makine (VM) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="10c10-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="10c10-107">Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="10c10-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="10c10-108">Daha fazla bilgi için bkz: Merhaba [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10c10-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="10c10-109">Merhaba ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="10c10-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="10c10-110">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="10c10-110">Assumptions</span></span>

<span data-ttu-id="10c10-111">tooinstall Oracle Data Guard, gereksinim duyduğunuz hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi:</span><span class="sxs-lookup"><span data-stu-id="10c10-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="10c10-112">Merhaba birincil VM (myVM1) çalışan bir Oracle örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="10c10-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="10c10-113">Merhaba hello Oracle yazılımı yalnızca yüklü bekleme VM (myVM2) sahip.</span><span class="sxs-lookup"><span data-stu-id="10c10-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="10c10-114">Merhaba toocreate hello VM'ler kullandığınız Market görüntüsü olan Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="10c10-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="10c10-115">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="10c10-115">Sign in tooAzure</span></span> 

<span data-ttu-id="10c10-116">Tooyour Azure aboneliği hello kullanarak oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="10c10-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="10c10-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c10-117">Create a resource group</span></span>

<span data-ttu-id="10c10-118">Hello kullanarak bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="10c10-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="10c10-119">Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="10c10-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="10c10-120">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:</span><span class="sxs-lookup"><span data-stu-id="10c10-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="10c10-121">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c10-121">Create an availability set</span></span>

<span data-ttu-id="10c10-122">Bir kullanılabilirlik kümesi oluşturmak isteğe bağlıdır, ancak kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="10c10-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="10c10-123">Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri yönergeleri](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="10c10-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="10c10-124">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c10-124">Create a virtual machine</span></span>

<span data-ttu-id="10c10-125">Hello kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="10c10-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="10c10-126">Merhaba aşağıdaki örnek adlı iki VM'ler oluşturur `myVM1` ve `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="10c10-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="10c10-127">Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="10c10-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="10c10-128">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="10c10-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="10c10-129">MyVM1 (birincil) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10c10-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="10c10-130">Merhaba VM oluşturduktan sonra Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="10c10-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="10c10-131">Not hello değerini `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="10c10-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="10c10-132">Bu adres tooaccess hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="10c10-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="10c10-133">MyVM2 oluşturun (bekleme):</span><span class="sxs-lookup"><span data-stu-id="10c10-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="10c10-134">Not hello değerini `publicIpAddress` myVM2 oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="10c10-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="10c10-135">Bağlantı için Hello TCP bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="10c10-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="10c10-136">Bu adım, uzaktan erişim toohello Oracle veritabanı izin dış uç noktalar yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="10c10-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="10c10-137">MyVM1 açık hello bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="10c10-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="10c10-138">Merhaba sonuç benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="10c10-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="10c10-139">MyVM2 açık hello bağlantı noktası:</span><span class="sxs-lookup"><span data-stu-id="10c10-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="10c10-140">Toohello sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="10c10-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="10c10-141">Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu.</span><span class="sxs-lookup"><span data-stu-id="10c10-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="10c10-142">Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makineniz için değer.</span><span class="sxs-lookup"><span data-stu-id="10c10-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="10c10-143">Merhaba veritabanı üzerinde myVM1 (birincil) oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c10-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="10c10-144">Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="10c10-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="10c10-145">Toohello Oracle süper kullanıcı anahtarı:</span><span class="sxs-lookup"><span data-stu-id="10c10-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="10c10-146">Merhaba veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10c10-146">Create hello database:</span></span>

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
<span data-ttu-id="10c10-147">Çıkış benzer toohello yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="10c10-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="10c10-148">Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="10c10-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="10c10-149">İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello /home/oracle/.bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar sonraki oturumlar için kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="10c10-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="10c10-150">Veri koruma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10c10-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="10c10-151">MyVM1 (birincil) arşiv günlük modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="10c10-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="10c10-152">Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="10c10-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="10c10-153">Bekleme Yinele günlükleri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10c10-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="10c10-154">(Kurtarma çok daha kolay hale getiren) Flashback açın ve bekleme ayarlayın\_dosya\_yönetim tooauto.</span><span class="sxs-lookup"><span data-stu-id="10c10-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="10c10-155">Exit SQL * Plus bundan sonra.</span><span class="sxs-lookup"><span data-stu-id="10c10-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="10c10-156">MyVM1 hizmette (birincil) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="10c10-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="10c10-157">Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10c10-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10c10-158">Girdileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="10c10-158">Add hello following entries:</span></span>

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

<span data-ttu-id="10c10-159">Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello listener.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10c10-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10c10-160">Girdileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="10c10-160">Add hello following entries:</span></span>

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

<span data-ttu-id="10c10-161">Veri koruma Aracısı'nı etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="10c10-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="10c10-162">Merhaba dinleyicisi başlatın:</span><span class="sxs-lookup"><span data-stu-id="10c10-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="10c10-163">MyVM2 hizmette ayarlayın (bekleme)</span><span class="sxs-lookup"><span data-stu-id="10c10-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="10c10-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="10c10-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="10c10-165">Oracle oturum açın:</span><span class="sxs-lookup"><span data-stu-id="10c10-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="10c10-166">Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10c10-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10c10-167">Girdileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="10c10-167">Add hello following entries:</span></span>

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

<span data-ttu-id="10c10-168">Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello listener.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10c10-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="10c10-169">Girdileri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="10c10-169">Add hello following entries:</span></span>

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

<span data-ttu-id="10c10-170">Merhaba dinleyicisi başlatın:</span><span class="sxs-lookup"><span data-stu-id="10c10-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="10c10-171">Merhaba veritabanı toomyVM2 geri yükleme (bekleme)</span><span class="sxs-lookup"><span data-stu-id="10c10-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="10c10-172">Merhaba parametre dosyası /tmp/initcdb1_stby.ora içeriği aşağıdaki hello ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10c10-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="10c10-173">Klasör Oluştur:</span><span class="sxs-lookup"><span data-stu-id="10c10-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="10c10-174">Bir parola dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="10c10-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="10c10-175">Merhaba veritabanı üzerinde myVM2 başlatın:</span><span class="sxs-lookup"><span data-stu-id="10c10-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="10c10-176">Merhaba veritabanı hello RMAN aracını kullanarak geri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="10c10-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="10c10-177">RMAN komutlarda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="10c10-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="10c10-178">Merhaba komutu tamamlandığında iletileri benzer toohello aşağıdaki görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c10-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="10c10-179">RMAN çıkın.</span><span class="sxs-lookup"><span data-stu-id="10c10-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="10c10-180">İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello /home/oracle/.bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar sonraki oturumlar için kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="10c10-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="10c10-181">Veri koruma Aracısı'nı etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="10c10-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="10c10-182">Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="10c10-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="10c10-183">Veri Koruma Yöneticisi'ni başlatın ve SYS ve parola kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="10c10-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="10c10-184">(İşletim sistemi kimlik doğrulamasını kullanmayın.) Merhaba aşağıdakileri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="10c10-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="10c10-185">Merhaba yapılandırmayı gözden geçir:</span><span class="sxs-lookup"><span data-stu-id="10c10-185">Review hello configuration:</span></span>
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

<span data-ttu-id="10c10-186">Merhaba Oracle Data Guard Kurulum tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="10c10-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="10c10-187">Merhaba sonraki bölümde nasıl tootest bağlantı hello ve geçebilir gösterilir.</span><span class="sxs-lookup"><span data-stu-id="10c10-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="10c10-188">Merhaba istemci makineden Hello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="10c10-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="10c10-189">Güncelleştirin veya istemci makinenizde hello tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="10c10-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="10c10-190">Bu genellikle $ORACLE_HOME\network\admin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="10c10-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="10c10-191">Merhaba IP adresleriyle değiştirin, `publicIpAddress` myVM1 ve myVM2 değerleri:</span><span class="sxs-lookup"><span data-stu-id="10c10-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="10c10-192">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="10c10-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="10c10-193">Test hello veri koruma yapılandırması</span><span class="sxs-lookup"><span data-stu-id="10c10-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="10c10-194">Merhaba veritabanında myVM1 (birincil) üzerinden geçiş</span><span class="sxs-lookup"><span data-stu-id="10c10-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="10c10-195">Birincil toostandby (cdb1 toocdb1_stby) gelen tooswitch:</span><span class="sxs-lookup"><span data-stu-id="10c10-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="10c10-196">Şimdi toohello bekleme veritabanı bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="10c10-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="10c10-197">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="10c10-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="10c10-198">MyVM2 hello veritabanında üzerinden geçiş (bekleme)</span><span class="sxs-lookup"><span data-stu-id="10c10-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="10c10-199">üzerinde tooswitch üzerinde myVM2 hello aşağıdakileri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="10c10-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="10c10-200">Bir kez daha, mümkün tooconnect toohello birincil veritabanı artık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="10c10-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="10c10-201">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="10c10-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="10c10-202">Merhaba yükleme ve Oracle Linux üzerinde veri koruma yapılandırmasını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="10c10-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="10c10-203">Merhaba sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="10c10-203">Delete hello virtual machine</span></span>

<span data-ttu-id="10c10-204">VM artık hello olduğunda komut tooremove hello kaynak grubu, VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="10c10-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="10c10-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="10c10-205">Next steps</span></span>

[<span data-ttu-id="10c10-206">Öğretici: yüksek oranda kullanılabilir sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="10c10-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="10c10-207">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="10c10-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
