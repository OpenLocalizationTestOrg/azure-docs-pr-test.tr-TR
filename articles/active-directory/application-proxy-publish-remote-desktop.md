---
title: "Azure AD uygulaması Proxy ile Uzak Masaüstü aaaPublish | Microsoft Docs"
description: "Merhaba temel Azure AD uygulama proxy'si bağlayıcılar hakkında bilgiler yer almaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Azure AD uygulama proxy'si ile Uzak Masaüstü yayımlama

Bu makalede yer almaktadır nasıl toodeploy uygulama ara sunucusu ile Uzak Masaüstü Hizmetleri (RDS) böylece uzak kullanıcılar hala üretken olabilirler.

Merhaba İzleyici Bu makale için tasarlanmıştır:
- Uzak Masaüstü Hizmetleri üzerinden şirket içi uygulamaları yayımlama tarafından daha fazla uygulamaları tootheir son kullanıcıların toooffer istediğiniz geçerli Azure AD uygulama proxy'si müşteriler.
- Azure AD uygulama proxy'si kullanarak bunların dağıtım tooreduce hello saldırı yüzeyini istediğiniz geçerli Uzak Masaüstü Hizmetleri müşteriler. Bu senaryo iki aşamalı doğrulamayı sınırlı sayıda sağlar ve tooRDS koşullu erişimi denetler.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Uygulama proxy'si hello standart RDS dağıtımda nasıl uyduğunu

Standart bir RDS dağıtma Windows Server'da çalışan çeşitli Uzak Masaüstü rol hizmetlerini içerir. Hello arayan [Uzak Masaüstü Hizmetleri mimarisi](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), birden çok dağıtım seçenekleri vardır. Merhaba hello arasındaki en dikkat çekici fark [RDS dağıtımı Azure AD uygulama proxy'si ile](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (diyagramı aşağıdaki hello gösterilir) ve hello diğer dağıtım seçenekleri, hello uygulama proxy'si senaryonun giden kalıcı sahip bağlantı hello bağlayıcı hizmetini çalıştıran hello sunucudan. Bir yük dengeleyici üzerinden açık gelen bağlantılar diğer dağıtımlar bırakın.

![RDS VM hello ve genel internet hello arasında uygulama Proxy yer alır](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

Bir RDS dağıtımında hello RD Web rolü ve hello RD Ağ Geçidi rol Internet'e yönelik makinelerde çalıştırın. Bu uç noktalar nedenleri aşağıdaki Merhaba sunulur:
- RD Web hello kullanıcı bir ortak uç nokta toosign sağlar ve görünüm hello çeşitli şirket içi uygulamalara ve masaüstlerine erişebilecekleri. Bir kaynak seçtikten sonra bir RDP bağlantısının hello yerel uygulama hello işletim sistemi üzerinde kullanılarak oluşturulur.
- Bir kullanıcı hello RDP bağlantı başlatır sonra RD Ağ Geçidi hello devreye. Hello RD Ağ Geçidi hello Internet gelen şifrelenmiş hello RDP trafiği işler ve kullanıcı hello şirket içi sunucu bağlandığı toohello çevirir. Bu senaryoda, RD Ağ Geçidi alma hello trafiği hello Azure AD uygulama proxy'si hello gelir.

>[!TIP]
>RDS önce dağıtılan henüz veya başlamadan önce daha fazla bilgi istiyorsanız nasıl çok öğrenin[sorunsuz bir şekilde Azure Resource Manager ve Azure Marketi RDS dağıtma](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Gereksinimler

- Her ikisi de RD Web hello ve RD Ağ Geçidi uç noktaları bulunmalıdır hello makine ve bir ortak kök ile aynı. Çoklu oturum açma deneyimini hello iki uygulama arasındaki alacak şekilde RD Web ve RD Ağ Geçidi tek bir uygulama olarak yayımlanır.

- Zaten yüklü olmalıdır [RDS dağıtılan](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), ve [uygulama Proxy etkin](active-directory-application-proxy-enable.md).

- Bu senaryo, son kullanıcılarınız hello RD Web sayfası bağlanan Windows 7 veya Windows 10 Masaüstü üzerinde Internet Explorer aracılığıyla Git varsayar. Diğer işletim sistemlerinin toosupport gerekirse bkz [diğer istemci yapılandırmaları için destek](#support-for-other-client-configurations).

  >[!NOTE]
  >Windows 10 oluşturanın güncelleştirmesi şu anda desteklenmiyor.

- Internet Explorer'hello RDS ActiveX eklenti etkinleştirin.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Merhaba birleşik RDS ve uygulama proxy'si senaryo dağıtma

RDS ve ortamınız için Azure AD uygulama proxy'si kurduktan sonra hello adımları toocombine hello iki çözümleri uygulayın. Bu adımları hello iki web dönük RDS uç noktaları (RD Web ve RD Ağ Geçidi) uygulamaları yayımlama ve uygulama proxy'si aracılığıyla, RDS toogo üzerinde trafiği yönlendirerek yol.

### <a name="publish-hello-rd-host-endpoint"></a>Yayımlama Hello RD konak uç noktası

1. [Yeni bir uygulama proxy'si uygulama yayımlama](application-proxy-publish-azure-portal.md) değerleri aşağıdaki hello ile:
   - İç URL: https://\<rdhost\>.com / nerede \<rdhost\> RD Web ve RD Ağ Geçidi paylaşan hello ortak köküdür.
   - Dış URL: Bu alan otomatik olarak hello hello uygulama adına göre doldurulur, ancak bunu değiştirebilirsiniz. RDS'yi eriştiklerinde, kullanıcılarınızın toothis URL gidin
   - Ön kimlik doğrulama yöntemi: Azure Active Directory
   - URL üstbilgileri çevir: Hayır
2. Kullanıcılar atama toohello yayımlanan RD uygulama. Tüm erişim tooRDS çok sahip olduklarından emin olun.
3. Merhaba tek oturum açma yöntemi Merhaba uygulaması bırakın **Azure AD çoklu oturum açma devre dışı özelliğini**. Kullanıcılarınızın tooauthenticate sorulur tooAzure AD ve bir kez tooRD Web, ancak sonra tek oturum açma tooRD ağ geçidi.
4. Çok Git**Azure Active Directory** > **uygulama kayıtlar** > *uygulamanız* > **ayarları**.
5. Seçin **özellikleri** ve güncelleştirme hello **giriş sayfası URL'si** alan toopoint tooyour RD Web uç noktası (https:// gibi\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Doğrudan RDS trafiği tooApplication Proxy

Toohello RDS dağıtımı yönetici olarak bağlanın ve hello dağıtımı için hello RD Ağ Geçidi sunucusu adını değiştirin. Bu bağlantıları hello Azure AD uygulama proxy'si Git sağlar.

1. Merhaba RD Bağlantı Aracısı rol çalıştıran toohello RDS sunucusuna bağlanın.
2. Başlatma **Sunucu Yöneticisi'ni**.
3. Seçin **Uzak Masaüstü Hizmetleri** hello soldaki hello bölmesinden.
4. Seçin **genel bakış**.
5. Hello dağıtımına genel bakış bölümünde içinde hello açılır menü seçip **dağıtım özelliklerini düzenleme**.
6. Merhaba Hello RD Ağ Geçidi sekmesinde, değiştirmek **sunucu adı** alan toohello uygulama proxy'si içindeki hello RD konak uç nokta için ayarladığınız dış URL.
7. Değişiklik hello **oturum açma yöntemi** çok alan**parola kimlik doğrulaması**.

  ![Dağıtım özellikleri RDS ekranda](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Her koleksiyon için komutu aşağıdaki hello çalıştırın. Değiştir  *\<yourcollectionname\>*  ve  *\<proxyfrontendurl\>*  kendi bilgilerle. Bu komut, çoklu oturum açma RD Web ve RD Ağ Geçidi arasında sağlar ve performansı en iyi duruma getirir:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Örneğin:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. tooverify hello değiştirilmesini hello özel RDP özelliklerinin yanı sıra RDWeb komutu aşağıdaki hello çalıştırmak için bu koleksiyonu yüklenecek hello RDP dosyası içeriği görüntüle:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Uzak Masaüstü yapılandırdıysanız, Azure AD uygulama proxy'si hello Internet'e bileşeni RDS'yi olarak gerçekleştirdiği Öğesini kaldırabilmeniz için diğer genel internet'e yönelik uç noktalar, RD Web ve RD Ağ Geçidi makinelerde hello.

## <a name="test-hello-scenario"></a>Test hello senaryosu

Windows 7 veya 10 bilgisayarda Internet Explorer ile Merhaba senaryosunu sınayın.

1. Ayarladığınız toohello dış URL gidin veya uygulamanızın hello Bul [MyApps Masası](https://myapps.microsoft.com).
2. Tooauthenticate tooAzure Active Directory istenir. Toohello uygulama atanmış bir hesap kullanın.
3. Tooauthenticate tooRD Web istenir.
4. RDS kimlik doğrulaması başarılı olduktan sonra hello Masaüstü veya ve çalışmaya başlama uygulama seçebilirsiniz.

## <a name="support-for-other-client-configurations"></a>Diğer istemci yapılandırmaları için destek

Bu makalede açıklanan hello Windows 7 veya 10, Internet Explorer ve hello RDS ActiveX eklenti sahip kullanıcılar için bir yapılandırmadır. Ancak, gerekirse, diğer işletim sistemleri veya tarayıcılar destekleyebilir. Merhaba, kullandığınız hello kimlik doğrulama yöntemi farktır.

| Kimlik doğrulama Yöntemi | Desteklenen istemci yapılandırması |
| --------------------- | ------------------------------ |
| Ön kimlik doğrulama    | Windows 7/10 kullanarak Internet Explorer + RDS ActiveX eklentisi |
| Geçiş | Tüm diğer Merhaba Microsoft Uzak Masaüstü uygulaması destekleyen işletim sistemi |

Merhaba ön kimlik doğrulama akışı hello geçiş akış'den daha fazla güvenlik avantajları sunar. Ön kimlik doğrulaması ile şirket içi kaynaklarınız için çoklu oturum açma, koşullu erişim ve iki aşamalı doğrulama gibi Azure AD kimlik doğrulama özellikleri yararlanabilirsiniz. Ayrıca, yalnızca trafik ulaştığında, ağ kimliği doğrulanmış emin olun.

toouse geçiş kimlik doğrulaması, var. yalnızca iki değişiklikler toohello adımları bu makalede listelenmektedir:
1. İçinde [yayımlama hello RD konak endpoint](#publish-the-rd-host-endpoint) 1. adımda, hello ön kimlik doğrulama yöntemi çok ayarlamak**geçiş**.
2. İçinde [doğrudan RDS trafiği tooApplication Proxy](#direct-rds-traffic-to-application-proxy), tamamen 8. adıma geçin.

## <a name="next-steps"></a>Sonraki adımlar

[Azure AD uygulama proxy'si ile uzaktan erişim tooSharePoint etkinleştir](application-proxy-enable-remote-access-sharepoint.md)  
[Azure AD uygulama proxy'si kullanarak uygulamalar uzaktan erişim için güvenlik konuları](application-proxy-security-considerations.md)
