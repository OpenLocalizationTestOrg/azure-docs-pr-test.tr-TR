---
title: aaaAzure RemoteApp SSS | Microsoft Docs
description: "Azure RemoteApp hakkında sık sorulan sorular yanıtlar toohello öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>Azure RemoteApp hakkında SSS
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Biz Azure RemoteApp hakkında sorularınız aşağıdaki hello duymadığınız. Başka var mı? Merhaba ziyaret [RemoteApp forumlarını](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) ve bize ne bildirin tooknow gerekir ya da aşağıda yorum açılır.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Aradığınızı bulamadınız mı? Yanıt alamadığınız bir sorunuz mu var?
Merhaba bilgileri bulamazsanız ihtiyacınız, veya biz burada kapsayan olmayan başka bir sorunuz varsa, lütfen toohello gidin [Azure RemoteApp Forumu](http://aka.ms/araforum) ve sorunuzu var. isteyin. Buraya her zaman daha fazla yanıt ekleyebiliriz.

## <a name="what-is-azure-remoteapp"></a>Azure RemoteApp nedir?
* **Azure RemoteApp nedir?** RemoteApp bir Azure hizmeti güvenli uzaktan erişim tooapplications birçok farklı kullanıcı aygıtlardan sağlamanıza yardımcı olur. [Azure RemoteApp](remoteapp-whatis.md) hakkında daha fazla bilgi okuyun
* **Merhaba dağıtım seçenekleri nelerdir?** İki tür RemoteApp koleksiyonu vardır: bulut ve karma. Aynı, etki alanına katılımda olduğu gibi, burada da size hangisinin gerektiği bir dizi etkene bağlıdır. Bu kararların tümü hakkında [burada](remoteapp-collections.md) konuşacağız.

## <a name="quick-tips-on-using-azure-remoteapp"></a>Azure RemoteApp kullanma hakkında hızlı ipuçları
* **Bağlantım ne zaman kesilecek? Bana hello önyükleme vermenizden önce ne kadar süreyle boşta olabilirim?** 4 saat. Siz veya kullanıcılarınız 4 saat işlem yapmadıysanız, Azure RemoteApp oturumunuz otomatik olarak kapanır. Kullanıma hello diğer varsayılan ayarları [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).
* **Bu hizmeti ücretsiz deneyebilir miyim?** Evet. 30 günlük ücretsiz bir deneme sürümü vardır. Merhaba deneme sona erdikten sonra üretimde kullanabildiğiniz) hesabın (veya hello hizmetini kullanarak stop Ücretli tooa geçiş yapabilir. Çok giderek ücretsiz deneme sürümünüzü başlatın[portal.azure.com](http://portal.azure.com) -yeni bir RemoteApp örneğini oluşturun. Merhaba ücretsiz deneme sürümü ile örnek başına 10 kullanıcılarla 2 RemoteApp örneği oluşturabilirsiniz. Bu deneme sürümünün yalnızca 30 gün ömrü olduğunu unutmayın.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Azure RemoteApp aboneliği ayrıntıları
* **Merhaba hizmet sınırları nelerdir?** Merhaba varsayılan ayarları hakkında bilgi edinin ve hizmet sınırları Azure RemoteApp [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md). Daha fazla sorunuz olup olmadığını biz de bilelim.
* **Kaç tane kullanıcıların toohave sahip mi?** En az 20 kullanıcı vardır. Bu toobe çok daha belirgin yineleyin izin ver - hello en az 20'dir. Size 20 kullanıcı için fatura edilecek. 
* **RemoteApp’in maliyeti ne kadar?** [Azure RemoteApp Fiyatlandırma Ayrıntıları](https://azure.microsoft.com/pricing/details/remoteapp/) makalesini inceleyin.
* **Bir tür koleksiyonun maliyeti bir başkasına göre daha mı yüksek?** Evet, koleksiyon gereksinimlerinize bağlı olarak daha yüksek olabilir. Karma koleksiyon Azure RemoteApp tooyour şirket içi ağ üzerinden bir bağlantı gerektiriyor. Mevcut bir VNET/Hızlı Rota kullanıyorsanız ek bir maliyet yoktur. Ancak yeni Azure VNET ve bir ağ geçidi veya hızlı rota kullanıyorsanız, Merhaba ücretlendirilir [VPN ağ geçidi](https://azure.microsoft.com/pricing/details/vpn-gateway) veya [hızlı rota](https://azure.microsoft.com/pricing/details/expressroute/). Bu maliyet (Merhaba bağlantılarda ayrıntılı), aylık Azure RemoteApp maliyetinin en üstündedir.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Koleksiyonlar - ne desteklenir, hangisini kullanmalısınız ve diğerleri
* **Özel iş kolu (LOB) uygulamaları destekleniyor mu?** Evet. toouse Azure remoteapp'te özel bir uygulama oluşturmak bir [özel şablon görüntüsü](remoteapp-create-custom-image.md)ve toohello RemoteApp koleksiyonu yükleyin.
* **Özel LOB Uygulamam Azure Remoteapp'te çalışacak mı?**  olan çıkışı tootest en iyi şekilde toofigure Merhaba. Merhaba denetleyin [RD Uyumluluk Merkezi](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Kuruluşum için hangi dağıtım yöntemi (bulut veya karma) en iyisidir?** Karma koleksiyonlar, çoklu oturum açma (SSO) ile tam tümleştirme isterseniz ve güvenli şirket içi ağ bağlantısı hello en eksiksiz deneyimi sağlar. Bulut koleksiyonları, birden çok kimlik doğrulama yöntemlerini kullanarak dağıtımınızı Çevik ve kolay bir şekilde tooisolate sağlar. Merhaba hakkında daha fazla bilgiyi [dağıtım seçenekleri](remoteapp-whatis.md).
* **İster şirket içi ister Azure üzerinde olsun SQL veya başka bir veritabanımız vardır. Hangi tür dağıtımı kullanmalıyız?** SQL veya arka uç veritabanınızın nerede olduğuna bağlıdır. Merhaba veritabanı özel bir ağda ise, hello karma koleksiyonunu kullanın. Merhaba veritabanı gösterilen toohello Internet ise ve istemci bağlantıları tooconnect tooit sağlar, hello bulut koleksiyonunu kullanabilirsiniz.
* **Sürücü eşleme, USB ve seri bağlantı noktası, pano paylaşımı ve yazıcı yeniden yönlendirme hakkında neler diyorsunuz?** Tüm bu özellikler Azure RemoteApp’te desteklenir. Pano paylaşımı ve yazıcı yeniden yönlendirme varsayılan olarak etkindir. Yeniden yönlendirme hakkında bilgileri [buradan](remoteapp-redirection.md) edinebilirsiniz. 

## <a name="template-images"></a>Şablon görüntüleri
* **Bir bulut ya da var olan sanal makine hello şablon olarak RemoteApp Koleksiyonum için kullanabilir miyim?** Evet! Azure VM temelinde görüntü oluşturabilirsiniz, aboneliğinizde yer alan hello görüntülerden birini kullanın veya özel bir görüntü oluşturun. Merhaba denetleyin [RemoteApp görüntü seçenekleri](remoteapp-imageoptions.md).

## <a name="network-options"></a>Ağ seçenekleri
* **Merhaba karma koleksiyona VNET gerekir. Mevcut sanal ağımızı kullanabilir miyiz?** Merhaba var olan bir Azure sanal vnet'se kullanabilirsiniz. Bkz: "1. adım: sanal ağınızı kurma" Merhaba içinde [karma koleksiyon yönergelerinde](remoteapp-create-hybrid-deployment.md) daha fazla bilgi için.
* **Sanal ağı bulut koleksiyonuyla kullanabilir miyim?** Aslında kullanabilirsiniz. Daha fazla bilgi için [Bulut koleksiyonu oluşturma](remoteapp-create-cloud-deployment.md) konusunu, özellikle de 1. Adım’ı inceleyin.

## <a name="authentication-options"></a>Kimlik doğrulaması seçenekleri
* **Kimlik doğrulaması hakkında ne denebilir? Hangi yöntemler destekleniyor?**  hello bulut koleksiyonu, Microsoft hesapları ve Office 365 hesabı Azure Active Directory hesaplarını destekler. Merhaba karma koleksiyon eşitlenmemiş Azure Active Directory hesaplarını destekler (gibi bir araç kullanarak [Azure Active Directory eşitleme](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) ile Merhaba, ya da özel olarak, Windows Server Active Directory dağıtımdan; eşitlendi Parola Eşitleme seçeneğini veya yapılandırılmış Active Directory Federasyon Hizmetleri (AD FS) Federasyon ile eşitlenmiş. [Multi-Factor Authentication (MFA)](https://azure.microsoft.com/services/multi-factor-authentication/) öğesini de yapılandırabilirsiniz.

> [!NOTE]
> Hello Azure Active Directory Kullanıcıları, aboneliğinizle ilişkili hello Kiracı olmalıdır. (Görüntülemek ve aboneliğinizi hello değiştirmek **ayarları** hello portal sekmesindedir. Bkz: [RemoteApp tarafından kullanılan değişiklik hello Azure Active Directory Kiracı](remoteapp-changetenant.md) daha fazla bilgi için.)
> 
> 

* **Neden my Azure Active Directory hesap erişimi veremez?**  hello Azure Active Directory Kullanıcıları, aboneliğinizle ilişkili hello dizininden olması gerekir. Görüntülemek veya hello portalında hello ayarları sekmesinde bu dizine değiştirin. Bkz: [RemoteApp tarafından kullanılan değişiklik hello Azure Active Directory Kiracı](remoteapp-changetenant.md) daha fazla bilgi için.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Hangi cihaz için istemciler - tooaccess Azure RemoteApp kullanabilir miyim?
Merhaba farklı istemcilerin yüklenmesiyle ilgili adımları yararlı istemci bilgilerini bulabilirsiniz [Azure remoteapp'te uygulamalarınıza erişme](remoteapp-clients.md).

* **Hangi cihazlar ve işletim sistemleri hello istemci uygulamaları destekliyor musunuz?**
  Birincisi, hello bilgisayarlar ve tabletler: 
  
  * Windows 10 (istemci önizleme)
  * Windows 8.1 ve Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Android tabletler
  * iPad cihazları

    Ve hello telefonlar:
  * iPhone
  * Android Phone
  * Windows Phone
    
    RemoteApp istemcisini hemen [indirin](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx).
* **Azure RemoteApp İnce İstemcileri destekliyor mu?** Evet, hello aşağıdaki Windows Embedded ince istemciler desteklenir:
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Enterprise
* **Uzak Masaüstü oturumu ana bilgisayarı (RDSH) hello için Windows Server'ın hangi sürümü destekleniyor mu?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Destek ve geri bildirim
* **RemoteApp için hello destek planı nedir?** Faturalama ve abonelik yönetimi desteği ücretsiz olarak sağlanır. Teknik Destek hello kullanılabilir [Azure hizmet planlarından](https://azure.microsoft.com/support/plans/). [Azure tartışma forumumuzdan](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp) da ücretsiz topluluk desteği alabilirsiniz. 
* **Geri bildirimi nasıl gönderirim?** Merhaba ziyaret [geri bildirim Forumunda](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Kimin toolearn Azure RemoteApp hakkında daha fazla iletişim kurabilirsiniz?** Toplama tooour içinde [tartışma Forumu](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp)harika yer toopost sorular olduğu, hello haftalık katılabilirsiniz [hello uzmanlara sorun Web Seminerimize](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), burada biz ilgili her şeyden RemoteApp konuşun.
* **RemoteApp belgeleri hakkında neler diyeceksiniz?** Bunu sorduğunuza çok memnun olduk. Ayrıca toohello Yardım hello portal Yardım bölümü içeriği (Merhaba tıklatmanız **?** Her sayfada hello Portalı'nda), kullanılabilir tooteach makaleler hello olan, RemoteApp hakkında:
  
  * **Başlarken:**
    * [RemoteApp nedir?](remoteapp-whatis.md)
    * [Merhaba RemoteApp şablon görüntülerinde neler var?](remoteapp-images.md)
    * [Lisanslama nasıl çalışır?](remoteapp-licensing.md)
    * [RemoteApp ve Office birlikte nasıl çalışır?](remoteapp-o365.md)
    * [RemoteApp’te yeniden yönlendirme nasıl işler](remoteapp-redirection.md)?
  * **Dağıtma:**
    * [Özel şablon görüntüsü oluşturma](remoteapp-create-custom-image.md)
    * [Karma koleksiyon oluşturma](remoteapp-create-hybrid-deployment.md)
    * [Bulut koleksiyonu oluşturma](remoteapp-create-cloud-deployment.md)
    * [RemoteApp için Azure Active Directory’yi yapılandırma](remoteapp-ad.md)
    * [RemoteApp’te uygulama yayımlama](remoteapp-publish.md)
  * **Yönetme:**
    
    * [Kullanıcı ekleme](remoteapp-user.md)
    * [RemoteApp’in yapılandırılması ve kullanılmasıyla ilgili en iyi uygulamalar](remoteapp-bestpractices.md)    
    
    Videolar! RemoteApp hakkında sayısız videomuz da vardır. Bazı giriş sağlar ([giriş tooAzure RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) diğerleri dağıtımıyla yol sırada ([bulut dağıtımı](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) ve [karma dağıtımı](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Bunları inceleyin!

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Toplama toorating bu makalede, aşağıda yorum yapmamanın, değişiklikleri toohello makalesi kendisini yapıp olduğunu biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Yukarı doğru ilerleyin ve tıklatın **GitHub üzerinde Düzenle** toomake değişiklikleri - olanlar gelen gözden geçirilmek üzere toous ve biz üzerlerinde edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada göreceğiniz.

