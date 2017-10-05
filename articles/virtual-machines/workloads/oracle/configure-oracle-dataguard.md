---
title: Bir Azure Linux sanal makinede Oracle Data Guard uygulamak | Microsoft Docs
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
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="38874-103">Bir Azure Linux sanal makinede Oracle veri koruma uygulama</span><span class="sxs-lookup"><span data-stu-id="38874-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="38874-104">Azure CLI oluşturmak ve komut satırından veya komut dosyalarında Azure kaynaklarınızı yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="38874-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="38874-105">Bu makalede, Azure Market görüntüsünden bir Oracle veritabanına 12 c veritabanını dağıtmak için Azure CLI kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="38874-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="38874-106">Bu makalede daha sonra adım adım gösterilmektedir nasıl yüklenir ve veri koruma Azure sanal makine (VM) yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="38874-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="38874-107">Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="38874-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="38874-108">Daha fazla bilgi için bkz: [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38874-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="38874-109">Ortamı hazırlama</span><span class="sxs-lookup"><span data-stu-id="38874-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="38874-110">Varsayımlar</span><span class="sxs-lookup"><span data-stu-id="38874-110">Assumptions</span></span>

<span data-ttu-id="38874-111">Oracle Data Guard yüklemek için aynı kullanılabilirlik kümesinde iki Azure sanal makineleri oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="38874-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="38874-112">Birincil VM (myVM1) çalışan bir Oracle örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="38874-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="38874-113">Bekleme yalnızca yüklü olan Oracle yazılım VM (myVM2) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="38874-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="38874-114">Oracle: Oracle VM oluşturmak için kullandığınız Market görüntüdür-veritabanı-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="38874-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="38874-115">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="38874-115">Sign in to Azure</span></span> 

<span data-ttu-id="38874-116">Azure aboneliğinizi kullanarak oturum [az oturum açma](/cli/azure/#login) komut ve izleyin ekrandaki yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="38874-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="38874-117">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="38874-117">Create a resource group</span></span>

<span data-ttu-id="38874-118">Kullanarak bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="38874-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="38874-119">Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="38874-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="38874-120">Aşağıdaki örnek, bir kaynak grubu oluşturur `myResourceGroup` içinde `westus` konumu:</span><span class="sxs-lookup"><span data-stu-id="38874-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="38874-121">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="38874-121">Create an availability set</span></span>

<span data-ttu-id="38874-122">Bir kullanılabilirlik kümesi oluşturmak isteğe bağlıdır, ancak kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="38874-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="38874-123">Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri yönergeleri](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="38874-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="38874-124">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="38874-124">Create a virtual machine</span></span>

<span data-ttu-id="38874-125">Kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="38874-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="38874-126">Aşağıdaki örnek adlı iki VM'ler oluşturur `myVM1` ve `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="38874-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="38874-127">Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="38874-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="38874-128">Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="38874-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="38874-129">MyVM1 (birincil) oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38874-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="38874-130">VM oluşturduktan sonra Azure CLI bilgileri aşağıdaki örneğe benzer şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="38874-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="38874-131">Değeri Not `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="38874-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="38874-132">VM erişmek için bu adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="38874-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="38874-133">MyVM2 oluşturun (bekleme):</span><span class="sxs-lookup"><span data-stu-id="38874-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="38874-134">Değeri Not `publicIpAddress` myVM2 oluşturduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="38874-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="38874-135">Bağlantı için TCP bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="38874-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="38874-136">Bu adım, Oracle veritabanı uzaktan erişime izin vermek dış uç noktalar yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="38874-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="38874-137">MyVM1 için bağlantı noktası açın:</span><span class="sxs-lookup"><span data-stu-id="38874-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="38874-138">Sonuç aşağıdaki yanıta benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="38874-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="38874-139">MyVM2 için bağlantı noktası açın:</span><span class="sxs-lookup"><span data-stu-id="38874-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="38874-140">Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="38874-140">Connect to the virtual machine</span></span>

<span data-ttu-id="38874-141">Sanal makine ile bir SSH oturumu oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="38874-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="38874-142">IP adresiyle değiştirin `publicIpAddress` sanal makineniz için değer.</span><span class="sxs-lookup"><span data-stu-id="38874-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="38874-143">Veritabanı üzerinde myVM1 (birincil) oluşturma</span><span class="sxs-lookup"><span data-stu-id="38874-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="38874-144">Veritabanını yüklemek için sonraki adım olacak şekilde Oracle yazılım Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="38874-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="38874-145">Oracle süper kullanıcı için anahtarı:</span><span class="sxs-lookup"><span data-stu-id="38874-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="38874-146">Veritabanı oluştur:</span><span class="sxs-lookup"><span data-stu-id="38874-146">Create the database:</span></span>

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
<span data-ttu-id="38874-147">Çıktı aşağıdaki yanıta benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="38874-147">Outputs should look similar to the following response:</span></span>

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

<span data-ttu-id="38874-148">ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="38874-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="38874-149">İsteğe bağlı olarak, böylece bu ayarlar sonraki oturumlar için kaydedilir /home/oracle/.bashrc dosyasına ORACLE_HOME ve ORACLE_SID ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38874-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="38874-150">Veri koruma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="38874-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="38874-151">MyVM1 (birincil) arşiv günlük modunu etkinleştir</span><span class="sxs-lookup"><span data-stu-id="38874-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="38874-152">Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="38874-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="38874-153">Bekleme Yinele günlükleri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38874-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="38874-154">(Kurtarma çok daha kolay hale getiren) Flashback açın ve bekleme ayarlayın\_dosya\_otomatik olarak yönetim.</span><span class="sxs-lookup"><span data-stu-id="38874-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="38874-155">Exit SQL * Plus bundan sonra.</span><span class="sxs-lookup"><span data-stu-id="38874-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="38874-156">MyVM1 hizmette (birincil) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="38874-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="38874-157">Düzenleyin veya $ORACLE_HOME\network\admin klasöründedir tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38874-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="38874-158">Aşağıdaki girdileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="38874-158">Add the following entries:</span></span>

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

<span data-ttu-id="38874-159">Düzenleyin veya $ORACLE_HOME\network\admin klasöründedir listener.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38874-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="38874-160">Aşağıdaki girdileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="38874-160">Add the following entries:</span></span>

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

<span data-ttu-id="38874-161">Veri koruma Aracısı'nı etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="38874-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="38874-162">Dinleyici başlatın:</span><span class="sxs-lookup"><span data-stu-id="38874-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="38874-163">MyVM2 hizmette ayarlayın (bekleme)</span><span class="sxs-lookup"><span data-stu-id="38874-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="38874-164">SSH myVM2 için:</span><span class="sxs-lookup"><span data-stu-id="38874-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="38874-165">Oracle oturum açın:</span><span class="sxs-lookup"><span data-stu-id="38874-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="38874-166">Düzenleyin veya $ORACLE_HOME\network\admin klasöründedir tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38874-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="38874-167">Aşağıdaki girdileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="38874-167">Add the following entries:</span></span>

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

<span data-ttu-id="38874-168">Düzenleyin veya $ORACLE_HOME\network\admin klasöründedir listener.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38874-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="38874-169">Aşağıdaki girdileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="38874-169">Add the following entries:</span></span>

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

<span data-ttu-id="38874-170">Dinleyici başlatın:</span><span class="sxs-lookup"><span data-stu-id="38874-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="38874-171">Veritabanını geri yüklemek için myVM2 (bekleme)</span><span class="sxs-lookup"><span data-stu-id="38874-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="38874-172">Parametre dosyası /tmp/initcdb1_stby.ora aşağıdaki içeriğe sahip oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38874-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="38874-173">Klasör Oluştur:</span><span class="sxs-lookup"><span data-stu-id="38874-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="38874-174">Bir parola dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="38874-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="38874-175">Veritabanı üzerinde myVM2 başlatın:</span><span class="sxs-lookup"><span data-stu-id="38874-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="38874-176">RMAN aracını kullanarak veritabanını geri yükleyin:</span><span class="sxs-lookup"><span data-stu-id="38874-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="38874-177">İçinde RMAN aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="38874-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="38874-178">Komut tamamlandığında, aşağıdakine benzer iletiler görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="38874-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="38874-179">RMAN çıkın.</span><span class="sxs-lookup"><span data-stu-id="38874-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="38874-180">İsteğe bağlı olarak, böylece bu ayarlar sonraki oturumlar için kaydedilir /home/oracle/.bashrc dosyasına ORACLE_HOME ve ORACLE_SID ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38874-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="38874-181">Veri koruma Aracısı'nı etkinleştirin:</span><span class="sxs-lookup"><span data-stu-id="38874-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="38874-182">Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma</span><span class="sxs-lookup"><span data-stu-id="38874-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="38874-183">Veri Koruma Yöneticisi'ni başlatın ve SYS ve parola kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="38874-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="38874-184">(İşletim sistemi kimlik doğrulamasını kullanmayın.) Aşağıdakileri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="38874-184">(Do not use OS authentication.) Perform the following:</span></span>

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

<span data-ttu-id="38874-185">Yapılandırmasını gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="38874-185">Review the configuration:</span></span>
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

<span data-ttu-id="38874-186">Oracle Data Guard Kurulum tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="38874-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="38874-187">Sonraki bölümde bağlantısını test etme ve geçebilir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="38874-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="38874-188">İstemci makineden veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="38874-188">Connect the database from the client machine</span></span>

<span data-ttu-id="38874-189">Güncelleştirin veya istemci makinenizde tnsnames.ora dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38874-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="38874-190">Bu genellikle $ORACLE_HOME\network\admin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="38874-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="38874-191">IP adresleriyle değiştirin, `publicIpAddress` myVM1 ve myVM2 değerleri:</span><span class="sxs-lookup"><span data-stu-id="38874-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="38874-192">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="38874-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="38874-193">Veri koruma yapılandırmayı test etme</span><span class="sxs-lookup"><span data-stu-id="38874-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="38874-194">Veritabanında myVM1 (birincil) üzerinden geçiş</span><span class="sxs-lookup"><span data-stu-id="38874-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="38874-195">Birincil bekleme moduna geçmek için (cdb1 cdb1_stby için):</span><span class="sxs-lookup"><span data-stu-id="38874-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

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

<span data-ttu-id="38874-196">Şimdi bekleme veritabanına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="38874-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="38874-197">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="38874-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="38874-198">Veritabanı myVM2 üzerinde üzerinden geçiş (bekleme)</span><span class="sxs-lookup"><span data-stu-id="38874-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="38874-199">Geçmek için myVM2 üzerinde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="38874-199">To switch over, run the following on myVM2:</span></span>
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

<span data-ttu-id="38874-200">Bir kez daha, şimdi birincil veritabanına bağlanabilmek için olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="38874-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="38874-201">Başlangıç SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="38874-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="38874-202">Yükleme ve Oracle Linux üzerinde veri koruma yapılandırmasını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="38874-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="38874-203">Sanal makineyi silin</span><span class="sxs-lookup"><span data-stu-id="38874-203">Delete the virtual machine</span></span>

<span data-ttu-id="38874-204">VM artık ihtiyacınız olduğunda, kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="38874-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="38874-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38874-205">Next steps</span></span>

[<span data-ttu-id="38874-206">Öğretici: yüksek oranda kullanılabilir sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="38874-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="38874-207">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="38874-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)
