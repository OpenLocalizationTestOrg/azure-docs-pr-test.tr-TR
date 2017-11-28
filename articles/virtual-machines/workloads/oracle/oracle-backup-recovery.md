---
title: "Yedekleme ve kurtarma, Azure Linux sanal makinede bir Oracle veritabanına 12 c veritabanı | Microsoft Docs"
description: "Yedekleme ve Azure ortamınızda bir Oracle veritabanına 12 c veritabanını kurtarma hakkında bilgi edinin."
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
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 9a2293f13b90e9a4cb11b4169fad969dd622a9a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="707c4-103">Yedekleme ve bir Azure Linux sanal makine üzerinde bir Oracle veritabanına 12 c veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="707c4-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="707c4-104">Komut oluşturma veya bir komut isteminden Azure kaynaklarınızı yönetmek için Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="707c4-104">You can use Azure CLI to create and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="707c4-105">Bu makalede, Azure Marketi galeri görüntünün bir Oracle veritabanına 12 c veritabanından dağıtmak için Azure CLI betiklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="707c4-105">In this article, we use Azure CLI scripts to deploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="707c4-106">Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="707c4-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="707c4-107">Daha fazla bilgi için bkz: [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="707c4-107">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="707c4-108">Ortamı hazırlama</span><span class="sxs-lookup"><span data-stu-id="707c4-108">Prepare the environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="707c4-109">1. adım: Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="707c4-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="707c4-110">Yedekleme ve kurtarma işlemini gerçekleştirmek için Oracle veritabanı 12 c yüklü bir örneğine sahip bir Linux VM önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="707c4-110">To perform the backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="707c4-111">VM'yi oluşturmak için kullandığınız Market görüntüsü adlı *Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="707c4-111">The Marketplace image you use to create the VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="707c4-112">Bir Oracle veritabanı oluşturmayı öğrenmek için bkz: [Oracle veritabanı hızlı başlangıç oluşturma](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="707c4-112">To learn how to create an Oracle database, see the [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-to-the-vm"></a><span data-ttu-id="707c4-113">2. adım: VM'ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="707c4-113">Step 2: Connect to the VM</span></span>

*   <span data-ttu-id="707c4-114">VM ile güvenli Kabuk (SSH) oturum oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="707c4-114">To create a Secure Shell (SSH) session with the VM, use the following command.</span></span> <span data-ttu-id="707c4-115">IP adresi ve ana bilgisayar adı birlikte yerine `publicIpAddress` , VM için değer.</span><span class="sxs-lookup"><span data-stu-id="707c4-115">Replace the IP address and the host name combination with the `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-the-database"></a><span data-ttu-id="707c4-116">3. adım: veritabanını hazırlama</span><span class="sxs-lookup"><span data-stu-id="707c4-116">Step 3: Prepare the database</span></span>

1.  <span data-ttu-id="707c4-117">Bu adım adlı bir VM üzerinde çalışan bir Oracle örneğini (cdb1) olduğunu varsayar *myVM*.</span><span class="sxs-lookup"><span data-stu-id="707c4-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="707c4-118">Çalıştırma *oracle* süper kullanıcı kök ve ardından dinleyicisi başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="707c4-118">Run the *oracle* superuser root, and then initialize the listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="707c4-119">(İsteğe bağlı) Veritabanı arşiv günlük modunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="707c4-119">(Optional) Make sure the database is in archive log mode:</span></span>

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
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  <span data-ttu-id="707c4-120">(İsteğe bağlı) Yürütme test etmek için bir tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="707c4-120">(Optional) Create a table to test the commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session to scott;
    Grant succeeded.
    SQL> grant create table to scott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  <span data-ttu-id="707c4-121">Doğrulamak veya yedekleme dosyasının konumunu ve boyutunu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707c4-121">Verify or change the backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="707c4-122">Veritabanını yedeklemek için Oracle kurtarma Yöneticisi'ni (RMAN) kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-122">Use Oracle Recovery Manager (RMAN) to back up the database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="707c4-123">4. adım: Uygulama tutarlı yedekleme Linux VM'ler</span><span class="sxs-lookup"><span data-stu-id="707c4-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="707c4-124">Uygulamayla tutarlı yedeklemeler yeni bir özelliktir Azure yedekleme.</span><span class="sxs-lookup"><span data-stu-id="707c4-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="707c4-125">Oluşturun ve önce ve VM anlık görüntüsü (anlık görüntü öncesi ve anlık görüntü sonrası) sonra çalıştırılacak komut dosyalarını seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-125">You can create and select scripts to execute before and after the VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="707c4-126">JSON dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="707c4-126">Download the JSON file.</span></span>

    <span data-ttu-id="707c4-127">VMSnapshotScriptPluginConfig.json https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig indirin.</span><span class="sxs-lookup"><span data-stu-id="707c4-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="707c4-128">Dosya içeriği şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="707c4-128">The file contents look similar to the following:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. <span data-ttu-id="707c4-129">VM /etc/azure klasörü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="707c4-129">Create the /etc/azure folder on the VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="707c4-130">JSON dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-130">Copy the JSON file.</span></span>

    <span data-ttu-id="707c4-131">VMSnapshotScriptPluginConfig.json /etc/azure klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-131">Copy VMSnapshotScriptPluginConfig.json to the /etc/azure folder.</span></span>

4. <span data-ttu-id="707c4-132">JSON dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="707c4-132">Edit the JSON file.</span></span>

    <span data-ttu-id="707c4-133">VMSnapshotScriptPluginConfig.json dosyasını içerecek şekilde düzenleyin `PreScriptLocation` ve `PostScriptlocation` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="707c4-133">Edit the VMSnapshotScriptPluginConfig.json file to include the `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="707c4-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="707c4-134">For example:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. <span data-ttu-id="707c4-135">Anlık görüntü öncesi ve anlık görüntü sonrası komut dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="707c4-135">Create the pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="707c4-136">Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "soğuk yedekleme" için bir örneği burada verilmiştir (Çevrimdışı Yedekleme, kapatma ve yeniden başlatma ile):</span><span class="sxs-lookup"><span data-stu-id="707c4-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="707c4-137">/Etc/Azure/pre_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="707c4-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="707c4-138">/Etc/Azure/post_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="707c4-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="707c4-139">Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "etkin yedek" için bir örneği burada verilmiştir (çevrimiçi yedekleme):</span><span class="sxs-lookup"><span data-stu-id="707c4-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="707c4-140">/Etc/Azure/post_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="707c4-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="707c4-141">/Etc/Azure/pre_script.SQL için gereksinimlerinizi başına dosyasının içeriğini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707c4-141">For /etc/azure/pre_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="707c4-142">/Etc/Azure/post_script.SQL için gereksinimlerinizi başına dosyasının içeriğini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707c4-142">For /etc/azure/post_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="707c4-143">Dosya izinleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="707c4-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="707c4-144">Komut dosyaları sınayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-144">Test the scripts.</span></span>

    <span data-ttu-id="707c4-145">Komut dosyalarını sınamak için ilk olarak, kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="707c4-145">To test the scripts, first, sign in as root.</span></span> <span data-ttu-id="707c4-146">Ardından, herhangi bir hata olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="707c4-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="707c4-147">Daha fazla bilgi için bkz: [Linux VM'ler için uygulamayla tutarlı yedekleme](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="707c4-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-to-back-up-the-vm"></a><span data-ttu-id="707c4-148">5. adım: VM'yi yedeklemek için kullanım Azure kurtarma Hizmetleri kasaları</span><span class="sxs-lookup"><span data-stu-id="707c4-148">Step 5: Use Azure Recovery Services vaults to back up the VM</span></span>

1.  <span data-ttu-id="707c4-149">Azure portalında arama **kurtarma Hizmetleri kasaları**.</span><span class="sxs-lookup"><span data-stu-id="707c4-149">In the Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfası](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="707c4-151">Üzerinde **kurtarma Hizmetleri kasaları** yeni bir kasa eklemek için dikey tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="707c4-151">On the **Recovery Services vaults** blade, to add a new vault, click **Add**.</span></span>

    ![Kurtarma Hizmetleri kasaları Sayfası Ekle](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="707c4-153">Devam etmek için tıklatın **myVault**.</span><span class="sxs-lookup"><span data-stu-id="707c4-153">To continue, click **myVault**.</span></span>

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="707c4-155">Üzerinde **myVault** dikey penceresinde tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="707c4-155">On the **myVault** blade, click **Backup**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfa yedekleme](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="707c4-157">Üzerinde **yedekleme hedefi** dikey penceresinde, varsayılan değerleri kullanmak **Azure** ve **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="707c4-157">On the **Backup Goal** blade, use the default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="707c4-158">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-158">Click **OK**.</span></span>

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="707c4-160">İçin **yedekleme İlkesi**, kullanın **DefaultPolicy**, ya da seçin **Yeni Oluştur ilke**.</span><span class="sxs-lookup"><span data-stu-id="707c4-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="707c4-161">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-161">Click **OK**.</span></span>

    ![Kurtarma Hizmetleri kasaları İlkesi ayrıntı sayfası yedekleme](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="707c4-163">Üzerinde **sanal makine Seç** dikey penceresinde, seçin **myVM1** onay kutusunu işaretleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="707c4-163">On the **Select virtual machines** blade, select the **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="707c4-164">Tıklatın **yedeklemeyi etkinleştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="707c4-164">Click the **Enable backup** button.</span></span>

    ![Kurtarma Hizmetleri kasaları öğelerini yedekleme Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="707c4-166">Tıklattıktan sonra **yedeklemeyi etkinleştir**, yedekleme işlemi zamanlanan saat süresi doluncaya kadar başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="707c4-166">After you click **Enable backup**, the backup process doesn't start until the scheduled time expires.</span></span> <span data-ttu-id="707c4-167">Hemen bir yedekleme ayarlamak için sonraki adımı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-167">To set up an immediate backup, complete the next step.</span></span>

8.  <span data-ttu-id="707c4-168">Üzerinde **myVault - yedekleme öğeleri** dikey altında **yedekleme öğesi sayısı**, yedekleme öğesi sayısı seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-168">On the **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select the backup item count.</span></span>

    ![Kurtarma Hizmetleri kasaları myVault Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="707c4-170">Üzerinde **yedekleme öğeleri (Azure sanal makine)** sayfanın sağ taraftaki dikey tıklayın üç nokta (**...** ) düğmesine tıklayın ve ardından **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="707c4-170">On the **Backup Items (Azure Virtual Machine)** blade, on the right side of the page, click the ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Yedekleme şimdi komutu Kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="707c4-172">Tıklatın **yedekleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="707c4-172">Click the **Backup** button.</span></span> <span data-ttu-id="707c4-173">Yedekleme işleminin tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="707c4-173">Wait for the backup process to finish.</span></span> <span data-ttu-id="707c4-174">Ardından, Git [adım 6: veritabanı dosyalarını kaldırmak](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="707c4-174">Then, go to [Step 6: Remove the database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="707c4-175">Yedekleme işinin durumunu görüntülemek için **işleri**.</span><span class="sxs-lookup"><span data-stu-id="707c4-175">To view the status of the backup job, click **Jobs**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfa işi](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="707c4-177">Yedekleme işinin durumu aşağıdaki görüntüde görünür:</span><span class="sxs-lookup"><span data-stu-id="707c4-177">The status of the backup job appears in the following image:</span></span>

    ![Kurtarma Hizmetleri kasaları iş durumu sayfası](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="707c4-179">Bir uygulama tutarlı yedekleme için günlük dosyasındaki hataları giderin.</span><span class="sxs-lookup"><span data-stu-id="707c4-179">For an application-consistent backup, address any errors in the log file.</span></span> <span data-ttu-id="707c4-180">Günlük dosyası /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0 bulunur.</span><span class="sxs-lookup"><span data-stu-id="707c4-180">The log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-the-database-files"></a><span data-ttu-id="707c4-181">6. adım: veritabanı dosyalarını kaldırma</span><span class="sxs-lookup"><span data-stu-id="707c4-181">Step 6: Remove the database files</span></span> 
<span data-ttu-id="707c4-182">Bu makalenin sonraki bölümlerinde kurtarma işlemini test öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="707c4-182">Later in this article, you'll learn how to test the recovery process.</span></span> <span data-ttu-id="707c4-183">Kurtarma işlemi sınayabilirsiniz önce veritabanı dosyalarını kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="707c4-183">Before you can test the recovery process, you have to remove the database files.</span></span>

1.  <span data-ttu-id="707c4-184">Tablo alanı ve yedekleme dosyalarını kaldırın:</span><span class="sxs-lookup"><span data-stu-id="707c4-184">Remove the tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="707c4-185">(İsteğe bağlı) Oracle örneğini kapatın:</span><span class="sxs-lookup"><span data-stu-id="707c4-185">(Optional) Shut down the Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-the-deleted-files-from-the-recovery-services-vaults"></a><span data-ttu-id="707c4-186">Kurtarma Hizmetleri kasalarının silinmiş dosyaları geri yükle</span><span class="sxs-lookup"><span data-stu-id="707c4-186">Restore the deleted files from the Recovery Services vaults</span></span>
<span data-ttu-id="707c4-187">Silinen dosyaların geri yüklemek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="707c4-187">To restore the deleted files, complete the following steps:</span></span>

1. <span data-ttu-id="707c4-188">Azure portalında arama *myVault* kurtarma Hizmetleri kasaları öğesi.</span><span class="sxs-lookup"><span data-stu-id="707c4-188">In the Azure portal, search for the *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="707c4-189">Üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-189">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![Kurtarma Hizmetleri kasaları myVault yedekleme öğeleri](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="707c4-191">Altında **yedekleme öğesi sayısı**, öğe sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-191">Under **BACKUP ITEM COUNT**, select the number of items.</span></span>

    ![Kurtarma Hizmetleri kasaları Azure sanal makine yedekleme öğesi sayısı](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="707c4-193">Üzerinde **myvm1** dikey penceresinde tıklatın **dosya kurtarma (Önizleme)**.</span><span class="sxs-lookup"><span data-stu-id="707c4-193">On the **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Dosya Kurtarma sayfası ekran görüntüsü kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="707c4-195">Üzerinde **dosya kurtarma (Önizleme)** bölmesinde tıklatın **karşıdan yükleme komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="707c4-195">On the **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="707c4-196">Ardından, yükleme (.sh) dosyasını istemci bilgisayarda bir klasöre kaydedin.</span><span class="sxs-lookup"><span data-stu-id="707c4-196">Then, save the download (.sh) file to a folder on the client computer.</span></span>

    ![Yükleme komut dosyasını kaydetme seçenekleri](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="707c4-198">VM .sh dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-198">Copy the .sh file to the VM.</span></span>

    <span data-ttu-id="707c4-199">Aşağıdaki örnekte nasıl güvenli bir kopyasını (scp) kullanmak için dosyayı VM'ye taşımak için komutu gösterir.</span><span class="sxs-lookup"><span data-stu-id="707c4-199">The following example shows how you to use a secure copy (scp) command to move the file to the VM.</span></span> <span data-ttu-id="707c4-200">İçeriği panoya kopyalayabilirsiniz ve içeriği VM üzerinde ayarlanmış yeni bir dosya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="707c4-200">You also can copy the contents to the clipboard, and then paste the contents in a new file that is set up on the VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="707c4-201">Aşağıdaki örnekte, IP adresi ve klasör değerleri güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="707c4-201">In the following example, ensure that you update the IP address and folder values.</span></span> <span data-ttu-id="707c4-202">Değerleri dosyasının kaydedildiği klasöre eşlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="707c4-202">The values must map to the folder where the file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="707c4-203">Dosyanın kök tarafından ait şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707c4-203">Change the file, so that it's owned by the root.</span></span>

    <span data-ttu-id="707c4-204">Aşağıdaki örnekte, dosyanın kök tarafından ait şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707c4-204">In the following example, change the file so that it's owned by the root.</span></span> <span data-ttu-id="707c4-205">Ardından, izinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="707c4-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="707c4-206">Aşağıdaki örnek, önceki komut dosyasını çalıştırın, sonra gördükleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="707c4-206">The following example shows what you should see after you run the preceding script.</span></span> <span data-ttu-id="707c4-207">Devam etmek için istendiğinde girin **Y**.</span><span class="sxs-lookup"><span data-stu-id="707c4-207">When you're prompted to continue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    The script requires 'open-iscsi' and 'lshw' to run.
    Do you want us to install 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' to continue with installation, 'N' to abort the operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting to recovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of the recovery point to this machine...

    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

7. <span data-ttu-id="707c4-208">Bağlanan birimler için erişim doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="707c4-208">Access to the mounted volumes is confirmed.</span></span>

    <span data-ttu-id="707c4-209">Çıkmak için girin **q**ve bağlanan birimler için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="707c4-209">To exit, enter **q**, and then search for the mounted volumes.</span></span> <span data-ttu-id="707c4-210">Bir komut isteminde eklenen birimlerin listesini oluşturmak için girin **df -k**.</span><span class="sxs-lookup"><span data-stu-id="707c4-210">To create a list of the added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Df -k komutu](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="707c4-212">Eksik dosyaları yeniden klasörlerine kopyalamak için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-212">Use the following script to copy the missing files back to the folders:</span></span>

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. <span data-ttu-id="707c4-213">Aşağıdaki komut dosyasında RMAN veritabanını kurtarmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-213">In the following script, use RMAN to recover the database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="707c4-214">Disk çıkarın.</span><span class="sxs-lookup"><span data-stu-id="707c4-214">Unmount the disk.</span></span>

    <span data-ttu-id="707c4-215">Azure portalında üzerinde **dosya kurtarma (Önizleme)** dikey penceresinde tıklatın **çıkarın diskleri**.</span><span class="sxs-lookup"><span data-stu-id="707c4-215">In the Azure portal, on the **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Diskleri komutunu çıkarın](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-the-entire-vm"></a><span data-ttu-id="707c4-217">Tüm VM geri yükleme</span><span class="sxs-lookup"><span data-stu-id="707c4-217">Restore the entire VM</span></span>

<span data-ttu-id="707c4-218">Kurtarma Hizmetleri kasalarının silinen dosyaların geri yerine tüm VM'yi geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="707c4-218">Instead of restoring the deleted files from the Recovery Services vaults, you can restore the entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="707c4-219">1. adım: Sil myVM</span><span class="sxs-lookup"><span data-stu-id="707c4-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="707c4-220">Azure portalında Git **myVM1** kasa ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="707c4-220">In the Azure portal, go to the **myVM1** vault, and then select **Delete**.</span></span>

    ![Kasa delete komutu](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-the-vm"></a><span data-ttu-id="707c4-222">2. adım: VM kurtarma</span><span class="sxs-lookup"><span data-stu-id="707c4-222">Step 2: Recover the VM</span></span>

1.  <span data-ttu-id="707c4-223">Git **kurtarma Hizmetleri kasaları**ve ardından **myVault**.</span><span class="sxs-lookup"><span data-stu-id="707c4-223">Go to **Recovery Services vaults**, and then select **myVault**.</span></span>

    ![myVault giriş](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="707c4-225">Üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-225">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![myVault öğeleri yedekleyin](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="707c4-227">Üzerinde **yedekleme öğeleri (Azure sanal makine)** dikey penceresinde, select **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="707c4-227">On the **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Kurtarma VM sayfası](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="707c4-229">Üzerinde **myvm1** dikey penceresinde, üç nokta işaretine (**...** ) düğmesine tıklayın ve ardından **geri VM**.</span><span class="sxs-lookup"><span data-stu-id="707c4-229">On the **myvm1** blade, click the ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![VM komutu geri yükleme](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="707c4-231">Üzerinde **seçin geri yükleme noktası** dikey penceresinde, geri yüklemek istediğiniz öğeyi seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="707c4-231">On the **Select restore point** blade, select the item that you want to restore, and then click **OK**.</span></span>

    ![Geri yükleme noktası seçin](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="707c4-233">Uygulama tutarlı yedeklemeyi etkinleştirdiyseniz, dikey Mavi çubuk görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="707c4-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="707c4-234">Üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, sanal makine adı seçin, bir kaynak grubu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="707c4-234">On the **Restore configuration** blade, select the virtual machine name, select the resource group, and then click **OK**.</span></span>

    ![Yapılandırma değerleri geri yükle](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="707c4-236">VM geri yüklemek için **geri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="707c4-236">To restore the VM, click the **Restore** button.</span></span>

8.  <span data-ttu-id="707c4-237">Geri yükleme işleminin durumunu görüntülemek için **işleri**ve ardından **yedekleme işlerini**.</span><span class="sxs-lookup"><span data-stu-id="707c4-237">To view the status of the restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Yedekleme işleri durumu komutu](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="707c4-239">Aşağıdaki şekilde geri yükleme işlemi durumunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="707c4-239">The following figure shows the status of the restore process:</span></span>

    ![Geri yükleme işlemi durumu](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-the-public-ip-address"></a><span data-ttu-id="707c4-241">3. adım: genel IP adresi ayarlama</span><span class="sxs-lookup"><span data-stu-id="707c4-241">Step 3: Set the public IP address</span></span>
<span data-ttu-id="707c4-242">VM geri yüklendikten sonra ortak IP adresini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-242">After the VM is restored, set up the public IP address.</span></span>

1.  <span data-ttu-id="707c4-243">Arama kutusuna **genel IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="707c4-243">In the search box, enter **public IP address**.</span></span>

    ![Ortak IP adresleri listesi](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="707c4-245">Üzerinde **ortak IP adresleri** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="707c4-245">On the **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="707c4-246">Üzerinde **ortak IP adresi oluştur** dikey penceresinde için **adı**, genel IP adı seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-246">On the **Create public IP address** blade, for **Name**, select the public IP name.</span></span> <span data-ttu-id="707c4-247">**Kaynak grubu** olarak **Var olanı kullan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="707c4-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="707c4-248">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="707c4-248">Then, click **Create**.</span></span>

    ![IP adresi oluşturun](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="707c4-250">Ortak IP adresine sahip ağ arabirimi VM için ilişkilendirmek için aramak ve seçmek **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="707c4-250">To associate the public IP address with the network interface for the VM, search for and select **myVMip**.</span></span> <span data-ttu-id="707c4-251">Ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="707c4-251">Then, click **Associate**.</span></span>

    ![IP adresi ilişkilendirme](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="707c4-253">İçin **kaynak türü**seçin **ağ arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="707c4-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="707c4-254">MyVM örneği tarafından kullanılan ağ arabirimi seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="707c4-254">Select the network interface that is used by the myVM instance, and then click **OK**.</span></span>

    ![Kaynak türü ve NIC değerleri seçin](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="707c4-256">Arayın ve portaldan verilen myVM örneği açın.</span><span class="sxs-lookup"><span data-stu-id="707c4-256">Search for and open the instance of myVM that is ported from the portal.</span></span> <span data-ttu-id="707c4-257">VM ile ilişkili IP adresi üzerinde myVM yer **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="707c4-257">The IP address that is associated with the VM appears on the myVM **Overview** blade.</span></span>

    ![IP adresi değeri](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-to-the-vm"></a><span data-ttu-id="707c4-259">4. adım: VM'ye bağlanın</span><span class="sxs-lookup"><span data-stu-id="707c4-259">Step 4: Connect to the VM</span></span>

*   <span data-ttu-id="707c4-260">VM'e bağlanmak için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-260">To connect to the VM, use the following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-the-database-is-accessible"></a><span data-ttu-id="707c4-261">5. adım: veritabanı erişilebilir olup olmadığını sınamak</span><span class="sxs-lookup"><span data-stu-id="707c4-261">Step 5: Test whether the database is accessible</span></span>
*   <span data-ttu-id="707c4-262">Erişilebilirlik sınamak için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-262">To test accessibility, use the following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="707c4-263">Varsa veritabanı **başlangıç** komutu bir hata oluşturur, veritabanını kurtarmak için bkz: [adım 6: kullanmak veritabanını kurtarmak için RMAN](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="707c4-263">If the database **startup** command generates an error, to recover the database, see [Step 6: Use RMAN to recover the database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-to-recover-the-database"></a><span data-ttu-id="707c4-264">6. adım: Veritabanını kurtarmak (isteğe bağlı) kullanım RMAN</span><span class="sxs-lookup"><span data-stu-id="707c4-264">Step 6: (Optional) Use RMAN to recover the database</span></span>
*   <span data-ttu-id="707c4-265">Veritabanını kurtarmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="707c4-265">To recover the database, use the following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="707c4-266">Yedekleme ve kurtarma Azure Linux VM'de Oracle veritabanı 12c veritabanının şimdi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="707c4-266">The backup and recovery of the Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="707c4-267">VM silme</span><span class="sxs-lookup"><span data-stu-id="707c4-267">Delete the VM</span></span>

<span data-ttu-id="707c4-268">VM artık ihtiyacınız olduğunda, kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="707c4-268">When you no longer need the VM, you can use the following command to remove the resource group, the VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="707c4-269">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="707c4-269">Next steps</span></span>

[<span data-ttu-id="707c4-270">Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="707c4-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="707c4-271">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="707c4-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



