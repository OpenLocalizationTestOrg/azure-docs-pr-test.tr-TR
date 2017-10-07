---
title: "yüksek kullanılabilirlik için Azure MFA sunucusu aaaConfigure | Microsoft Docs"
description: "Azure multi-Factor Authentication sunucusu yüksek kullanılabilirlik sağlamak yapılandırmalarında birden çok örneğini dağıtın."
services: multi-factor-authentication
keywords: Azure MFA
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Azure multi-Factor Authentication sunucusu yüksek kullanılabilirlik için yapılandırma

tooachieve yüksek oranda kullanılabilirlik Azure sunucu MFA dağıtımınız ile toodeploy gereken birden çok MFA sunucusu. Bu bölümde, Azure MFS sunucu dağıtımı, yüksek kullanılabilirlik hedeflerini bir yük dengeli tasarım tooachieve bilgi sağlar.

## <a name="mfa-server-overview"></a>MFA sunucusu genel bakış

Hello Azure MFA sunucusu hizmet mimarisi diyagramı aşağıdaki hello gösterildiği gibi birçok bileşenden oluşur:

 ![MFA sunucusu mimarisi](./media/mfa-server-high-availability/mfa-ha-architecture.png)

MFA sunucusu hello Azure çok faktörlü kimlik doğrulaması yazılımı yüklü olan bir Windows sunucusudur. Merhaba MFA sunucusu örneğini Azure toofunction hello MFA hizmeti tarafından etkinleştirilmesi gerekir. Birden fazla MFA sunucusu içi yüklü olabilir.

yüklenen ilk MFA sunucusu hello hello Azure MFA hizmeti varsayılan olarak etkinleştirme sırasında ana MFA sunucusu hello. Hello Yöneticisi MFA sunucusu hello PhoneFactor.pfdata veritabanı yazılabilir bir kopyası bulunur. MFA sunucusu örneklerinin sonraki yüklemelerini slaves bilinir. Merhaba MFA slaves çoğaltılmış salt okunur veritabanının bir kopyasını hello PhoneFactor.pfdata sahip. MFA sunucusu uzak yordam çağrısı (RPC) kullanarak bilgileri çoğaltarak. Tüm MFA sunucularının topluca ya da etki alanına katılmış veya tek başına tooreplicate bilgileri olması gerekir.

İki faktörlü kimlik doğrulaması gerekli olduğunda MFA ana ve bağımlı MFA sunucuları hello MFA hizmeti ile iletişim kurar. Örneğin, bir kullanıcı iki öğeli kimlik doğrulama gerektiren toogain erişim tooan uygulama çalıştığında hello kullanıcı ilk gibi Active Directory (AD) bir kimlik sağlayıcısı tarafından doğrulanır.

AD ile başarılı kimlik doğrulamasından sonra MFA sunucusu hello hello MFA hizmeti ile iletişim kurar. Merhaba MFA sunucusu hello MFA hizmeti tooallow bildirimden bekler veya hello kullanıcı erişimi toohello uygulaması reddedin.

Merhaba MFA ana sunucu çevrimdışı olursa, kimlik doğrulamaları hala işlenebilir, ancak değişiklikleri toohello MFA veritabanı gerektiren işlemler işlenemiyor. (Örnekler: Merhaba Ayrıca kullanıcılar, Self Servis PIN değişiklikleri ve kullanıcı bilgilerini değiştirme)

## <a name="deployment"></a>Dağıtım

Yük Dengeleme Azure MFA sunucusu ve ilişkili bileşenler için önemli noktalar aşağıdaki hello göz önünde bulundurun.

* **RADIUS Standart tooachieve yüksek kullanılabilirlik kullanarak**. RADIUS sunucuları olarak Azure MFA sunucuları kullanıyorsanız, bir MFA sunucusu birincil RADIUS kimlik doğrulaması hedefi ve diğer Azure MFA sunucusu ikincil kimlik doğrulama hedefleri olarak potansiyel olarak yapılandırabilirsiniz. Merhaba ikincil kimlik doğrulamasını doğrulanabilmesinden önce hello birincil kimlik doğrulaması hedefte kimlik doğrulama başarısız olduğunda bir zaman aşımı dönemi toooccur için beklemeniz gerekir çünkü ancak, bu yöntem tooachieve yüksek kullanılabilirlik pratik olmayabilir Hedef. Daha verimli tooload hello RADIUS arasındaki trafiğin yükünü dengelemek hello RADIUS istemcisi ve hello RADIUS sunucuları (Bu durumda, hello Azure MFA RADIUS sunucuları olarak hareket sunucuları) olan böylelikle işaret edebilir tek bir URL ile Merhaba RADIUS istemcileri yapılandırabilirsiniz.
* **Toomanually MFA slaves Yükselt**. Hello Yöneticisi Azure MFA sunucusunun çevrimdışı olması durumunda hello ikincil Azure MFA sunucuları tooprocess MFA istekleri devam eder. Ancak, bir ana MFA sunucusu kullanılabilir olana kadar Yöneticileri olmayan kullanıcılar ekleyebilir veya MFA ayarları değiştirebilirsiniz ve kullanıcılar hello kullanıcı portalı kullanarak değişiklikleri yapabilirler değil. Bir MFA bağımlı toohello yöneticisi rolü yükseltme her zaman el ile bir işlemdir.
* **Bileşenlerinin separability**. Azure MFA sunucusu oluşur yüklenebilir çeşitli bileşenleri hello hello aynı Windows Server örneği veya farklı örnekleri. Bu bileşenlerin hello Kullanıcı Portalı, mobil uygulama Web hizmeti ve hello ADFS bağdaştırıcı (aracı) içerir. Bu separability olası toouse hello Web uygulaması proxy'si toopublish hello Kullanıcı Portalı ve mobil uygulama Web sunucusu hello çevre ağından kolaylaştırır. Bu tür bir yapılandırma toohello ekler hello Aşağıdaki diyagramda gösterildiği gibi tasarımın genel güvenlik. Ayrıca Hello MFA Kullanıcı Portalı ve mobil uygulama Web sunucusu HA yük dengeli yapılandırmasında dağıtılabilir.

   ![MFA sunucusu çevre ağı ile](./media/mfa-server-high-availability/mfasecurity.png)

* **Tek kullanımlık parola (OTP) SMS (diğer adıyla tek yönlü SMS) üzerinden trafik yükü dengelenmiş ise Yapışkan oturumları hello kullanılmasını gerektiren**. Tek yönlü SMS hello MFA sunucusu toosend hello kullanıcılar bir OTP içeren bir kısa mesaj neden olan bir kimlik doğrulama seçenektir. Merhaba kullanıcı, bir komut istemi penceresi toocomplete hello MFA testini hello OTP girer. Azure MFA sunucuları dengelemek hello hello ilk kimlik doğrulaması isteği sunan aynı sunucu hello OTP ileti hello kullanıcıdan alır hello sunucu olması gerekir; başka bir MFA sunucusu hello OTP yanıt alırsa, hello kimlik doğrulaması sınaması başarısız olur. Daha fazla bilgi için bkz: [SMS eklenen tooAzure MFA sunucusu üzerinden bir zaman parola](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Yük dengeli dağıtımı hello Kullanıcı Portalı ve mobil uygulama Web hizmeti gerektirir Yapışkan oturumları**. Yük Dengeleme varsa MFA Kullanıcı Portalı hello ve hello mobil uygulama Web hizmeti, her oturum gerekiyor toostay hello üzerinde aynı sunucu.

## <a name="high-availability-deployment"></a>Yüksek kullanılabilirlik dağıtımı

Merhaba Aşağıdaki diyagramda tam bir HA yük dengeli uygulama, Azure MFA ve başvuru için ADFS birlikte bileşenlerinin gösterilmektedir.

 ![Azure MFA Server HA uygulama](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Aşağıdaki diyagram önceki hello gelenlere numaralı hello alanı için öğelerindeki hello unutmayın.

1. iki Azure MFA sunucusu (MFA1 ve MFA2) hello Dengeli (mfaapp.contoso.com) yükleyin ve bir statik bağlantı noktası (4443) tooreplicate hello PhoneFactor.pfdata veritabanı yapılandırılmış toouse şunlardır. Merhaba Web hizmeti SDK'sı her hello MFA sunucusu tooenable iletişimi hello ADFS sunucularıyla TCP bağlantı noktası 443 üzerinden yüklenir. Hello MFA sunucusu, durum bilgisi olmayan bir yük dengeli yapılandırmasında dağıtılır. Ancak, toouse OTP SMS istediyseniz, durum bilgisi olan Yük Dengeleme kullanmanız gerekir.
   ![Azure MFA Server - App server HA](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > RPC dinamik bağlantı noktaları kullandığından, RPC potansiyel olarak kullanabileceğiniz dinamik bağlantı noktaları toohello aralığı yukarı tooopen güvenlik duvarları önerilmez. Bir güvenlik duvarınız varsa **arasında** MFA uygulama sunucularınızın hello MFA sunucusu toocommunicate statik bağlantı noktası, bağlantı noktası hello çoğaltma trafiği için bağımlı ve asıl sunucuları arasındaki ve açık güvenlik duvarını yapılandırmanız gerekiyor. Bir DWORD kayıt defteri değerinde oluşturarak hello statik bağlantı noktası zorlayabilirsiniz ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` adlı ```Pfsvc_ncan_ip_tcp_port``` ve tooan kullanılabilir statik bağlantı noktası hello değerini ayarlar. Her zaman hello bağımlı MFA sunucuları toohello Yöneticisi tarafından başlatılan bağlantıları, hello statik bağlantı noktası yalnızca hello yöneticisinde gereklidir, ancak herhangi bir zamanda bir ikincil toobe hello ana yükseltebilirsiniz olduğundan, tüm MFA sunucularında hello statik bağlantı noktasına ayarlamanız gerekir.

2. Merhaba iki kullanıcı portalı/MFA mobil uygulama (MFA yukarı MAS1 ve MFA yukarı MAS2) sunucularıdır içinde dengelendiği bir **durum bilgisi olan** yapılandırma (mfa.contoso.com). Yapışkan oturumları Yük Dengeleme hello MFA Kullanıcı Portalı ve mobil uygulama hizmeti için bir gereksinim olan bir geri çağırma.
   ![Azure MFA sunucusu - kullanıcı portalı ile mobil uygulama hizmeti HA](./media/mfa-server-high-availability/mfaportal.png)
3. Merhaba ADFS sunucu grubu yük dengeli ve hello çevre ağında toohello Internet yük dengeli ADFS proxy üzerinden yayımlanan ' dir. Her ADFS sunucusu hello ADFS Aracısı toocommunicate hello Azure MFA TCP bağlantı noktası 443 bir tek bir yük dengeli URL (mfaapp.contoso.com) kullanarak sunucuları ile kullanır.

## <a name="next-steps"></a>Sonraki adımlar

* [Azure MFA sunucusu yükleme ve yapılandırma](multi-factor-authentication-get-started-server.md)
