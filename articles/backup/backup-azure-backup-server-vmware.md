---
title: "Azure yedekleme sunucusu VMware sunucularıyla yukarı aaaBack | Microsoft Docs"
description: "Azure yedekleme sunucusu tooback bir VMware vCenter/ESXi sunucuları tooAzure veya disk kullanın. Bu makalede adımı sağlar yedekleme (veya koruma) için adım adım yönerge = VMware iş yükleri."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a>VMware server tooAzure yedekleyin

Bu makalede korunmasına nasıl yardımcı tooconfigure Azure yedekleme sunucusu toohelp VMware sunucu iş yükleri açıklanmaktadır. Bu makalede Azure yedekleme sunucusu zaten olduğunu varsayar. Azure yedekleme sunucusu sahip değilseniz, bkz: [tooback Azure yedekleme sunucusu kullanarak iş yüklerini hazırlama](backup-azure-microsoft-azure-backup.md).

Azure yedekleme sunucusu yedeklemek veya VMware vCenter Server sürüm 6.5, 6.0 ve 5.5 korunmasına yardımcı olma.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Güvenli bağlantı toohello vCenter sunucusu oluşturma

Varsayılan olarak, Azure yedekleme sunucusu her bir HTTPS kanaldan vCenter Server ile iletişim kurar. tooturn hello güvenli iletişimi Azure yedekleme sunucusuna hello VMware sertifika yetkilisi (CA) sertifikası yüklemeniz önerilir. Güvenli iletişim gerektirmez ve toodisable hello HTTPS gereksinimi tercih ediyorsanız, bkz: [devre dışı bırak güvenli iletişim protokolü](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). Azure yedekleme sunucusu hello vCenter sunucusu arasında güvenli bir bağlantı toocreate hello Azure yedekleme sunucusu güvenilen sertifika içeri aktarın.

Genellikle, hello vSphere Web istemcisi aracılığıyla hello Azure yedekleme sunucusu makine tooconnect toohello vCenter Server sunucusunda bir tarayıcı kullanın. Merhaba hello Azure yedekleme sunucusu tarayıcı tooconnect toohello vCenter sunucusu, ilk kullanışınızda hello bağlantı güvenli değil. Görüntü aşağıdaki hello hello güvenli bağlantı gösterir.

![Güvenli bağlantı tooVMware sunucusu örneği](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix Bu sorun ve güvenli bir bağlantı oluşturmak, hello güvenilen kök CA sertifikaları indirin.

1. Azure yedekleme sunucusu üzerinde Hello tarayıcıda hello URL toohello vSphere Web istemcisi girin. Merhaba vSphere Web istemci oturum açma sayfası görüntülenir.

    ![vSphere Web istemcisi](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Yöneticiler ve geliştiriciler için hello bilgiler Hello altındaki hello bulun **indirme güvenilen kök CA sertifikaları** bağlantı.

    ![Bağlantı toodownload hello güvenilen kök CA sertifikaları](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Merhaba vSphere Web istemci oturum açma sayfası görmüyorsanız, tarayıcınızın proxy ayarlarını denetleyin.

2. Tıklatın **indirme güvenilen kök CA sertifikaları**.

    Merhaba vCenter Server dosya tooyour yerel bilgisayara yükler. Merhaba dosya adının adlı **karşıdan**. Tarayıcınıza bağlı olarak, aldığınız soran bir ileti olup olmadığını tooopen veya hello dosyasını kaydedin.

    ![sertifikaları indirildiğinde iletiyi yükle](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Merhaba dosya tooa konumu Azure yedekleme sunucusuna kaydedin. Merhaba dosyasını kaydettiğinizde, hello .zip dosya adı uzantısına ekleyin.

    Merhaba, hello hello sertifikalar hakkında bilgi içeren bir .zip dosyası dosyasıdır. Merhaba .zip uzantısı ile Merhaba ayıklama araçlarını kullanabilirsiniz.

4. Sağ **download.zip**ve ardından **tümünü Ayıkla** tooextract hello içeriği.

    Merhaba .zip dosyasını ayıklar adlı içeriği tooa klasörü **sertifikaları**. İki tür dosyası hello sertifikaları klasöründe yer alır. Merhaba kök sertifika dosyasını.0 ve.1 gibi numaralı bir dizi ile başlayan bir uzantı var.
    
    Merhaba CRL dosyası .r0 veya .r1 gibi bir dizi ile başlayan bir uzantı var. Merhaba CRL dosyası bir sertifika ile ilişkilidir.

    ![Yerel olarak ayıklanan dosyasını indirin ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. Merhaba, **sertifikaları** klasörünü hello kök sertifika dosyasını sağ tıklatın ve ardından **yeniden adlandırma**.

    ![Kök sertifikayı yeniden adlandırma ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Merhaba kök sertifikanın uzantısı too.crt değiştirin. Toochange hello uzantısı istediğinizden eminseniz tıklatın sorulduğunda **Evet** veya **Tamam**. Aksi takdirde hello dosyanın hedeflenen işlevini değiştirin. bir kök sertifikası temsil eden hello dosya değişiklikleri tooan simgesi Hello simgesi.

6. Merhaba kök sertifikayı sağ tıklatın ve hello açılır menüsünden seçin **sertifikayı yükle**.

    Merhaba **Sertifika Alma Sihirbazı'nı** iletişim kutusu görüntülenir.

7. Merhaba, **Sertifika Alma Sihirbazı'nı** iletişim kutusunda **yerel makine** hello sertifika ve ardından hello hedefi olarak **sonraki** toocontinue.

    ![Sertifika Depolama Hedef seçenekleri ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Tooallow değişiklikleri toohello bilgisayar isteyip istemediğinizi sorulursa tıklatın **Evet** veya **Tamam**, tooall hello değişiklikleri.

8. Merhaba üzerinde **sertifika deposu** sayfasında, **tüm sertifikaları deposu aşağıdaki hello Yerleştir**ve ardından **Gözat** toochoose hello sertifika deposu.

    ![Bir özel depolama nokta sertifikaları Yerleştir](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Merhaba **sertifika deposu Seç** iletişim kutusu görüntülenir.

    ![Sertifika depolama klasör hiyerarşisi](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Seçin **güvenilen kök sertifika yetkilileri** hello sertifikaları ve ardından için hello hedef klasör olarak **Tamam**.

    ![Sertifika hedef klasör](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Merhaba **güvenilen kök sertifika yetkilileri** klasörü hello sertifika deposu olarak onaylandı. **İleri**’ye tıklayın.

    ![Sertifika Deposu klasörü](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Merhaba üzerinde **Sertifika Alma Sihirbazı Tamamlanıyor hello** sayfasında, bu hello sertifika hello istenen klasöründe olduğunu doğrulayın ve ardından **son**.

    ![Sertifika hello uygun klasöründe olduğunu doğrulayın](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Bir iletişim kutusu görüntülenirse, hello başarılı sertifika alma doğrulanır.

11. Toohello vCenter Server tooconfirm, bağlantının güvenli olduğunu oturum açın.

  Merhaba sertifika içeri aktarma başarılı değil ve güvenli bir bağlantı kurulamıyor, hello VMware vSphere üzerinde belgelerine [sunucu sertifikaları alma](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Kuruluşunuz içinde güvenli sınırları olan ve hello HTTPS protokolünü üzerinde tooturn istemiyorsanız, aşağıdaki yordamı toodisable hello güvenli iletişim hello kullanın.

### <a name="disable-secure-communication-protocol"></a>Güvenli iletişim protokolü devre dışı bırak

Kuruluşunuz hello HTTPS protokolünü gerek yoksa, aşağıdaki adımları toodisable HTTPS hello kullanın. toodisable Merhaba varsayılan davranışı, hello varsayılan davranışı yoksayar bir kayıt defteri anahtarı oluşturun.

1. Metin bir .txt dosyasına aşağıdaki hello kopyalayıp yeniden açın.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Merhaba dosya tooyour Azure yedekleme sunucusu bilgisayara kaydedin. Merhaba dosya adı için DisableSecureAuthentication.reg kullanın.

3. Merhaba dosya tooactivate hello kayıt defteri girişini çift tıklatın.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Merhaba vCenter Server bir rol ve kullanıcı hesabı oluşturun

Merhaba vCenter sunucusu, bir önceden tanımlanmış bir dizi ayrıcalık rolüdür. Bir vCenter sunucusu Yöneticisi hello rolü oluşturur. tooassign izinleri Merhaba yönetici rol olan kullanıcı hesaplarını çiftleri. tooestablish hello gerekli kullanıcı kimlik bilgilerini tooback hello vCenter Server bilgisayarınızı belirli ayrıcalıklarına sahip bir rol oluşturmak ve ardından hello kullanıcı hesabı hello rolü ile ilişkilendir.

Azure yedekleme sunucusu kullanıcı adı ve parola tooauthenticate hello vCenter Server ile kullanır. Azure Backup sunucusu bu kimlik bilgileri tüm yedekleme işlemleri için kimlik doğrulaması olarak kullanır.

tooadd bir vCenter sunucusu rolü ve kendi ayrıcalıklarını bir yedekleme Yöneticisi için:

1. Oturum toohello vCenter Server ve ardından hello vcenter Server'daki **Gezgini** öğesine tıklayın **Yönetim**.

    ![VCenter Server gezinti panelinde yönetim seçeneği](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. İçinde **Yönetim** seçin **rolleri**ve ardından hello **rolleri** paneli tıklatın hello rol simgesi (Merhaba + simgesi) ekleyin.

    ![Rol Ekle](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Merhaba **Rol Oluştur** iletişim kutusu görüntülenir.

    ![Rolü oluşturma](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. Merhaba, **Rol Oluştur** iletişim kutusunda hello **rol adı** kutusuna *BackupAdminRole*. Merhaba rol adı ne olursa olsun, ister olabilir, ancak hello rolün amaçla tanınabilir olmalıdır.

4. VCenter'ün uygun sürümüne hello Hello ayrıcalıklarını seçin ve ardından **Tamam**. Aşağıdaki tablonun hello vCenter 6.0 ve vCenter 5.5 için gerekli hello ayrıcalıkları tanımlar.

  Merhaba ayrıcalıkları seçtiğinizde hello simgesi sonraki toohello üst etiket tooexpand hello üst ve görünüm hello alt ayrıcalıkları'ı tıklatın. tooselect hello VirtualMachine ayrıcalıkları, gereksinim duyduğunuz toogo hello birkaç düzeylerine üst alt hiyerarşisi. Tooselect üst ayrıcalık içindeki tüm alt ayrıcalıklar gerekmez.

  ![Üst alt ayrıcalık hiyerarşisi](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Tıklattıktan sonra **Tamam**, hello yeni rol görünür hello rolleri panelindeki hello listesinde.

|VCenter 6.0 için ayrıcalıkları| VCenter 5.5 için ayrıcalıkları|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Bir vCenter Server kullanıcı hesabı ve izinler oluşturma

Merhaba rol ayrıcalıklarıyla ayarladıktan sonra bir kullanıcı hesabı oluşturun. Merhaba kullanıcı hesabı adı ve parola kimlik doğrulaması için kullanılan hello kimlik bilgilerini sağlar sahiptir.

1. bir kullanıcı hesabında hello vCenter Server toocreate **Gezgini** öğesine tıklayın **kullanıcılar ve gruplar**.

    ![Kullanıcılar ve gruplar seçeneği](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Merhaba **vCenter kullanıcılar ve gruplar** panelinde görüntülenir.

    ![vCenter kullanıcılar ve gruplar paneli](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. Merhaba, **vCenter kullanıcılar ve gruplar** paneli, select hello **kullanıcılar** sekmesini ve sonra hello kullanıcılar simgesini (Merhaba + simgesi) ekleyin.

    Merhaba **yeni kullanıcı** iletişim kutusu görüntülenir.

3. Merhaba, **yeni kullanıcı** iletişim kutusunda, hello kullanıcının bilgileri ekleyin ve ardından **Tamam**. Bu yordamda BackupAdmin hello kullanıcı adınızdır.

    ![Yeni kullanıcı iletişim kutusu](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    Merhaba yeni kullanıcı hesabı hello listesinde görüntülenir.

4. Merhaba rolünde hello tooassociate hello kullanıcı hesabıyla **Gezgini** öğesine tıklayın **genel izinleri**. Merhaba, **genel izinleri** paneli, select hello **Yönet** sekmesini ve sonra hello simgesini (Merhaba + simgesi) ekleyin.

    ![Genel izinleri paneli](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Merhaba **genel izinleri kök - ekleme izni** iletişim kutusu görüntülenir.

5. Merhaba, **genel izin kök - ekleme izni** iletişim kutusu, tıklatın **Ekle** toochoose hello kullanıcı veya grup.

    ![Kullanıcı veya grup seçin](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Merhaba **kullanıcıları/Grupları Seç** iletişim kutusu görüntülenir.

6. Merhaba, **kullanıcıları/Grupları Seç** iletişim kutusunda, seçin **BackupAdmin** ve ardından **Ekle**.

    İçinde **kullanıcılar**, hello *etki alanı\kullanıcı adı* biçiminde hello kullanıcı hesabı için kullanılır. Farklı bir etki alanı toouse istiyorsanız, hello tercih **etki alanı** listesi.

    ![BackupAdmin kullanıcı ekleme](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Tıklatın **Tamam** tooadd hello seçili kullanıcıların toohello **ekleme izni** iletişim kutusu.

7. Merhaba kullanıcı tanımladınız, hello kullanıcı toohello rolü atayın. İçinde **atanan rolü**, hello aşağı açılan listeden seçin **BackupAdminRole**ve ardından **Tamam**.

    ![Kullanıcı toorole atayın](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Merhaba üzerinde **Yönet** hello sekmesinde **genel izinleri** panelinde, hello yeni kullanıcı hesabı ve ilişkili hello rol hello listesinde görünür.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>VCenter sunucusu kimlik bilgilerini Azure yedekleme sunucusu kurma

Merhaba VMware server tooAzure yedekleme sunucusu eklemeden önce yükleme [Azure yedekleme sunucusu için Güncelleştirme 1](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. Azure yedekleme sunucusu tooopen hello Azure yedekleme sunucusu masaüstünde hello simgesini çift tıklatın.

    ![Azure yedekleme sunucusu simgesi](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Merhaba masaüstünde hello simgesi bulamazsanız, Azure yedekleme sunucusu hello yüklü uygulamalar listesinden açın. Hello Azure yedekleme sunucusu uygulama adı, Microsoft Azure yedekleme denir.

2. Hello Azure yedekleme sunucusu konsolunda **Yönetim**, tıklatın **üretim sunucuları**ve hello araç şeridinde, ardından **yönetmek VMware**.

    ![Azure yedekleme sunucusu konsol](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Merhaba **kimlik bilgilerini Yönet** iletişim kutusu görüntülenir.

    ![Azure yedekleme sunucusu kimlik bilgilerini Yönet iletişim kutusu](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. Merhaba, **kimlik bilgilerini Yönet** iletişim kutusu, tıklatın **Ekle** tooopen hello **kimlik bilgileri Ekle** iletişim kutusu.

4. Merhaba, **kimlik bilgileri Ekle** iletişim kutusunda, bir ad ve hello yeni kimlik bilgisi için bir açıklama girin. Ardından hello kullanıcı adı ve parola belirtin. Merhaba adı *Contoso Vcenter kimlik bilgisi* kullanılan hello sonraki yordamda tooidentify hello kimlik bilgisi. Kullanım hello aynı kullanıcı adı ve için kullanılan parola hello vCenter Server. Merhaba vCenter Server ve Azure yedekleme sunucusu içinde değilse hello aynı etki alanı **kullanıcı adı**, hello etki alanını belirtin.

    ![Azure yedekleme sunucusu kimlik bilgileri Ekle iletişim kutusu](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Tıklatın **Ekle** tooadd hello yeni kimlik bilgisi tooAzure yedekleme sunucusu. Yeni bir kimlik bilgisi Hello görünür hello hello listesinde **kimlik bilgilerini Yönet** iletişim kutusu.
    
    ![Azure yedekleme sunucusu kimlik bilgilerini Yönet iletişim kutusu](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. tooclose hello **kimlik bilgilerini Yönet** iletişim kutusunda, hello **X** hello sağ üst köşedeki.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Merhaba vCenter Server tooAzure Yedekleme Sunucusu Ekle

Üretim Sunucusu Ekleme Sihirbazı'nı kullanılan tooadd hello vCenter Server tooAzure yedekleme sunucusu olur.

Üretim Sunucusu Ekleme Sihirbazı, aşağıdaki yordamın tam hello tooopen:

1. Hello Azure yedekleme sunucusu konsolunda **Yönetim**, tıklatın **üretim sunucuları**ve ardından **Ekle**.

    ![Açık Üretim Sunucusu Ekleme Sihirbazı](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Merhaba **Üretim Sunucusu Ekleme Sihirbazı'nı** iletişim kutusu görüntülenir.

    ![Üretim Sunucusu Ekleme Sihirbazı](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Merhaba üzerinde **üretim sunucusu seçin türü** sayfasında **VMware sunucuları**ve ardından **sonraki**.

3. İçinde **sunucu adı/IP adresi**, hello tam etki alanı adı (FQDN) veya hello VMware sunucusunun IP adresini belirtin. Tüm hello ESXi sunucuları hello tarafından yönetiliyorsa aynı vCenter hello vCenter adı kullanabilirsiniz.

    ![VMware server FQDN veya IP adresi belirtin](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. İçinde **SSL bağlantı noktası**, hello kullanılan toocommunicate hello VMware sunucusuyla bağlantı noktasını girin. Farklı bir bağlantı gerekli olduğunu bilmiyorsanız hello varsayılan bağlantı noktası, bağlantı noktası 443'ü kullanın.

5. İçinde **kimlik bilgisi belirtin**, hello daha önce oluşturduğunuz kimlik bilgisi seçin.

    ![Kimlik bilgisi belirtin](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Tıklatın **Ekle** tooadd hello VMware sunucu toohello listesi **eklenen VMware sunucuları**ve ardından **sonraki** toomove toohello sonraki sayfaya hello Sihirbazı.

    ![VMWare server ve kimlik bilgisi Ekle](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. Merhaba, **Özet** sayfasında, **Ekle** tooadd hello belirtilen VMware server tooAzure yedekleme sunucusu.

    ![VMware server tooAzure Yedekleme Sunucusu Ekle](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  Merhaba VMware server yedekleme aracısız yedeğidir ve hello yeni sunucu hemen eklenir. Merhaba **son** sayfasında sonuçları hello gösterir.

  ![Son sayfası](./media/backup-azure-backup-server-vmware/summary-screen.png)

  vCenter Server tooAzure yedekleme sunucusu, yineleme hello önceki birden çok örneğini bu bölümdeki adımları tooadd.

Merhaba vCenter Server tooAzure yedekleme sunucusu ekledikten sonra hello sonraki toocreate bir koruma grubu adımdır. Merhaba koruma grubu kısa veya uzun vadeli bekletme için çeşitli detayları hello ve burada tanımlayın ve hello yedekleme ilkesini uygulamak olduğunu belirtir. Merhaba yedekleme İlkesi, yedeklemeler olduğunda ve ne yedeklenir hello zamanlamadır.


## <a name="configure-a-protection-group"></a>Bir koruma grubunu yapılandırın

System Center Data Protection Manager veya Azure yedekleme sunucusu önce kullanmadıysanız bkz [planlama disk yedeklemeleri](https://technet.microsoft.com/library/hh758026.aspx) tooprepare donanım ortamınızı. Uygun depolama alanına sahip denetledikten sonra hello yeni koruma grubu oluşturma Sihirbazı'nı tooadd VMware sanal makineleri kullanın.

1. Hello Azure yedekleme sunucusu konsolunda **koruma**, hello araç şeridinde tıklatıp **yeni** tooopen hello yeni koruma grubu oluşturma Sihirbazı.

    ![Açık hello yeni koruma grubu oluşturma Sihirbazı](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Merhaba **yeni koruma grubu oluşturma** Sihirbazı iletişim kutusu görüntülenir.

    ![Yeni koruma grubu oluşturma Sihirbazı iletişim kutusu](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Tıklatın **sonraki** tooadvance toohello **koruma grubu türünü seçin** sayfası.

2. Merhaba üzerinde **seçin koruma grubu türünü** sayfasında **sunucuları** ve ardından **sonraki**. Merhaba **grup üyelerini seçin** sayfası görüntülenir.

3. Merhaba üzerinde **grup üyelerini seçin** sayfası, hello kullanılabilir üyeler ve seçili hello üyeleri görünür. Tooprotect istediğiniz ve ardından hello üyeleri seçin **sonraki**.

    ![Grup üyelerini seçin](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Diğer klasörlere veya sanal makineleri içeren bir klasör seçerseniz bir üye seçin, bu klasör ve VM'ler da seçilir. Merhaba ekleme hello klasör ve VM'ler hello üst klasörde klasör düzeyinde koruma adı verilir. tooremove bir klasör veya VM, Temizle hello onay kutusu.

    Bir VM veya bir VM'yi içeren bir klasör zaten korumalı tooAzure ise, bu VM yeniden seçemezsiniz. Bir VM korumalı tooAzure olduktan sonra diğer bir deyişle, onu yeniden yinelenen kurtarma noktaları için bir VM oluşturulmasını engeller korunamaz. Hangi Azure yedekleme sunucusu örneği zaten koruyan bir üye, noktası toohello üye toosee hello sunucusunu koruyan hello adını toosee istiyorsanız.

4. Merhaba üzerinde **veri koruma yöntemini seçin** sayfasında, hello koruma grubu için bir ad girin. Kısa vadeli koruma (toodisk) ve çevrimiçi koruma seçilir. Toouse çevrimiçi koruma (tooAzure) isterseniz, kısa vadeli koruma toodisk kullanmanız gerekir. Tıklatın **sonraki** tooproceed toohello kısa vadeli koruma aralık.

    ![Veri koruma yöntemini seçin](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Merhaba üzerinde **kısa vadeli hedefleri belirtin** sayfası için **bekletme aralığı**, hello tooretain kurtarma noktaları istediğiniz gün sayısını belirtin *depolanan toodisk*. Toochange hello zaman ve ne zaman kurtarma noktaları alınır gün istiyorsanız, **Değiştir**. Merhaba kısa vadeli kurtarma noktaları tam yedeklemeler edilir. Artımlı yedeklemeler değiller. Merhaba kısa vadeli hedefleri ile memnun kaldığınızda, tıklatın **sonraki**.

    ![Kısa vadeli hedefleri belirtin](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Merhaba üzerinde **Disk ayırmayı gözden** sayfasında, gözden geçirin ve gerekirse hello VM'ler için hello disk alanını değiştirin. Merhaba önerilen disk ayırmaları hello belirtilen hello bekletme aralığı temel **kısa vadeli hedefleri belirtin** sayfasında, iş yükü hello türü ve hello hello boyutunu korunan verileri (3. adımda tanımlanan).  

  - **Veri boyutu:** hello koruma grubundaki hello verilerin boyutu.
  - **Disk alanı:** hello hello koruma grubu için disk alanı miktarını önerilir. Bu ayar toomodify istiyorsanız, her veri kaynağı büyür tahmin hello miktardan biraz daha büyük toplam alan ayırın.
  - **Verileri birlikte bulundurma:** üzerinde birlikte bulundurmaya kapatırsanız, birden çok veri kaynağı hello koruma tooa tek çoğaltma ve kurtarma noktası birimi eşleyebilirsiniz. Birlikte bulundurma, tüm iş yükleri için desteklenmez.
  - **Otomatik olarak Büyüt:** hello ilk ayırma hello korumalı gruptaki veri boyutunu aşarsa bu ayarı üzerinde kapatma, System Center Data Protection Manager tooincrease hello disk boyutu yüzde 25 ile çalışır..
  - **Depolama havuzu ayrıntıları:** hello depolama havuzu kalan disk boyutu ve toplam dahil hello durumunu gösterir.

    ![Disk ayırmayı İncele](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Merhaba alanı ayırma ile memnun kaldığınızda, tıklatın **sonraki**.

7. Merhaba üzerinde **çoğaltma oluşturma yöntemini seçin** sayfasında, nasıl toogenerate hello ilk kopyalama ya da Azure yedekleme sunucusu üzerindeki hello korumalı verilere yönelik çoğaltma istediğinizi belirtin.

    Merhaba varsayılandır **hello ağ üzerinden otomatik olarak** ve **şimdi**. Merhaba varsayılan kullanırsanız, yoğun olmayan bir zamanı belirtin öneririz. Seçin **sonra** ve gününü ve saatini belirtin.

    Büyük miktarlarda veri veya en iyi durumdan daha az ağ koşulları için Çıkarılabilir medya kullanarak çevrimdışı hello veri çoğaltmayı düşünebilirsiniz.

    Seçimlerinizi yaptıktan sonra tıklatın **sonraki**.

    ![Çoğaltma oluşturma yöntemini seçin](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Merhaba üzerinde **tutarlılık denetimi seçenekleri** nasıl ve ne zaman tooautomate hello tutarlılık denetimlerinin sayfasında, seçin. Çoğaltma verileri tutarsız hale geldiğinde veya belirlenmiş bir zamanlamaya üzerinde tutarlılık denetimleri çalıştırabilirsiniz.

    Tooconfigure otomatik tutarlılık denetimlerinin istemiyorsanız, el ile denetim çalıştırabilirsiniz. Merhaba koruma bölmesinde hello Azure yedekleme sunucusu konsolunun hello koruma grubuna sağ tıklayın ve ardından **tutarlılık denetimi gerçekleştir**.

    Tıklatın **sonraki** toomove toohello sonraki sayfa.

9. Merhaba üzerinde **çevrimiçi koruma verilerini belirtin** sayfasında, tooprotect istediğiniz bir veya daha fazla veri kaynağını seçin. Merhaba üyeleri ayrı ayrı seçin veya tıklatın **Tümünü Seç** toochoose tüm üyeleri. Merhaba üyeleri seçtikten sonra tıklatın **sonraki**.

    ![Çevrimiçi koruma verilerini belirtin](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Merhaba üzerinde **çevrimiçi yedekleme zamanlamasını belirtin** sayfasında, hello disk yedeğinden hello zamanlama toogenerate kurtarma noktalarını belirtin. Merhaba kurtarma noktası oluşturulduktan sonra Azure kurtarma Hizmetleri kasasına aktarılan toohello var. İle çevrimiçi yedekleme zamanlamasını hello memnun kaldığınızda, tıklatın **sonraki**.

    ![Çevrimiçi Yedekleme zamanlamasını belirtin](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Merhaba üzerinde **çevrimiçi bekletme ilkesini belirtin** sayfasında, ne kadar süreyle tooretain hello yedek verileri Azure istediğinizi belirtin. Hello İlkesi tanımlandıktan sonra tıklatın **sonraki**.

    ![Çevrimiçi bekletme ilkesini belirtin](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Ne kadar veri Azure'da tutabilirsiniz için süre sınırı yoktur. Kurtarma noktası verilerini Azure'da depoladığınızda hello yalnızca korumalı örneği başına birden fazla 9999 kurtarma noktaları olamaz sınırıdır. Bu örnekte, hello korumalı örneği hello VMware sunucusudur.

12. Merhaba üzerinde **Özet** sayfasında, ayarları ve koruma grubu üyeleri için hello ayrıntılarını gözden geçirin ve ardından **Grup Oluştur**.

    ![Koruma grubu üyesi ve ayar özeti](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Sonraki adımlar
Azure yedekleme sunucusu tooprotect VMware iş yükleri kullanırsanız, Azure yedekleme sunucusu toohelp korumak kullanarak ilgilenebilirsiniz bir [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [Microsoft SharePoint grubu](./backup-azure-backup-sharepoint-mabs.md), veya bir [SQL Server veritabanı](./backup-azure-sql-mabs.md).

Merhaba aracısını kaydetmeden sorunları hakkında daha fazla bilgi için bkz: hello koruma grubu yapılandırma veya işler, yedekleme [sorun giderme Azure yedekleme sunucusu](./backup-azure-mabs-troubleshoot.md).
