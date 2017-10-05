---
title: Oracle Data Guard Azure Linux VM'de uygulamak | Microsoft Docs
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
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="54361-103">Azure Linux VM'de Oracle veri koruma uygulama</span><span class="sxs-lookup"><span data-stu-id="54361-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="54361-104">Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54361-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="54361-105">Bir Oracle Market galeri görüntüsü 12 C'den veritabanı dağıtmak için Azure CLI kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="54361-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="54361-106">Oracle veritabanı oluşturulduktan sonra bu belgede, adım adım yükleme ve veri koruma Azure VM yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="54361-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="54361-107">Başlamadan önce Azure CLI’nin yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54361-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="54361-108">Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="54361-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="54361-109">Ortamı hazırlama</span><span class="sxs-lookup"><span data-stu-id="54361-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="54361-110">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="54361-110">Assumptions</span></span>

<span data-ttu-id="54361-111">Oracle Data Guard yüklemeyi gerçekleştirmek için aynı kullanılabilirlik kümesinde iki Azure sanal makineleri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54361-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="54361-112">Sanal makineleri oluşturmak için kullandığınız Market görüntü "Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="54361-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="54361-113">Birincil VM (myVM1) çalışan bir Oracle örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="54361-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="54361-114">Bekleme yalnızca yüklü olan Oracle yazılım VM (myVM2) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="54361-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="54361-115">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="54361-115">Log in to Azure</span></span> 

<span data-ttu-id="54361-116">[az login](/cli/azure/#login) komutuyla Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="54361-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="54361-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-117">Create a resource group</span></span>

<span data-ttu-id="54361-118">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54361-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="54361-119">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="54361-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="54361-120">Aşağıdaki örnek `westus` konumunda `myResourceGroup` adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54361-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="54361-121">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-121">Create availability set</span></span>

<span data-ttu-id="54361-122">Bu adım isteğe bağlıdır ancak önerilir.</span><span class="sxs-lookup"><span data-stu-id="54361-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="54361-123">bkz: [Azure kullanılabilirlik kümeleri Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="54361-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="54361-124">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-124">Create virtual machine</span></span>

<span data-ttu-id="54361-125">[az vm create](/cli/azure/vm#create) komutuyla bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54361-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="54361-126">Aşağıdaki örnek, 2 VM adlı oluşturur `myVM1` ve `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="54361-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="54361-127">Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="54361-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="54361-128">Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="54361-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="54361-129">MyVM1 (birincil) oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="54361-130">VM oluşturulduktan sonra Azure CLI bilgileri aşağıdaki örneğe benzer şekilde gösterir: Al Not `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="54361-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="54361-131">Bu adres, VM’ye erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54361-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="54361-132">MyVM2 oluşturun (bekleme)</span><span class="sxs-lookup"><span data-stu-id="54361-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="54361-133">Not edin `publicIpAddress` oluşturulduktan sonra da.</span><span class="sxs-lookup"><span data-stu-id="54361-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="54361-134">Bağlantı için TCP bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="54361-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="54361-135">Adım Oracle DB uzaktan erişim sağlayan dış uç noktalar yapılandırmak için aşağıdaki komutu yürütün.</span><span class="sxs-lookup"><span data-stu-id="54361-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="54361-136">MyVM1 için açık bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="54361-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="54361-137">Sonuç aşağıdaki yanıta benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="54361-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="54361-138">MyVM2 için açık bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="54361-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="54361-139">Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="54361-139">Connect to virtual machine</span></span>

<span data-ttu-id="54361-140">Sanal makine ile bir SSH oturumu oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="54361-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="54361-141">IP adresini, sanal makinenizin `publicIpAddress` ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54361-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="54361-142">MyVM1 üzerinde veritabanı oluşturma (birincil)</span><span class="sxs-lookup"><span data-stu-id="54361-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="54361-143">Veritabanını yüklemek için sonraki adım olacak şekilde Oracle yazılım Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="54361-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="54361-144">İlk adım, 'oracle' süper kullanıcı çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="54361-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="54361-145">Veritabanı oluştur:</span><span class="sxs-lookup"><span data-stu-id="54361-145">create the database:</span></span>

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
<span data-ttu-id="54361-146">Çıktı aşağıdaki yanıta benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="54361-146">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="54361-147">ORACLE_SID ve ORACLE_HOME değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="54361-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="54361-148">Böylece bu ayarlar sonraki oturumlar için kaydedilir isteğe bağlı olarak, eklenen ORACLE_HOME ve ORACLE_SID .bashrc dosyasına kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54361-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="54361-149">Veri koruma yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="54361-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="54361-150">MyVM1 (birincil) arşiv günlük modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="54361-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="54361-151">Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54361-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="54361-152">Bekleme Yinele günlükleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="54361-153">(Hangi kurtarma çok daha önce yaptığınız) Flashback açmak ve otomatik olarak STANDBY_FILE_MANAGEMENT ayarlayın</span><span class="sxs-lookup"><span data-stu-id="54361-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="54361-154">MyVM1 (birincil) üzerinde hizmeti Kurulumu</span><span class="sxs-lookup"><span data-stu-id="54361-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="54361-155">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu tnsnames.ora dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="54361-156">Aşağıdaki girdileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="54361-156">Add the following entries</span></span>

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

<span data-ttu-id="54361-157">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu listener.ora dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="54361-158">Aşağıdaki girdileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="54361-158">Add the following entries</span></span>

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

<span data-ttu-id="54361-159">Dinleyici Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="54361-160">Hizmeti Kurulumu myVM2 üzerinde (bekleme)</span><span class="sxs-lookup"><span data-stu-id="54361-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="54361-161">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu tnsnames.ora dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="54361-162">Aşağıdaki girdileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="54361-162">Add the following entries</span></span>

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

<span data-ttu-id="54361-163">Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu listener.ora dosya oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="54361-164">Aşağıdaki girdileri ekleyin</span><span class="sxs-lookup"><span data-stu-id="54361-164">Add the following entries</span></span>

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

<span data-ttu-id="54361-165">Dinleyici Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="54361-166">Veri koruma Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="54361-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="54361-167">Veritabanını geri yüklemek için myVM2 (bekleme)</span><span class="sxs-lookup"><span data-stu-id="54361-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="54361-168">Bir parametre dosyası oluştur ' / tmp/initcdb1_stby.ora' aşağıdakilere içeriğiyle</span><span class="sxs-lookup"><span data-stu-id="54361-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="54361-169">Klasör Oluştur</span><span class="sxs-lookup"><span data-stu-id="54361-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="54361-170">Parola dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="54361-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="54361-171">Veritabanı myVM2 üzerinde Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="54361-172">RMAN yardımcı programını kullanarak veritabanını geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="54361-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="54361-173">İçinde RMAN aşağıdaki komutları yürütün</span><span class="sxs-lookup"><span data-stu-id="54361-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="54361-174">Veri koruma Aracısı'nı etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="54361-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="54361-175">Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="54361-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="54361-176">SYS ve parola (OS kimlik doğrulaması kullanmayan yapın) kullanarak oturum açın ve veri koruma Yöneticisi'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="54361-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="54361-177">Aşağıdakileri gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="54361-177">Perform the followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="54361-178">Yapılandırmasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="54361-178">Review the configuration</span></span>
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

<span data-ttu-id="54361-179">Bu, Oracle Data Guard Kurulum tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="54361-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="54361-180">Sonraki bölümde bağlantısı ve geçişi test etme gösterilir</span><span class="sxs-lookup"><span data-stu-id="54361-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="54361-181">İstemci makineden veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="54361-181">Connect database from client machine</span></span>

<span data-ttu-id="54361-182">Güncelleştirme veya genellikle $ORACLE_HOME\network\admin bulunur, istemci makinenizde tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="54361-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="54361-183">IP ile değiştirmek, `publicIpAddress` myVM1 ve myVM2 için</span><span class="sxs-lookup"><span data-stu-id="54361-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="54361-184">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="54361-185">Test veri koruma yapılandırması</span><span class="sxs-lookup"><span data-stu-id="54361-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="54361-186">Veritabanı geçiş myVM1 (birincil) üzerinde</span><span class="sxs-lookup"><span data-stu-id="54361-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="54361-187">Birincil bekleme moduna geçmek için (cdb1 cdb1_stby için)</span><span class="sxs-lookup"><span data-stu-id="54361-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="54361-188">Artık bekleme veritabanına bağlanabilmek için olması gerekir</span><span class="sxs-lookup"><span data-stu-id="54361-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="54361-189">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="54361-190">Veritabanı anahtarda geri myVM2 (bekleme)</span><span class="sxs-lookup"><span data-stu-id="54361-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="54361-191">Geri geçiş yapmak için aşağıdakilere myVM2 üzerinde çalıştırın</span><span class="sxs-lookup"><span data-stu-id="54361-191">To switch back, run the followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="54361-192">Bir kez daha, şimdi birincil veritabanına bağlanabilmek için olmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="54361-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="54361-193">Sqlplus Başlat</span><span class="sxs-lookup"><span data-stu-id="54361-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="54361-194">Bu, yükleme ve veri koruma yapılandırmasını Oracle linux üzerinde tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="54361-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="54361-195">Sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="54361-195">Delete virtual machine</span></span>

<span data-ttu-id="54361-196">Kaynak Grubu, VM ve tüm ilgili kaynaklar artık gerekli olmadığında aşağıdaki komut kullanılarak kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="54361-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="54361-197">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="54361-197">Next steps</span></span>

[<span data-ttu-id="54361-198">Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi</span><span class="sxs-lookup"><span data-stu-id="54361-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="54361-199">VM dağıtımı CLI örneklerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="54361-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)
