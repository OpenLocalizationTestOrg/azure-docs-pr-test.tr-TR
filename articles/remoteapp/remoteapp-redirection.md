---
title: "Azure RemoteApp aaaUsing yeniden yönlendirmeyi | Microsoft Docs"
description: "Bilgi nasıl RemoteApp tooconfigure ve kullanım yeniden yönlendirme"
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
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Azure Remoteapp'te yeniden yönlendirme kullanma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Aygıt yeniden yönlendirme kullanıcılarınızın hello aygıtları ekli tootheir yerel bilgisayar, telefon veya tablet kullanarak uzak uygulamaları ile etkileşime olanak tanır. Örneğin, Azure RemoteApp aracılığıyla Skype verdiyse, kullanıcı kendi PC toowork Skype ile yüklenmiş hello kamera gerekir. Bu da yazıcılar, konuşmacılar, izleyiciler ve aralığı, USB bağlantılı bir çevre birimleri için geçerlidir.

RemoteApp hello Uzak Masaüstü Protokolü (RDP) ve RemoteFX tooprovide yeniden yönlendirme yararlanır.

## <a name="what-redirection-is-enabled-by-default"></a>Hangi yeniden yönlendirme varsayılan olarak etkin mi?
RemoteApp kullandığınızda, yeniden yönlendirme aşağıdaki hello varsayılan olarak etkinleştirilir. Parantez içindeki Hello bilgileri hello RDP ayarını gösterir.

* Ses hello yerel bilgisayarda yürütmek (**bu bilgisayarda yürütmek**). (audiomode:i:0)
* Ses hello yerel bilgisayar ve gönderme toohello uzak bilgisayarda yakalama (**bu bilgisayardan kayıt**). (audiocapturemode:i:1)
* Yazdırma toolocal yazıcıları (redirectprinters:i:1)
* COM bağlantı noktaları (redirectcomports:i:1)
* Akıllı kart cihazı (redirectsmartcards:i:1)
* Pano (özelliği toocopy ve Yapıştır) (redirectclipboard:i:1)
* Yazı tipi düzeltmeye temizleyin (yazı tipi düzeltmeye izin ver: i:1)
* Tüm desteklenen Tak ve Kullan cihazları yönlendirin. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Başka bir yeniden yönlendirme ne var mı?
İki yeniden yönlendirme seçenekleri varsayılan olarak devre dışıdır:

* Sürücü yeniden yönlendirme (sürücü eşleme): hello uzak oturumda eşlenen sürücüler, yerel bilgisayarınızın diskleri haline. Merhaba uzak oturumda çalışırken bu kaydettiğinizde veya açık dosyalardan yerel sürücülerinizi olanak tanır.
* USB yeniden yönlendirme: hello uzak oturumundan hello USB aygıtları ekli tooyour yerel bilgisayar kullanabilirsiniz.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Remoteapp'te yeniden yönlendirme ayarlarınızı değiştirin
SDK ile Merhaba Microsoft Azure PowerShell kullanarak bir koleksiyon için hello aygıt yeniden yönlendirme ayarlarını değiştirebilirsiniz. Yükledikten sonra yeni PowerShell ve SDK Merhaba, ilk olarak, aboneliğinizin açıklanan toomanage yapılandırın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

Ardından aşağıdaki tooset hello özel RDP özelliklere komutu benzer toohello kullanın:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Unutmayın  *`n*  ayrı ayrı özellikler arasında ayırıcı olarak kullanılır.)

tooget hangi özel RDP özellikleri yapılandırılır, listesini hello aşağıdaki cmdlet'i çalıştırın. Yalnızca özel özellikler çıkış sonuçları olarak gösterilir ve varsayılan özellikleri hello değil dikkat edin:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Özel özellikler ayarladığınızda, tüm özel özellikleri her zaman belirtmeniz gerekir; Aksi takdirde hello ayar toodisabled döner.   

### <a name="common-examples"></a>Ortak örnekler
Aşağıdaki cmdlet'i tooenable sürücü yönlendirmesi hello kullan:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Bu cmdlet tooenable kullanmak USB ve sürücü yeniden yönlendirme:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Bu cmdlet toodisable Pano paylaşımı kullanın:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Emin toocompletely günlük hello koleksiyonundaki tüm kullanıcılar devre dışı olması (ve yalnızca kesmeden) hello değişiklik test önce. tooensure kullanıcılar tamamen kapalı, Git toohello oturum **oturumları** sekmesinde hello koleksiyonundaki hello Azure portal ve bağlantısı kesilmiş veya oturum açtığı tüm kullanıcıları oturumunu. Bazen bu hello oturumunda Explorer'da hello yerel sürücüler tooshow birkaç saniye sürebilir.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Windows istemci USB yeniden yönlendirme ayarlarını değiştirin
Toouse USB yeniden yönlendirme tooRemoteApp bağlanan bir bilgisayarda istiyorsanız toohappen gereksinim 2 eylemler vardır. 1 - yöneticinize Azure PowerShell kullanarak tooenable USB yeniden yönlendirme hello koleksiyonu düzeyinde gerekir. 2 - toouse USB yeniden yönlendirme istediğiniz her cihazda tooenable izin bir Grup İlkesi gerekir. Bu adım toouse USB yeniden yönlendirme istediği her kullanıcı için yapılan toobe gerekir.

> [!NOTE]
> Azure RemoteApp ile USB yeniden yönlendirme yalnızca Windows bilgisayarları için desteklenir.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>Merhaba RemoteApp koleksiyonu için USB yeniden yönlendirme özelliğini etkinleştirin
Cmdlet tooenable USB yeniden yönlendirme hello koleksiyonu düzeyinde aşağıdaki hello kullan:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>Merhaba istemci bilgisayar için USB yeniden yönlendirme özelliğini etkinleştirin
Bilgisayarınızda tooconfigure USB yeniden yönlendirme ayarları:

1. Açık hello yerel Grup İlkesi Düzenleyicisi'ni (GPEDIT. MSC). (Gpedit.msc bir komut isteminden çalıştırın.)
2. Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.
3. Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.
4. Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar hello RemoteFX USB yeniden yönlendirme erişim hakları**.
5. Yönetim izinleri olan bir komut istemi açın ve hello aşağıdaki komutu çalıştırın:
   
        gpupdate /force
6. Merhaba bilgisayarı yeniden başlatın.

Ayrıca, hello Grup İlkesi Yönetimi Aracı toocreate kullanabilir ve etki alanınızdaki hello USB yeniden yönlendirme ilkesi tüm bilgisayarlar için uygulayabilirsiniz:

1. Merhaba etki alanı denetleyicisi olarak hello etki alanı yöneticisi olarak oturum.
2. Merhaba Grup İlkesi Yönetim Konsolu'nu açın. (Tıklatın **Başlat > Yönetim Araçları > Grup İlkesi Yönetimi**.)
3. Toohello etki alanı veya toocreate hello İlkesi istediğiniz kuruluş birimine gidin.
4. Sağ **varsayılan etki alanı ilkesi**ve ardından **Düzenle**.
5. Açık **Bilgisayar Yapılandırması\İlkeler\Yönetim Şablonları\Windows Bileşenleri\Uzak Masaüstü Hizmetleri\Uzak Masaüstü Bağlantısı Client\RemoteFX USB aygıtı yeniden yönlendirme**.
6. Çift **izin RDP yeniden yönlendirme, diğer desteklenen RemoteFX USB aygıtları bu bilgisayardan**.
7. Seçin **etkin**ve ardından **Yöneticiler ve kullanıcılar hello RemoteFX USB yeniden yönlendirme erişim hakları**.
8. **Tamam** düğmesine tıklayın.  

