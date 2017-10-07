---
title: "NPS uzantısı kullanılarak Azure MFA ile aaaVPN tümleştirme | Microsoft Docs"
description: "Bu makalede, Microsoft Azure için hello ağ ilkesi sunucusu (NPS) uzantısını kullanarak Azure MFA ile VPN altyapınız tümleştirme anlatılmaktadır."
services: active-directory
keywords: "Azure MFA, VPN, Azure Active Directory, ağ ilkesi sunucusu uzantısı tümleştirme"
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 5e120f7633121385d9cc5d7bec97ecaa1ec7cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-vpn-infrastructure-with-azure-multi-factor-authentication-mfa-using-hello-network-policy-server-nps-extension-for-azure"></a>VPN altyapınız ile Azure çok faktörlü kimlik doğrulaması (Merhaba ağ ilkesi sunucusu (NPS) uzantısıyla için Azure MFA) tümleştirme

## <a name="overview"></a>Genel Bakış

Hello Azure Ağ İlkesi Hizmeti (NPS) uzantısı sağlayan kuruluşların toosafeguard Uzaktan Kimlik Doğrulama Çevirmeli Kullanıcı Hizmeti (RADIUS) istemci kimlik doğrulaması kullanarak bulut tabanlı [Azure çok faktörlü kimlik doğrulama (MFA)](multi-factor-authentication-get-started-server-rdg.md), iki aşamalı doğrulama sağlar.

Bu makalede, bir VPN kullanarak tooconnect tooyour ağ deneyen kullanıcılar için Azure tooenable güvenli iki aşamalı doğrulama için hello NPS uzantısını kullanarak hello NPS altyapı Azure MFA ile tümleştirmek için yönergeler sağlar. 

Merhaba Ağ İlkesi ve Erişim Hizmetleri (NPS), kuruluşların hello yeteneklerini aşağıdaki sağlar:

* Merhaba yönetimi ve bağlanabilecek, ne zaman bağlantılara izin verilir, günün bağlantıları hello süresi ve istemcilerin gerekir tooconnect kullanın vb. güvenlik düzeyini hello ağ istekleri toospecify denetimi için merkezi konumlarını belirtin. Bu ilkelerin her VPN veya Uzak Masaüstü (RD) Ağ Geçidi sunucusunda belirtmek yerine, bu ilkeler merkezi bir konumda bir kez belirtilebilir. Merhaba RADIUS protokolü kullanılır tooprovide hello merkezi kimlik doğrulama, yetkilendirme ve hesap oluşturma (AAA). 
* Kurmak ve cihazları Kısıtlanmamış veya kısıtlanmış erişim toonetwork kaynaklara erişim izni verilmiş olup olmadığını belirleyen Ağ Erişim Koruması (NAP) istemci sistem durumu ilkeleri zorlayın.
* Bir yol tooenforce kimlik doğrulama ve yetkilendirme access too802.1x özellikli kablosuz erişim noktaları ve Ethernet anahtarları için sağlar.    

Daha fazla bilgi için bkz: [ağ ilkesi sunucusu (NPS)](https://docs.microsoft.com/windows-server/networking/technologies/nps/nps-top). 

tooenhance güvenlik ve yüksek düzeyi sağlamak uyumluluğunu, kuruluşların NPS tümleştirebilirsiniz ile Azure MFA tooensure kullanıcılar iki aşamalı doğrulamayı kullanmak mümkün toobe bağlanmak toohello hello VPN sunucuda sanal bağlantı noktası. Erişim izni kullanıcılar toobe için kendi kullanıcı adı/parola bileşimi kullanıcı hello bilgilerle kendi denetiminde sahip sağlamaları gerekir. Bu bilgiler güvenilir ve kolayca çoğaltılması, cep telefonu numarası, telefona numarası, uygulama, bir mobil cihaz ve benzerleri gibi.

Hello Azure NPS uzantısı kullanılabilirliğini önceki toohello, NPS tooimplement iki aşamalı doğrulama için onlardan müşteriler tümleşik ve Azure MFA ortamları tooconfigure var ve ayrı bir MFA sunucusu hello şirket içi ortamda korumak Uzak Masaüstü Ağ geçidi ve Azure multi-Factor Authentication sunucusu RADIUS kullanan belgelenmiştir.

Azure hello NPS uzantısı Hello kullanılabilirliğini kuruluşlar hello seçim toodeploy şirket tabanlı MFA çözümünü ya bir bulut tabanlı MFA çözüm toosecure RADIUS istemci kimlik doğrulaması şimdi sağlar.
 
## <a name="authentication-flow"></a>Kimlik doğrulama akışı
Bir kullanıcı tooa sanal bağlantı noktasına bir VPN sunucusuna bağlandığında, bunlar ilk kullanıcı adı/parola ve sertifika tabanlı kimlik doğrulama yöntemlerinin bir birleşimini hello kullanılmasına izin protokolleri çeşitli kullanarak kimliğini doğrulaması gerekir. 

Ayrıca tooauthenticating ve kimlik doğrulama, kullanıcıların hello dışarıdan arama izinleri uygun olmalıdır. Basit uygulamalarında, erişim izni bu çevirmeli izinler doğrudan hello Active Directory kullanıcı nesneleri üzerinde ayarlanır. 

 ![Kullanıcı özellikleri](./media/nps-extension-vpn/image1.png)

Basit uygulamalar için her VPN sunucusu verir veya erişimi her yerel VPN sunucusunda tanımlanan ilkelere bağlı olarak reddeder.

Daha büyük ve daha fazla ölçeklenebilir uygulamalarında hello bu verme ilkeleri veya VPN erişimi RADIUS sunucularına merkezi reddedin. Bu durumda, hello VPN sunucu bağlantı isteklerini ileten bir erişim sunucusu (RADIUS istemcisi) ve hesap iletileri tooa RADIUS sunucusu gibi davranır. tooconnect toohello sunucuda sanal bağlantı noktası hello VPN, kullanıcıların kimliğinin doğrulanması gerekir ve RADIUS sunucularına merkezi olarak tanımlanması hello koşullara uyan. 

Hello Azure NPS uzantısı hello NPS ile tümleştirildiğinde hello başarılı kimlik doğrulaması akışı aşağıdaki gibidir:

1. Merhaba VPN sunucusu hello kullanıcı adı ve parola tooconnect tooa kaynağını, Uzak Masaüstü oturumu gibi içeren bir VPN kullanıcı kimlik doğrulama isteği alır. 
2. Bir RADIUS istemcisi olarak işlev gören, VPN sunucusu hello istek tooa RADIUS Erişim-İstek iletisi dönüştürür ve hello ileti gönderir (parola şifrelenir) hello NPS uzantısı yüklü olduğu toohello RADIUS (NPS) sunucusu. 
3. Merhaba kullanıcı adı ve parola birleşiminin Active Directory'de doğrulanır. Varsa hello kullanıcı adı / parola yanlış, hello RADIUS sunucusu bir erişim reddi iletisi gönderir. 
4. Belirtilen tüm koşulları olarak NPS bağlantı isteğini hello ve ağ ilkeleri karşılanmadığı (örneğin, süresi gün veya grup üyeliği kısıtlamaları), hello NPS uzantısı Azure MFA ile ikincil kimlik doğrulama isteği tetikler. 
5. Azure MFA, Azure Active Directory ile iletişim kurar, hello kullanıcının ayrıntılarını alır ve (SMS mesajı, mobil uygulama ve benzeri) hello kullanıcı tarafından yapılandırılan hello yöntemini kullanarak hello ikincil kimlik doğrulaması gerçekleştirir. 
6. Merhaba MFA testini Başarı sonucu hello sonuç toohello NPS uzantısı Azure MFA ile iletişim kurar.
7. Hello bağlantı denemesi kimliği doğrulanmış ve yetkilendirilmiş sonra hello uzantısı yüklendiği hello NPS sunucusunun RADIUS Erişim Kabul iletisi toohello VPN sunucusu (RADIUS istemcisi) gönderir.
8. Merhaba kullanıcı erişimi toohello VPN sunucuda sanal bağlantı noktası verilir ve şifreli bir VPN tüneli oluşturur.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde hello Önkoşullar hello Uzak Masaüstü Ağ geçidi ile Azure MFA tümleştirme önce gerekli ayrıntıları. Başlamadan önce aşağıdaki önkoşulların yerinde hello olması gerekir.

* VPN altyapısı
* Ağ İlkesi ve Erişim Hizmetleri (NPS) rol
* Azure MFA lisans
* Windows Server yazılımı
* Kitaplıkları
* Azure AD synched ile şirket içi AD 
* Azure Active Directory GUID kimliği

### <a name="vpn-infrastructure"></a>VPN altyapısı
Bu makalede, Microsoft Windows Server 2016 yerinde kullanarak çalışma VPN altyapısına sahip ve bu hello VPN sunucusu şu anda yapılandırılmış tooforward bağlantı isteklerini tooa RADIUS sunucusu değil varsayar. Bu kılavuzda hello VPN altyapısı toouse merkezi bir RADIUS sunucusuna yapılandırır.

Yerinde bir çalışma altyapısı yoksa, bu altyapı hello Microsoft ve üçüncü taraf sitelerine bulabilirsiniz çok sayıda VPN Kurulumu öğreticileri sağlanan aşağıdaki hello Kılavuzu tarafından hızlı bir şekilde oluşturabilirsiniz. 

### <a name="network-policy-and-access-services-nps-role"></a>Ağ İlkesi ve Erişim Hizmetleri (NPS) rol

Merhaba NPS rol hizmetinin hello RADIUS sunucusu ve istemci işlevselliği sağlar. Bu makalede hello NPS rol bir üye sunucu veya etki alanı denetleyicisinde ortamınızda yüklediğiniz varsayılır. Bu kılavuzdaki VPN yapılandırması için RADIUS yapılandırır. Merhaba NPS rolü bir sunucuya yüklemek _diğer_ VPN sunucunuzun daha.

Hello NPS rolü yükleme hakkında bilgi için Windows Server 2012 hizmet veya üzeri, bkz: [bir NAP sistem durumu ilkesi sunucusu yükleme](https://technet.microsoft.com/library/dd296890.aspx). Ağ erişim ilkesi (NAP), Windows Server 2016'da kullanım dışıdır. NPS, bir etki alanı denetleyicisinde de dahil olmak üzere hello öneri tooinstall NPS için en iyi uygulamaları bir açıklaması için bkz: [NPS için en iyi uygulamaları](https://technet.microsoft.com/library/cc771746).

### <a name="licenses"></a>Lisansları

Gerekli bir Azure AD Premium, Enterprise Mobility artı güvenlik (EMS) veya bir MFA abonelik kullanılabilir olan Azure MFA bir lisans kullanılır. Daha fazla bilgi için bkz: [nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md). Test amacıyla bir deneme aboneliği kullanabilirsiniz.

### <a name="software"></a>Yazılım

Merhaba NPS uzantısı gerektiren Windows Server 2008 R2 SP1 veya üstü yüklü hello NPS rol hizmetine sahip. Bu kılavuzdaki tüm hello adımları, Windows Server 2016 kullanılarak gerçekleştirilen.

### <a name="libraries"></a>Kitaplıkları

iki kitaplığı aşağıdaki hello gereklidir:

* [Visual Studio 2013 (X64) için Visual C++ yeniden dağıtılabilir paketleri](https://www.microsoft.com/download/details.aspx?id=40784)
* _Microsoft Azure Active Directory için Windows PowerShell modülü sürümü 1.1.166.0_ ya da daha yüksek. Merhaba en son sürümü ve yükleme yönergeleri için bkz: [Microsoft Azure Active Directory PowerShell modülü sürüm yayın geçmişi](https://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx).

Bu kitaplıklar hello NPS uzantısı Kurulum dosyaları (sürüm 0.9.1.2), aksi takdirde durumları var olan belgeler rağmen ile paket yok. En azından, Visual Studio 2013 için hello Visual C++ yeniden dağıtılabilir paketleri yüklemeniz gerekir. zaten hello Kurulum işleminin bir parçası olarak çalışan bir yapılandırma komut dosyası aracılığıyla mevcut değilse hello Microsoft Azure Active Directory için Windows PowerShell Modülü yüklü. Olup olmadığını gerek tooinstall önceden bu modül zaten yüklü.

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Şirket içi Active Directory ile Azure Active Directory synched 

toouse hello NPS uzantısı, şirket içi kullanıcıları Azure Active Directory ile eşitlenen ve çok faktörlü kimlik doğrulaması için etkinleştirilmiş olmalıdır. Bu kılavuz, şirket içi kullanıcıları Azure AD Connect kullanarak Active Directory'e ile eşitlenir varsayar. Kullanıcılara MFA için etkinleştirmeye yönelik yönergeler aşağıda verilmiştir.
Azure AD hakkında bilgi için bağlanmak, bkz: [şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Azure Active Directory GUID kimliği 
tooinstall NPS Merhaba, tooknow hello hello Azure Active Directory GUİD'si gerekir. Merhaba sonraki bölümde hello hello Azure Active Directory GUID'sini bulmak için yönergeler sağlanmıştır.

## <a name="configure-radius-for-vpn-connections"></a>VPN bağlantıları için RADIUS yapılandırın

Bir üye sunucuda hello NPS sunucusu rolünü yüklediyseniz tooconfigure tooauthenticate gerekir ve VPN bağlantıları isteme VPN istemcisi yetkisi verin. 

Bu bölümde hello ağ ilkesi sunucusu rolünü yüklediyseniz ancak kullanım için altyapınızda yapılandırmadınız varsayar.

>[!NOTE]
>Merkezi bir RADIUS sunucusuna kimlik doğrulaması için kullandığı bir çalışma VPN sunucusu zaten varsa, bu bölümü atlayabilirsiniz.
>

### <a name="register-server-in-active-directory"></a>Sunucusu Active Directory'de Kaydettir
toofunction düzgün Bu senaryoda, Active Directory'de kayıtlı toobe hello NPS sunucusu gerekir.

1. Sunucu Yöneticisi'ni açın.
2. Sunucu Yöneticisi'nde **Araçları**ve ardından **ağ ilkesi sunucusu**. 
3. Merhaba ağ ilkesi sunucusu konsolunda sağ **NPS (yerel)**ve ardından **Active Directory'de kayıt sunucusu**. Tıklatın **Tamam** iki kez.

 ![Ağ İlkesi Sunucusu](./media/nps-extension-vpn/image2.png)

4. Merhaba konsolunu hello sonraki yordam için açık bırakın.

### <a name="use-wizard-tooconfigure-radius-server"></a>Sihirbaz tooconfigure RADIUS sunucusu kullan
Standart (Sihirbaz tabanlı) kullanabilirsiniz veya gelişmiş yapılandırma seçeneği tooconfigure hello RADIUS sunucusu. Bu bölümde hello hello sihirbaz tabanlı standart yapılandırma seçeneğinin kullanımını varsayar.

1. Merhaba ağ ilkesi sunucusu konsolunda **NPS (yerel)**.
2. Standart yapılandırmada seçin **çevirmeli veya VPN bağlantıları için RADIUS sunucusu**ve ardından **yapılandırma VPN veya çevirmeli**.

 ![VPN bağlantısını yapılandırma](./media/nps-extension-vpn/image3.png)

3. Merhaba Select çevirmeli ya da sanal özel ağ bağlantıları türü sayfasında, seçin **sanal özel ağ bağlantıları**, tıklatıp **sonraki**.

 ![Sanal özel ağ](./media/nps-extension-vpn/image4.png)

4. Merhaba belirtin çevirmeli veya VPN sunucusu sayfasında, tıklatın **Ekle**.
5. Merhaba, **yeni RADIUS istemcisi** iletişim kutusu, kolay bir ad sağlayın, hello çözümlenebilir adını veya hello VPN sunucusunun IP adresini girin ve paylaşılan gizli bir parola girin. Bu paylaşılan gizli parola uzun ve karmaşık olun. Merhaba sonraki bölümdeki adımları için gerek duyduğunuz bu parolayı kaydedin.

 ![Yeni RADIUS istemcisi](./media/nps-extension-vpn/image5.png)

6. Tıklatın **Tamam**ve ardından **sonraki**.
7. Merhaba üzerinde **kimlik doğrulama yöntemleri yapılandırma** hello varsayılan seçimi sayfasında, (Microsoft Şifreli kimlik doğrulaması sürüm 2 (MS-CHAPv2) veya başka bir seçenek belirleyin ve **sonraki**.

  >[!NOTE]
  >Genişletilebilir Kimlik Doğrulama Protokolü (EAP) yapılandırırsanız, MS CHAPv2 veya PEAP kullanmanız gerekir. Diğer bir EAP desteklenir.
 
8. Merhaba kullanıcı gruplarını belirtin sayfasında, tıklatın **Ekle** ve varsa, uygun bir grup seçin. Aksi takdirde, hello seçim boş toogrant erişim tooall kullanıcıları bırakın.

 ![Kullanıcı gruplarını belirtin](./media/nps-extension-vpn/image7.png)

9. **İleri**’ye tıklayın.
10. Merhaba IP filtreleri belirtin sayfasında, tıklatın **sonraki**.
11. Merhaba şifreleme ayarlarını belirtin sayfasında, hello varsayılan ayarları kabul edin ve **sonraki**.

 ![Şifreleme belirtin](./media/nps-extension-vpn/image8.png)

12. Hello bir bölge adı belirtin, hello adını boş bırakın, hello varsayılan ayarı kabul etmek ve tıklayın **sonraki**.

 ![Bir bölge adı belirtin](./media/nps-extension-vpn/image9.png)

13. Merhaba Tamamlanıyor yeni çevirmeli veya sanal özel ağ bağlantıları ve RADIUS istemcileri sayfasında, tıklatın **son**.

 ![Tam bağlantıları](./media/nps-extension-vpn/image10.png)

### <a name="verify-radius-configuration"></a>RADIUS yapılandırmasını doğrulayın.
Bu bölümde hello Sihirbazı kullanılarak oluşturulan hello yapılandırma ayrıntılarını verir.

1. Merhaba NPS sunucusunda, hello NPS (yerel) konsolunda, RADIUS istemcileri'ni genişletin ve seçin **RADIUS istemcileri**.
2. Merhaba RADIUS istemcisi Sihirbazı kullanılarak oluşturulan Hello ayrıntılar bölmesine sağ tıklayın ve **özellikleri**. RADIUS istemciniz (Merhaba VPN sunucusu) Hello özelliklerini aşağıda gösterilen benzer toothose olmalıdır.

 ![VPN özellikleri](./media/nps-extension-vpn/image11.png)

3. Tıklatın **iptal**.
4. Merhaba NPS (yerel) konsolunda, hello NPS sunucusunda genişletin **ilkeleri**seçip **bağlantı isteği ilkeleri**. Aşağıdaki hello görüntü benzer hello VPN bağlantıları İlkesi görmeniz gerekir.

 ![Bağlantı istekleri](./media/nps-extension-vpn/image12.png)

5. İlkeleri altında seçin **ağ ilkeleri**. Aşağıdaki hello görüntü benzer bir sanal özel ağ (VPN) bağlantıları İlkesi gerekir.

 ![Ağ Özellikleri](./media/nps-extension-vpn/image13.png)

## <a name="configure-vpn-server-toouse-radius-authentication"></a>VPN sunucusu toouse RADIUS kimlik doğrulamasını yapılandırma
Bu bölümde, hello VPN sunucusu toouse RADIUS kimlik doğrulamasını yapılandırın. Bu bölümde VPN sunucusunun çalışma yapılandırmaya sahip ancak hello VPN sunucu toouse RADIUS kimlik doğrulaması yapılandırılmamış olduğu varsayılır. Merhaba VPN sunucusunu yapılandırdıktan sonra yapılandırma beklendiği gibi çalıştığını doğrulayın.

>[!NOTE]
>RADIUS kimlik doğrulaması kullanan çalışan bir VPN sunucusu yapılandırması zaten varsa, bu bölümü atlayabilirsiniz.
>

### <a name="configure-authentication-provider"></a>Kimlik doğrulama sağlayıcısı yapılandırma
1. Merhaba VPN sunucusunda, Sunucu Yöneticisi'ni açın.
2. Sunucu Yöneticisi'nde **Araçları**ve ardından **Yönlendirme ve Uzaktan erişim**.
3. Merhaba Yönlendirme ve Uzaktan erişim konsolunda sağ  **\[sunucu adı\] (yerel)**ve ardından **özellikleri**.

 ![Yönlendirme ve Uzaktan erişim](./media/nps-extension-vpn/image14.png)
 
4. Merhaba, **[sunucu adı} (yerel) özellikleri** iletişim kutusunda, hello **güvenlik** sekmesi. 
5. Merhaba üzerinde **güvenlik** kimlik doğrulama sağlayıcısı altında sekmesini **RADIUS kimlik doğrulaması**ve ardından **yapılandırma**.

 ![RADIUS Kimlik Doğrulaması](./media/nps-extension-vpn/image15.png)
 
6. Merhaba RADIUS kimlik doğrulaması iletişim kutusunda tıklatın **Ekle**.
7. İçinde sunucu adı RADIUS sunucusu Ekle Merhaba, hello önceki bölümde yapılandırılan hello RADIUS sunucusu hello adı veya hello IP adresini ekleyin.
8. Paylaşılan gizlilik tıklatın **değişiklik** ve hello paylaşılan oluşturulur ve daha önce kaydedilen gizli parola ekleyin.
9. Merhaba değeri tooa değeri arasındaki zaman aşımı (saniye)'de, değiştirme **30** ve **60**. Bu gerekli tooallow toocomplete hello ikinci kimlik doğrulama faktörü yeterli zamandır.
 
 ![RADIUS sunucusu Ekle](./media/nps-extension-vpn/image16.png)
 
10. Tıklatın **Tamam** tüm iletişim kutularını kapatma işlemi tamamlanana kadar.

### <a name="test-vpn-connectivity"></a>VPN bağlantısını test etme
Bu bölümde, hello VPN istemci kimlik doğrulaması ve tooconnect tooVPN sanal bağlantı noktası çalıştığınızda hello RADIUS sunucusu tarafından yetkili onaylayın. Bu bölümde, bir VPN istemci olarak Windows 10 kullandığınızı varsayar. 

>[!NOTE]
>Önceden yapılandırılmış bir VPN istemci tooconnect toohello VPN sunucusu ve kaydedilen hello ayarları, hello adımları ilgili tooconfiguring ve bir VPN bağlantısı nesnesi kaydetme atlayabilirsiniz.
>

1. VPN istemci bilgisayarında **Başlat**ve ardından **ayarları** (dişli simgesi).
2. Pencere ayarlar'ı **ağ ve Internet**.
3. Tıklatın **VPN**.
4. Tıklatın **bir VPN bağlantısı Ekle**.
5. Bir VPN bağlantısı Ekle, VPN sağlayıcısı sonra uygun şekilde alanları kalan tam hello hello olarak Windows (yerleşik) belirtin ve tıklatın **kaydetmek**. 

 ![VPN bağlantısı Ekle](./media/nps-extension-vpn/image17.png)
 
6. Açık hello **ağ ve Paylaşım Merkezi** Denetim Masası'nda.
7. Tıklatın **Bağdaştırıcı ayarlarını değiştir**.

 ![Bağdaştırıcı ayarlarını değiştir](./media/nps-extension-vpn/image18.png)

8. Merhaba VPN ağ bağlantısına sağ tıklayın ve Özellikler'i tıklatın. 

 ![VPN ağ özellikleri](./media/nps-extension-vpn/image19.png)

9. Merhaba VPN Özellikleri iletişim kutusunda, hello tıklatın **güvenlik** sekmesi. 
10. Merhaba Güvenlik sekmesinde, yalnızca olun **Microsoft CHAP Version 2 (MS-CHAP v2)** seçilir ve Tamam'ı tıklatın.

 ![Protokollere izin ver](./media/nps-extension-vpn/image20.png)

11. Merhaba VPN bağlantısı sağ tıklayın ve **Bağlan**.
12. Hello Ayarları sayfasında, tıklatın **Bağlan**.

Aşağıda gösterildiği gibi hello güvenlik günlüğüne olay kimliği 6272'in, olarak hello RADIUS sunucusunda başarılı bir bağlantı görüntülenir.

 ![Olay Özellikleri](./media/nps-extension-vpn/image21.png)

## <a name="troubleshoot-guide"></a>Sorun giderme kılavuzu
VPN yapılandırması hello VPN sunucusu toouse merkezi bir RADIUS sunucusuna kimlik doğrulaması ve yetkilendirme için yapılandırılmış önce çalışır durumda olduğunu varsayalım. Bu durumda, hello RADIUS sunucusu veya hello kullanımını geçersiz kullanıcı adı veya parola yanlış yapılandırılması tarafından hello soruna neden olduğunu olasıdır. Örneğin, hello kullanıcı hello alternatif UPN soneki kullanırsanız, hello oturum açma denemesi başarısız olabilir (kullanması gereken en iyi sonuçlar için aynı hesap adına hello). 

Bu sorunlar, ideal yer toostart olduğundan tooexamine hello güvenlik olay günlüklerini tootroubleshoot hello RADIUS sunucusu. zaman toosave arama olaylar için hello rol tabanlı ağ ilkesi ve erişim sunucusu özel görünüm Olay Görüntüleyicisi'nde göster aşağıdaki kullanabilirsiniz. Olay Kimliği 6273 burada hello ağ ilkesi sunucusu tooa kullanıcıya erişim engellendi olayları gösterir. 

 ![Olay Görüntüleyicisi](./media/nps-extension-vpn/image22.png)
 
## <a name="configure-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulamasını yapılandırma
Bu bölümde, mfa ve iki aşamalı doğrulama için hesapları kurma için kullanıcıları etkinleştirme için yönergeler sağlar. 

### <a name="enable-multi-factor-authentication"></a>Multi-factor authentication’ı etkinleştirme
Bu bölümde, Azure AD hesapları için MFA etkinleştirin. Kullanım hello **Klasik portal** tooenable kullanıcılar için MFA. 

1. Bir tarayıcı açın ve çok gidin[https://manage.windowsazure.com](https://manage.windowsazure.com). 
2. Hello Yöneticisi olarak oturum açın.
3. Hello portalında, sol gezinti hello tıklatın **ACTIVE DIRECTORY**.

 ![Varsayılan dizini](./media/nps-extension-vpn/image23.png)

4. Merhaba adı sütununda tıklatın **varsayılan dizin** (veya başka bir dizin (uygunsa).
5. Merhaba hızlı başlangıç sayfasında, tıklatın **yapılandırma**.

 ![Varsayılan yapılandırma](./media/nps-extension-vpn/image24.png)

6. Hello yapılandırma sayfasında, aşağı kaydırın ve hello çok faktörlü kimlik doğrulaması bölümünde tıklayın **hizmet ayarlarını Yönet**.

 ![MFA ayarları yönetme](./media/nps-extension-vpn/image25.png)
 
7. Merhaba çok faktörlü kimlik doğrulaması sayfasında hello varsayılan hizmet ayarlarını gözden geçirin ve ardından **kullanıcılar**. 

 ![MFA Kullanıcıları](./media/nps-extension-vpn/image26.png)
 
8. MFA için tooenable ister ve ardından hello kullanıcıları Hello Kullanıcılar sayfasında, seçin **etkinleştirmek**.

 ![Özellikler](./media/nps-extension-vpn/image27.png)
 
9. İstendiğinde, tıklatın **etkinleştirmek çok öğeli kimlik doğrulama**.

 ![MFA'yı etkinleştirin](./media/nps-extension-vpn/image28.png)
 
10. **Kapat**’a tıklayın. 
11. Merhaba sayfayı yenileyin. Merhaba MFA durum değiştirilen tooEnabled ' dir.

Hakkında bilgi için tooenable kullanıcıları çok faktörlü kimlik doğrulaması için bkz. [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](multi-factor-authentication-get-started-cloud.md). 

### <a name="configure-accounts-for-two-step-verification"></a>İki aşamalı doğrulama için hesaplarını yapılandırma
Bir hesap MFA için etkinleştirildikten sonra kullanıcıların güvenilir cihaz toouse iki aşamalı doğrulamayı kullandıktan hello ikinci kimlik doğrulama faktörü için başarılı bir şekilde yapılandırmadığınız sürece hello MFA İlkesi tarafından yönetilen tooresources içinde mümkün toosign değildir.

Bu bölümde, iki aşamalı doğrulamayla birlikte kullanmak için güvenilir bir aygıt yapılandırın. Vardır, tooconfigure için çeşitli seçenekler bu hello aşağıdakiler dahil:

* **Mobil uygulama**. Bir Windows Phone, Android veya iOS aygıtında hello Microsoft Authenticator uygulamasını yükleyin. Kuruluşunuzun ilkelerine bağlı olarak, gerekli toouse hello uygulamada iki moddan birini şunlardır: (tooyour aygıt bir bildirim gönderilir) bildirimlerin Doğrulamalar için veya doğrulama kodunu kullan (gerekli tooenter bir doğrulama kodu Her 30 saniyede güncelleştirmeleri). 
* **Cep telefonu araması veya SMS**. Bir otomatik telefon çağrısı veya SMS mesajı ya da alabilir. Merhaba telefon araması seçeneğiyle hello aramayı yanıtlamalı ve hello # oturum tooauthenticate tuşuna basın. Merhaba metin seçeneğiyle toohello SMS mesajı yanıtlayın veya oturum açma hello arabirimine hello doğrulama kodunu girin.
* **Ofis telefonu araması**. Bu işlem olan hello otomatik telefon aramaları için yukarıda açıklanan aynıdır.

Doğrulama için aygıt toouse hello mobil uygulama tooreceive anında iletme bildirimi ayarlamak için bu yönergeleri izleyin.

1. Çok oturum[https://aka.ms/mfasetup](https://aka.ms/mfasetup) veya herhangi bir sitede gibi [https://portal.azure.com](https://portal.azure.com), burada MFA etkin kimlik bilgilerinizi kullanarak tooauthenticate gerekli. 
2. Kullanıcı adı ve parola ile imzalama sırasında tooset hello hesabı ek güvenlik doğrulaması isteyen bir ekran ile sunulur.

 ![Ek güvenlik](./media/nps-extension-vpn/image29.png)

3. Tıklatın **şimdi kurmak**.
4. Merhaba ek güvenlik doğrulama sayfasında, bir kişi bir türü (kimlik doğrulama telefon, ofis telefonu veya mobil uygulama) seçin. Ardından bir ülke veya bölgeyi seçin ve bir yöntem seçin. Merhaba yöntemi seçtiğiniz kişi türüne göre değişir. Örneğin, mobil uygulama seçerseniz, seçebileceğiniz olup olmadığını doğrulama veya toouse bir doğrulama kodu için tooreceive bildirimleri. izleyin hello adımlar varsayar seçtiğiniz **mobil uygulama** türü hello başvurun.

 ![Telefon kimlik doğrulama](./media/nps-extension-vpn/image30.png)

5. Mobil uygulama seçin, **doğrulama için bildirimlerin**ve ardından **ayarlanan**. 

 ![Mobil uygulama doğrulama](./media/nps-extension-vpn/image31.png)
 
6. Henüz yapmadıysanız, hello authenticator mobil uygulamasında cihazınıza yükleyin. 
7. Barkod sunulan hello mobil uygulama tooscan hello Hello yönergeleri izleyin veya hello bilgileri el ile girin ve ardından **Bitti**.

 ![Mobil uygulama yapılandırma](./media/nps-extension-vpn/image32.png)

8. Merhaba ek güvenlik doğrulama sayfasında, tıklatın **kişi benim** ve yanıt gönderilen toonotification tooyour aygıt.
9. Erişim toohello mobil uygulamayı kaybetmeniz ve tıklatın durumda hello ek güvenlik doğrulama sayfasında, kişi bir sayı girin **sonraki**.

 ![Cep telefonu numarası](./media/nps-extension-vpn/image33.png)
 
10. Ek güvenlik doğrulaması Hello üzerinde tıklatın **Bitti**.

Merhaba aygıt yapılandırılmış tooprovide ikinci bir doğrulama yöntemi sunulmuştur. İki aşamalı doğrulama hesaplarını ayarlama hakkında daha fazla bilgi için bkz: [Hesabımı iki aşamalı doğrulama için ayarlama](./end-user/multi-factor-authentication-end-user-first-time.md).

## <a name="install-and-configure-nps-extension"></a>Yükleme ve NPS uzantısı yapılandırma

Bu bölümde hello VPN sunucusu ile istemci kimlik doğrulaması için VPN toouse Azure MFA yapılandırmaya yönelik yönergeler sağlar.

Yükleyip hello NPS uzantısı yapılandırdıktan sonra bu sunucu tarafından işlenen tüm RADIUS tabanlı istemci kimlik doğrulaması gerekli toouse Azure MFA kullanılır. Aksi takdirde tüm VPN kullanıcıları Azure MFA kaydedilen, yapılandırılmış toouse MFA olmayan başka bir RADIUS sunucusu tooauthenticate kullanıcıların ayarlayabilirsiniz. Veya yalnızca MFA'kaydedilirse, ikinci bir kimlik doğrulama faktörü zorluğu olan kullanıcılar tooprovide izin veren bir kayıt defteri girdisi oluşturabilirsiniz. 

Adlı yeni bir dize değeri oluşturun _HKLM\SOFTWARE\Microsoft\AzureMfa REQUIRE_USER_MATCH_ve hello değeri tooTRUE ya da FALSE olarak ayarlayın. 

 ![Kullanıcı eşleşmesi iste](./media/nps-extension-vpn/image34.png)
 
Merhaba değer kümesi tooTRUE veya, tüm kimlik doğrulama isteklerini konu tooan MFA testini ayarlanmaz ise. TooFALSE Hello değeri ayarlarsanız, MFA güçlükler de MFA kaydedilen toousers verilir. Yalnızca hello ekleme süresi sırasında FALSE ayarını test veya üretim ortamlarında kullanın.

### <a name="acquire-azure-active-directory-guid-id"></a>Azure Active Directory GUID kimliği alma

Merhaba NPS uzantısı hello yapılandırmasını bir parçası olarak, Azure AD kiracınız için toosupply yönetici kimlik bilgileri ve hello Azure Active Directory kimliği gerekir. Merhaba adımları nasıl tooget hello Kiracı kimliği Göster

1. Azure Portalı ' toohello oturum [https://portal.azure.com](https://portal.azure.com) hello genel Yöneticisi hello Azure olarak Kiracı.
2. Sol gezinti hello hello tıklatın **Azure Active Directory** simgesi.
3. **Özellikler**'e tıklayın.
4. toocopy dizin kimliği toohello Pano, select hello **kopyalama** simgesi.
 
 ![Dizin kimliği](./media/nps-extension-vpn/image35.png)

### <a name="install-hello-nps-extension"></a>Merhaba NPS uzantısını yükleyin
Merhaba NPS uzantısı tasarımınızda hello RADIUS sunucusu olarak toobe hello ağ ilkesi olan bir sunucuda yüklü ve Erişim Hizmetleri (NPS) rolü yüklü ve bu işlevler gerekir. Merhaba NPS uzantısı, Uzak Masaüstü sunucusuna yüklemeyin.

1. Merhaba NPS uzantısını [https://aka.ms/npsmfa](https://aka.ms/npsmfa). 
2. Merhaba kurulum yürütülebilir dosya (NpsExtnForAzureMfaInstaller.exe) toohello NPS sunucusuna kopyalayın.
3. Merhaba NPS sunucusunda, çift **NpsExtnForAzureMfaInstaller.exe**. İstenirse, tıklatın **çalıştırmak**.
4. Azure MFA iletişim kutusu için Hello NPS uzantısı, hello yazılım lisans koşullarını gözden denetleyin **toohello lisans şart ve koşullarını kabul ediyorum**, tıklatıp **yükleme**.

 ![NPS uzantısı](./media/nps-extension-vpn/image36.png)
 
5. Azure MFA iletişim kutusu için Hello NPS uzantısı,'ı tıklatın **Kapat**.  

 ![Kurulum başarılı](./media/nps-extension-vpn/image37.png) 
 
### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Sertifikaları kullanmak için bir PowerShell Betiği kullanılarak hello NPS uzantısı ile yapılandırma
tooensure güvenli iletişimler ve Güvencesi, tooconfigure sertifikaları hello NPS uzantısı tarafından kullanılmak üzere gerekir. Merhaba NPS bileşenler, NPS ile otomatik olarak imzalanan bir sertifika kullanmak için yapılandırır bir Windows PowerShell komut dosyası içerir. 

Merhaba betik hello aşağıdaki eylemleri gerçekleştirir:

* Kendinden imzalı bir sertifika oluşturur
* Sertifika tooservice üzerinde Azure AD asıl ortak anahtarı ilişkilendirir
* Merhaba yerel makine deposunda sertifika depoları hello
* Verir toohello sertifikanın özel anahtar toohello ağ kullanıcı erişimi
* Ağ İlkesi Sunucusu hizmetini yeniden başlatır

Kendi sertifikaları toouse isterseniz, üzerinde Azure AD tooassociate hello ortak sertifika toohello hizmet ilkesi gerekir ve benzeri.
toouse hello komut dosyası, Azure Active Directory yönetici kimlik bilgilerinizle hello uzantısı sağlayın ve Azure Active Directory Kiracı kimliği daha önce kopyaladığınız hello. Merhaba betiği hello NPS uzantısı yüklediğiniz her NPS sunucusunda çalıştırın.

1. Bir yönetici Windows PowerShell komut istemini açın.
2. Merhaba PowerShell isteminde _cd 'c:\Program Files\Microsoft\AzureMfa\Config'_ve basın **ENTER**.
3. Tür _.\AzureMfsNpsExtnConfigSetup.ps1_ve basın **ENTER**. 
 * Hello Azure Active Directory PowerShell modülü yüklüyse hello betik toosee denetler. Yüklenmemişse, hello betik hello modülünü yükler.
 
 ![PowerShell](./media/nps-extension-vpn/image38.png)
 
4. Merhaba betik hello yükleme hello PowerShell modülünün doğruladıktan sonra hello Azure Active Directory PowerShell modülü iletişim kutusu görüntüler. Hello iletişim kutusunda, Azure AD yönetici kimlik bilgilerinizi ve parola girin ve tıklayın **oturum**. 
 
 ![PowerShell oturum açma](./media/nps-extension-vpn/image39.png)
 
5. İstendiğinde, kopyaladığınız toohello Pano önceki hello Kiracı kimliği yapıştırın ve tuşuna basın **ENTER**. 

 ![Kiracı Kimliği](./media/nps-extension-vpn/image40.png)

6. Merhaba komut dosyası otomatik olarak imzalanan bir sertifika oluşturur ve başka yapılandırma değişiklikleri yapar. Merhaba görüntü aşağıda gösterildiği gibi Hello çıkışı yapılır.

 ![Otomatik olarak imzalanan sertifika](./media/nps-extension-vpn/image41.png)

7. Merhaba sunucusunu yeniden başlatın.
 
### <a name="verify-configuration"></a>Yapılandırmayı doğrulama
tooverify hello yapılandırma tooestablish VPN sunucusu ile yeni bir VPN bağlantısı gerekir. Merhaba bağlantı kurulmadan önce kimlik bilgilerinizi birincil kimlik doğrulaması için başarıyla girildikten sonra VPN bağlantısı hello hello ikincil kimlik doğrulama toosucceed için aşağıda gösterildiği gibi bekler. 

 ![Yapılandırmayı doğrulama](./media/nps-extension-vpn/image42.png)

Başarılı bir şekilde Azure MFA önceden yapılandırılmış hello ikincil doğrulama yöntemi, kimlik doğrulaması, bağlı toohello kaynak demektir. Ancak, Hello ikincil kimlik doğrulaması başarılı olmazsa, erişim tooresource reddedilir. 

Aşağıda, hello Doğrulayıcı hello örnekte kullanılan tooprovide hello ikincil kimlik doğrulaması Windows Phone Uygulama şeklindedir.

 ![Kullanıcı hesabının doğrulanması](./media/nps-extension-vpn/image43.png)

Merhaba ikincil yöntemini kullanarak başarıyla doğrulandıktan sonra erişim toohello hello VPN sunucuda sanal bağlantı noktası verilir. Ancak, gerekli toouse güvenilen bir cihazda bir mobil uygulama kullanarak bir ikincil kimlik doğrulama yöntemi olduğundan hello işlem günlüğünde yalnızca bir kullanıcı adı kullanarak daha daha güvenli olan / parola bileşimi.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Başarılı oturum açma olayları için Olay Görüntüleyicisi'ni günlüklerini görüntüle
tooview hello başarılı oturum açma olaylarını Windows Olay Görüntüleyicisi günlüklerinde hello Windows PowerShell komut tooquery hello Windows Güvenlik günlüğü hello NPS sunucusunda aşağıdaki hello verebilir.

tooquery başarılı oturum açma olaylarını hello Güvenlik Olay Görüntüleyicisi günlüklerinde, komutu aşağıdaki hello kullanın,
* _Get-WinEvent - günlükadı güvenlik_ | burada {$_.ID - eq '6272'in '} | FL 

 ![Güvenlik Olay Görüntüleyicisi](./media/nps-extension-vpn/image44.png)
 
Aşağıda gösterildiği gibi hello güvenlik günlüğü veya hello Ağ İlkesi ve Erişim Hizmetleri özel görünümü de görüntüleyebilirsiniz:

 ![Ağ İlkesi erişimi](./media/nps-extension-vpn/image45.png)

Azure MFA için hello NPS uzantısı yüklendiği hello sunucuda Olay Görüntüleyicisi'ni uygulama günlüklerini belirli toohello uzantısına bulabilirsiniz **uygulama ve Hizmetleri Logs\Microsoft\AzureMfa**. 

* _Get-WinEvent - günlükadı güvenlik_ | burada {$_.ID - eq '6272'in '} | FL

 ![Olay (Event) Sayısı](./media/nps-extension-vpn/image46.png)

## <a name="troubleshoot-guide"></a>Sorun giderme kılavuzu
Merhaba yapılandırma beklendiği gibi çalışmıyorsa, iyi toostart tootroubleshoot kullanıcı hello tooverify yapılandırılmış toouse Azure MFA numarasıdır. Çok bağlanmak hello kullanıcınız[https://portal.azure.com](https://portal.azure.com). İkincil kimlik doğrulaması için istenir ve başarıyla için kimlik doğrulaması, Azure mfa yapılandırması hatalı ortadan kaldırabilirsiniz.

Azure MFA için hello kullanıcıları çalışıyorsanız hello ilgili olay günlüklerini gözden geçirmelidir. Bunlar hello önceki bölümde tartışılan hello güvenlik olayı, ağ geçidi işletimsel ve Azure MFA günlüklerini içerir. 

Güvenlik günlüğü başarısız oturum açma olayı (olay kimliği 6273) gösteren bir örnek çıktı aşağıdadır:

 ![Güvenlik günlüğü](./media/nps-extension-vpn/image47.png)

Merhaba AzureMFA günlükleri ilgili bir olayın aşağıdadır:

 ![Azure MFA günlükleri](./media/nps-extension-vpn/image48.png)

Gelişmiş tooperform seçenekleri, başvurun hello NPS veritabanı biçim günlük dosyalarının hello NPS hizmetinin yüklendiği sorunlarını giderin. Bu günlük dosyaları oluşturulur _%SystemRoot%\System32\Logs_ klasörü virgülle ayrılmış metin dosyalarını olarak. Bu bir açıklaması için günlük dosyaları, bkz: [NPS veritabanı biçimi günlük dosyalarını yorumlama](https://technet.microsoft.com/library/cc771748.aspx). 

Bu günlük dosyalarındaki Hello girişler bir elektronik tablo veya bir veritabanına alma olmadan zor toointerpret oluşur. Bir sayı bulabilirsiniz IAS ayrıştırıcıları çevrimiçi tooassist günlük dosyalarını size yorumlama hello. Bir hello çıktısını aşağıdadır böyle indirilebilir [paylaşılan yazılım uygulama](http://www.deepsoftware.com/iasviewer): 

 ![Paylaşılan yazılım uygulama](./media/nps-extension-vpn/image49.png)

Son olarak, için ek seçenekleri sorun giderme, Wireshark gibi bir iletişim kuralı çözümleyicisi kullanabilir veya [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). Merhaba Wireshark aşağıdaki görüntüden hello VPN sunucusu ile Merhaba NPS sunucusu arasında hello RADIUS iletileri gösterir.

 ![Microsoft Message Analyzer](./media/nps-extension-vpn/image50.png)

Daha fazla bilgi için bkz: [varolan NPS altyapınızı Azure çok faktörlü kimlik doğrulamasıyla tümleştirmek](multi-factor-authentication-nps-extension.md).  

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md)

[RADIUS kullanan Uzak Masaüstü Ağ Geçidi ve Azure Multi-Factor Authentication Sunucusu](multi-factor-authentication-get-started-server-rdg.md)

[Şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](../active-directory/connect/active-directory-aadconnect.md)

