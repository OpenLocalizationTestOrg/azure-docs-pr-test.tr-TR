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
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Yedekleme ve bir Azure Linux sanal makine üzerinde bir Oracle veritabanına 12 c veritabanını kurtarma

Komut oluşturma veya bir komut isteminden Azure kaynaklarınızı yönetmek için Azure CLI kullanın. Bu makalede, Azure Marketi galeri görüntünün bir Oracle veritabanına 12 c veritabanından dağıtmak için Azure CLI betiklerini kullanın.

Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun. Daha fazla bilgi için bkz: [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-the-environment"></a>Ortamı hazırlama

### <a name="step-1-prerequisites"></a>1. adım: Önkoşullar

*   Yedekleme ve kurtarma işlemini gerçekleştirmek için Oracle veritabanı 12 c yüklü bir örneğine sahip bir Linux VM önce oluşturmanız gerekir. VM'yi oluşturmak için kullandığınız Market görüntüsü adlı *Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest*.

    Bir Oracle veritabanı oluşturmayı öğrenmek için bkz: [Oracle veritabanı hızlı başlangıç oluşturma](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-to-the-vm"></a>2. adım: VM'ye bağlanın

*   VM ile güvenli Kabuk (SSH) oturum oluşturmak için aşağıdaki komutu kullanın. IP adresi ve ana bilgisayar adı birlikte yerine `publicIpAddress` , VM için değer.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-the-database"></a>3. adım: veritabanını hazırlama

1.  Bu adım adlı bir VM üzerinde çalışan bir Oracle örneğini (cdb1) olduğunu varsayar *myVM*.

    Çalıştırma *oracle* süper kullanıcı kök ve ardından dinleyicisi başlatılamadı:

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

2.  (İsteğe bağlı) Veritabanı arşiv günlük modunda olduğundan emin olun:

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
3.  (İsteğe bağlı) Yürütme test etmek için bir tablo oluşturun:

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
4.  Doğrulamak veya yedekleme dosyasının konumunu ve boyutunu değiştirin:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Veritabanını yedeklemek için Oracle kurtarma Yöneticisi'ni (RMAN) kullanın:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>4. adım: Uygulama tutarlı yedekleme Linux VM'ler

Uygulamayla tutarlı yedeklemeler yeni bir özelliktir Azure yedekleme. Oluşturun ve önce ve VM anlık görüntüsü (anlık görüntü öncesi ve anlık görüntü sonrası) sonra çalıştırılacak komut dosyalarını seçin.

1. JSON dosyasını indirin.

    VMSnapshotScriptPluginConfig.json https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig indirin. Dosya içeriği şuna benzer:

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

2. VM /etc/azure klasörü oluşturun:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. JSON dosyasını kopyalayın.

    VMSnapshotScriptPluginConfig.json /etc/azure klasörüne kopyalayın.

4. JSON dosyasını düzenleyin.

    VMSnapshotScriptPluginConfig.json dosyasını içerecek şekilde düzenleyin `PreScriptLocation` ve `PostScriptlocation` parametreleri. Örneğin:

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

5. Anlık görüntü öncesi ve anlık görüntü sonrası komut dosyalarını oluşturun.

    Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "soğuk yedekleme" için bir örneği burada verilmiştir (Çevrimdışı Yedekleme, kapatma ve yeniden başlatma ile):

    /Etc/Azure/pre_script.sh için:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    /Etc/Azure/post_script.sh için:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Anlık görüntü öncesi ve anlık görüntü sonrası betikleri "etkin yedek" için bir örneği burada verilmiştir (çevrimiçi yedekleme):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    /Etc/Azure/post_script.sh için:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    /Etc/Azure/pre_script.SQL için gereksinimlerinizi başına dosyasının içeriğini değiştirin:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    /Etc/Azure/post_script.SQL için gereksinimlerinizi başına dosyasının içeriğini değiştirin:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Dosya izinleri değiştirin:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Komut dosyaları sınayın.

    Komut dosyalarını sınamak için ilk olarak, kök olarak oturum açın. Ardından, herhangi bir hata olduğundan emin olun:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Daha fazla bilgi için bkz: [Linux VM'ler için uygulamayla tutarlı yedekleme](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-to-back-up-the-vm"></a>5. adım: VM'yi yedeklemek için kullanım Azure kurtarma Hizmetleri kasaları

1.  Azure portalında arama **kurtarma Hizmetleri kasaları**.

    ![Kurtarma Hizmetleri kasaları sayfası](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Üzerinde **kurtarma Hizmetleri kasaları** yeni bir kasa eklemek için dikey tıklayın **Ekle**.

    ![Kurtarma Hizmetleri kasaları Sayfası Ekle](./media/oracle-backup-recovery/recovery_service_02.png)

3.  Devam etmek için tıklatın **myVault**.

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Üzerinde **myVault** dikey penceresinde tıklatın **yedekleme**.

    ![Kurtarma Hizmetleri kasaları sayfa yedekleme](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Üzerinde **yedekleme hedefi** dikey penceresinde, varsayılan değerleri kullanmak **Azure** ve **sanal makine**. **Tamam** düğmesine tıklayın.

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_05.png)

6.  İçin **yedekleme İlkesi**, kullanın **DefaultPolicy**, ya da seçin **Yeni Oluştur ilke**. **Tamam** düğmesine tıklayın.

    ![Kurtarma Hizmetleri kasaları İlkesi ayrıntı sayfası yedekleme](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Üzerinde **sanal makine Seç** dikey penceresinde, seçin **myVM1** onay kutusunu işaretleyin ve ardından **Tamam**. Tıklatın **yedeklemeyi etkinleştir** düğmesi.

    ![Kurtarma Hizmetleri kasaları öğelerini yedekleme Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Tıklattıktan sonra **yedeklemeyi etkinleştir**, yedekleme işlemi zamanlanan saat süresi doluncaya kadar başlamıyor. Hemen bir yedekleme ayarlamak için sonraki adımı tamamlayın.

8.  Üzerinde **myVault - yedekleme öğeleri** dikey altında **yedekleme öğesi sayısı**, yedekleme öğesi sayısı seçin.

    ![Kurtarma Hizmetleri kasaları myVault Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Üzerinde **yedekleme öğeleri (Azure sanal makine)** sayfanın sağ taraftaki dikey tıklayın üç nokta (**...** ) düğmesine tıklayın ve ardından **Şimdi Yedekle**.

    ![Yedekleme şimdi komutu Kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_09.png)

10. Tıklatın **yedekleme** düğmesi. Yedekleme işleminin tamamlanması için bekleyin. Ardından, Git [adım 6: veritabanı dosyalarını kaldırmak](#step-6-remove-the-database-files).

    Yedekleme işinin durumunu görüntülemek için **işleri**.

    ![Kurtarma Hizmetleri kasaları sayfa işi](./media/oracle-backup-recovery/recovery_service_10.png)

    Yedekleme işinin durumu aşağıdaki görüntüde görünür:

    ![Kurtarma Hizmetleri kasaları iş durumu sayfası](./media/oracle-backup-recovery/recovery_service_11.png)

11. Bir uygulama tutarlı yedekleme için günlük dosyasındaki hataları giderin. Günlük dosyası /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0 bulunur.

### <a name="step-6-remove-the-database-files"></a>6. adım: veritabanı dosyalarını kaldırma 
Bu makalenin sonraki bölümlerinde kurtarma işlemini test öğreneceksiniz. Kurtarma işlemi sınayabilirsiniz önce veritabanı dosyalarını kaldırmanız gerekir.

1.  Tablo alanı ve yedekleme dosyalarını kaldırın:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (İsteğe bağlı) Oracle örneğini kapatın:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-the-deleted-files-from-the-recovery-services-vaults"></a>Kurtarma Hizmetleri kasalarının silinmiş dosyaları geri yükle
Silinen dosyaların geri yüklemek için aşağıdaki adımları tamamlayın:

1. Azure portalında arama *myVault* kurtarma Hizmetleri kasaları öğesi. Üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe sayısını seçin.

    ![Kurtarma Hizmetleri kasaları myVault yedekleme öğeleri](./media/oracle-backup-recovery/recovery_service_12.png)

2. Altında **yedekleme öğesi sayısı**, öğe sayısını seçin.

    ![Kurtarma Hizmetleri kasaları Azure sanal makine yedekleme öğesi sayısı](./media/oracle-backup-recovery/recovery_service_13.png)

3. Üzerinde **myvm1** dikey penceresinde tıklatın **dosya kurtarma (Önizleme)**.

    ![Dosya Kurtarma sayfası ekran görüntüsü kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_14.png)

4. Üzerinde **dosya kurtarma (Önizleme)** bölmesinde tıklatın **karşıdan yükleme komut dosyası**. Ardından, yükleme (.sh) dosyasını istemci bilgisayarda bir klasöre kaydedin.

    ![Yükleme komut dosyasını kaydetme seçenekleri](./media/oracle-backup-recovery/recovery_service_15.png)

5. VM .sh dosyasını kopyalayın.

    Aşağıdaki örnekte nasıl güvenli bir kopyasını (scp) kullanmak için dosyayı VM'ye taşımak için komutu gösterir. İçeriği panoya kopyalayabilirsiniz ve içeriği VM üzerinde ayarlanmış yeni bir dosya yapıştırın.

    > [!IMPORTANT]
    > Aşağıdaki örnekte, IP adresi ve klasör değerleri güncelleştirdiğinizden emin olun. Değerleri dosyasının kaydedildiği klasöre eşlenmelidir.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Dosyanın kök tarafından ait şekilde değiştirin.

    Aşağıdaki örnekte, dosyanın kök tarafından ait şekilde değiştirin. Ardından, izinleri değiştirin.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Aşağıdaki örnek, önceki komut dosyasını çalıştırın, sonra gördükleri gösterir. Devam etmek için istendiğinde girin **Y**.

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

7. Bağlanan birimler için erişim doğrulanır.

    Çıkmak için girin **q**ve bağlanan birimler için arama yapın. Bir komut isteminde eklenen birimlerin listesini oluşturmak için girin **df -k**.

    ![Df -k komutu](./media/oracle-backup-recovery/recovery_service_16.png)

8. Eksik dosyaları yeniden klasörlerine kopyalamak için aşağıdaki komut dosyasını kullanın:

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
9. Aşağıdaki komut dosyasında RMAN veritabanını kurtarmak için kullanın:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Disk çıkarın.

    Azure portalında üzerinde **dosya kurtarma (Önizleme)** dikey penceresinde tıklatın **çıkarın diskleri**.

    ![Diskleri komutunu çıkarın](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-the-entire-vm"></a>Tüm VM geri yükleme

Kurtarma Hizmetleri kasalarının silinen dosyaların geri yerine tüm VM'yi geri yükleyebilirsiniz.

### <a name="step-1-delete-myvm"></a>1. adım: Sil myVM

*   Azure portalında Git **myVM1** kasa ve ardından **silmek**.

    ![Kasa delete komutu](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-the-vm"></a>2. adım: VM kurtarma

1.  Git **kurtarma Hizmetleri kasaları**ve ardından **myVault**.

    ![myVault giriş](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe sayısını seçin.

    ![myVault öğeleri yedekleyin](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Üzerinde **yedekleme öğeleri (Azure sanal makine)** dikey penceresinde, select **myvm1**.

    ![Kurtarma VM sayfası](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Üzerinde **myvm1** dikey penceresinde, üç nokta işaretine (**...** ) düğmesine tıklayın ve ardından **geri VM**.

    ![VM komutu geri yükleme](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Üzerinde **seçin geri yükleme noktası** dikey penceresinde, geri yüklemek istediğiniz öğeyi seçin ve ardından **Tamam**.

    ![Geri yükleme noktası seçin](./media/oracle-backup-recovery/recover_vm_06.png)

    Uygulama tutarlı yedeklemeyi etkinleştirdiyseniz, dikey Mavi çubuk görüntülenir.

6.  Üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, sanal makine adı seçin, bir kaynak grubu seçin ve ardından **Tamam**.

    ![Yapılandırma değerleri geri yükle](./media/oracle-backup-recovery/recover_vm_07.png)

7.  VM geri yüklemek için **geri** düğmesi.

8.  Geri yükleme işleminin durumunu görüntülemek için **işleri**ve ardından **yedekleme işlerini**.

    ![Yedekleme işleri durumu komutu](./media/oracle-backup-recovery/recover_vm_08.png)

    Aşağıdaki şekilde geri yükleme işlemi durumunu gösterir:

    ![Geri yükleme işlemi durumu](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-the-public-ip-address"></a>3. adım: genel IP adresi ayarlama
VM geri yüklendikten sonra ortak IP adresini ayarlayın.

1.  Arama kutusuna **genel IP adresi**.

    ![Ortak IP adresleri listesi](./media/oracle-backup-recovery/create_ip_00.png)

2.  Üzerinde **ortak IP adresleri** dikey penceresinde tıklatın **Ekle**. Üzerinde **ortak IP adresi oluştur** dikey penceresinde için **adı**, genel IP adı seçin. **Kaynak grubu** olarak **Var olanı kullan**’ı seçin. Sonra, **Oluştur**’a tıklayın.

    ![IP adresi oluşturun](./media/oracle-backup-recovery/create_ip_01.png)

3.  Ortak IP adresine sahip ağ arabirimi VM için ilişkilendirmek için aramak ve seçmek **myVMip**. Ardından **ilişkilendirmek**.

    ![IP adresi ilişkilendirme](./media/oracle-backup-recovery/create_ip_02.png)

4.  İçin **kaynak türü**seçin **ağ arabirimi**. MyVM örneği tarafından kullanılan ağ arabirimi seçin ve ardından **Tamam**.

    ![Kaynak türü ve NIC değerleri seçin](./media/oracle-backup-recovery/create_ip_03.png)

5.  Arayın ve portaldan verilen myVM örneği açın. VM ile ilişkili IP adresi üzerinde myVM yer **genel bakış** dikey.

    ![IP adresi değeri](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-to-the-vm"></a>4. adım: VM'ye bağlanın

*   VM'e bağlanmak için aşağıdaki komut dosyasını kullanın:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-the-database-is-accessible"></a>5. adım: veritabanı erişilebilir olup olmadığını sınamak
*   Erişilebilirlik sınamak için aşağıdaki komut dosyasını kullanın:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Varsa veritabanı **başlangıç** komutu bir hata oluşturur, veritabanını kurtarmak için bkz: [adım 6: kullanmak veritabanını kurtarmak için RMAN](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-to-recover-the-database"></a>6. adım: Veritabanını kurtarmak (isteğe bağlı) kullanım RMAN
*   Veritabanını kurtarmak için aşağıdaki komutu kullanın:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Yedekleme ve kurtarma Azure Linux VM'de Oracle veritabanı 12c veritabanının şimdi tamamlandı.

## <a name="delete-the-vm"></a>VM silme

VM artık ihtiyacınız olduğunda, kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanabilirsiniz:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma](../../linux/create-cli-complete.md)

[VM dağıtımı Azure CLI örnekleri keşfedin](../../linux/cli-samples.md)



