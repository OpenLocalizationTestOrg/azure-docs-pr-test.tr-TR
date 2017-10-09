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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Yedekleme ve bir Azure Linux sanal makine üzerinde bir Oracle veritabanına 12 c veritabanını kurtarma

Azure CLI toocreate kullanın ve bir komut isteminden Azure kaynaklarınızı yönetmek veya betiklerini kullanın. Bu makalede, Azure CLI betikleri toodeploy Azure Marketi galeri görüntünün bir Oracle veritabanına 12 c veritabanından kullanırız.

Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun. Daha fazla bilgi için bkz: Merhaba [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Merhaba ortamını hazırlayın

### <a name="step-1-prerequisites"></a>1. adım: Önkoşullar

*   tooperform hello yedekleme ve kurtarma işlemi, Oracle veritabanı 12 c yüklü bir örneğine sahip bir Linux VM önce oluşturmanız gerekir. Merhaba Market görüntüsü kullandığınız VM adlandırılan toocreate hello *Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest*.

    toolearn nasıl toocreate bir Oracle veritabanına bkz hello [Oracle veritabanı hızlı başlangıç oluşturma](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>2. adım: toohello VM bağlanma

*   Güvenli Kabuk (SSH) oturumu hello VM ile toocreate komutu aşağıdaki hello kullanın. Başlangıç IP adresi ve hello ana bilgisayar adı birleşimi ile hello yerine `publicIpAddress` , VM için değer.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>3. adım: hello veritabanını hazırlama

1.  Bu adım adlı bir VM üzerinde çalışan bir Oracle örneğini (cdb1) olduğunu varsayar *myVM*.

    Merhaba çalıştırmak *oracle* süper kullanıcı kök ve hello dinleyicisi başlatılamadı:

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

2.  (İsteğe bağlı) Merhaba veritabanı arşiv günlük modunda olduğundan emin olun:

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
3.  (İsteğe bağlı) Bir tablo tootest hello yürütme oluşturun:

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
4.  Doğrulamak veya hello yedekleme dosyasının konumunu ve boyutunu değiştirin:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Oracle kurtarma Yöneticisi'ni (RMAN) tooback hello veritabanını kullanın:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>4. adım: Uygulama tutarlı yedekleme Linux VM'ler

Uygulamayla tutarlı yedeklemeler yeni bir özelliktir Azure yedekleme. Oluşturun ve komut dosyaları tooexecute önce ve sonra hello VM anlık görüntü (anlık görüntü öncesi ve sonrası anlık görüntü) seçin.

1. Merhaba JSON dosyasını indirin.

    VMSnapshotScriptPluginConfig.json https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig indirin. Merhaba dosya içeriklerini benzer toohello aşağıdaki bakın:

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

2. Merhaba VM üzerinde Hello /etc/azure klasörü oluşturun:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Merhaba JSON dosyasını kopyalayın.

    VMSnapshotScriptPluginConfig.json toohello /etc/azure klasörüne kopyalayın.

4. Merhaba JSON dosyasını düzenleyin.

    Merhaba VMSnapshotScriptPluginConfig.json dosya tooinclude hello Düzenle `PreScriptLocation` ve `PostScriptlocation` parametreleri. Örneğin:

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

5. Merhaba, anlık görüntü öncesi ve anlık görüntü sonrası komut dosyalarını oluşturun.

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

    /Etc/Azure/pre_script.SQL için gereksinimlerinizi başına hello dosyasının Merhaba içeriğine değiştirin:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    /Etc/Azure/post_script.SQL için gereksinimlerinizi başına hello dosyasının Merhaba içeriğine değiştirin:

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

7. Merhaba betikleri sınayın.

    tootest hello komut dosyaları, ilk olarak, kök olarak oturum açın. Ardından, herhangi bir hata olduğundan emin olun:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Daha fazla bilgi için bkz: [Linux VM'ler için uygulamayla tutarlı yedekleme](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>5. adım: Hello VM yukarı tooback kullanım Azure kurtarma Hizmetleri kasaları

1.  İçinde Azure portal Merhaba, arama **kurtarma Hizmetleri kasaları**.

    ![Kurtarma Hizmetleri kasaları sayfası](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Merhaba üzerinde **kurtarma Hizmetleri kasaları** dikey, tooadd yeni bir kasa tıklayın **Ekle**.

    ![Kurtarma Hizmetleri kasaları Sayfası Ekle](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, tıklatın **myVault**.

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Merhaba üzerinde **myVault** dikey penceresinde tıklatın **yedekleme**.

    ![Kurtarma Hizmetleri kasaları sayfa yedekleme](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Merhaba üzerinde **yedekleme hedefi** dikey penceresinde, kullanım hello varsayılan değerleri **Azure** ve **sanal makine**. **Tamam** düğmesine tıklayın.

    ![Kurtarma Hizmetleri kasaları ayrıntı sayfaları](./media/oracle-backup-recovery/recovery_service_05.png)

6.  İçin **yedekleme İlkesi**, kullanın **DefaultPolicy**, ya da seçin **Yeni Oluştur ilke**. **Tamam** düğmesine tıklayın.

    ![Kurtarma Hizmetleri kasaları İlkesi ayrıntı sayfası yedekleme](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Merhaba üzerinde **sanal makine Seç** dikey penceresinde, select hello **myVM1** onay kutusunu işaretleyin ve ardından **Tamam**. Merhaba tıklatın **yedeklemeyi etkinleştir** düğmesi.

    ![Kurtarma Hizmetleri kasaları öğeleri toohello yedekleme Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Tıklattıktan sonra **yedeklemeyi etkinleştir**, hello yedekleme işlemi hello zamanlanmış süresi sona erene kadar başlamıyor. Sonraki adım hello tooset, tam hemen bir yedek ayarlama.

8.  Merhaba üzerinde **myVault - yedekleme öğeleri** dikey altında **yedekleme öğesi sayısı**, seçin hello yedekleme öğesi sayısı.

    ![Kurtarma Hizmetleri kasaları myVault Ayrıntı Sayfası](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Merhaba üzerinde **yedekleme öğeleri (Azure sanal makine)** hello sayfasının hello sağ taraftaki dikey tıklayın hello üç nokta (**...** ) düğmesine tıklayın ve ardından **Şimdi Yedekle**.

    ![Yedekleme şimdi komutu Kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_09.png)

10. Merhaba tıklatın **yedekleme** düğmesi. Merhaba yedekleme işlemi toofinish bekleyin. Ardından, çok Git[adım 6: kaldırmak hello veritabanı dosyalarını](#step-6-remove-the-database-files).

    Merhaba yedekleme işinin tooview hello durumu tıklatın **işleri**.

    ![Kurtarma Hizmetleri kasaları sayfa işi](./media/oracle-backup-recovery/recovery_service_10.png)

    Merhaba hello yedekleme işinin durumunu görüntü aşağıdaki hello görünür:

    ![Kurtarma Hizmetleri kasaları iş durumu sayfası](./media/oracle-backup-recovery/recovery_service_11.png)

11. Bir uygulama tutarlı yedekleme için hello günlük dosyasındaki hataları giderin. Merhaba günlük dosyası /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0 bulunur.

### <a name="step-6-remove-hello-database-files"></a>6. adım: hello veritabanı dosyaları kaldırın 
Bu makalenin sonraki bölümlerinde nasıl tootest hello kurtarma işlemi öğreneceksiniz. Merhaba kurtarma işlemi test etmeden önce tooremove hello veritabanı dosyaları sahiptir.

1.  Merhaba belirtilmedi ve yedekleme dosyalarını kaldırın:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (İsteğe bağlı) Merhaba Oracle örneğini kapatın:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Kurtarma Hizmetleri kasaları hello hello silinmiş dosyaları geri yükle
silinen dosyaları, aşağıdaki adımları tam hello toorestore hello:

1. Merhaba Hello Azure portal, arama *myVault* kurtarma Hizmetleri kasaları öğesi. Merhaba üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe hello sayısını seçin.

    ![Kurtarma Hizmetleri kasaları myVault yedekleme öğeleri](./media/oracle-backup-recovery/recovery_service_12.png)

2. Altında **yedekleme öğesi sayısı**, öğe hello sayısını seçin.

    ![Kurtarma Hizmetleri kasaları Azure sanal makine yedekleme öğesi sayısı](./media/oracle-backup-recovery/recovery_service_13.png)

3. Merhaba üzerinde **myvm1** dikey penceresinde tıklatın **dosya kurtarma (Önizleme)**.

    ![Dosya Kurtarma sayfası ekran görüntüsü hello kurtarma Hizmetleri kasaları](./media/oracle-backup-recovery/recovery_service_14.png)

4. Merhaba üzerinde **dosya kurtarma (Önizleme)** bölmesinde tıklatın **karşıdan yükleme komut dosyası**. Daha sonra hello yükleme (.sh) dosya tooa klasör hello istemci bilgisayara kaydedin.

    ![Yükleme komut dosyasını kaydetme seçenekleri](./media/oracle-backup-recovery/recovery_service_15.png)

5. Merhaba .sh dosya toohello VM kopyalayın.

    Aşağıdaki örnek hello nasıl güvenli kopyalama (scp) komut toomove toouse hello dosya toohello VM gösterir. Merhaba VM üzerinde ayarladığınız yeni dosyasındaki hello içeriği toohello Pano ve Yapıştır hello içeriği kopyalayabilirsiniz.

    > [!IMPORTANT]
    > Aşağıdaki örneğine hello hello IP adresi ve klasör değerleri güncelleştirdiğinizden emin olun. Merhaba değerleri hello dosyasının kaydedildiği toohello klasörü eşlemeniz gerekir.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Merhaba kök tarafından ait şekilde hello dosyasını değiştirin.

    Böylece hello kök tarafından ait aşağıdaki örneğine hello hello dosyasını değiştirin. Ardından, izinleri değiştirin.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Merhaba aşağıdaki örnek komut dosyası önceki hello çalıştırın, sonra gördükleri gösterir. Sorulduğunda toocontinue, girin **Y**.

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

7. Erişim toohello takılı birimleri onaylandı.

    tooexit, girin **q**ve takılı hello birimler için arama yapın. Merhaba listesini eklenen bir komut isteminde şunu girin toocreate **df -k**.

    ![Merhaba df -k komutu](./media/oracle-backup-recovery/recovery_service_16.png)

8. Komut dosyası toocopy hello eksik aşağıdaki kullanım hello dosyalar geri toohello klasörler:

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
9. Komut dosyası izleyen hello RMAN toorecover hello veritabanı kullanın:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Merhaba disk çıkarın.

    Merhaba hello üzerinde Azure portal'ın **dosya kurtarma (Önizleme)** dikey penceresinde tıklatın **çıkarın diskleri**.

    ![Diskleri komutunu çıkarın](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Geri yükleme tüm VM hello

Merhaba kurtarma Hizmetleri kasalarının hello silinen dosyaların geri yerine geri yükleyebileceğiniz tüm VM hello.

### <a name="step-1-delete-myvm"></a>1. adım: Sil myVM

*   Toohello Hello Azure portal, Git **myVM1** kasa ve ardından **silmek**.

    ![Kasa delete komutu](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>2. adım: hello VM kurtarma

1.  Çok Git**kurtarma Hizmetleri kasaları**ve ardından **myVault**.

    ![myVault giriş](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Merhaba üzerinde **genel bakış** dikey altında **yedekleme öğeleri**, öğe hello sayısını seçin.

    ![myVault öğeleri yedekleyin](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Merhaba üzerinde **yedekleme öğeleri (Azure sanal makine)** dikey penceresinde, select **myvm1**.

    ![Kurtarma VM sayfası](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Merhaba üzerinde **myvm1** dikey penceresinde hello üç nokta düğmesine (**...** ) düğmesine tıklayın ve ardından **geri VM**.

    ![VM komutu geri yükleme](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Merhaba üzerinde **seçin geri yükleme noktası** dikey penceresinde, toorestore istediğiniz ve ardından select hello öğesi **Tamam**.

    ![Select hello geri yükleme noktası](./media/oracle-backup-recovery/recover_vm_06.png)

    Uygulama tutarlı yedeklemeyi etkinleştirdiyseniz, dikey Mavi çubuk görüntülenir.

6.  Merhaba üzerinde **geri yükleme yapılandırmasını** dikey penceresinde, select hello sanal makine adı, hello kaynak grubu seçin ve ardından **Tamam**.

    ![Yapılandırma değerleri geri yükle](./media/oracle-backup-recovery/recover_vm_07.png)

7.  toorestore hello VM tıklatın hello **geri** düğmesi.

8.  tooview hello durumu hello geri yükleme işleminin **işleri**ve ardından **yedekleme işlerini**.

    ![Yedekleme işleri durumu komutu](./media/oracle-backup-recovery/recover_vm_08.png)

    Merhaba aşağıdaki şekilde hello hello geri yükleme işleminin durumunu gösterir:

    ![Merhaba geri yükleme işlemi durumu](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>3. adım: hello genel IP adresi ayarlama
Hello VM geri yüklendikten sonra hello ortak IP adresi ayarlamak.

1.  Merhaba arama kutusuna **genel IP adresi**.

    ![Ortak IP adresleri listesi](./media/oracle-backup-recovery/create_ip_00.png)

2.  Merhaba üzerinde **ortak IP adresleri** dikey penceresinde tıklatın **Ekle**. Merhaba üzerinde **ortak IP adresi oluştur** dikey penceresinde için **adı**seçin hello genel IP adı. **Kaynak grubu** olarak **Var olanı kullan**’ı seçin. Sonra, **Oluştur**’a tıklayın.

    ![IP adresi oluşturun](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello ortak IP adresiyle hello ağ arabirimi hello VM için arama için ve select **myVMip**. Ardından **ilişkilendirmek**.

    ![IP adresi ilişkilendirme](./media/oracle-backup-recovery/create_ip_02.png)

4.  İçin **kaynak türü**seçin **ağ arabirimi**. Merhaba myVM örneği tarafından kullanılan hello ağ arabirimi seçin ve ardından **Tamam**.

    ![Kaynak türü ve NIC değerleri seçin](./media/oracle-backup-recovery/create_ip_03.png)

5.  Arayın ve hello portalından verilen myVM hello örneği açın. Merhaba hello VM ile ilişkili IP adresi görünür hello myVM üzerinde **genel bakış** dikey.

    ![IP adresi değeri](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>4. adım: toohello VM bağlanma

*   tooconnect toohello VM, komut dosyası izleyen hello kullan:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>5. adım: hello veritabanı erişilebilir olup olmadığını sınamak
*   tootest erişilebilirlik, aşağıdaki komut dosyası kullan hello:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Merhaba, veritabanı **başlangıç** komut, bir hata, toorecover hello veritabanı oluşturur, bkz: [adım 6: kullanım RMAN toorecover hello veritabanı](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>6. adım: (İsteğe bağlı) kullanım RMAN toorecover hello veritabanı
*   toorecover hello veritabanı, aşağıdaki komut dosyası kullan hello:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Merhaba yedekleme ve kurtarma hello Oracle veritabanı 12c veritabanının Azure Linux VM'de şimdi tamamlandı.

## <a name="delete-hello-vm"></a>Merhaba VM silme

VM artık hello olduğunda komut tooremove hello kaynak grubu, hello VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Öğretici: yüksek oranda kullanılabilir sanal makineleri oluşturma](../../linux/create-cli-complete.md)

[VM dağıtımı Azure CLI örnekleri keşfedin](../../linux/cli-samples.md)



