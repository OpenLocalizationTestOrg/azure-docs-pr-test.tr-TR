---
title: "Azure RemoteApp, kullanıcı verilerini ve ayarlarını nasıl kaydedilsin mi? | Microsoft Belgeleri"
description: "Azure RemoteApp kullanıcı profili diski kullanarak kullanıcı verilerini nasıl kaydeder öğrenin."
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
ms.openlocfilehash: 4993bf507536659d7951e1552559cf0a6061d345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Azure RemoteApp, kullanıcı verilerini ve ayarlarını nasıl kaydedilsin mi?
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp, aygıtları ve oturumlar kullanıcı kimliği ve özelleştirmeleri kaydeder. Bu kullanıcı verileri bir kullanıcı profili diski (UPD) bilinen bir kullanıcı başına koleksiyona göre disk depolanır. Disk kullanıcı izler ve burada oturum bağımsız olarak tutarlı bir deneyim, kullanıcının sahip sağlar.

Kullanıcı profili diskleri kullanıcıya tamamen saydam — kullanıcıların belgeleri kendi belgeleri klasöre kaydedin (ne yerel bir sürücünün görünüyor üzerinde) ve uygulama ayarlarına normal olarak değiştirin. Aynı anda tüm kişisel ayarları Azure RemoteApp için herhangi bir aygıttan bağlanırken kalıcı olmasını sağlar. Tüm kullanıcı görür verilerini aynı yerde olabilir.

Her UPD 50 GB kalıcı depolama vardır ve her iki kullanıcı verileri ve uygulama ayarlarını içerir. 

Kullanıcı profili verilerini özellikleri için okumaya devam edin.

> [!NOTE]
> UPD devre dışı bırakmanız gerekir? Bu artık - Pavithra'nın blog gönderisi kullanıma yapabileceğiniz [devre dışı kullanıcı profili diskleri (UPD) Azure remoteapp'te](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), Ayrıntılar için.
> 
> 

## <a name="how-can-an-admin-get-to-the-data"></a>Nasıl bir yönetici verileri alabilir miyim?
Kullanıcılarınız (için olağanüstü durum kurtarma veya kullanıcının şirketten ayrılması durumunda) verilerine erişmek gerekiyorsa, Azure desteğine başvurun ve toplama ve kullanıcı kimliği için abonelik bilgileri sağlayın. Azure RemoteApp ekibi VHD için bir URL sağlayacaktır. Bu VHD indirin ve tüm belgeleri veya gereksinim duyduğunuz dosyaları alabilirsiniz. VHD bir indirme bit almak için 50 GB olduğuna dikkat edin.

## <a name="is-the-data-backed-up"></a>Verilerin yedeklendiği?
Evet, kullanıcı verilerini her coğrafi konumu yedeğini kaydedin. Veriler salt okunur ve normal veri (kişi almak için Azure RemoteApp) olduğu gibi aynı şekilde erişilebilir birincil veri merkezi kapalı olduğunda. Verileri gerçek zamanlı yedekleme konumuna kopyalanır ve farklı sürümlerini kopyalarını tutma. Bu nedenle, veri bozulması, biz önceden bilinen bir iyi sürüme geri yükleme mümkün olmayacak ancak birincil veri merkezi kapalı ise, kullanıcı verilerini diğer konumdan almak mümkün olacaktır.

## <a name="how-do-users-see-the-upd-on-the-server-side"></a>Kullanıcıların nasıl sunucu tarafında UPD görürüm?
Her kullanıcının kendi UPD eşlemeleri sunucuda kendi dizin olacaktır: c:\Users\username.

## <a name="whats-the-best-way-to-use-outlook-and-upd"></a>Outlook ve UPD kullanmak için en iyi yolu nedir?
Azure RemoteApp oturumlar arasında Outlook durumu (posta kutularını, pst) kaydeder. Kullanıcı profili verilerini depolanması için PST ihtiyacımız etkinleştirmek için (c:\users\<kullanıcı adı >). Bu veriler, konumunu değiştirmeyin bu nedenle sürece için varsayılan konum, oturumlar arasında verileri korunur.

Ayrıca "önbelleğe alınmış" modu Outlook'ta kullanın ve arama için "sunucu/çevrimiçi" modunu kullanmak öneririz.

Kullanıma [bu makalede](remoteapp-outlook.md) Outlook ve Azure RemoteApp kullanma hakkında daha fazla bilgi için.

## <a name="what-about-redirection"></a>Yeniden yönlendirme hakkında neler?
Kullanıcıların ayarıyla yerel aygıtlarına erişim sağlamak için Azure RemoteApp yapılandırabilirsiniz [yeniden yönlendirme](remoteapp-redirection.md). Yerel aygıtlar sonra UPD verilere mümkün olacaktır.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Bir ağ paylaşımı olarak my UPD kullanabilir miyim?
Hayır. UPD bir ağ paylaşımı olarak kullanılamaz. Kullanıcıya bir UPD yalnızca kullanıcının Azure RemoteApp için etkin olarak bağlı olduğunda kullanılabilir.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Bir kullanıcı koleksiyondan silerseniz, kendi UPD silinir mi?
Hayır, bir kullanıcıyı sildiğinizde, biz otomatik olarak UPD silmeyin - koleksiyon silene kadar bunun yerine, verileri depolarız. koleksiyonu ettikten 90 gün sonra tüm UPD silin. 

Koleksiyondan bir UPD silme gerekiyorsa Azure RemoteApp - başvurun UPD bizim taraftan silebilirsiniz.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Kullanıcılarım UPD (geçerli veya silinen kullanıcılar) erişebilir mi?
Evet, başvurursanız [Azure RemoteApp](mailto:remoteappforum@microsoft.com), biz verilere erişmek için bir URL ile ayarlayabilirsiniz. Erişim süresi dolmadan önce UPD herhangi bir veri veya dosyaları indirmek yaklaşık 10 saat sahip olacaksınız.

## <a name="are-upds-available-offline"></a>UPD çevrimdışı var mı?
Çevrimdışı erişim UPD için yukarıda açıklanan 10 saat erişim penceresinde ötesinde sağladığımız değil hemen. Biz şu anda uzun süre erişimi sağlamak için bir yolu yoktur, yani Upd'lerde virüsten koruma yazılımı çalıştıran veya bir denetim için verilere erişme gibi daha karmaşık görevleri tamamlamak yeterli.

## <a name="do-registry-key-settings-persist"></a>Kayıt defteri anahtarı ayarlarının kalıcı?
Evet, herhangi bir şey HKEY_Current_User yazılmış UPD parçasıdır.

## <a name="can-i-disable-upds-for-a-collection"></a>I UPD bir koleksiyon için devre dışı bırakabilirim?
Evet, Azure RemoteApp UPD bir abonelik için devre dışı bırakmak isteyebilirsiniz, ancak bu kendiniz yapamazsınız. Bu, UPD Abonelikteki tüm koleksiyonlar için devre dışı bırakılacak olduğunu anlamına gelir.

Aşağıdaki durumlardan birinde UPD devre dışı bırakmak isteyebilirsiniz: 

* Erişim ve denetim, kullanıcı verilerinin tam ihtiyacı (için denetleme ve finansal kurumlara gibi amacıyla gözden geçirin).
* 3. taraf kullanıcı yönetim çözümleri şirket içi profil ve etki alanına katılmış Azure RemoteApp dağıtımınızda kullanmaya devam etmek istiyor var. Bu profili Aracısı altın görüntüye yüklenmesi gerekir. 
* Herhangi bir yerel veri depolama alanı gerekmez veya Bulut veya dosya paylaşımı tüm verileriniz ve denetlemek için istediğiniz Azure RemoteApp kullanarak yerel olarak verilerini kaydetme.

Bkz: [devre dışı kullanıcı profili diskleri (UPD) Azure remoteapp'te](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) daha fazla bilgi için.

## <a name="can-i-restrict-users-from-saving-data-to-the-system-drive"></a>Kullanıcılar sistem sürücüsüne verileri kaydetme kısıtlayabilir miyiz?
Evet, ancak koleksiyonu oluşturmadan önce şablon görüntüsü ayarlamak gerekir. Sistem sürücüsü erişimi engellemek için aşağıdaki adımları kullanın:

1. Çalıştırma **gpedit.msc** şablon görüntüsü üzerinde.
2. Gidin **kullanıcı yapılandırması > Yönetim Şablonları > Windows bileşenlerini > Explorer**.
3. Aşağıdaki seçenekleri belirleyin:
   * **Bilgisayarım belirtilen sürücüleri gizle**
   * **Bilgisayarım'dan sürücülere erişimi engelle**

## <a name="can-i-seed-upds-i-want-to-put-some-data-in-the-upd-thats-available-the-first-time-the-user-signs-in"></a>UPD çekirdek? Kullanıcı oturum açtığında ilk kez kullanılabilir UPD bazı veriler koymak istediğiniz.
Evet, şablon görüntüsü oluşturduğunuzda, varsayılan profil bilgileri ekleyebilirsiniz. Bu bilgileri daha sonra UPD eklenir.

## <a name="can-i-change-the-size-of-the-upd-depending-on-how-much-data-i-want-to-store"></a>Saklamak istediğiniz ne kadar veri bağlı olarak UPD boyutunu değiştirebilir miyim?
Hayır, tüm UPD 50 GB depolama alanı olması. Farklı miktarda veri depolamak istiyorsanız, aşağıdakileri deneyin:

1. UPD koleksiyon için devre dışı bırakın.
2. Bir dosya paylaşımına erişmek kullanıcılar için ayarlayın.
3. Dosya Paylaşımı bir başlangıç komut dosyası kullanarak yükleyin. Azure remoteapp'te başlatma komut dosyaları hakkında ayrıntılı bilgi için aşağıya bakın.
4. Tüm veriler dosya paylaşımına kaydetmek için doğrudan kullanıcılar.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Azure Remoteapp'te nasıl bir başlangıç betiği çalıştırılsın mı?
Bir başlangıç betiği çalıştırmak istiyorsanız, koleksiyon için kullanacağınız şablon görüntüsü, zamanlanmış bir görev oluşturarak başlayın. (Bunu *önce* Sysprep'i çalıştırın.) 

![Bir sistem görevi oluşturma](./media/remoteapp-upd/upd1.png)

![Bir kullanıcı oturum açtığında çalıştırılan bir sistem görevi oluşturma](./media/remoteapp-upd/upd2.png)

Üzerinde **genel** sekmesinde, değiştirdiğinizden emin olun **kullanıcı hesabı** "BUILTIN\Users." güvenlik altında

![Bir gruba kullanıcı hesabını değiştirme](./media/remoteapp-upd/upd4.png)

Kullanıcının kimlik bilgilerini kullanarak, başlangıç komut dosyası, zamanlanmış bir görev başlatır. Çalıştırılacak görev zamanlama her bir kullanıcı oturum açtığında.

![Görev için tetikleyici "olarak oturum açma" belirlenmiş](./media/remoteapp-upd/upd3.png)

Aynı zamanda [Grup İlkesi tabanlı başlatma komut dosyaları](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-the-start-menu-would-that-work"></a>Ne hakkında bir başlangıç betiği Başlat menüsünde yerleştirme? Bu işe?
Diğer bir deyişle, ı config penceresi komut dosyası çalıştıran bir .bat dosyası oluşturun ve c:\ProgramData\Microsoft\Windows\Start Menu\Programlar\Başlangıç klasörüne kaydedin ve sağlayabilirsiniz ardından bu komut dosyasını bir kullanıcı bir RemoteApp oturumu başlattığında Çalıştır?

Hayır, bu da başlatma komut dosyaları Başlat menüsünde desteklemiyor RDSH kullanan Azure RemoteApp ile desteklenmiyor.

## <a name="can-i-use-mstscexe-the-remote-desktop-program-to-configure-logon-scripts"></a>Oturum açma komut dosyalarını yapılandırmak için mstsc.exe (Uzak Masaüstü programı) kullanabilir miyim?
Nope, Azure RemoteApp tarafından desteklenmiyor.

## <a name="can-i-store-data-on-the-vm-locally"></a>VM'de yerel olarak veri depolayabilir miyim?
Hayır, herhangi bir yere dışında VM UPD içinde depolanan veriler kaybolacak. Yoktur yüksek şansı kullanıcı aynı VM sonraki elde değil Azure RemoteApp oturum süresi. Böylece kullanıcı aynı VM kaydolma ve veriler kaybedilir kullanıcı VM Kalıcılık bulundurmayan. Ayrıca, koleksiyon güncelleştiriyoruz, var olan VM'ler VM üzerinde depolanan tüm verileri kaybolur anlamına gelen yeni bir küme VM'lerin - değiştirilir. Azure dosyaları, bir sanal ağ içinde veya DropBox gibi bir bulut depolama sistemi kullanarak bulut üzerinde bir dosya sunucusu gibi paylaşılan depolama UPD verilerini depolamak için önerilir.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>PowerShell kullanarak bir VM üzerinde nasıl bir Azure dosya paylaşımını bağlama?
Sürücü gibi bağlamak için Net PSDrive cmdlet'i kullanabilirsiniz:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


Kimlik bilgileriniz aşağıdakileri çalıştırarak da kaydedebilirsiniz:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Olanak tanıyan atlayın - Credential parametresinde yeni PSDrive cmdlet'i.

