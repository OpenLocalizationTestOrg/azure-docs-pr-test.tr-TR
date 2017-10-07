---
title: "aaaHow Azure RemoteApp kullanıcı verilerini ve ayarları? | Microsoft Belgeleri"
description: "Azure RemoteApp hello kullanıcı profili diski kullanarak kullanıcı verilerini nasıl kaydeder öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Azure RemoteApp, kullanıcı verilerini ve ayarlarını nasıl kaydedilsin mi?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp, aygıtları ve oturumlar kullanıcı kimliği ve özelleştirmeleri kaydeder. Bu kullanıcı verileri bir kullanıcı profili diski (UPD) bilinen bir kullanıcı başına koleksiyona göre disk depolanır. Merhaba disk hello kullanıcı izler ve burada oturum bağımsız olarak tutarlı bir deneyim hello kullanıcının sahip sağlar.

Kullanıcı profili diskleri olan tamamen saydam toohello kullanıcı — kullanıcıların belgeleri tootheir Belgeler klasörünü (ne toobe yerel bir sürücünün bulunur) kaydedin ve uygulama ayarlarına normal olarak değiştirin. AT hello aynı zaman, tüm kişisel ayarları kalıcı tooAzure RemoteApp herhangi bir aygıttan bağlanırken. Tüm hello kullanıcının gördüğü olduğu hello verilerini aynı yerde.

Her UPD 50 GB kalıcı depolama vardır ve her iki kullanıcı verileri ve uygulama ayarlarını içerir. 

Kullanıcı profili verilerini özellikleri için okumaya devam edin.

> [!NOTE]
> Toodisable UPD hello? Bu artık - Pavithra'nın blog gönderisi kullanıma yapabileceğiniz [devre dışı kullanıcı profili diskleri (UPD) Azure remoteapp'te](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), Ayrıntılar için.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Nasıl bir yönetici toohello veri alabilir miyim?
Kullanıcılarınız (için olağanüstü durum kurtarma veya hello kullanıcı hello şirketten ayrılması durumunda) biri için tooaccess hello veri gerekiyorsa, Azure desteğine başvurun ve hello koleksiyonu ve hello kullanıcı kimliği için hello abonelik bilgilerini sağlayın. Hello Azure RemoteApp ekibi URL toohello VHD sağlayacaktır. Bu VHD indirin ve tüm belgeleri veya gereksinim duyduğunuz dosyaları alabilirsiniz. Bu hello VHD bit toodownload sürer için 50 GB olduğuna dikkat edin.

## <a name="is-hello-data-backed-up"></a>Merhaba verilerin yedeklendiği?
Evet, her coğrafi konumu hello kullanıcı verilerini bir yedeğini kaydedin. Merhaba veriler salt okunur ve olabilir hello normal veri yolu olduğu gibi hello aynı erişilen (Azure RemoteApp tooget başvurun,), hello birincil veri merkezi kapalı olduğunda. Merhaba veri kopyalanan gerçek zamanlı toohello yedekleme konumu ve farklı sürümlerini kopyalarını tutma. Bu nedenle, veri bozulması, biz mümkün toorestore olmaz, daha önce iyi sürüm ancak hello birincil veri merkezi ise aşağı mümkün tooget kullanıcı verilerini olacaktır bilinen tooa hello başka bir konuma.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Kullanıcıların nasıl hello sunucu tarafında hello UPD görürüm?
Her kullanıcının kendi dizin tootheir UPD eşlemeleri hello sunucuda olacaktır: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Merhaba en iyi şekilde toouse Outlook ve UPD nedir?
Azure RemoteApp oturumlar arasında hello Outlook durumu (posta kutularını, pst) kaydeder. tooenable bunu hello kullanıcı profili verilerini depolanan PST toobe hello (c:\users\<kullanıcı adı >). Bu hello verileri, hello konumunu değiştirmeyin bu nedenle sürece için hello varsayılan konumu, oturumlar arasında hello veriler korunur.

Ayrıca "önbelleğe alınmış" modu Outlook'ta kullanın ve arama için "sunucu/çevrimiçi" modunu kullanmak öneririz.

Kullanıma [bu makalede](remoteapp-outlook.md) Outlook ve Azure RemoteApp kullanma hakkında daha fazla bilgi için.

## <a name="what-about-redirection"></a>Yeniden yönlendirme hakkında neler?
Azure RemoteApp toolet kullanıcıları ayarlama işlemleri tarafından yerel aygıtlar erişim yapılandırabilirsiniz [yeniden yönlendirme](remoteapp-redirection.md). Yerel aygıtlar sonra hello UPD mümkün tooaccess hello verileri olacaktır.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Bir ağ paylaşımı olarak my UPD kullanabilir miyim?
Hayır. UPD bir ağ paylaşımı olarak kullanılamaz. Bir UPD hello kullanıcı etkin olduğunda yalnızca kullanılabilir toohello kullanıcı tooAzure RemoteApp bağlı olur.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Bir kullanıcı koleksiyondan silerseniz, kendi UPD silinir mi?
Hayır, bir kullanıcıyı sildiğinizde, biz otomatik olarak hello UPD silmeyin - hello koleksiyonu silene kadar bunun yerine, hello veri depolarız. Merhaba koleksiyonunu silin ettikten 90 gün sonra tüm UPD silin. 

Toodelete UPD koleksiyondan gerekiyorsa, Azure RemoteApp başvurun - UPD bizim taraftan silebilirsiniz.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Kullanıcılarım UPD (geçerli veya silinen kullanıcılar) erişebilir mi?
Evet, başvurursanız [Azure RemoteApp](mailto:remoteappforum@microsoft.com), size bir URL tooaccess ile Merhaba veri ayarlayabilirsiniz. Merhaba erişim süresi dolmadan önce herhangi bir veri ya da hello UPD dosyalarından 10 saat toodownload hakkında sahip olacaksınız.

## <a name="are-upds-available-offline"></a>UPD çevrimdışı var mı?
Yukarıda açıklanan hello 10 saat erişim penceresinde ötesinde çevrimdışı erişim tooUPDs sağlamaz hemen. Bu, biz şu anda sizinle hello Upd'lerde virüsten koruma yazılımı çalıştıran veya bir denetim için verilere erişme gibi yeterince uzun toocomplete daha karmaşık görevleri için erişim yolu tooprovide sahip olmadığını anlamına gelir.

## <a name="do-registry-key-settings-persist"></a>Kayıt defteri anahtarı ayarlarının kalıcı?
Evet, herhangi bir şey tooHKEY_Current_User yazılmış hello UPD parçasıdır.

## <a name="can-i-disable-upds-for-a-collection"></a>I UPD bir koleksiyon için devre dışı bırakabilirim?
Evet, bir abonelik için Azure RemoteApp toodisable UPD isteyebilir, ancak bu kendiniz yapamazsınız. Bu, UPD hello Abonelikteki tüm koleksiyonlar için devre dışı bırakılacak olduğunu anlamına gelir.

Aşağıdaki durumlarda hello hiçbirinde toodisable UPD isteyebilirsiniz: 

* Erişim ve denetim, kullanıcı verilerinin tam ihtiyacı (için denetleme ve finansal kurumlara gibi amacıyla gözden geçirin).
* 3. taraf kullanıcı yönetim çözümleri şirket içi profil ve etki alanına katılmış Azure RemoteApp dağıtımınızda kullanarak toocontinue istediğiniz var. Bu hello altın görüntüye yüklenen hello profil Aracısı toobe gerektirir. 
* Herhangi bir yerel veri depolama alanı gerekmez veya hello Bulut veya dosya paylaşımında tüm veriniz varsa ve Azure RemoteApp kullanarak yerel olarak veri toocontrol kaydetme istersiniz.

Bkz: [devre dışı kullanıcı profili diskleri (UPD) Azure remoteapp'te](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) daha fazla bilgi için.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Kullanıcıların veri toohello sistem sürücüsü kaydetme kısıtlayabilir miyiz?
Evet, ancak hello koleksiyonu oluşturmadan önce Yukarı hello şablonunda görüntü tooset gerekir. Aşağıdaki adımları tooblock erişim toohello sistem sürücüsünün hello kullan:

1. Çalıştırma **gpedit.msc** hello şablon görüntüsü üzerinde.
2. Çok gidin**kullanıcı yapılandırması > Yönetim Şablonları > Windows bileşenlerini > Explorer**.
3. Seçenekler aşağıdaki hello seçin:
   * **Bilgisayarım belirtilen sürücüleri gizle**
   * **Erişim toodrives Bilgisayarım'dan engelle**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>UPD çekirdek? Bazı veriler hello kullanılabilir hello ilk zaman hello kullanıcı UPD, oturum açtığında tooput istiyorum.
Evet, hello şablon görüntüsü oluşturduğunuzda, bilgi toohello varsayılan profili ekleyebilirsiniz. Bu bilgileri daha sonra toohello UPD eklenir.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Merhaba UPD hello boyutunu değiştirebilir miyim bağlı olarak ne kadar veri toostore istiyorum?
Hayır, tüm UPD 50 GB depolama alanı olması. Toostore farklı miktarlarda verinin istiyorsanız hello aşağıdakileri deneyin:

1. UPD hello koleksiyonu için devre dışı bırakın.
2. Kullanıcıların tooaccess için dosya paylaşımı ayarlayın.
3. Bir başlangıç komut dosyası kullanarak yük hello dosya paylaşımı. Azure remoteapp'te başlatma komut dosyaları hakkında ayrıntılı bilgi için aşağıya bakın.
4. Kullanıcıların toosave tüm verileri toohello dosya paylaşımına yönlendirin.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Azure Remoteapp'te nasıl bir başlangıç betiği çalıştırılsın mı?
Bir başlangıç betiği toorun istiyorsanız, başlangıç hello şablon görüntüsü zamanlanmış bir görev oluşturarak hello koleksiyon için toouse adımıdır. (Bunu *önce* Sysprep'i çalıştırın.) 

![Bir sistem görevi oluşturma](./media/remoteapp-upd/upd1.png)

![Bir kullanıcı oturum açtığında çalıştırılan bir sistem görevi oluşturma](./media/remoteapp-upd/upd2.png)

Merhaba üzerinde **genel** sekmesinde, emin toochange hello olması **kullanıcı hesabı** güvenlik altında çok "BUILTIN\Users."

![Merhaba kullanıcı hesabı tooa grubunu değiştir](./media/remoteapp-upd/upd4.png)

Merhaba zamanlanmış görev hello kullanıcının kimlik bilgilerini kullanarak, başlangıç betiği çalıştırır. Merhaba görev toorun zamanlama her bir kullanıcı oturum açtığında.

![Kümesi hello tetikleyicisi için "oturum açma" Merhaba görevi](./media/remoteapp-upd/upd3.png)

Aynı zamanda [Grup İlkesi tabanlı başlatma komut dosyaları](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Ne hakkında bir başlangıç betiği hello yerleştirme Başlat menüsü? Bu işe?
Diğer bir deyişle, ı config penceresi komut dosyası çalıştıran bir .bat dosyası oluşturun ve toohello c:\ProgramData\Microsoft\Windows\Start Menu\Programlar\Başlangıç klasörüne kaydedin ve sağlayabilirsiniz ardından bu komut dosyasını bir kullanıcı bir RemoteApp oturumu başlattığında Çalıştır?

Hayır, bu da başlatma komut dosyaları hello Başlat menüsünde desteklemiyor RDSH kullanan Azure RemoteApp ile desteklenmiyor.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>Mstsc.exe (Merhaba Uzak Masaüstü programı) tooconfigure oturum açma komut dosyalarını kullanabilir miyim?
Nope, Azure RemoteApp tarafından desteklenmiyor.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Yerel olarak hello VM üzerinde veri depolayabilir miyim?
Hayır, herhangi bir yere hello UPD hello VM dışında depolanan veriler kaybolacak. Yoktur yüksek fırsat hello kullanıcı olmayan hello alma aynı VM hello Azure RemoteApp oturum açtığında. Merhaba kullanıcı içine imzalayacak değil böylece biz kullanıcı VM Kalıcılık bulundurmayan aynı VM hello ve hello veriler kaybolur. Ayrıca, biz hello koleksiyonu güncelleştirdiğinizde, var olan VM'ler VM kendisini hello üzerinde depolanan tüm verileri anlamına gelir yeni VM'ler - kümesi ile değiştirilir hello kaybolur. Merhaba, hello UPD, Azure dosyaları, VNET içinde veya DropBox gibi bulut depolama sistemini kullanma hello buluta bir dosya sunucusu gibi paylaşılan depolama toostore verileri önerilir.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>PowerShell kullanarak bir VM üzerinde nasıl bir Azure dosya paylaşımını bağlama?
Merhaba Net PSDrive cmdlet toomount hello sürücü, aşağıdaki gibi kullanabilirsiniz:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Kimlik bilgilerinizi hello aşağıdakini çalıştırarak da kaydedebilirsiniz:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Olanak tanıyan Atla hello - hello yeni PSDrive kimlik bilgisi parametresi.

