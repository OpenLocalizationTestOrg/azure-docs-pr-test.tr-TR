---
title: "bir Azure Linux sanal makine üzerinde Oracle ASM yukarı aaaSet | Microsoft Docs"
description: "Hızlı bir şekilde Oracle ASM yukarı ve Azure ortamınızda çalışan alın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Bir Azure Linux sanal makinede Oracle ASM ayarlayın  

Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar. Bu öğretici hello yükleme ve yapılandırma, Oracle otomatik Depolama Yönetimi (ASM) ile birlikte temel Azure sanal makine dağıtımı kapsar.  Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:

> [!div class="checklist"]
> * Oluştur ve tooan Oracle veritabanı VM Bağlan
> * Yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma
> * Oracle kılavuz altyapısını yükleme ve yapılandırma
> * Bir Oracle ASM Yüklemeyi Başlat
> * ASM tarafından yönetilen bir Oracle DB oluştur


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Merhaba ortamını hazırlayın

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

toocreate bir kaynak grubu kullanmak hello [az grubu oluşturma](/cli/azure/group#create) komutu. Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir kapsayıcısıdır. Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello içinde *eastus* bölge.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>VM oluşturma

toocreate bir sanal makine hello Oracle veritabanı görüntüyü temel alarak ve toouse Oracle ASM yapılandırmak, hello kullanma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnek Standard_DS2_v2 boyutu 50 GB dört eklenen veri disklerini ile myVM adlı VM oluşturur. Merhaba varsayılan anahtar konumunda Bunlar zaten yoksa, ayrıca SSH anahtarları oluşturur.  toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Merhaba VM oluşturduktan sonra Azure CLI aşağıdaki örneğine benzer toohello bilgileri görüntüler. Not hello değeri `publicIpAddress`. Bu adres tooaccess hello VM kullanın.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Toohello VM Bağlan

toocreate ile SSH oturumu bir VM Merhaba ve diğer ayarları yapılandırmak, komutu aşağıdaki hello kullanın. Başlangıç IP adresi ile hello yerine `publicIpAddress` , VM için değer.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Oracle ASM yükleyin

Oracle ASM, aşağıdaki adımları tam hello tooinstall. 

Oracle ASM yükleme hakkında daha fazla bilgi için bkz: [ASMLib Oracle yüklemeler için Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).  

1. Sipariş toocontinue ASM yüklemesiyle kök olarak toologin gerekir:

   ```bash
   sudo su -
   ```
   
2. Bu ek komutlar tooinstall Oracle ASM bileşenleri çalıştırın:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Oracle ASM yüklü olduğunu doğrulayın:

   ```bash
   rpm -qa |grep oracleasm
   ```

    Bu komutun çıktısı Hello bileşenleri aşağıdaki hello listesi:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM belirli kullanıcılar ve sipariş toofunction rollerinde doğru gerektirir. Aşağıdaki komutları hello hello önkoşul kullanıcı hesapları ve grupları oluşturun: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Kullanıcılar ve gruplar oluşturulduğundan doğru doğrulayın:

   ```bash
   id grid
   ```

    Merhaba bu komutun çıktısı hello listesi kullanıcılar ve gruplar:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Kullanıcı için bir klasör oluşturun *kılavuz* ve hello sahibi:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Oracle ASM ayarlayın

Bu öğretici için hello varsayılan kullanıcıdır *kılavuz* ve hello varsayılan grup *asmadmin*. Bu hello olun *oracle* kullanıcı hello asmadmin grubunun bir parçasıdır. Oracle ASM yüklemenizi, aşağıdaki adımları tam hello yukarı tooset:

1. Merhaba Oracle ASM kitaplığı sürücüsünü ayarı içerir hello varsayılan kullanıcı (Kılavuz) ve varsayılan grup (asmadmin) tanımlama hello sürücü toostart önyükleme yapılandırma yanı sıra (y seçin) ve önyükleme disklerde tooscan (y seçin). Tooanswer hello hello komutu aşağıdaki istemleri gerekir:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   Bu komutun çıktısı Hello izleyerek, yanıtlanan istemleri toobe ile durdurma benzer toohello görünmelidir.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Görünüm hello disk yapılandırması:
   ```bash
   cat /proc/partitions
   ```

   Bu komutun çıktısı Hello benzer toohello kullanılabilir diskleri listesi aşağıdaki gibi görünmelidir

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Biçim disk */dev/sdc* hello çalıştırarak komutu aşağıdaki ve hello yanıtlama ile ister:
   - *n*Yeni bölüm için
   - *p* birincil bölüm
   - *1* tooselect hello ilk bölüm
   - basın `enter` hello varsayılan ilk silindir için
   - basın `enter` hello varsayılan son silindir için
   - basın *w* toowrite hello değişiklikleri toohello bölümleme tablosu  

   ```bash
   fdisk /dev/sdc
   ```
   
   Yukarıda verilen hello yanıtlar kullanarak hello çıktı hello fdisk komutu için hello aşağıdaki gibi görünmelidir:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Yineleme hello Fdisk komutu için önceki `/dev/sdd`, `/dev/sde`, ve `/dev/sdf`.

5. Merhaba disk yapılandırmasını kontrol edin:

   ```bash
   cat /proc/partitions
   ```

   Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Merhaba Oracle ASM hizmet durumunu denetleyin ve hello Oracle ASM hizmetini başlatın:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Oracle ASM diskleri oluşturun:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Oracle ASM diskleri listele:

   ```bash
   service oracleasm listdisks
   ```   

   Merhaba hello komutunun çıkışını Oracle ASM diskleri aşağıdaki hello listesi:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Merhaba kök, oracle ve kılavuz kullanıcıların Hello parolalarını değiştirin. **Bu yeni parolalar Not** daha sonra hello yükleme sırasında kullandığınız gibi.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Başlangıç klasörü iznini değiştirin:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Karşıdan yükle ve Oracle kılavuz altyapıyı hazırlama

toodownload ve hello Oracle kılavuz altyapısı yazılımı, aşağıdaki adımları tam hello hazırlayın:

1. Oracle kılavuz altyapı hello indirme [Oracle ASM indirme sayfası](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   Başlıklı hello indirme altında **Oracle veritabanı Linux x86-64 12c sürüm 1 kılavuz altyapısına (12.1.0.2.0)**, hello iki .zip dosyalarını indirin.

2. Merhaba .zip dosyaları tooyour istemci bilgisayara indirdikten sonra güvenli kopyalama Protokolü (SCP) toocopy hello dosyaları tooyour VM kullanabilirsiniz:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH, Oracle VM sipariş toomove hello .zip dosyalarıyla hello Azure geri / klasör iptal et. Ardından, hello dosyaları hello sahibini değiştirin:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Merhaba dosyaları ayıklayın. (Yükleme hello Linux sıkıştırmasını aracı önceden yüklüyse.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. Değiştirme izni:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Yapılandırılan güncelleştirme takas alanı. Oracle kılavuz bileşenleri en az 6.8 GB takas alanı tooinstall kılavuz gerekir. Oracle Linux görüntüleri için azure'da Hello varsayılan takas dosya boyutu yalnızca 2048 MB'tır. Tooincrease gerek `ResourceDisk.SwapSizeMB` hello içinde `/etc/waagent.conf` dosya ve güncelleştirilmiş hello ayarları tootake etkisi sırayla hello WALinuxAgent hizmetini yeniden başlatın. Salt okunur bir dosya olduğundan, toochange dosya izinleri tooenable yazma erişimi gerekir.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Arama `ResourceDisk.SwapSizeMB` değiştirip hello değeri çok**8192**. Toopress gerekir `insert` tooenter ekleme modu, hello değeri türü **8192** ve tuşuna basarak `esc` tooreturn toocommand modu. toowrite hello değişiklikleri ve çıkma hello dosya türünü `:wq` ve basın `enter`.
   
   > [!NOTE]
   > Her zaman kullanmanız önerilir `WALinuxAgent` tooconfigure takas alanı böylece her zaman hello yerel diskteki kısa ömürlü (geçici disk) en iyi performans için oluşturulur. Daha fazla bilgi için bkz: [nasıl tooadd bir takas dosyası Linux Azure sanal makinelerinde](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Yerel istemci ve VM toorun x11 hazırlama
Oracle ASM yapılandırma, bir grafik arabirim toocomplete hello yükleme ve yapılandırma gerektirir. Bu yükleme hello x11 Protokolü toofacilitate kullanıyoruz. X11 zaten olan bir istemci sistem (Mac veya Linux) kullanıyorsanız, özellikleri etkinleştirilmiş ve yapılandırılmış - bu yapılandırmasını atla ve özel tooWindows makineler kurulumu. 

1. [PuTTY karşıdan](http://www.putty.org/) ve [Xming karşıdan](https://xming.en.softonic.com/) tooyour Windows bilgisayarı. Merhaba varsayılan değerlerle devam etmeden önce bu uygulamaların her ikisi de toocomplete hello yüklemesi gerekir.

2. PuTTY yükledikten sonra bir komut istemi açın, hello PuTTY klasörünü (örneğin, C:\Program Files\PuTTY) değiştirin ve çalıştırın `puttygen.exe` içinde bir anahtar toogenerate sipariş.

3. PuTTY anahtar oluşturma Aracı'nda:
   
   1. Merhaba seçerek bir anahtar oluşturmak `Generate` düğmesi.
   2. Başlangıç anahtarı (Ctrl + C) Hello içeriğini kopyalayın.
   3. Select hello `Save private key` düğmesi.
   4. Başlangıç anahtarı bir parola ile güvenli hale getirme hakkında hello uyarıyı yok sayın ve ardından `OK`.

   ![PuTTY anahtar oluşturucunun ekran görüntüsü](./media/oracle-asm/puttykeygen.png)

4. VM'nizi, şu komutları çalıştırın:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Adlı bir dosya oluşturun `authorized_keys`. Bu dosyada hello anahtar Hello içeriğini yapıştırın ve hello dosyasını kaydedin.

   > [!NOTE]
   > başlangıç anahtarı hello dize içermelidir `ssh-rsa`. Ayrıca, başlangıç anahtarı Merhaba içeriğine tek satırlık metin olmalıdır.
   >  

6. İstemci sisteminizde Putty'yi başlatın. Merhaba, **kategori** bölmesinde çok Git**bağlantı** > **SSH** > **Auth**. Merhaba, **kimlik doğrulama için özel anahtar dosyası** kutusunda, daha önce oluşturulan toohello anahtarı göz atın.

   ![Merhaba SSH kimlik doğrulaması seçeneklerinin ekran görüntüsü](./media/oracle-asm/setprivatekey.png)

7. Merhaba, **kategori** bölmesinde çok Git**bağlantı** > **SSH** > **X11**. Select hello **X11 Enable iletimi** onay kutusu.

   ![Ekran görüntüsü hello SSH X11 seçenekleri iletme](./media/oracle-asm/enablex11.png)

8. Merhaba, **kategori** bölmesinde çok Git**oturum**. Oracle ASM VM girin `<publicIPaddress>` hello ana bilgisayar adı iletişim kutusunda, yeni bir dolgu `Saved Session` adlandırın ve ardından tıklatın `Save`.  Kaydedildikten sonra tıklayın `open` tooconnect tooyour Oracle ASM sanal makine.  Merhaba, bağlandığınız ilk kez uyarı hello uzak sistem, kayıt defterinde önbelleğe alınmaz. Tıklayın `yes` tooadd onu ve devam edin.

   ![Merhaba PuTTY oturum seçeneklerinin ekran görüntüsü](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Oracle kılavuz altyapısı yükleme

tooinstall Oracle kılavuz altyapı, aşağıdaki adımları tam hello:

1. Olarak oturum açın **kılavuz**. (İçin bir parola istenmesini olmadan mümkün toosign olmalıdır.) 

   > [!NOTE]
   > Windows çalıştırıyorsanız, hello yüklemeye başlamadan önce Xming başlatıldığından emin olun.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Oracle kılavuz altyapı 12c sürüm 1 yükleyicisi açılır. (Merhaba yükleyici toostart birkaç dakika sürebilir.)

2. Merhaba üzerinde **yükleme seçeneği** sayfasında **yüklenir ve tek başına bir sunucu için Oracle kılavuz altyapı yapılandırma**.

   ![Merhaba Yükleyicisi'nin yükleme seçeneği sayfasının ekran görüntüsü](./media/oracle-asm/install01.png)

3. Hello üzerinde **ürün dilleri seçin** sayfasında, olun **İngilizce** veya istediğiniz hello dil seçilidir.  `next` öğesine tıklayın.

4. Merhaba üzerinde **ASM Disk grubu oluşturma** sayfa:
   - Merhaba disk grubu için bir ad girin.
   - Altında **artıklık**seçin **dış**.
   - Altında **ayırma birimi boyutu**seçin **4**.
   - Altında **disk Ekle**seçin **ORCLASMSP**.
   - `next` öğesine tıklayın.

5. Merhaba üzerinde **belirtin ASM parola** sayfası, select hello **bu hesaplar için aynı parolayı kullanın** seçeneği ve bir parola girin.

   ![Merhaba Yükleyicisi'nin belirtin ASM parola sayfasının ekran görüntüsü](./media/oracle-asm/install04.png)

6. Merhaba üzerinde **yönetimi seçeneklerini belirtin** sayfasında hello seçeneği tooconfigure EM bulut denetim sahip. Biz bu seçenek atlanıyor - tıklatın `next` toocontinue. 

7. Merhaba üzerinde **ayrıcalıklı işletim sistemi gruplarına** sayfasında, hello varsayılan ayarları kullanın. Tıklatın `next` toocontinue.

8. Merhaba üzerinde **yükleme konumu belirtin** sayfasında, hello varsayılan ayarları kullanın. Tıklatın `next` toocontinue.

9. Merhaba üzerinde **Envanter Oluştur** sayfasında, hello stok dizini çok değiştirmek`/u01/app/grid/oraInventory`. Tıklatın `next` toocontinue.

   ![Merhaba Yükleyicisi'nin Envanter Oluştur sayfasının ekran görüntüsü](./media/oracle-asm/install08.png)

10. Merhaba üzerinde **kök komut dosyası yürütme Yapılandırması** sayfası, select hello **otomatik yapılandırma komut dosyaları çalıştırmak** onay kutusu. Merhaba seçip **"root" kullanıcı kimlik bilgisi kullanma** seçeneği ve hello kök kullanıcı parolasını girin.

    ![Merhaba Yükleyicisi'nin kök komut dosyası yürütme yapılandırma sayfasının ekran görüntüsü](./media/oracle-asm/install09.png)

11. Merhaba üzerinde **gerçekleştirmek önkoşul denetler** sayfasında hello geçerli kurulumu başarısız olur hatalarla. Bu beklenen bir davranıştır. `Fix & Check Again` öğesini seçin.

12. Merhaba, **düzeltmesi betik** iletişim kutusu, tıklatın `OK`.

13. Merhaba üzerinde **Özet** sayfasında, seçtiğiniz ayarları gözden geçirin ve ardından `Install`.

    ![Merhaba Yükleyicisi'nin Özet sayfasının ekran görüntüsü](./media/oracle-asm/install12.png)

14. Toobe ayrıcalıklı bir kullanıcı olarak çalıştırmanız gerekir, yapılandırma komut bildiren bir uyarı iletişim kutusu görüntülenir. Tıklatın `Yes` toocontinue.

15. Merhaba üzerinde **son** sayfasında, `Close` toofinish hello yükleme.

## <a name="set-up-your-oracle-asm-installation"></a>Oracle ASM yüklemenizi ayarlayın

Oracle ASM yüklemenizi, aşağıdaki adımları tam hello yukarı tooset:

1. Hala oturum açmaya olarak olun **kılavuz**, sizin X11 gelen oturum. Toohit gerekebilecek `enter` toorevive hello terminal. Ardından hello Oracle otomatik Depolama Yönetimi yapılandırma Yardımcısı'nı başlatın:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Oracle ASM yapılandırma Yardımcısı'nı açar.

2. Merhaba, **yapılandırma ASM: Disk gruplarının** iletişim kutusunda, hello `Create` düğmesine tıklayın ve ardından `Show Advanced Options`.

3. Merhaba, **Disk grubu oluşturma** iletişim kutusunda:

   - Merhaba disk grubu adı girin **veri**.
   - Altında **üye diskleri Seç**seçin **ORCL_DATA** ve **ORCL_DATA1**.
   - Altında **ayırma birimi boyutu**seçin **4**.
   - Tıklatın `ok` toocreate hello disk grubu.
   - Tıklatın `ok` tooclose hello onay penceresi.

   ![Merhaba Disk grubu oluştur iletişim kutusunun ekran görüntüsü](./media/oracle-asm/asm02.png)

4. Merhaba, **yapılandırma ASM: Disk gruplarının** iletişim kutusunda, hello `Create` düğmesine tıklayın ve ardından `Show Advanced Options`.

5. Merhaba, **Disk grubu oluşturma** iletişim kutusunda:

   - Merhaba disk grubu adı girin **FRA**.
   - Altında **artıklık**seçin **dış (hiçbiri)**.
   - Altında **üye diskleri Seç**seçin **ORCL_FRA**.
   - Altında **ayırma birimi boyutu**seçin **4**.
   - Tıklatın `ok` toocreate hello disk grubu.
   - Tıklatın `ok` tooclose hello onay penceresi.

   ![Merhaba Disk grubu oluştur iletişim kutusunun ekran görüntüsü](./media/oracle-asm/asm04.png)

6. Seçin **çıkış** tooclose ASM yapılandırma Yardımcısı.

   ![Ekran görüntüsü hello yapılandırma ASM: çıkış düğmesi Disk gruplar iletişim kutusu](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Merhaba veritabanı oluşturma

Oracle veritabanı yazılımını Hello hello Azure Market görüntüsü üzerinde zaten yüklü. toocreate bir veritabanı, şu adımları tam hello:

1. Kullanıcıların toohello Oracle süper kullanıcı geçin ve günlüğe kaydetme için hello dinleyici başlatılamadı:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Veritabanı yapılandırma Yardımcısı'nı açar.

2. Merhaba üzerinde **veritabanı işlemi** sayfasında, `Create Database`.

3. Merhaba üzerinde **oluşturma modu** sayfa:

   - Merhaba veritabanı için bir ad girin.
   - İçin **depolama türü**, olun **otomatik Depolama Yönetimi (ASM)** seçilir.
   - İçin **veritabanı dosya konumu**, hello varsayılan kullanmak ASM önerilen konum.
   - İçin **Hızlı Kurtarma alanında**, hello varsayılan kullanmak ASM önerilen konum.
   - yazın bir **yönetici parolasını** ve **parolayı onaylayın**.
   - olun `create as container database` seçilir.
   - yazın bir `pluggable database name` değeri.

4. Merhaba üzerinde **Özet** sayfasında, seçtiğiniz ayarları gözden geçirin ve ardından `Finish` toocreate hello veritabanı.

   ![Merhaba Özet sayfasının ekran görüntüsü](./media/oracle-asm/createdb03.png)

5. Merhaba veritabanı oluşturuldu. Merhaba üzerinde **son** sayfasında, bu veritabanı toounlock ek hesapları toouse seçeneği ve hello parolalarını değiştirme hello sahip. Bunu toodo istiyorsanız seçin **parola yönetimi** -Aksi takdirde tıklayın `close`.

## <a name="delete-hello-vm"></a>Merhaba VM silme

Oracle otomatik Depolama Yönetimi, hello Oracle DB hello Azure Market görüntüsünden üzerinde başarıyla yapılandırdınız.  Bu VM artık gerektiğinde komutu tooremove hello kaynak grubu, VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Öğretici: Oracle DataGuard yapılandırın](configure-oracle-dataguard.md)

[Öğretici: Oracle GoldenGate yapılandırın](Configure-oracle-golden-gate.md)

Gözden geçirme [bir Oracle DB Mimari](oracle-design.md)
