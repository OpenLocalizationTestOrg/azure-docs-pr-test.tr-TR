---
title: "Azure Remoteapp'te yeniden yönlendirme kullanma | Microsoft Docs"
description: "Yapılandırma ve Remoteapp'te yeniden yönlendirmeyi kullanma hakkında bilgi edinin"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Azure Remoteapp'te yeniden yönlendirme kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Aygıt yeniden yönlendirme, yerel bilgisayar, telefon veya tablet bağlı cihazların kullanarak uzak uygulamaları ile etkileşim kullanıcılarınızın olanak tanır. Örneğin, Azure RemoteApp aracılığıyla Skype verdiyse, kullanıcı Skype ile çalışmak için kendi bilgisayarlarında yüklü kamera gerekir. Bu da yazıcılar, konuşmacılar, izleyiciler ve aralığı, USB bağlantılı bir çevre birimleri için geçerlidir.

RemoteApp RemoteFX ve Uzak Masaüstü Protokolü (RDP) yeniden yönlendirme sağlamak için yararlanır.

## <a name="what-redirection-is-enabled-by-default"></a>Hangi yeniden yönlendirme varsayılan olarak etkin mi?
RemoteApp kullandığınızda, aşağıdaki yeniden yönlendirme varsayılan olarak etkinleştirilir. Parantez içindeki bilgileri RDP ayarı gösterir.

* Yerel bilgisayarda bulunan ses çıkar (**bu bilgisayarda yürütmek**). (audiomode:i:0)
* Yerel bilgisayardan ses yakalamak ve uzak bilgisayara Gönder (**bu bilgisayardan kayıt**). (audiocapturemode:i:1)
* Yerel yazıcılara (redirectprinters:i:1) yazdırma
* COM bağlantı noktaları (redirectcomports:i:1)
* Akıllı kart cihazı (redirectsmartcards:i:1)
* Pano (kopyalamak ve yapıştırmak için yeteneği) (redirectclipboard:i:1)
* Yazı tipi düzeltmeye temizleyin (yazı tipi düzeltmeye izin ver: i:1)
* Tüm desteklenen Tak ve Kullan cihazları yönlendirin. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Başka bir yeniden yönlendirme ne var mı?
İki yeniden yönlendirme seçenekleri varsayılan olarak devre dışıdır:

* Sürücü yeniden yönlendirme (sürücü eşleme): uzak oturumda eşlenen sürücüler, yerel bilgisayarınızın diskleri haline. Uzak oturumda çalışırken bu kaydettiğinizde veya açık dosyalardan yerel sürücülerinizi olanak tanır.
* USB yeniden yönlendirme: uzaktan oturumunda yerel bilgisayarınıza bağlı USB aygıtlarını kullanabilir.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Remoteapp'te yeniden yönlendirme ayarlarınızı değiştirin
SDK ile Microsoft Azure PowerShell kullanarak bir koleksiyon için cihaz yeniden yönlendirme ayarlarını değiştirebilirsiniz. Yeni PowerShell ve SDK'yı yükledikten sonra açıklandığı gibi aboneliğinizi yönetmek için ilk yapılandırma [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).

Ardından özel RDP özelliği ayarlamak için aşağıdakine benzer bir komutu kullanın:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Unutmayın  *`n*  ayrı ayrı özellikler arasında ayırıcı olarak kullanılır.)

Hangi özel RDP özellikleri yapılandırılmış bir listesini almak için aşağıdaki cmdlet'i çalıştırın. Yalnızca özel özellikler çıkış sonuçları ve varsayılan özellikleri gösterildiğine dikkat edin:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Özel özellikler ayarladığınızda, tüm özel özellikleri her zaman belirtmeniz gerekir; Aksi takdirde ayarı devre dışı olarak döner.   

### <a name="common-examples"></a>Ortak örnekler
Sürücü yeniden yönlendirmeyi etkinleştirmek için aşağıdaki cmdlet'i kullanın:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

USB ve sürücü etkinleştirmek için bu cmdlet'i kullanın yeniden yönlendirme:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Pano paylaşımını devre dışı bırakmak için bu cmdlet'i kullanın:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Koleksiyondaki tüm kullanıcı tamamen oturumunu (yalnızca kesmeden) emin olun ve değişiklik test önce. Tamamen oturum emin olmak için Git **oturumları** sekmesinde Azure portalında koleksiyonundaki ve bağlantısı kesilmiş veya oturum açtığı tüm kullanıcıları oturumunu. Bazen yerel sürücüler Explorer'da oturum içinde göstermek için birkaç saniye sürebilir.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Windows istemci USB yeniden yönlendirme ayarlarını değiştirin
RemoteApp bağlayan bir bilgisayardaki USB yeniden yönlendirme kullanmak istiyorsanız, gerçekleşmesi gereken 2 eylemler vardır. 1 - USB yeniden yönlendirme koleksiyon düzeyinde Azure PowerShell kullanarak etkinleştirmek yöneticinize gerekir. 2 - USB yeniden yönlendirme kullanmak istediğiniz her cihazda BT bir Grup İlkesi etkinleştirmeniz gerekir. Bu adım, USB yeniden yönlendirme kullanmak istediği her kullanıcı için yapılması gerekir.

> [!NOTE]
> Azure RemoteApp ile USB yeniden yönlendirme yalnızca Windows bilgisayarları için desteklenir.
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a>RemoteApp koleksiyonu için USB yeniden yönlendirme özelliğini etkinleştirin
Koleksiyon düzeyinde USB yeniden yönlendirmeyi etkinleştirmek için aşağıdaki cmdlet'i kullanın:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a>İstemci bilgisayar için USB yeniden yönlendirme özelliğini etkinleştirin
Bilgisayarınızda USB yeniden yönlendirme ayarlarını yapılandırmak için:

1. Yerel Grup İlkesi Düzenleyicisi'ni (GPEDIT. açın MSC). (Gpedit.msc bir komut isteminden çalıştırın.)
2. Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.
3. Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.
4. Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar RemoteFX USB yeniden yönlendirme erişim hakları**.
5. Yönetim izinleri olan bir komut istemi açın ve aşağıdaki komutu çalıştırın:
   
        gpupdate /force
6. Bilgisayarı yeniden başlatın.

Grup İlkesi Yönetimi aracını, oluşturmak ve etki alanınızdaki tüm bilgisayarlar için USB yeniden yönlendirme ilkesini uygulamak için de kullanabilirsiniz:

1. Etki alanı denetleyicisi ile etki alanı yöneticisi olarak oturum açın.
2. Grup İlkesi Yönetim Konsolu'nu açın. (Tıklatın **Başlat > Yönetim Araçları > Grup İlkesi Yönetimi**.)
3. Etki alanı veya bir ilke oluşturmak istediğiniz kuruluş birimine gidin.
4. Sağ **varsayılan etki alanı ilkesi**ve ardından **Düzenle**.
5. Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.
6. Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.
7. Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar RemoteFX USB yeniden yönlendirme erişim hakları**.
8. **Tamam** düğmesine tıklayın.  

