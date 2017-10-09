---
title: "bir Azure Linux sanal makine üzerinde veritabanı aaaBack yukarı ve Kurtarma bir Oracle veritabanına 12c | Microsoft Docs"
description: "Azure ortamınızda nasıl tooback yedeklemek ve kurtarmak bir Oracle veritabanına 12 c veritabanı öğrenin."
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
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="0605b-103">Yedekleme ve bir Azure Linux sanal makine üzerinde bir Oracle veritabanına 12 c veritabanını kurtarma</span><span class="sxs-lookup"><span data-stu-id="0605b-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="0605b-104">Azure CLI toocreate kullanın ve bir komut isteminden Azure kaynaklarınızı yönetmek veya betiklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0605b-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="0605b-105">Bu makalede, Azure CLI betikleri toodeploy Azure Marketi galeri görüntünün bir Oracle veritabanına 12 c veritabanından kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0605b-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="0605b-106">Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0605b-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="0605b-107">Daha fazla bilgi için bkz: Merhaba [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0605b-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="0605b-108">Merhaba ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="0605b-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="0605b-109">1. adım: Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0605b-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="0605b-110">tooperform hello yedekleme ve kurtarma işlemi, Oracle veritabanı 12 c yüklü bir örneğine sahip bir Linux VM önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0605b-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="0605b-111">Merhaba Market görüntüsü kullandığınız VM adlandırılan toocreate hello *Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="0605b-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="0605b-112">toolearn nasıl toocreate bir Oracle veritabanına bkz hello [Oracle veritabanı hızlı başlangıç oluşturma](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="0605b-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="0605b-113">2. adım: toohello VM bağlanma</span><span class="sxs-lookup"><span data-stu-id="0605b-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="0605b-114">Güvenli Kabuk (SSH) oturumu hello VM ile toocreate komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0605b-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="0605b-115">Başlangıç IP adresi ve hello ana bilgisayar adı birleşimi ile hello yerine `publicIpAddress` , VM için değer.</span><span class="sxs-lookup"><span data-stu-id="0605b-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="0605b-116">3. adım: hello veritabanını hazırlama</span><span class="sxs-lookup"><span data-stu-id="0605b-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="0605b-117">Bu adım adlı bir VM üzerinde çalışan bir Oracle örneğini (cdb1) olduğunu varsayar *myVM*.</span><span class="sxs-lookup"><span data-stu-id="0605b-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="0605b-118">Merhaba çalıştırmak *oracle* süper kullanıcı kök ve hello dinleyicisi başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="0605b-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
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
    hello listener supports no services
    hello command completed successfully
    ```

2.  <span data-ttu-id="0605b-119">(İsteğe bağlı) Merhaba veritabanı arşiv günlük modunda olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="0605b-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="0605b-120">(İsteğe bağlı) Bir tablo tootest hello yürütme oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0605b-120">(Optional) Create a table tootest hello commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
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
4.  <span data-ttu-id="0605b-121">Doğrulamak veya hello yedekleme dosyasının konumunu ve boyutunu değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0605b-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="0605b-122">Oracle kurtarma Yöneticisi'ni (RMAN) tooback hello veritabanını kullanın:</span><span class="sxs-lookup"><span data-stu-id="0605b-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="0605b-123">4. adım: Uygulama tutarlı yedekleme Linux VM'ler</span><span class="sxs-lookup"><span data-stu-id="0605b-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="0605b-124">Uygulamayla tutarlı yedeklemeler yeni bir özelliktir Azure yedekleme.</span><span class="sxs-lookup"><span data-stu-id="0605b-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="0605b-125">Oluşturun ve komut dosyaları tooexecute önce ve sonra hello VM anlık görüntü (anlık görüntü öncesi ve sonrası anlık görüntü) seçin.</span><span class="sxs-lookup"><span data-stu-id="0605b-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="0605b-126">Merhaba JSON dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="0605b-126">Download hello JSON file.</span></span>

    <span data-ttu-id="0605b-127">VMSnapshotScriptPluginConfig.json https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig indirin.</span><span class="sxs-lookup"><span data-stu-id="0605b-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="0605b-128">Merhaba dosya içeriklerini benzer toohello aşağıdaki bakın:</span><span class="sxs-lookup"><span data-stu-id="0605b-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="0605b-129">Merhaba VM üzerinde Hello /etc/azure klasörü oluşturun:</span><span class="sxs-lookup"><span data-stu-id="0605b-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="0605b-130">Merhaba JSON dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="0605b-131">VMSnapshotScriptPluginConfig.json toohello /etc/azure klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="0605b-132">Merhaba JSON dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="0605b-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="0605b-133">Merhaba VMSnapshotScriptPluginConfig.json dosya tooinclude hello Düzenle `PreScriptLocation` ve `PostScriptlocation` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="0605b-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="0605b-134">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="0605b-134">For example:</span></span>

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

5. <span data-ttu-id="0605b-135">Merhaba, anlık görüntü öncesi ve anlık görüntü sonrası komut dosyalarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0605b-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="0605b-136">Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "soğuk yedekleme" için bir örneği burada verilmiştir (Çevrimdışı Yedekleme, kapatma ve yeniden başlatma ile):</span><span class="sxs-lookup"><span data-stu-id="0605b-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="0605b-137">/Etc/Azure/pre_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="0605b-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="0605b-138">/Etc/Azure/post_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="0605b-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="0605b-139">Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "etkin yedek" için bir örneği burada verilmiştir (çevrimiçi yedekleme):</span><span class="sxs-lookup"><span data-stu-id="0605b-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="0605b-140">/Etc/Azure/post_script.sh için:</span><span class="sxs-lookup"><span data-stu-id="0605b-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="0605b-141">/Etc/Azure/pre_script.SQL için gereksinimlerinizi başına hello dosyasının Merhaba içeriğine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0605b-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="0605b-142">/Etc/Azure/post_script.SQL için gereksinimlerinizi başına hello dosyasının Merhaba içeriğine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0605b-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="0605b-143">Dosya izinleri değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0605b-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="0605b-144">Merhaba betikleri sınayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-144">Test hello scripts.</span></span>

    <span data-ttu-id="0605b-145">tootest hello komut dosyaları, ilk olarak, kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0605b-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="0605b-146">Ardından, herhangi bir hata olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="0605b-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="0605b-147">Daha fazla bilgi için bkz: [Linux VM'ler için uygulamayla tutarlı yedekleme](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="0605b-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="0605b-148">5. adım: Hello VM yukarı tooback kullanım Azure kurtarma Hizmetleri kasaları</span><span class="sxs-lookup"><span data-stu-id="0605b-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="0605b-149">İçinde Azure portal Merhaba, arama **kurtarma Hizmetleri kasaları**.</span><span class="sxs-lookup"><span data-stu-id="0605b-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfası](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="0605b-151">Merhaba üzerinde **kurtarma Hizmetleri kasaları** dikey, tooadd yeni bir kasa tıklayın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0605b-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Kurtarma Hizmetleri kasaları Sayfası Ekle](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="0605b-153">toocontinue, tıklatın **myVault**.</span><span class="sxs-lookup"><span data-stu-id="0605b-153">toocontinue, click **myVault**.</span></span>

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="0605b-155">Merhaba üzerinde **myVault** dikey penceresinde tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="0605b-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfa yedekleme](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="0605b-157">Merhaba üzerinde **yedekleme hedefi** dikey penceresinde, kullanım hello varsayılan değerleri **Azure** ve **sanal makine**.</span><span class="sxs-lookup"><span data-stu-id="0605b-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="0605b-158">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-158">Click **OK**.</span></span>

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="0605b-160">İçin **yedekleme İlkesi**, kullanın **DefaultPolicy**, ya da seçin **Yeni Oluştur ilke**.</span><span class="sxs-lookup"><span data-stu-id="0605b-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="0605b-161">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-161">Click **OK**.</span></span>

    ![Kurtarma Hizmetleri kasaları İlkesi ayrıntı sayfası yedekleme](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="0605b-163">Merhaba üzerinde **sanal makine Seç** dikey penceresinde, select hello **myVM1** onay kutusunu işaretleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0605b-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="0605b-164">Merhaba tıklatın **yedeklemeyi etkinleştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0605b-164">Click hello **Enable backup** button.</span></span>

    ![Kurtarma Hizmetleri kasaları öğeleri toohello yedekleme Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="0605b-166">Tıklattıktan sonra **yedeklemeyi etkinleştir**, hello yedekleme işlemi hello zamanlanmış süresi sona erene kadar başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="0605b-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="0605b-167">Sonraki adım hello tooset, tam hemen bir yedek ayarlama.</span><span class="sxs-lookup"><span data-stu-id="0605b-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="0605b-168">Merhaba üzerinde **myVault - yedekleme öğeleri** dikey altında **yedekleme öğesi sayısı**, seçin hello yedekleme öğesi sayısı.</span><span class="sxs-lookup"><span data-stu-id="0605b-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Kurtarma Hizmetleri kasaları myVault Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="0605b-170">Merhaba üzerinde **yedekleme öğeleri (Azure sanal makine)** hello sayfasının hello sağ taraftaki dikey tıklayın hello üç nokta (**...** ) düğmesine tıklayın ve ardından **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="0605b-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Yedekleme şimdi komutu Kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="0605b-172">Merhaba tıklatın **yedekleme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0605b-172">Click hello **Backup** button.</span></span> <span data-ttu-id="0605b-173">Merhaba yedekleme işlemi toofinish bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0605b-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="0605b-174">Ardından, çok Git[adım 6: kaldırmak hello veritabanı dosyalarını](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="0605b-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="0605b-175">Merhaba yedekleme işinin tooview hello durumu tıklatın **işleri**.</span><span class="sxs-lookup"><span data-stu-id="0605b-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Kurtarma Hizmetleri kasaları sayfa işi](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="0605b-177">Merhaba hello yedekleme işinin durumunu görüntü aşağıdaki hello görünür:</span><span class="sxs-lookup"><span data-stu-id="0605b-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Kurtarma Hizmetleri kasaları iş durumu sayfası](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="0605b-179">Bir uygulama tutarlı yedekleme için hello günlük dosyasındaki hataları giderin.</span><span class="sxs-lookup"><span data-stu-id="0605b-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="0605b-180">Merhaba günlük dosyası /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0 bulunur.</span><span class="sxs-lookup"><span data-stu-id="0605b-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="0605b-181">6. adım: hello veritabanı dosyaları kaldırın</span><span class="sxs-lookup"><span data-stu-id="0605b-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="0605b-182">Bu makalenin sonraki bölümlerinde nasıl tootest hello kurtarma işlemi öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="0605b-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="0605b-183">Merhaba kurtarma işlemi test etmeden önce tooremove hello veritabanı dosyaları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0605b-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="0605b-184">Merhaba belirtilmedi ve yedekleme dosyalarını kaldırın:</span><span class="sxs-lookup"><span data-stu-id="0605b-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="0605b-185">(İsteğe bağlı) Merhaba Oracle örneğini kapatın:</span><span class="sxs-lookup"><span data-stu-id="0605b-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="0605b-186">Kurtarma Hizmetleri kasaları hello hello silinmiş dosyaları geri yükle</span><span class="sxs-lookup"><span data-stu-id="0605b-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="0605b-187">silinen dosyaları, aşağıdaki adımları tam hello toorestore hello:</span><span class="sxs-lookup"><span data-stu-id="0605b-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="0605b-188">Merhaba Hello Azure portal, arama *myVault* kurtarma Hizmetleri kasaları öğesi.</span><span class="sxs-lookup"><span data-stu-id="0605b-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="0605b-189">Merhaba üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe hello sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="0605b-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Kurtarma Hizmetleri kasaları myVault yedekleme öğeleri](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="0605b-191">Altında **yedekleme öğesi sayısı**, öğe hello sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="0605b-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Kurtarma Hizmetleri kasaları Azure sanal makine yedekleme öğesi sayısı](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="0605b-193">Merhaba üzerinde **myvm1** dikey penceresinde tıklatın **dosya kurtarma (Önizleme)**.</span><span class="sxs-lookup"><span data-stu-id="0605b-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Dosya Kurtarma sayfası ekran görüntüsü hello kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="0605b-195">Merhaba üzerinde **dosya kurtarma (Önizleme)** bölmesinde tıklatın **karşıdan yükleme komut dosyası**.</span><span class="sxs-lookup"><span data-stu-id="0605b-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="0605b-196">Daha sonra hello yükleme (.sh) dosya tooa klasör hello istemci bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0605b-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Yükleme komut dosyasını kaydetme seçenekleri](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="0605b-198">Merhaba .sh dosya toohello VM kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="0605b-199">Aşağıdaki örnek hello nasıl güvenli kopyalama (scp) komut toomove toouse hello dosya toohello VM gösterir.</span><span class="sxs-lookup"><span data-stu-id="0605b-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="0605b-200">Merhaba VM üzerinde ayarladığınız yeni dosyasındaki hello içeriği toohello Pano ve Yapıştır hello içeriği kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0605b-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0605b-201">Aşağıdaki örneğine hello hello IP adresi ve klasör değerleri güncelleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0605b-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="0605b-202">Merhaba değerleri hello dosyasının kaydedildiği toohello klasörü eşlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0605b-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="0605b-203">Merhaba kök tarafından ait şekilde hello dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0605b-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="0605b-204">Böylece hello kök tarafından ait aşağıdaki örneğine hello hello dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0605b-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="0605b-205">Ardından, izinleri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0605b-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="0605b-206">Merhaba aşağıdaki örnek komut dosyası önceki hello çalıştırın, sonra gördükleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="0605b-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="0605b-207">Sorulduğunda toocontinue, girin **Y**.</span><span class="sxs-lookup"><span data-stu-id="0605b-207">When you're prompted toocontinue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. <span data-ttu-id="0605b-208">Erişim toohello takılı birimleri onaylandı.</span><span class="sxs-lookup"><span data-stu-id="0605b-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="0605b-209">tooexit, girin **q**ve takılı hello birimler için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="0605b-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="0605b-210">Merhaba listesini eklenen bir komut isteminde şunu girin toocreate **df -k**.</span><span class="sxs-lookup"><span data-stu-id="0605b-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Merhaba df -k komutu](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="0605b-212">Komut dosyası toocopy hello eksik aşağıdaki kullanım hello dosyalar geri toohello klasörler:</span><span class="sxs-lookup"><span data-stu-id="0605b-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="0605b-213">Komut dosyası izleyen hello RMAN toorecover hello veritabanı kullanın:</span><span class="sxs-lookup"><span data-stu-id="0605b-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="0605b-214">Merhaba disk çıkarın.</span><span class="sxs-lookup"><span data-stu-id="0605b-214">Unmount hello disk.</span></span>

    <span data-ttu-id="0605b-215">Merhaba hello üzerinde Azure portal'ın **dosya kurtarma (Önizleme)** dikey penceresinde tıklatın **çıkarın diskleri**.</span><span class="sxs-lookup"><span data-stu-id="0605b-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Diskleri komutunu çıkarın](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="0605b-217">Geri yükleme tüm VM hello</span><span class="sxs-lookup"><span data-stu-id="0605b-217">Restore hello entire VM</span></span>

<span data-ttu-id="0605b-218">Merhaba kurtarma Hizmetleri kasalarının hello silinen dosyaların geri yerine geri yükleyebileceğiniz tüm VM hello.</span><span class="sxs-lookup"><span data-stu-id="0605b-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="0605b-219">1. adım: Sil myVM</span><span class="sxs-lookup"><span data-stu-id="0605b-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="0605b-220">Toohello Hello Azure portal, Git **myVM1** kasa ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="0605b-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Kasa delete komutu](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="0605b-222">2. adım: hello VM kurtarma</span><span class="sxs-lookup"><span data-stu-id="0605b-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="0605b-223">Çok Git**kurtarma Hizmetleri kasaları**ve ardından **myVault**.</span><span class="sxs-lookup"><span data-stu-id="0605b-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![myVault giriş](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="0605b-225">Merhaba üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe hello sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="0605b-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![myVault öğeleri yedekleyin](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="0605b-227">Merhaba üzerinde **yedekleme öğeleri (Azure sanal makine)** dikey penceresinde, select **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="0605b-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Kurtarma VM sayfası](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="0605b-229">Merhaba üzerinde **myvm1** dikey penceresinde hello üç nokta düğmesine (**...** ) düğmesine tıklayın ve ardından **geri VM**.</span><span class="sxs-lookup"><span data-stu-id="0605b-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![VM komutu geri yükleme](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="0605b-231">Merhaba üzerinde **seçin geri yükleme noktası** dikey penceresinde, toorestore istediğiniz ve ardından select hello öğesi **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0605b-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Select hello geri yükleme noktası](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="0605b-233">Uygulama tutarlı yedeklemeyi etkinleştirdiyseniz, dikey Mavi çubuk görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0605b-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="0605b-234">Merhaba üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, select hello sanal makine adı, hello kaynak grubu seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0605b-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Yapılandırma değerleri geri yükle](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="0605b-236">toorestore hello VM tıklatın hello **geri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0605b-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="0605b-237">tooview hello durumu hello geri yükleme işleminin **işleri**ve ardından **yedekleme işlerini**.</span><span class="sxs-lookup"><span data-stu-id="0605b-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Yedekleme işleri durumu komutu](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="0605b-239">Merhaba aşağıdaki şekilde hello hello geri yükleme işleminin durumunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="0605b-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Merhaba geri yükleme işlemi durumu](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="0605b-241">3. adım: hello genel IP adresi ayarlama</span><span class="sxs-lookup"><span data-stu-id="0605b-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="0605b-242">Hello VM geri yüklendikten sonra hello ortak IP adresi ayarlamak.</span><span class="sxs-lookup"><span data-stu-id="0605b-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="0605b-243">Merhaba arama kutusuna **genel IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="0605b-243">In hello search box, enter **public IP address**.</span></span>

    ![Ortak IP adresleri listesi](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="0605b-245">Merhaba üzerinde **ortak IP adresleri** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0605b-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="0605b-246">Merhaba üzerinde **ortak IP adresi oluştur** dikey penceresinde için **adı**seçin hello genel IP adı.</span><span class="sxs-lookup"><span data-stu-id="0605b-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="0605b-247">**Kaynak grubu** olarak **Var olanı kullan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0605b-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="0605b-248">Sonra, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0605b-248">Then, click **Create**.</span></span>

    ![IP adresi oluşturun](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="0605b-250">tooassociate hello ortak IP adresiyle hello ağ arabirimi hello VM için arama için ve select **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="0605b-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="0605b-251">Ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="0605b-251">Then, click **Associate**.</span></span>

    ![IP adresi ilişkilendirme](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="0605b-253">İçin **kaynak türü**seçin **ağ arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="0605b-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="0605b-254">Merhaba myVM örneği tarafından kullanılan hello ağ arabirimi seçin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0605b-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Kaynak türü ve NIC değerleri seçin](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="0605b-256">Arayın ve hello portalından verilen myVM hello örneği açın.</span><span class="sxs-lookup"><span data-stu-id="0605b-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="0605b-257">Merhaba hello VM ile ilişkili IP adresi görünür hello myVM üzerinde **genel bakış** dikey.</span><span class="sxs-lookup"><span data-stu-id="0605b-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![IP adresi değeri](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="0605b-259">4. adım: toohello VM bağlanma</span><span class="sxs-lookup"><span data-stu-id="0605b-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="0605b-260">tooconnect toohello VM, komut dosyası izleyen hello kullan:</span><span class="sxs-lookup"><span data-stu-id="0605b-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="0605b-261">5. adım: hello veritabanı erişilebilir olup olmadığını sınamak</span><span class="sxs-lookup"><span data-stu-id="0605b-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="0605b-262">tootest erişilebilirlik, aşağıdaki komut dosyası kullan hello:</span><span class="sxs-lookup"><span data-stu-id="0605b-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0605b-263">Merhaba, veritabanı **başlangıç** komut, bir hata, toorecover hello veritabanı oluşturur, bkz: [adım 6: kullanım RMAN toorecover hello veritabanı](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="0605b-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="0605b-264">6. adım: (İsteğe bağlı) kullanım RMAN toorecover hello veritabanı</span><span class="sxs-lookup"><span data-stu-id="0605b-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="0605b-265">toorecover hello veritabanı, aşağıdaki komut dosyası kullan hello:</span><span class="sxs-lookup"><span data-stu-id="0605b-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="0605b-266">Merhaba yedekleme ve kurtarma hello Oracle veritabanı 12c veritabanının Azure Linux VM'de şimdi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="0605b-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="0605b-267">Merhaba VM silme</span><span class="sxs-lookup"><span data-stu-id="0605b-267">Delete hello VM</span></span>

<span data-ttu-id="0605b-268">VM artık hello olduğunda komut tooremove hello kaynak grubu, hello VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0605b-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="0605b-269">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0605b-269">Next steps</span></span>

[<span data-ttu-id="0605b-270">Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0605b-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="0605b-271">VM dağıtımı Azure CLI örnekleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="0605b-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)



