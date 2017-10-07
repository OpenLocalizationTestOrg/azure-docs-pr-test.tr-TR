---
title: "Azure MFA NPS uzantısı ile Masaüstü Ağ Geçidi tümleştirme aaaRemote | Microsoft Docs"
description: "Bu makalede, Microsoft Azure için hello ağ ilkesi sunucusu (NPS) uzantısını kullanarak Azure MFA ile Uzak Masaüstü Ağ Geçidi altyapınızı tümleştirme anlatılmaktadır."
services: active-directory
keywords: "Azure MFA, Uzak Masaüstü Ağ geçidi, Azure Active Directory, ağ ilkesi sunucusu uzantısı tümleştirme"
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
ms.openlocfilehash: ae5f6864416582bd82b787005ca787988d23a813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="integrate-your-remote-desktop-gateway-infrastructure-using-hello-network-policy-server-nps-extension-and-azure-ad"></a>Uzak Masaüstü Ağ Geçidi altyapınızı Hello ağ ilkesi sunucusu (NPS) uzantısı Azure AD ile tümleştirme

Bu makalede ayrıntıları Uzak Masaüstü Ağ Geçidi altyapınızı Azure çok faktörlü kimlik doğrulama (MFA) ile tümleştirmek için Microsoft Azure için hello ağ ilkesi sunucusu (NPS) uzantısını kullanarak sağlar. 

Hello Azure Ağ İlkesi Hizmeti (NPS) uzantısı sağlayan Azure kullanarak müşteriler toosafeguard Uzaktan Kimlik Doğrulama Çevirmeli Kullanıcı Hizmeti (RADIUS) istemci kimlik doğrulaması bulut tabanlı [çok faktörlü kimlik doğrulama (MFA)](multi-factor-authentication.md). Bu çözüm güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı eklemek için iki aşamalı doğrulama sağlar.

Bu makalede, Azure için hello NPS uzantısını kullanarak hello NPS altyapı Azure MFA ile tümleştirmek için adım adım yönergeler sağlar. Bu, Uzak Masaüstü Ağ Geçidi tooa üzerinde toolog deneyen kullanıcılar için güvenli doğrulaması sağlar. 

Merhaba Ağ İlkesi ve Erişim Hizmetleri (NPS) verir kuruluşlar özelliği toodo hello aşağıdaki hello:
* Bağlanabilecek kişileri belirterek hello yönetim ve ağ isteklerinin denetim merkezi konumlarını tanımlayın, ne zaman bağlantılara izin verilir, günün hello bağlantıları süresini ve istemciler gerekir tooconnect kullanın vb. güvenlik hello düzeyi. Bu ilkelerin her VPN veya Uzak Masaüstü (RD) Ağ Geçidi sunucusunda belirtmek yerine, bu ilkeler, bir kez merkezi bir konumda belirtilebilir. Merhaba RADIUS protokolü, kimlik doğrulama, yetkilendirme ve hesap oluşturma (AAA) hello merkezi sağlar. 
* Kurmak ve cihazları Kısıtlanmamış veya kısıtlanmış erişim toonetwork kaynaklara erişim izni verilmiş olup olmadığını belirleyen Ağ Erişim Koruması (NAP) istemci sistem durumu ilkeleri zorlayın.
* Bir yol tooenforce kimlik doğrulama ve yetkilendirme access too802.1x özellikli kablosuz erişim noktaları ve Ethernet anahtarları için sağlar.    

Genellikle, kuruluşların NPS (RADIUS) toosimplify kullanın ve VPN hello yönetimini merkezileştirme ilkeleri. Bununla birlikte, çoğu kuruluş ayrıca NPS toosimplify kullanabilir ve RD Masaüstü Bağlantı Yetkilendirme İlkeleri (RD CAP) hello yönetimini merkezileştirme. 

Kuruluşlar, ayrıca Azure MFA tooenhance güvenliği NPS tümleştirmek ve yüksek bir uyumluluk düzeyini sağlamak. Bu, kullanıcıların iki aşamalı doğrulama toolog toohello Uzak Masaüstü Ağ Geçidi üzerinde kurmak sağlamaya yardımcı olur. Erişim izni kullanıcılar toobe için kendi kullanıcı adı/parola bileşimi kullanıcı hello bilgilerle kendi denetiminde sahip sağlamaları gerekir. Bu bilgiler güvenilir ve kolayca çoğaltılması, cep telefonu numarası, telefona numarası, uygulama, bir mobil cihaz ve benzerleri gibi.

Hello Azure NPS uzantısı kullanılabilirliğini önceki toohello, NPS tooimplement iki aşamalı doğrulama için onlardan müşteriler tümleşik ve Azure MFA ortamları tooconfigure var ve ayrı bir MFA sunucusu hello şirket içi ortamda korumak içinde belirtilen [Uzak Masaüstü Ağ geçidi ve Azure multi-Factor Authentication sunucusu RADIUS kullanan](multi-factor-authentication-get-started-server-rdg.md).

Azure hello NPS uzantısı Hello kullanılabilirliğini kuruluşlar hello seçim toodeploy şirket tabanlı MFA çözümünü ya bir bulut tabanlı MFA çözüm toosecure RADIUS istemci kimlik doğrulaması şimdi sağlar.

## <a name="authentication-flow"></a>Kimlik doğrulama akışı

Kullanıcılar için bir RD Bağlantı Yetkilendirme İlkesi (RD CAP) ve bir RD kaynak yetkilendirme ilkesi (RD RAP) belirtilen hello koşullara uyması gerekir, Uzak Masaüstü Ağ geçidi, üzerinden toonetwork kaynaklara erişmelerine toobe verildi. RD CAP yetkili tooconnect tooRD ağ geçitleri kim belirtin. RD RAP belirtin hello ağ kaynaklarına, Uzak Masaüstü veya uzak uygulamalar gibi hello kullanıcı izin verilir tooconnect toothrough hello RD Ağ geçidi. 

RD Ağ Geçidi yapılandırılmış toouse RD CAP için bir merkezi ilke deposu olabilir. RD Ağ Geçidi hello üzerinde işlenene olarak RD RAP bir merkezi ilke kullanamazsınız. RD Ağ Geçidi yapılandırılmış toouse RD CAP için bir merkezi ilke deposu hello merkezi ilke deposu olarak hizmet veren bir RADIUS istemcisi tooanother NPS sunucusu örneğidir.

Hello Azure NPS uzantısı hello NPS ve Uzak Masaüstü Ağ geçidi ile tümleştirildiğinde hello başarılı kimlik doğrulaması akışı aşağıdaki gibidir:

1. Merhaba Uzak Masaüstü Ağ Geçidi sunucusu bir kaynaktan Uzak Masaüstü kullanıcı tooconnect tooa, Uzak Masaüstü oturumu gibi bir kimlik doğrulama isteği alır. Bir RADIUS istemcisi olarak işlev gören, hello Uzak Masaüstü Ağ Geçidi sunucusu hello istek tooa RADIUS Erişim-İstek iletisi dönüştürür ve hello NPS uzantısı yüklendiği hello message toohello RADIUS (NPS) sunucusu gönderir. 
2. hello kullanıcı adı ve parola birleşimi Active Directory'de doğrulanır ve hello kullanıcının kimliği doğrulanır.
3. Tüm koşullar belirtildiği gibi hello NPS bağlantı isteğini hello ve hello ağ ilkeleri karşılanmadığı (örneğin, süresi gün veya grup üyeliği kısıtlamaları), hello NPS uzantısı Azure MFA ile ikincil kimlik doğrulama isteği tetikler. 
4. Azure MFA, Azure AD ile iletişim kurar, hello kullanıcının ayrıntılarını alır ve (SMS mesajı, mobil uygulama ve benzeri) hello kullanıcı tarafından yapılandırılan hello yöntemini kullanarak hello ikincil kimlik doğrulaması gerçekleştirir. 
5. Merhaba MFA testini Başarı sonucu hello sonuç toohello NPS uzantısı Azure MFA ile iletişim kurar.
6. Merhaba uzantısı yüklendiği hello NPS sunucusu hello RD CAP İlkesi toohello Uzak Masaüstü Ağ Geçidi sunucusu için bir RADIUS Erişim Kabul iletisi gönderir.
7. Merhaba kullanıcıya erişim izni toohello istenen hello RD Ağ geçidi üzerinden ağ kaynağı.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde hello Önkoşullar hello Uzak Masaüstü Ağ geçidi ile Azure MFA tümleştirme önce gerekli ayrıntıları. Başlamadan önce aşağıdaki önkoşulların yerinde hello olması gerekir.  

* Uzak Masaüstü Hizmetleri (RDS) altyapısı
* Azure MFA lisans
* Windows Server yazılımı
* Ağ İlkesi ve Erişim Hizmetleri (NPS) rol
* Azure AD synched ile şirket içi AD 
* Azure Active Directory GUID kimliği

### <a name="remote-desktop-services-rds-infrastructure"></a>Uzak Masaüstü Hizmetleri (RDS) altyapısı
Çalışan bir Uzak Masaüstü Hizmetleri (RDS) altyapısının yerinde olması gerekir. Ardından Azure içinde hızlı bir şekilde bu altyapı oluşturabilirsiniz, istemiyorsanız hello aşağıdakileri kullanarak hızlı başlangıç şablonu: [Uzak Masaüstü Oturum Koleksiyonu Oluştur dağıtım](https://github.com/Azure/azure-quickstart-templates/tree/ad20c78b36d8e1246f96bb0e7a8741db481f957f/rds-deployment). 

İsterseniz toomanually hızlı bir şekilde test amacıyla, bir şirket içi RDS altyapı izleme hello adımları toodeploy bir oluşturun. 
**Daha fazla bilgi edinin**: [dağıtmak RDS Azure Hızlı Başlangıç ile](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-in-azure) ve [temel RDS altyapı dağıtımı](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-deploy-infrastructure). 

### <a name="licenses"></a>Lisansları
Gerekli bir Azure AD Premium, Enterprise Mobility artı güvenlik (EMS) veya bir MFA abonelik kullanılabilir olan Azure MFA bir lisans kullanılır. Daha fazla bilgi için bkz: [nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md). Test amacıyla bir deneme aboneliği kullanabilirsiniz.

### <a name="software"></a>Yazılım
Merhaba NPS uzantısı gerektiren Windows Server 2008 R2 SP1 veya üstü yüklü hello NPS rol hizmetine sahip. Bu bölümdeki tüm hello adımlar, Windows Server 2016 kullanılarak gerçekleştirilen.

### <a name="network-policy-and-access-services-nps-role"></a>Ağ İlkesi ve Erişim Hizmetleri (NPS) rol
Merhaba NPS rol hizmetinin işlevselliğinin yanı sıra ağ erişim ilkesi sistem durumu hizmeti hello RADIUS sunucusu ve istemci sağlar. Bu rol altyapınızda en az iki bilgisayara yüklenmesi gerekir: Uzak Masaüstü Ağ geçidi ve başka bir hello üye sunucu veya etki alanı denetleyicisi. Varsayılan olarak, hello rol hello Uzak Masaüstü Ağ Geçidi yapılandırılmış hello bilgisayarda zaten.  Ayrıca hello NPS rolü üzerinde en az bir etki alanı denetleyicisi veya üye sunucu gibi başka bir bilgisayara yüklemeniz gerekir.

Merhaba NPS rolü yükleme hakkında bilgi için Windows Server 2012 veya daha eski hizmet için bkz: [bir NAP sistem durumu ilkesi sunucusu yükleme](https://technet.microsoft.com/library/dd296890.aspx). NPS, bir etki alanı denetleyicisinde de dahil olmak üzere hello öneri tooinstall NPS için en iyi uygulamaları bir açıklaması için bkz: [NPS için en iyi uygulamaları](https://technet.microsoft.com/library/cc771746).

### <a name="azure-active-directory-synched-with-on-premises-active-directory"></a>Şirket içi Active Directory ile Azure Active Directory synched 
toouse hello NPS uzantısı, şirket içi kullanıcıları Azure AD ile eşitlenen ve MFA için etkinleştirilmiş olmalıdır. Bu bölümde, şirket içi kullanıcıların AD Connect kullanan Azure AD ile eşitlenir varsayar. Azure AD hakkında bilgi için bağlanmak, bkz: [şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](../active-directory/connect/active-directory-aadconnect.md). 

### <a name="azure-active-directory-guid-id"></a>Azure Active Directory GUID kimliği
NPS tooinstall, tooknow hello hello Azure AD GUİD'si gerekir. Hello GUID hello Azure AD değerini bulmak için yönergeler aşağıda verilmiştir.

## <a name="configure-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulamasını yapılandırma 
Bu bölümde Azure MFA hello Uzak Masaüstü Ağ geçidi ile tümleştirmek için yönergeler sağlar. Yönetici olarak, kullanıcılar, çok faktörlü aygıtları veya uygulamaları kendi kendine kaydedebilmek için hello Azure MFA hizmetini yapılandırmanız gerekir.

Merhaba adımları [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](multi-factor-authentication-get-started-cloud.md) tooenable MFA, Azure AD kullanıcılarınızın. 

### <a name="configure-accounts-for-two-step-verification"></a>İki aşamalı doğrulama için hesaplarını yapılandırma
Bir hesap oturum açamazsınız MFA için etkinleştirildikten sonra tooresources MFA İlkesi tarafından hello hello ikinci kimlik doğrulama faktörü kimlik doğrulaması için iki aşamalı doğrulama kullanarak bir güvenilen cihazı toouse başarılı bir şekilde yapılandırmadığınız sürece kapsamındadır.

Merhaba adımları [ne Azure çok faktörlü kimlik doğrulaması için beni anlama geliyor?](./end-user/multi-factor-authentication-end-user.md) toounderstand ve cihazlarınızı MFA için kullanıcı hesabınızla düzgün bir şekilde yapılandırmak.

## <a name="install-and-configure-nps-extension"></a>Yükleme ve NPS uzantısı yapılandırma
Bu bölümde hello ile Uzak Masaüstü Ağ Geçidi istemci kimlik doğrulaması için RDS altyapı toouse Azure MFA yapılandırmaya yönelik yönergeler sağlar.

### <a name="acquire-azure-active-directory-guid-id"></a>Azure Active Directory GUID kimliği alma

Merhaba NPS uzantısı hello yapılandırmasını bir parçası olarak, Azure AD kiracınız için toosupply yönetici kimlik bilgileri ve hello Azure AD kimliği gerekir. Aşağıdaki adımları hello nasıl tooget hello Kiracı kimliği Göster

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello genel Yöneticisi hello Azure olarak Kiracı.
2. Sol gezinti hello hello seçin **Azure Active Directory** simgesi.
3. Seçin **özellikleri**.
4. Merhaba özellikleri dikey penceresinde hello dizin kimliği, yanında hello tıklatın **kopyalama** toocopy hello kimliği tooclipboard aşağıda gösterildiği gibi simgesi.

 ![Özellikler](./media/nps-extension-remote-desktop-gateway/image1.png)

### <a name="install-hello-nps-extension"></a>Merhaba NPS uzantısını yükleyin
Merhaba NPS uzantısı hello Ağ İlkesi ve Erişim Hizmetleri (NPS) rolü yüklü olan bir sunucuya yükleyin. Bu, hello RADIUS sunucusu tasarımınızın görür. 

>[!Important]
> Uzak Masaüstü Ağ Geçidi sunucunuzda hello NPS uzantısı yüklemeyin emin olun.
> 

1. Merhaba karşıdan [NPS uzantısı](https://aka.ms/npsmfa). 
2. Merhaba kurulum yürütülebilir dosya (NpsExtnForAzureMfaInstaller.exe) toohello NPS sunucusuna kopyalayın.
3. Merhaba NPS sunucusunda, çift **NpsExtnForAzureMfaInstaller.exe**. İstenirse, tıklatın **çalıştırmak**.
4. Azure MFA iletişim kutusu için Hello NPS uzantısı, hello yazılım lisans koşullarını gözden denetleyin **toohello lisans şart ve koşullarını kabul ediyorum**, tıklatıp **yükleme**.
 
  ![Azure MFA Kurulumu](./media/nps-extension-remote-desktop-gateway/image2.png)

5. Azure MFA iletişim kutusu için Hello NPS uzantısı, Kapat'ı tıklatın. 

  ![Azure MFA için NPS uzantısı](./media/nps-extension-remote-desktop-gateway/image3.png)

### <a name="configure-certificates-for-use-with-hello-nps-extension-using-a-powershell-script"></a>Sertifikaları kullanmak için bir PowerShell Betiği kullanılarak hello NPS uzantısı ile yapılandırma
Ardından, hello NPS uzantısı tooensure güvenli iletişimler ve güvence tarafından kullanılmak üzere tooconfigure sertifikalar gerekir. Merhaba NPS bileşenler, NPS ile otomatik olarak imzalanan bir sertifika kullanmak için yapılandırır bir Windows PowerShell komut dosyası içerir. 

Merhaba betik hello aşağıdaki eylemleri gerçekleştirir:

* Kendinden imzalı bir sertifika oluşturur
* Sertifika tooservice üzerinde Azure AD asıl ortak anahtarı ilişkilendirir
* Merhaba yerel makine deposunda sertifika depoları hello
* Verir erişim toohello sertifikanın özel anahtar toohello ağ kullanıcısı
* Ağ İlkesi Sunucusu hizmetini yeniden başlatır

Kendi sertifikaları toouse isterseniz, üzerinde Azure AD tooassociate hello ortak sertifika toohello hizmet ilkesi gerekir ve benzeri.

toouse hello betik hello uzantısı ile Azure AD yönetici kimlik bilgilerinizi sağlayın ve daha önce kopyaladığınız Azure AD Kiracı kimliği hello. Merhaba betiği hello NPS uzantısı yüklü olduğu her NPS sunucusunda çalıştırın. Ardından aşağıdaki hello:

1. Bir yönetici Windows PowerShell komut istemini açın.
2. Merhaba PowerShell isteminde **cd 'c:\Program Files\Microsoft\AzureMfa\Config'**ve basın **ENTER**.
3. Tür _.\AzureMfsNpsExtnConfigSetup.ps1_ve basın **ENTER**. Hello Azure Active Directory PowerShell modülü yüklüyse hello betik toosee denetler. Yüklü değilse, hello betik hello modülünü yükler.

  ![Azure AD PowerShell](./media/nps-extension-remote-desktop-gateway/image4.png)
  
4. Merhaba betik hello yükleme hello PowerShell modülünün doğruladıktan sonra hello Azure Active Directory PowerShell modülü iletişim kutusu görüntüler. Hello iletişim kutusunda, Azure AD yönetici kimlik bilgilerinizi ve parola girin ve tıklayın **oturum**.

  ![PowerShell hesap açın](./media/nps-extension-remote-desktop-gateway/image5.png)

5. İstendiğinde, kopyaladığınız toohello Pano önceki hello Kiracı kimliği yapıştırın ve tuşuna basın **ENTER**.

  ![Kiracı kimliği girin](./media/nps-extension-remote-desktop-gateway/image6.png)

6. Merhaba komut dosyası otomatik olarak imzalanan bir sertifika oluşturur ve başka yapılandırma değişiklikleri yapar. Merhaba çıktısı hello görüntü aşağıda gösterildiği gibi olmalıdır.

  ![Otomatik olarak imzalanan sertifika](./media/nps-extension-remote-desktop-gateway/image7.png)

## <a name="configure-nps-components-on-remote-desktop-gateway"></a>Uzak Masaüstü Ağ Geçidi üzerinde NPS bileşenlerini yapılandırma
Bu bölümde, hello Uzak Masaüstü Ağ Geçidi bağlantısı Yetkilendirme İlkeleri ve diğer RADIUS ayarlarını yapılandırın.

RADIUS iletileri hello NPS sunucusunun yüklendiği hello Uzak Masaüstü Ağ geçidi ve hello NPS sunucusu arasında değiştirilebilmesi Hello kimlik doğrulaması akışı gerektirir. Başka bir deyişle, hello NPS uzantısı yüklendiği Uzak Masaüstü Ağ geçidi ve hello NPS sunucusunda RADIUS istemci ayarları yapılandırmanız gerekir. 

### <a name="configure-remote-desktop-gateway-connection-authorization-policies-toouse-central-store"></a>Uzak Masaüstü Ağ Geçidi bağlantısı Yetkilendirme İlkeleri toouse merkezi deposu yapılandırma
Uzak Masaüstü Bağlantısı Yetkilendirme İlkeleri (RD CAP) bağlanan tooa Uzak Masaüstü Ağ Geçidi sunucusu için hello gereksinimleri belirtin. RD CAP yerel olarak depolanabilir (varsayılan) veya bunlar depolanabilir NPS çalıştıran merkezi bir RD CAP Deposu içinde. Azure MFA RDS ile tümleştirilmesi tooconfigure, merkezi bir depo toospecify hello kullanımını gerekir.

1. Merhaba RD Ağ Geçidi sunucusunda açın **Sunucu Yöneticisi'ni**. 
2. Başlangıç menüsünde **Araçları**, çok noktası**Uzak Masaüstü Hizmetleri**ve ardından **Uzak Masaüstü Ağ Geçidi Yöneticisi**.

  ![Uzak Masaüstü Hizmetleri](./media/nps-extension-remote-desktop-gateway/image8.png)

3. Hello RD Ağ Geçidi Yöneticisi, sağ  **\[sunucu adı\] (yerel)**, tıklatıp **özellikleri**.

  ![Sunucu adı](./media/nps-extension-remote-desktop-gateway/image9.png)

4. Merhaba Hello Özellikleri iletişim kutusunda seçin **RD CAP** deposu sekmesinde.
5. Merhaba RD CAP Deposu sekmesinde seçin **merkezi NPS çalıştıran sunucuyu**. 
6. Merhaba, **NPS çalıştıran hello sunucusu için bir ad veya IP adresi girin** alanı, tür hello IP adresini veya sunucu adını hello NPS uzantısı yüklendiği hello sunucu.

  ![Adı veya IP adresini girin](./media/nps-extension-remote-desktop-gateway/image10.png)
  
7. **Ekle**'ye tıklayın.
8. Merhaba, **paylaşılan gizliliği** iletişim kutusu, bir paylaşılan gizlilik girin ve ardından **Tamam**. Bu paylaşılan gizliliği kaydedin ve hello kayıt güvenli bir şekilde depoladığınızdan emin olun.

 >[!NOTE]
 >Paylaşılan gizliliği kullanılır hello RADIUS sunucuları ve istemciler arasında tooestablish güven. Uzun ve karmaşık bir parola oluşturun.
 >

 ![Paylaşılan gizlilik](./media/nps-extension-remote-desktop-gateway/image11.png)

9. Tıklatın **Tamam** tooclose hello iletişim kutusu.

### <a name="configure-radius-timeout-value-on-remote-desktop-gateway-nps"></a>Uzak Masaüstü Ağ Geçidi NPS üzerinden RADIUS zaman aşımı değerini yapılandırın
tooensure var olan toovalidate kullanıcıların kimlik bilgilerini zaman, iki aşamalı doğrulamayı gerçekleştirmek, yanıtları almak ve tooRADIUS iletilerine yanıt, gerekli tooadjust hello RADIUS zaman aşımı değeri değildir.

1. Merhaba RD Ağ Geçidi sunucusu, Sunucu Yöneticisi ' nde tıklayın **Araçları**ve ardından **ağ ilkesi sunucusu**. 
2. Merhaba, **NPS (yerel)** genişletin **RADIUS istemcileri ve sunucuları**seçip **uzak RADIUS sunucu**.

 ![Uzak RADIUS sunucusu](./media/nps-extension-remote-desktop-gateway/image12.png)

3. Merhaba Ayrıntılar bölmesinde, çift **TH Ağ Geçidi sunucusu GRUBUNU**.

 >[!NOTE]
 >Merhaba merkezi sunucu NPS ilkeleri için yapılandırıldığında bu RADIUS sunucu grubu oluşturuldu. Merhaba RD Ağ Geçidi RADIUS iletileri toothis sunucu veya sunucu grubu hello grubundaki olandan daha fazla olması durumunda iletir.
 >

4. Merhaba, **TH Ağ Geçidi sunucu grubu özellikleri** iletişim kutusunda, select hello IP adresi veya hello toostore RD CAP yapılandırılmış NPS sunucusu ve ardından adını **Düzenle**. 

 ![TH Ağ Geçidi sunucusu grubu](./media/nps-extension-remote-desktop-gateway/image13.png)

5. Merhaba, **RADIUS sunucusu Düzenle** iletişim kutusu, select hello **Yük Dengeleme** sekmesi.
6. Merhaba, **Yük Dengeleme** sekmede hello **bırakılan isteği kabul edilmeden önce yanıt olmadan saniye sayısı** alan, 30-60 saniye arasında 3 tooa değerinden hello varsayılan değeri değiştirin.
7. Merhaba, **sunucu olarak kullanılamaz olduğu belirlendiğinde isteklerinin arasındaki saniye sayısını** alan, eşit tooor hello önceki adımda belirttiğiniz hello değerden daha büyük olan 30 saniye tooa değer hello varsayılan değerini değiştirin.

 ![RADIUS sunucusu Düzenle](./media/nps-extension-remote-desktop-gateway/image14.png)

8.  Tamam iki tooclose hello iletişim kutuları'ı tıklatın.

### <a name="verify-connection-request-policies"></a>Bağlantı isteği ilkeleri doğrulayın 
Merhaba RD Ağ Geçidi toouse bağlantısı Yetkilendirme İlkeleri için bir merkezi ilke deposu yapılandırırken varsayılan olarak, yapılandırılmış tooforward CAP istekleri toohello NPS sunucusu hello RD Ağ Geçidi sağlar. işlemler hello RADIUS erişim isteğini hello Azure MFA uzantılı Hello NPS sunucusu yüklü. Aşağıdaki adımları hello nasıl tooverify hello varsayılan bağlantı isteği ilkesi gösterir. 

1. Merhaba NPS (yerel) konsolunda, RD Ağ geçidi, hello genişletin **ilkeleri**seçip **bağlantı isteği ilkeleri**.
2. Sağ **bağlantı isteği ilkeleri**, çift tıklayın ve **TH Ağ Geçidi YETKİLENDİRME İlkesi**.
3. Merhaba, **TH Ağ Geçidi YETKİLENDİRME İlkesi Özellikleri** iletişim kutusunda, hello **ayarları** sekmesi.
4. Üzerinde **ayarları** iletme bağlantı isteği altında sekmesini **kimlik doğrulama**. RADIUS istemci kimlik doğrulaması için yapılandırılmış tooforward isteği sayısıdır.

 ![Kimlik doğrulama ayarları](./media/nps-extension-remote-desktop-gateway/image15.png)
 
5. Tıklatın **iptal**. 

## <a name="configure-nps-on-hello-server-where-hello-nps-extension-is-installed"></a>NPS'yi hello NPS uzantısı yüklendiği hello sunucusunda yapılandırın
Merhaba NPS sunucusu hello NPS uzantısı yüklü gereksinimlerini toobe mümkün tooexchange RADIUS hello NPS hello Uzak Masaüstü Ağ Geçidi sunucusunda iletilerle olduğu. Bu ileti tooenable exchange, hello NPS uzantısı hizmetinin yüklendiği hello sunucusundaki tooconfigure hello NPS bileşenler gerekir. 

### <a name="register-server-in-active-directory"></a>Sunucusu Active Directory'de Kaydettir
toofunction düzgün Bu senaryoda, Active Directory'de kayıtlı toobe hello NPS sunucusu gerekir.

1. Açık **Sunucu Yöneticisi'ni**.
2. Sunucu Yöneticisi'nde **Araçları**ve ardından **ağ ilkesi sunucusu**. 
3. Merhaba ağ ilkesi sunucusu konsolunda sağ **NPS (yerel)**ve ardından **Active Directory'de kayıt sunucusu**. 
4. Tıklatın **Tamam** iki kez.

 ![AD kayıt sunucu](./media/nps-extension-remote-desktop-gateway/image16.png)

5. Merhaba konsolunu hello sonraki yordam için açık bırakın.

### <a name="create-and-configure-radius-client"></a>Oluşturma ve RADIUS istemci yapılandırma 
Merhaba Uzak Masaüstü Ağ geçidi bir RADIUS istemcisi toohello NPS sunucusu olarak yapılandırılmış toobe gerekir. 

1. Merhaba NPS uzantısı yüklü olduğu, hello hello NPS sunucusunda **NPS (yerel)** konsolunda, sağ **RADIUS istemcileri** tıklatıp **yeni**.

 ![Yeni RADIUS istemcisi](./media/nps-extension-remote-desktop-gateway/image17.png)

2. Merhaba, **yeni RADIUS istemcisi** iletişim kutusunda, aşağıdaki gibi kolay bir ad sağlayın _ağ geçidi_, ve IP adresi veya hello Uzak Masaüstü Ağ Geçidi sunucusunun DNS adı hello. 
3. Merhaba, **paylaşılan gizlilik** ve hello **paylaşılan gizliliği onayla** alanları girin hello önce kullandığınız aynı gizliliği.

 ![Ad ve adres](./media/nps-extension-remote-desktop-gateway/image18.png)

4. Tıklatın **Tamam** tooclose hello yeni RADIUS istemcisi iletişim kutusu.

### <a name="configure-network-policy"></a>Ağ İlkesi yapılandırma
Geri çağırma hello NPS sunucusu hello Azure MFA uzantısı ile Merhaba atanmış merkezi ilke hello bağlantı yetkilendirme ilkesi (CAP) için deposudur. Bu nedenle, tooimplement bir CAP hello NPS sunucusu tooauthorize geçerli bağlantılarını isteklerinde gerekir.  

1. Merhaba NPS (yerel) konsolda **ilkeleri**, tıklatıp **ağ ilkeleri**.
2. Sağ **bağlantıları tooother erişim sunucuları**, tıklatıp **Çoğaltma İlkesi**. 

 ![Yinelenen İlkesi](./media/nps-extension-remote-desktop-gateway/image19.png)

3. Sağ **kopya bağlantı tooother erişim sunucuları**, tıklatıp **özellikleri**.

 ![Ağ Özellikleri](./media/nps-extension-remote-desktop-gateway/image20.png)

4. Merhaba, **kopya bağlantı tooother erişim sunucuları** iletişim kutusu ilke adı girin uygun bir ad gibi **RDG_CAP**. Denetleme **ilkesi etkinleştirilmiş**seçip **erişim izni verme**. İsteğe bağlı olarak, ağ erişimi türünde seçin **Uzak Masaüstü Ağ Geçidi**, veya olarak bırakılabilir **belirtilmemiş**.

 ![Bağlantıları kopyası](./media/nps-extension-remote-desktop-gateway/image21.png)

5.  Hello tıklatın **kısıtlamaları** sekmesini tıklatın ve denetleme **bir kimlik doğrulama yöntemi anlaşması olmadan izin istemcileri tooconnect**.

 ![İstemcilerin tooconnect](./media/nps-extension-remote-desktop-gateway/image22.png)

6. İsteğe bağlı olarak, hello tıklayın **koşullar** sekmesinde ve hello bağlantı toobe, örneğin, belirli bir Windows grubu üyeliği yetkili için karşılanması gereken koşulları ekleyin.

 ![Koşullar](./media/nps-extension-remote-desktop-gateway/image23.png)

7. **Tamam** düğmesine tıklayın. İstendiğinde tooview Merhaba, ilgili Yardım konusunu tıklatın **Hayır**.
8. Yeni ilke hello hello ilkesi etkinleştirilmiş hello listesinin başında olduğundan ve erişim verir emin olun.

 ![Ağ ilkeleri](./media/nps-extension-remote-desktop-gateway/image24.png)

## <a name="verify-configuration"></a>Yapılandırmayı doğrulama
tooverify hello yapılandırma, uygun bir RDP istemci ile Merhaba Uzak Masaüstü Ağ Geçidi üzerinde toolog gerekir. Emin toouse bağlantısı yetkilendirme ilkeleri tarafından izin verilen ve Azure MFA için etkinleştirilmiş bir hesap olabilir. 

Aşağıdaki hello görüntüsündeki Göster hello kullanabilirsiniz **Uzak Masaüstü Web erişimi** sayfası.

![Uzak Masaüstü Web erişimi](./media/nps-extension-remote-desktop-gateway/image25.png)

Kimlik bilgilerinizi birincil kimlik doğrulaması için başarıyla girildikten sonra hello Uzak Masaüstü Bağlantısı iletişim kutusu uzaktan bağlantıyı başlatan bir durumu aşağıda gösterildiği gibi gösterir. 

Başarılı bir şekilde Azure MFA önceden yapılandırılmış hello ikincil kimlik doğrulama yöntemi, kimlik doğrulaması, bağlı toohello kaynak demektir. Ancak, Hello ikincil kimlik doğrulaması başarılı olmazsa, erişim tooresource reddedilir. 

![Uzak bağlantı başlatma](./media/nps-extension-remote-desktop-gateway/image26.png)

Aşağıda, hello Doğrulayıcı hello örnekte kullanılan tooprovide hello ikincil kimlik doğrulaması Windows Phone Uygulama şeklindedir.

![Hesaplar](./media/nps-extension-remote-desktop-gateway/image27.png)

Merhaba ikincil kimlik doğrulama yöntemini kullanarak başarıyla doğrulandıktan sonra normal olarak Uzak Masaüstü Ağ Geçidi hello içine kaydedilir. Gerekli toouse güvenilen bir cihazda bir mobil uygulama kullanarak bir ikincil kimlik doğrulama yöntemi olduğundan, ancak hello oturum açma işleminiz Aksi durumda olacak çok daha güvenlidir.

### <a name="view-event-viewer-logs-for-successful-logon-events"></a>Başarılı oturum açma olayları için Olay Görüntüleyicisi'ni günlüklerini görüntüle
tooview hello başarılı oturum açma olayları hello Windows Olay Görüntüleyicisi günlüklerinde, Windows PowerShell komut tooquery hello Windows Terminal Hizmetleri ve Windows güvenlik günlüklerini takip hello verebilir.

Merhaba ağ geçidi işlem günlüklerinde tooquery başarılı oturum açma olayları _(olay görüntüleyici\uygulamalar ve hizmetler Logs\Microsoft\Windows\TerminalServices-Gateway\Operational_, hello aşağıdaki komutları kullanın:

* _Get-WinEvent - günlükadı Microsoft-Windows-TerminalServices-ağ geçidi/Operational_ | burada {$_.ID - eq '300'} | FL 
* Bu komut hello kullanıcı kaynak yetkilendirme ilkesi gereksinimleri (RD RAP) sınamadan ve erişim verildi Göster Windows olayları görüntüler.

![Görünüm Olay Görüntüleyicisi](./media/nps-extension-remote-desktop-gateway/image28.png)

* _Get-WinEvent - günlükadı Microsoft-Windows-TerminalServices-ağ geçidi/Operational_ | burada {$_.ID - eq '200'} | FL
* Bu komut, kullanıcı bağlantısı yetkilendirme ilkesi gereksinimlerini sağlandığında göstermek hello olayları görüntüler.

![Bağlantı Yetkilendirme](./media/nps-extension-remote-desktop-gateway/image29.png)

Bu günlük ve filtre olay kimlikleri, 300 ve 200 üzerinde de görüntüleyebilirsiniz. Merhaba Güvenlik Olay Görüntüleyicisi günlüklerinde tooquery başarılı oturum açma olaylarını hello aşağıdaki komutu kullanın:

* _Get-WinEvent - günlükadı güvenlik_ | burada {$_.ID - eq '6272'in '} | FL 
* Bu komut üzerinde çalıştırılabilir merkezi NPS hello veya RD Ağ Geçidi sunucusu hello. 

![Başarılı oturum açma olayları](./media/nps-extension-remote-desktop-gateway/image30.png)

Aşağıda gösterildiği gibi hello güvenlik günlüğü veya hello Ağ İlkesi ve Erişim Hizmetleri özel görünümü de görüntüleyebilirsiniz:

![Ağ İlkesi ve Erişim Hizmetleri](./media/nps-extension-remote-desktop-gateway/image31.png)

Azure MFA için hello NPS uzantısı yüklendiği hello sunucuda Olay Görüntüleyicisi'ni uygulama günlüklerini belirli toohello uzantısına bulabilirsiniz _uygulama ve Hizmetleri Logs\Microsoft\AzureMfa_. 

![Olay Görüntüleyicisi'ni uygulama günlükleri](./media/nps-extension-remote-desktop-gateway/image32.png)

## <a name="troubleshoot-guide"></a>Sorun giderme kılavuzu

Merhaba yapılandırma beklendiği gibi çalışmıyorsa, hello ilk yer toostart tootroubleshoot kullanıcı hello tooverify yapılandırılmış toouse Azure MFA numarasıdır. Toohello bağlanmak hello kullanıcınız [Azure portal](https://portal.azure.com). Kullanıcıların başarıyla ikincil doğrulama için istenir ve kimlik doğrulaması, Azure mfa yapılandırması hatalı ortadan kaldırabilirsiniz.

Azure MFA için hello kullanıcıları çalışıyorsanız hello ilgili olay günlüklerini gözden geçirmelidir. Bunlar hello önceki bölümde tartışılan hello güvenlik olayı, ağ geçidi işletimsel ve Azure MFA günlüklerini içerir. 

Aşağıda, güvenlik günlüğü başarısız oturum açma olayı (olay kimliği 6273) gösteren bir örnek çıktı verilmiştir.

![Başarısız oturum açma olayı](./media/nps-extension-remote-desktop-gateway/image33.png)

Merhaba AzureMFA günlükleri ilgili bir olayın aşağıdadır:

![Azure MFA günlük](./media/nps-extension-remote-desktop-gateway/image34.png)

Gelişmiş tooperform seçenekleri, başvurun hello NPS veritabanı biçim günlük dosyalarının hello NPS hizmetinin yüklendiği sorunlarını giderin. Bu günlük dosyaları oluşturulur _%SystemRoot%\System32\Logs_ klasörü virgülle ayrılmış metin dosyalarını olarak. 

Bu bir açıklaması için günlük dosyaları, bkz: [NPS veritabanı biçimi günlük dosyalarını yorumlama](https://technet.microsoft.com/library/cc771748.aspx). Bu günlük dosyalarındaki Hello girişleri bir elektronik tablo veya bir veritabanına alma olmadan zor toointerpret olabilir. Birkaç IAS ayrıştırıcıları bulabilirsiniz günlük dosyalarını size yorumlama hello çevrimiçi tooassist. 

Merhaba aşağıdaki görüntü hello çıkışını bir gösterir böyle indirilebilir [paylaşılan yazılım uygulama](http://www.deepsoftware.com/iasviewer). 

![Paylaşılan yazılım uygulama](./media/nps-extension-remote-desktop-gateway/image35.png)

Son olarak, için ek seçenekleri sorun giderme, bir iletişim kuralı çözümleyicisi kullanabilir böyle [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx). 

Merhaba Microsoft Message Analyzer aşağıda görüntüden hello kullanıcı adını içeren RADIUS protokolü filtre ağ trafiğini gösterir **Contoso\AliceC**.

![Microsoft Message Analyzer](./media/nps-extension-remote-desktop-gateway/image36.png)

## <a name="next-steps"></a>Sonraki adımlar
[Nasıl tooget Azure çok faktörlü kimlik doğrulaması](multi-factor-authentication-versions-plans.md)

[RADIUS kullanan Uzak Masaüstü Ağ Geçidi ve Azure Multi-Factor Authentication Sunucusu](multi-factor-authentication-get-started-server-rdg.md)

[Şirket içi dizinlerinizi Azure Active Directory ile tümleştirme](../active-directory/connect/active-directory-aadconnect.md)
