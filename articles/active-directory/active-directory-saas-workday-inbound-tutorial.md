---
title: "Öğretici: Workday ile şirket içi Active Directory ve Azure Active Directory sağlama otomatik olarak bir kullanıcı için yapılandırma | Microsoft Docs"
description: "Bilgi nasıl toouse Workday kimlik verilerinin Active Directory ve Azure Active Directory için kaynak olarak."
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 1a2c375a-1bb1-4a61-8115-5a69972c6ad6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/26/2017
ms.author: asmalser
ms.openlocfilehash: d4eb3237b8fe7614606c58b39fbefcb44f4060fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workday-for-automatic-user-provisioning-with-on-premises-active-directory-and-azure-active-directory"></a>Öğretici: Workday ile şirket içi Active Directory ve Azure Active Directory sağlama otomatik olarak bir kullanıcı için yapılandırın.
Bu öğreticinin Hello hedefi tooperform tooimport Workday kişilerden Active Directory ve Azure Active Directory'de bazı öznitelikler tooWorkday isteğe bağlı geri yazma ile ihtiyacınız adımları hello tooshow ' dir. 



## <a name="overview"></a>Genel Bakış

Merhaba [hizmet sağlama Azure Active Directory kullanıcı](active-directory-saas-app-provisioning.md) hello ile tümleşir [Workday İnsan Kaynakları API](https://community.workday.com/sites/default/files/file-hosting/productionapi/Human_Resources/v21.1/Get_Workers.html) , kullanıcı hesaplarını tooprovision sipariş. Azure AD kullanıcı sağlama iş akışları şu Bu bağlantı tooenable hello kullanır:

* **Kullanıcıların tooActive Directory sağlama** -Workday kullanıcı seçili kümeleri bir veya daha fazla Active Directory ormanları eşitleyin. 

* **Yalnızca bulut kullanıcıları tooAzure Active Directory sağlama** -hello ikinci kullanarak Active Directory ve Azure Active Directory içinde mevcut karma kullanıcılar sağlanabilir [AAD Connect](connect/active-directory-aadconnect.md). Ancak, salt bulut olan kullanıcılar doğrudan tooAzure Active Directory'yi kullanarak Azure AD kullanıcısının hizmet sağlama hello Workday'den sağlanabilir.

* **Geri yazma e-posta adresleri tooWorkday** -hizmet sağlama hello Azure AD kullanıcı seçili Azure AD kullanıcı öznitelikleri geri tooWorkday, hello e-posta adresi gibi yazabilirsiniz.

### <a name="scenarios-covered"></a>Kapsanan senaryolar

Hizmet sağlama hello Azure AD kullanıcı tarafından desteklenen iş akışları sağlama hello Workday kullanıcı İnsan Kaynakları ve kimlik yaşam döngüsü yönetimi senaryoları aşağıdaki hello otomasyonunu sağlar:

* **Yeni çalışan işe alma** - tooWorkday, yeni bir çalışan eklendiğinde, bir kullanıcı hesabı otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak oluşturulur ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları ](active-directory-saas-app-provisioning.md), hello e-posta adresi tooWorkday arkasına yazma ile.

* **Çalışan özniteliği ve profil güncelleştirmeleri** - zaman (kendi adı, başlık veya Yöneticisi gibi) bir çalışan kaydı iş günü içinde güncelleştirilir, kendi kullanıcı hesabına otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak güncelleştirilir ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).

* **Çalışan sonlandırmalar** - çalışan iş günü içinde sonlandırıldığında kendi kullanıcı hesabına otomatik olarak Active Directory, Azure Active Directory ve Office 365 isteğe bağlı olarak devre dışıdır ve [Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).

* **Çalışan yeniden anlaşır** - çalışan iş günü içinde rehired eski hesaplarına otomatik olarak yeniden etkinleştiren (bağlı olarak, tercihinize) yeniden sağlanan tooActive Directory, Azure Active Directory ve isteğe bağlı olarak Office 365 ve veya[Azure AD tarafından desteklenen diğer SaaS uygulamaları](active-directory-saas-app-provisioning.md).


## <a name="planning-your-solution"></a>Çözümünüzü planlarken

Merhaba önkoşulları aşağıdaki ve okuma hello nasıl hakkında yönergeler aşağıdaki denetleyin, Workday entegrasyonu başlamadan önce geçerli bir Active Directory mimarisi ve kullanıcı gereksinimlerini hazırlama hello Azure Active tarafından sağlanan solution(s) toomatch Dizin.

### <a name="prerequisites"></a>Ön koşullar

Bu öğreticide gösterilen hello senaryo aşağıdaki öğelerindeki hello zaten sahip olduğunuzu varsayar:

* Genel yönetici erişimi olan geçerli bir Azure AD Premium P1 abonelik
* Sınama ve tümleştirme amaçları için bir iş günü uygulama Kiracı
* Workday toocreate sistem tümleştirme kullanıcı yönetici izinleri ve test amacıyla marka değişiklikleri tootest çalışan verilerini
* TooActive Directory sağlama kullanıcı için 2012 veya daha fazla Windows hizmeti çalıştıran bir etki alanına katılmış gerekli toohost hello sunucusudur [şirket içi eşitleme Aracısı](https://go.microsoft.com/fwlink/?linkid=847801)
* [Azure AD Connect](connect/active-directory-aadconnect.md) Active Directory ve Azure AD arasında eşitlemek için

> [!NOTE]
> Azure AD kiracınıza Avrupa'da bulunuyorsa, lütfen hello bakın [bilinen sorunlar](#known-issues) bölümüne bakın.


### <a name="solution-architecture"></a>Çözüm mimarisi

Azure AD sağlama ve kimlik yaşam döngüsü yönetimi Workday tooActive Directory, Azure AD, SaaS uygulamaları ve ötesinde çözmek bağlayıcılar toohelp sağlama zengin bir özellik kümesi sağlar. Hangi özellikleri kullanır ve hello çözümü ayarlama nasıl kuruluşunuzun ortamlarına ve gereksinimlerine bağlı olarak farklılık gösterir. İlk adım olarak, mevcut ve kuruluşunuzdaki dağıtılan hello aşağıdaki kaç, hisse senedi alın:

* Kaç tane Active Directory ormanları kullanılıyor?
* Kaç tane Active Directory etki alanları kullanılıyor?
* Kaç tane Active Directory kuruluş birimlerini (OU) kullanılıyor?
* Kaç tane Azure Active Directory kiracıları kullanılıyor?
* Sağlanan toobe tooboth Active Directory ve Azure Active Directory (örneğin "karma" kullanıcılar) ihtiyaç duyan kullanıcılar var mı?
* Sağlanan toobe tooAzure Active Directory, ancak Active Directory değil (örneğin "yalnızca bulut" kullanıcılar) olması gereken kullanıcılar var mı?
* Kullanıcı e-posta adreslerini geri tooWorkday yazılan toobe gerekiyor mu?

Yanıtlar toothese sorular olduktan sonra dağıtım başlangıç kılavuzu izleyerek aşağıdaki sağlama İş gününüzün planlayabilirsiniz.

#### <a name="using-provisioning-connector-apps"></a>Sağlama bağlayıcı uygulamaları kullanma

Azure Active Directory Workday ve çok sayıda diğer SaaS uygulamaları için önceden tümleştirilmiş sağlama bağlayıcıları destekler. 

Tek bir sağlama bağlayıcı tek kaynak sistem API hello ile arabirimleri ve sağlama verileri tooa tek hedef sistem yardımcı olur. Azure AD destekleyen çoğu sağlama bağlayıcılar tek kaynak ve hedef sistem (örneğin, Azure AD tooServiceNow) için ve Kurulum hello uygulama ekleyerek hello Azure AD uygulama galerisinde ' (örneğin ServiceNow) söz konusu olabilir. 

Azure AD'de sağlama bağlayıcı örnekleri ve app örnekleri arasında bire bir ilişki vardır:

| Kaynak sistemi | Hedef sistem |
| ---------- | ---------- | 
| Azure AD kiracısı | SaaS uygulaması |


Ancak, Workday ve Active Directory ile çalışırken, birden çok kaynak ve hedef sistemleri toobe ilgili olarak kabul vardır:

| Kaynak sistemi | Hedef sistem | Notlar |
| ---------- | ---------- | ---------- |
| İş günü | Active Directory ormanı | Her bir orman ayrı hedef sistem olarak kabul edilir |
| İş günü | Azure AD kiracısı | Yalnızca bulut kullanıcıları için gerektiği şekilde |
| Active Directory ormanı | Azure AD kiracısı | Bu akış AAD Connect tarafından bugün işlenir |
| Azure AD kiracısı | İş günü | E-posta adreslerini geri yazma için |

Bu birden çok iş akışı toomultiple kaynak ve hedef sistemleri, Azure AD toofacilitate hello Azure AD uygulama Galerisi'nden ekleyebilirsiniz birden fazla sağlama bağlayıcı uygulamalar sağlar:

![AAD uygulama Galerisi](./media/active-directory-saas-workday-inbound-tutorial/WD_Gallery.PNG)

* **İş günü tooActive Directory sağlama** -kullanıcı hesabı Workday tooa tek Active Directory ormanından sağlama bu uygulamayı kolaylaştırır. Birden çok ormanınız varsa, bu uygulamanın bir örneği hello Azure AD uygulama galerisinde tooprovision için gereksinim duyduğunuz her Active Directory ormanı için ekleyebilirsiniz.

* **İş günü tooAzure AD sağlama** -sırada AAD Connect kullanılan toosynchronize Active Directory Kullanıcıları tooAzure Active Directory olmalıdır hello aracı, bu uygulama kullanılan toofacilitate olabilir Workday tooa tek yalnızca bulut kullanıcılardan sağlama Azure Active Directory kiracısı.

* **İş günü geri yazma** -bu uygulamayı Azure Active Directory tooWorkday kullanıcının e-posta adresleri için geri yazma kolaylaştırır.

> [!TIP]
> Merhaba normal "Workday" uygulaması, çoklu oturum açma Workday ve Azure Active Directory arasında ayarlamak için kullanılır. 

Nasıl tooset ayarlama ve bu özel yapılandırma olan bölümleri Bu öğreticinin kalan hello hello konusunun bağlayıcı uygulamalar sağlama. Tooconfigure hangi sistemlerinde tooprovision için ve kaç tane Active Directory ormanları ve Azure AD ihtiyacınız bağlıdır seçtiğiniz hangi kiracılar ortamınızda uygulamalardır.

![Genel Bakış](./media/active-directory-saas-workday-inbound-tutorial/WD_Overview.PNG)

## <a name="configure-a-system-integration-user-in-workday"></a>Bir sistem tümleştirme kullanıcı iş günü içinde yapılandırın
Bunlar bir iş günü sistem tümleştirme hesabı tooconnect toohello için Workday İnsan Kaynakları API kimlik bilgileri gerektiren tüm hello Workday sağlama bağlayıcı ortak gerekli değildir. Bu bölümde, nasıl toocreate bir sistem Tümleştirici hesap iş günü içinde açıklanmıştır.

> [!NOTE]
> Bu yordam, olası toobypass kullanılır ve bunun yerine bir iş günü genel yönetici hello sistem tümleştirme aynı hesabı kullan. Bu tanıtımları için düzgün çalışıyor, ancak üretim dağıtımları için önerilmez.

### <a name="create-an-integration-system-user"></a>Tümleştirme sistemi kullanıcısı oluştur

**Tümleştirme sistemi kullanıcısı toocreate:**

1. Workday Kiracı yönetici hesabı kullanarak oturum açın. Merhaba, **Workday çalışma ekranı**, girin hello arama kutusuna kullanıcı oluşturmak ve ardından **tümleştirme sistemi kullanıcısı Oluştur**. 
   
    ![Kullanıcı oluşturma](./media/active-directory-saas-workday-inbound-tutorial/IC750979.png "kullanıcı oluşturma")
2. Tam hello **tümleştirme sistemi kullanıcısı Oluştur** yeni bir tümleştirme sistemi kullanıcısı için bir kullanıcı adı ve parola sağlayarak görev.  
 * Merhaba bırakın **gerektiren yeni parolayı sonraki oturum açma** seçeneği işaretsiz, bu kullanıcının program aracılığıyla oturum açan olduğundan. 
 * Merhaba bırakın **oturum zaman aşımı dakika** ile varsayılan değeri 0 olan engeller hello kullanıcı oturumları erken zaman aşımı. 
   
    ![Tümleştirme sistemi kullanıcısı Oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750980.png "tümleştirme sistemi kullanıcısı oluştur")

### <a name="create-a-security-group"></a>Bir güvenlik grubu oluşturun
Merhaba kullanıcı tooit atayın ve toocreate bir Kısıtlanmamış tümleştirme sistemi güvenlik grubunu gerekir.

**toocreate bir güvenlik grubu:**

1. Girin hello arama kutusuna güvenlik grubu oluşturun ve ardından **güvenlik grubu oluşturma**. 
   
    ![Güvenlik grubu oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750981.png "güvenlik grubu oluştur")
2. Tam hello **güvenlik grubu oluşturma** görev.  
3. Tümleştirme sistemi güvenlik grubu seç — hello Kısıtlanmamış **kiralanan güvenlik grubu türü** açılır.
4. Üyeleri açıkça eklenen bir güvenlik grubu toowhich oluşturun. 
   
    ![Güvenlik grubu oluştur](./media/active-directory-saas-workday-inbound-tutorial/IC750982.png "güvenlik grubu oluştur")

### <a name="assign-hello-integration-system-user-toohello-security-group"></a>Merhaba tümleştirme sistem kullanıcı toohello güvenlik grubu atayın

**tooassign hello tümleştirme sistemi kullanıcısı:**

1. Güvenlik grubunu Düzenle hello arama kutusuna girin ve ardından **güvenlik grubunu Düzenle**. 
   
    ![Güvenlik grubunu Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750983.png "güvenlik grubunu Düzenle")
2. Arama ve ada göre hello yeni tümleştirme güvenlik grubu seçin. 
   
    ![Güvenlik grubunu Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750984.png "güvenlik grubunu Düzenle")
3. Merhaba yeni tümleştirme sistemi kullanıcı toohello yeni güvenlik grubunu ekleyin. 
   
    ![Sistem güvenlik grubu](./media/active-directory-saas-workday-inbound-tutorial/IC750985.png "sistem güvenlik grubu")  

### <a name="configure-security-group-options"></a>Güvenlik grubu seçeneklerini yapılandırın
Bu adımda, toohello yeni güvenlik grubu için izinleri **almak** ve **Put** etki alanı güvenlik ilkeleri aşağıdaki hello tarafından güvenliği sağlanan hello nesneleri işlemleri:

* Harici hesap sağlama
* Çalışan verileri: Ortak çalışan raporları
* Çalışan verileri: Tüm Pozisyonlar
* Çalışan verileri: Geçerli personel bilgileri
* Çalışan verileri: Çalışan profilindeki iş başlığı

**tooconfigure güvenlik grubu seçenekleri:**

1. Etki alanı güvenlik ilkeleri hello arama kutusuna girin ve sonra hello bağlantısını tıklatın **işlevsel alanı için etki alanı güvenlik ilkeleri**.  
   
    ![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750986.png "etki alanı güvenlik ilkeleri")  
2. Sistem ve select hello arama **sistem** işlevsel alan.  **Tamam** düğmesine tıklayın.  
   
    ![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750987.png "etki alanı güvenlik ilkeleri")  
3. Merhaba sistem işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **güvenlik Yönetim** seçip hello etki alanı güvenlik ilkesi **Harici hesap sağlama**.  
   
    ![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750988.png "etki alanı güvenlik ilkeleri")  
4. Tıklatın **izinleri Düzenle**ve ardından hello **izinleri Düzenle**iletişim sayfasında, hello yeni güvenlik grubu toohello listesi güvenlik grupları eklemek **almak** ve **Put** tümleştirme izinleri. 
   
    ![İzni Düzenle](./media/active-directory-saas-workday-inbound-tutorial/IC750989.png "düzenleme izni")  
5. İşlevsel alanlara seçme tooreturn toohello ekran yukarıdaki 1. adım ve bu süre, personel, arama seçin hello yineleyin **işlevsel alan personel** tıklatıp **Tamam**.
   
    ![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750990.png "etki alanı güvenlik ilkeleri")  
6. Merhaba Staffing işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **çalışan verileri: Staffing** ve bunların güvenlik ilkeleri kalan her biri için adımı yukarıdaki 4 yineleyin:

   * Çalışan verileri: Ortak çalışan raporları
   * Çalışan verileri: Tüm Pozisyonlar
   * Çalışan verileri: Geçerli personel bilgileri
   * Çalışan verileri: Çalışan profilindeki iş başlığı
   
7. Yineleme adım 1 ' seçeneğini belirleyerek işlevsel alan tooreturn toohello ekranı üzerinde ve bu süre, arama için **irtibat bilgileri**hello Staffing işlevsel alanı seçin ve tıklatın **Tamam**.

8.  Merhaba Staffing işlevsel alan için güvenlik ilkelerini Hello listesinde genişletin **çalışan verileri: çalışma kişi bilgilerini**ve yineleme yukarıda adım 4'hello güvenlik ilkeleri için:

    * Çalışan verileri: İş e-posta

    ![Etki alanı güvenlik ilkeleri](./media/active-directory-saas-workday-inbound-tutorial/IC750991.png "etki alanı güvenlik ilkeleri")  
    
### <a name="activate-security-policy-changes"></a>Güvenlik İlkesi değişikliklerini etkinleştir

**tooactivate güvenlik ilkesi değişikliklerini:**

1. Girin hello arama kutusuna etkinleştirin ve daha sonra hello bağlantıdaki **etkinleştirme bekleyen güvenlik ilkesi değişikliklerini**. 
   
    ![Etkinleştirme](./media/active-directory-saas-workday-inbound-tutorial/IC750992.png "etkinleştir") 
2. Bekleyen Güvenlik İlkesi değişikliklerini etkinleştir görev denetim amacıyla bir açıklama girin ve ardından başlangıç hello **Tamam**. 
   
    ![Bekleyen güvenlik ayarlarını etkinleştir](./media/active-directory-saas-workday-inbound-tutorial/IC750993.png "bekleyen güvenlik ayarlarını etkinleştir")   
3. Tam hello görev hello onay kutusunu işaretleyerek hello sonraki ekranında **Onayla**ve ardından **Tamam**. 
   
    ![Bekleyen güvenlik ayarlarını etkinleştir](./media/active-directory-saas-workday-inbound-tutorial/IC750994.png "bekleyen güvenlik ayarlarını etkinleştir")  

## <a name="configuring-user-provisioning-from-workday-tooactive-directory"></a>Workday tooActive Directory kullanıcı sağlamayı yapılandırma
Workday tooeach için sağlama gerektiren Active Directory ormanı'ndan sağlama bu yönergeleri tooconfigure kullanıcı hesabı izleyin.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1. Kısım: hello sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma

**tooconfigure Workday tooActive Directory sağlama:**

1.  Çok Git<https://portal.azure.com>

2.  Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**

3.  Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.

4.  Seçin **bir uygulama eklemek**ve select hello **tüm** kategorisi.

5.  Arama **Workday sağlama tooActive dizin**ve bu uygulama hello Galerisi'nden ekleyin.

6.  Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**

7.  Değişiklik hello **sağlama** **modu** çok**otomatik**

8.  Tam hello **yönetici kimlik bilgileri** gibi bölümünde:

   * **Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin. **Gibi görünmelidir:username@contoso4**

   * **Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir

   * **Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin. Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve wd3 impl hello doğru ortamı dize ile değiştirilir.

   * **Active Directory ormanı -** hello Get-ADForest powershell komutunu tarafından döndürülen Active Directory ormanınızın "Name" Merhaba. Bu genellikle bir dize gibi olur: *contoso.com*

   * **Active Directory kapsayıcısı -** hello kapsayıcı AD ormanınızdaki tüm kullanıcıları içeren bir dize girin. Örnek: *OU standart kullanıcılar, OU = Kullanıcılar, DC = contoso, DC = test =*

   * **Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.

   * Merhaba tıklatın **Bağlantıyı Sına** düğmesi. Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini. Başarısız olursa hello Workday kimlik iş günü içinde geçerli olduğunu denetleyin. 

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_1.PNG)

### <a name="part-2-configure-attribute-mappings"></a>2. Kısım: öznitelik eşlemelerini yapılandırın 

Bu bölümde, kullanıcı verilerini Workday'deki Active Directory ile nasıl akacağını yapılandırır.

1.  Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme Workday çalışanları tooOnPremises**.

2.  Merhaba, **kaynak nesne kapsamı** alan, hangi kullanıcı kümeleri için iş günü içinde öznitelik tabanlı bir filtre kümesi tanımlayarak tooAD, sağlama kapsamında olmalıdır seçebilirsiniz. "tüm kullanıcılar iş günü içinde" Hello varsayılan kapsamıdır. Örnek filtreler:

   * Örnek: Çalışan kimlikleri toousers 1000000 2000000 arasındaki kapsam

      * Öznitelik: WorkerID

      * İşleci: REGEX eşleşmiyor

      * Değer: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Örnek: Yalnızca çalışanlar ve değil contingent çalışanları 

      * Öznitelik: EmployeeID

      * İşleci: NULL değil

3.  Merhaba, **hedef nesne eylemleri** alan, genel filtre uygulayabilirsiniz hangi eylemleri Active Directory üzerinde gerçekleştirilen toobe izin verilir. **Oluşturma** ve **güncelleştirme** en sık kullanılan.

4.  Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz.

5. Üzerinde var olan bir öznitelik eşleme tooupdate tıklatın veya tıklatın **yeni eklemesi** Merhaba ekranında tooadd yeni eşlemeler hello sonundaki. Bir tek özniteliği eşlemesi bu özellikleri destekler:

      * **Eşleme türü**

         * **Doğrudan** – hello hello Workday özniteliği toohello AD özniteliğinin değeri, hiçbir değişiklik olmadan yazar

         * **Sabit** -hello AD özniteliği için bir statik, sabit dize değeri yazma

         * **İfade** – toowrite hello AD özniteliği, bir veya daha fazla iş günü özniteliklerini temel alarak özel bir değere izin verir. [Daha fazla bilgi için bu makalede ifadeleri bkz](active-directory-saas-writing-expressions-for-attribute-mappings.md).

      * **Kaynak özniteliği** -Workday hello kullanıcı özniteliği.

      * **Varsayılan değer** – isteğe bağlıdır. Merhaba eşleme Hello kaynak özniteliği boş bir değer varsa, bu değer yerine yazacaksınız.
            Bu boş tooleave en yaygın yapılandırmadır.

      * **Hedef öznitelik** – hello Active Directory'deki kullanıcı özniteliği.

      * **Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar Workday ve Active Directory arasında tanımlayın. Bu genellikle, çalışan kimliği alanı genellikle hello çalışan kimliği öznitelikleri Active Directory'de birine eşlenmiş iş günü için ayarlanır.

      * **Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir. Olduğunda birden çok, bu alana göre tanımlanan sırayla değerlendirilir. Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.

      * **Bu eşleme Uygula**
       
         * **Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri

         * **Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak

6. toosave, eşlemeleri tıklatın **kaydetmek** eşleme özniteliği bölümünün hello üstünde.

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_2.PNG)

**Aşağıda bazı örnek, bazı ortak ifadelerle Workday ve Active Directory arasında öznitelik eşlemelerini verilmiştir**

-   toohello parentDistinguishedName AD özniteliği eşlemeleri hello ifade kullanılan tooprovision belirli OU bir veya daha fazla iş günü kaynak özniteliklerini temel alarak bir kullanıcı tooa olabilir. Bu örnek kullanıcılar Şehir verilerine bağlı olarak farklı OU'lar iş günü içinde yerleştirir.

-   toohello userPrincipalName AD özniteliği eşlemeleri hello ifadesi oluşturma UPN firstName.LastName@contoso.com. Geçersiz özel karakterler yerini alır.

-   [Burada ifadeleri yazma belge yok](active-directory-saas-writing-expressions-for-attribute-mappings.md)

  
| İŞ GÜNÜ ÖZNİTELİĞİ | ACTIVE DIRECTORY ÖZNİTELİĞİ |  KİMLİĞİ EŞLEŞİYOR MU? | OLUŞTUR / GÜNCELLEŞTİR |
| ---------- | ---------- | ---------- | ---------- |
|  **WorkerID**  |  EmployeeID | **Evet** | Yazılan üzerinde yalnızca oluştur | 
|  **Belediye**   |   m   |     | Oluştur + güncelleştir |
|  **Şirket**         | Şirket   |     |  Oluştur + güncelleştir |
|  **CountryReferenceTwoLetter**      |   Ortak |     |   Oluştur + güncelleştir |
| **CountryReferenceTwoLetter**    |  C  |     |         Oluştur + güncelleştir |
| **SupervisoryOrganization**  | Bölüm  |     |  Oluştur + güncelleştir |
|  **PreferredNameData**  |  Görünen adı |     |   Oluştur + güncelleştir |
| **EmployeeID**    |  CN =    |   |   Yazılan üzerinde yalnızca oluştur |
| **Faks**      | facsimileTelephoneNumber     |     |    Oluştur + güncelleştir |
| **FirstName**   | givenName       |     |    Oluştur + güncelleştir |
| **Anahtar (\[etkin\],, "0", "True", "1")** |  AccountDisabled      |     | Oluştur + güncelleştir |
| **Mobil**  |    Mobil       |     |       Yazılan üzerinde yalnızca oluştur |
| **EmailAddress**    | Posta    |     |     Oluştur + güncelleştir |
| **ManagerReference**   | Yöneticisi  |     |  Oluştur + güncelleştir |
| **WorkSpaceReference** | physicalDeliveryOfficeName    |     |  Oluştur + güncelleştir |
| **Posta kodu**  |   posta kodu  |     | Oluştur + güncelleştir |
| **LocalReference** |  preferredLanguage  |     |  Oluştur + güncelleştir |
| ** Değiştirin (Mid (Değiştir (\[EmployeeID\],, "(\[\\\\/\\\\\\\\\\\\\[\\\\\]\\\\:\\\\;\\\\|\\\\=\\\\,\\\\+\\\\\*\\\\?\\ \\ &lt; \\ \\ &gt; \]) "," ",), 1, 20)," ([\\\\.) \* \$] (file:///\\.) *$)", , "", , )**      |    SAMAccountName            |     |         Yazılan üzerinde yalnızca oluştur |
| **Soyadı**   |   sn   |     |  Oluştur + güncelleştir |
| **CountryRegionReference** |  St     |     | Oluştur + güncelleştir |
| **AddressLineData**    |  StreetAddress  |     |   Oluştur + güncelleştir |
| **PrimaryWorkTelephone**  |  telephoneNumber   |     | Yazılan üzerinde yalnızca oluştur |
| **BusinessTitle**   |  Başlık     |     |  Oluştur + güncelleştir |
| **Join("@",Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace( Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Replace(Join(".", [FirstName], [LastName]), , "([Øø])", , "oe", , ), , "[Ææ]", , "ae", , ), , "([äãàâãåáąÄÃÀÂÃÅÁĄA])", , "a", , ), , "([B])", , "b", , ), , "([CçčćÇČĆ])", , "c", , ), , "([ďĎD])", , "d", , ), , "([ëèéêęěËÈÉÊĘĚE])", , "e", , ), , "([F])", , "f", , ), , "([G])", , "g", , ), , "([H])", , "h", , ), , "([ïîìíÏÎÌÍI])", , "i", , ), , "([J])", , "j", , ), , "([K])", , "k", , ), , "([ľłŁĽL])", , "l", , ), , "([M])" ,, "m",), "([ñńňÑŃŇN])", "n",), "([öòőõôóÖÒŐÕÔÓO])", "o",), "([P])", "p",), "([Q])", "q",), "([řŘR])", "r",), "([ßšśŠŚS])", "s",), "([TŤť])", "t",), "([üùûúůűÜÙÛÚŮŰU])", "u",), "([V])", "v",), "([]) w" harfinin, "w",), "([ýÿýŸÝY])", "y",), "([źžżŹŽŻZ])", "z",), "",,, "",), "contoso.com")**   | userPrincipalName     |     | Oluştur + güncelleştir                                                   
| **Anahtar (\[belediye\], "OU standart kullanıcılar, OU = Kullanıcılar, OU = varsayılan, OU = konumları, DC = contoso, DC = com =", "Dallas" "OU standart kullanıcılar, OU = Kullanıcılar, OU = Dallas, OU = konumları, DC = contoso, DC = com =", "Ankara'da" "OU standart kullanıcılar, OU = Kullanıcılar, OU = Ankara'da, OU = konumları, DC = contoso, DC = com =", "Seattle", "OU standart kullanıcılar, OU = Kullanıcılar, OU = Seattle, OU = konumları, DC = contoso, DC = com =", "Londra", "OU standart kullanıcılar = OU Kullanıcılar, OU = Londra, OU = konumları, DC = contoso, DC = com = ")**  | parentDistinguishedName     |     |  Oluştur + güncelleştir |
  
### <a name="part-3-configure-hello-on-premises-synchronization-agent"></a>3. Kısım: hello şirket içi eşitleme Aracısı'nı yapılandırma

Sipariş tooprovision tooActive şirket içi dizin, bir aracı hello desire Active Directory ormanındaki bir etki alanına katılmış sunucuda yüklenmesi gerekir. Merhaba yordamı tamamlamak için gerekli kimlik bilgileri etki alanı yöneticisi (veya Kurumsal Yönetici).

**[Hello şirket içi eşitleme Aracısı buradan indirebilirsiniz](https://go.microsoft.com/fwlink/?linkid=847801)**

Aracıyı yükledikten sonra ortamınız için tooconfigure hello Aracısı aşağıda hello Powershell komutlarını çalıştırın.

**#1 komutu**

> CD C:\\Program dosyaları\\Microsoft Azure Active Directory Eşitleme Aracı\\modülleri\\AADSyncAgent

> Import-module AADSyncAgent.psd1

**Komut #2**

> Ekleme ADSyncAgentActiveDirectoryConfiguration

* Giriş: "Dizin", başlangıç AD orman adı, kısmen girildiği gibi adı \#2
* Giriş: Yönetici kullanıcı adı ve parolası Active Directory ormanı için

**Komut #3**

> Ekleme ADSyncAgentAzureActiveDirectoryConfiguration

* Giriş: Genel yönetici kullanıcı adı ve parola Azure AD kiracınız için

**Komut #4**

> Get-AdSyncAgentProvisioningTasks

* Eylem: veriler döndürülür onaylayın. Bu komut, Azure AD kiracınıza uygulamalarında sağlama Workday otomatik olarak bulur. Örnek çıktı:

> Ad: AD Ormanım
>
> Etkin: True
>
> DirectoryName: mydomain.contoso.com
>
> Belgeli: yanlış
>
> Tanımlayıcı: WDAYdnAppDelta.c2ef8d247a61499ba8af0a29208fb853.4725aa7b-1103-41e6-8929-75a5471a5203

**Komut #5**

> Start-AdSyncAgentSynchronization-otomatik

**Komut #6**

> net stop aadsyncagent

**Komut #7**

> net start aadsyncagent

### <a name="part-4-start-hello-service"></a>4. Kısım: Başlangıç hello hizmeti
Bölümleri 1-3 tamamladıktan sonra hello Azure Yönetim Portalı geri hizmetinde sağlama hello başlatabilirsiniz.

1.  Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.

2. **Kaydet** düğmesine tıklayın.

3. Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.

4. Hangi kullanıcıların gibi bireysel eşitleme olayları dışında Workday okunur ve ardından sonradan eklenen veya güncelleştirilen tooActive dizin görüntülenebilir hello **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**

5.  Merhaba aracı makine üzerindeki Hello Windows Uygulama günlüğü hello Aracısı üzerinden gerçekleştirilen tüm işlemleri gösterir.

6. Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.

![Azure portalına](./media/active-directory-saas-workday-inbound-tutorial/WD_3.PNG)


## <a name="configuring-user-provisioning-tooazure-active-directory"></a>Kullanıcı tooAzure Active Directory hazırlama yapılandırma
Sağlama tooAzure Active Directory nasıl yapılandırdığınıza hello tabloda ayrıntılı olarak sağlama gereksinimlerinizi bağlıdır.

| Senaryo | Çözüm |
| -------- | -------- |
| **Sağlanan toobe tooActive Directory ve Azure AD kullanıcıların gerekir** | Kullanım  **[AAD bağlanma](connect/active-directory-aadconnect.md)** |
| **Kullanıcılar gerek sağlanan toobe tooActive Directory yalnızca** | Kullanım  **[AAD bağlanma](connect/active-directory-aadconnect.md)** |
| **Kullanıcıların, sağlanan toobe tooAzure AD yalnızca (yalnızca bulutta) gerekir.** | Kullanım hello **Workday tooAzure Active Directory sağlama** hello uygulama galerisinde uygulama |

Azure AD Connect ayarlama hakkında yönergeler için bkz: Merhaba [Azure AD Connect belgelerini](connect/active-directory-aadconnect.md).

Aşağıdaki bölümlerde hello Workday ve Azure AD tooprovision yalnızca bulut kullanıcıları arasında bir bağlantı ayarı açıklanmaktadır.

> [!IMPORTANT]
> Sağlanan toobe tooAzure AD ve şirket içi Active Directory olması gereken yalnızca bulut kullanıcılar varsa, yalnızca aşağıdaki hello yordamı izleyin.

### <a name="part-1-adding-hello-azure-ad-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1. Kısım: hello Azure AD sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma

**tooconfigure Workday tooAzure yalnızca bulut kullanıcıları için Active Directory sağlama:**

1.  Çok Git<https://portal.azure.com>.

2.  Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**

3.  Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.

4.  Seçin **bir uygulama eklemek**ve ardından hello **tüm** kategorisi.

5.  Arama **Workday tooAzure AD sağlama**ve bu uygulama hello Galerisi'nden ekleyin.

6.  Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**

7.  Değişiklik hello **sağlama** **modu** çok**otomatik**

8.  Tam hello **yönetici kimlik bilgileri** gibi bölümünde:

   * **Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin. Gibi görünmelidir:username@contoso4

   * **Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir

   * **Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin. Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve (gerekirse) wd3 impl hello doğru ortamı dize ile değiştirilir.

   * **Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.

   * Merhaba tıklatın **Bağlantıyı Sına** düğmesi.

   * Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini. Başarısız olursa, o hello Workday URL'si iki kez kontrol edin ve kimlik bilgilerini iş günü içinde geçerli.


### <a name="part-2-configure-attribute-mappings"></a>2. Kısım: öznitelik eşlemelerini yapılandırın 

Bu bölümde, kullanıcı verilerini Workday'deki Azure Active Directory'ye yalnızca bulut kullanıcıları için nasıl akacağını yapılandırır.

1.  Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme çalışanları tooAzure AD**.

2.   Merhaba, **kaynak nesne kapsamı** alan, hangi kullanıcı kümeleri için iş günü içinde öznitelik tabanlı bir filtre kümesi tanımlayarak tooAzure AD, sağlama kapsamında olmalıdır seçebilirsiniz. "tüm kullanıcılar iş günü içinde" Hello varsayılan kapsamıdır. Örnek filtreler:

   * Örnek: Çalışan kimlikleri toousers 1000000 2000000 arasındaki kapsam

      * Öznitelik: WorkerID

      * İşleci: REGEX eşleşmiyor

      * Değer: (1[0-9][0-9][0-9][0-9][0-9][0-9])

   * Örnek: Yalnızca contingent çalışanları ve değil Normal çalışanlar

      * Öznitelik: ContingentID

      * İşleci: NULL değil

3.  Merhaba, **hedef nesne eylemleri** alan, genel filtre uygulayabilirsiniz hangi eylemleri üzerinde Azure AD gerçekleştirilen toobe izin verilir. **Oluşturma** ve **güncelleştirme** en sık kullanılan.

4.  Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz.

5. Üzerinde var olan bir öznitelik eşleme tooupdate tıklatın veya tıklatın **yeni eklemesi** Merhaba ekranında tooadd yeni eşlemeler hello sonundaki. Bir tek özniteliği eşlemesi bu özellikleri destekler:

   * **Eşleme türü**

      * **Doğrudan** – hello hello Workday özniteliği toohello AD özniteliğinin değeri, hiçbir değişiklik olmadan yazar

      * **Sabit** -hello AD özniteliği için bir statik, sabit dize değeri yazma

      * **İfade** – toowrite hello AD özniteliği, bir veya daha fazla iş günü özniteliklerini temel alarak özel bir değere izin verir. [Daha fazla bilgi için bu makalede ifadeleri bkz](active-directory-saas-writing-expressions-for-attribute-mappings.md).

   * **Kaynak özniteliği** -Workday hello kullanıcı özniteliği.

   * **Varsayılan değer** – isteğe bağlıdır. Merhaba eşleme Hello kaynak özniteliği boş bir değer varsa, bu değer yerine yazacaksınız.
            Bu boş tooleave en yaygın yapılandırmadır.

   * **Hedef öznitelik** – Azure AD'de hello kullanıcı özniteliği.

   * **Eşleşen nesneleri bu öznitelik kullanarak** – Bu eşleme kullanılmalıdır olup olmadığına bakılmaksızın toouniquely kullanıcılar Workday ve Azure AD arasında tanımlayın. Bu genellikle, çalışan kimliği alanı genellikle Azure AD'de hello çalışan ID özniteliği (yeni) ya da uzantı özniteliği eşlenen iş günü için ayarlanır.

   * **Öncelik eşleşen** – birden çok öznitelikleri eşleşen ayarlanabilir. Olduğunda birden çok, bu alana göre tanımlanan sırayla değerlendirilir. Bir eşleşme olarak başka eşleştirme öznitelikleri değerlendirilir.

   * **Bu eşleme Uygula**

     * **Her zaman** – hem kullanıcı oluşturulması bu eşleme uygulamak ve güncelleştirme eylemleri

     * **Yalnızca oluşturma sırasında** -bu eşlemenin yalnızca kullanıcı oluşturma eylemlerini uygulamak

6. toosave, eşlemeleri tıklatın **kaydetmek** eşleme özniteliği bölümünün hello üstünde.

### <a name="part-3-start-hello-service"></a>3. Kısım: Başlangıç hello hizmeti
Bölümleri 1-2 tamamladıktan sonra hizmet sağlama hello başlatabilirsiniz.

1.  Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.

2. **Kaydet** düğmesine tıklayın.

3. Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.

4. Bireysel eşitleme olayları hello görüntülenebilir **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**

5. Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.


## <a name="configuring-writeback-of-email-addresses-tooworkday"></a>E-posta adresleri tooWorkday geri yazma yapılandırma
Kullanıcı e-posta adreslerini bu yönergeleri tooconfigure geri yazma, Azure Active Directory tooWorkday izleyin.

### <a name="part-1-adding-hello-provisioning-connector-app-and-creating-hello-connection-tooworkday"></a>1. Kısım: hello sağlama bağlayıcı uygulama ekleme ve hello bağlantı tooWorkday oluşturma

**tooconfigure Workday tooActive Directory sağlama:**

1.  Çok Git<https://portal.azure.com>

2.  Merhaba sol gezinti çubuğunda seçin **Azure Active Directory**

3.  Seçin **kurumsal uygulamalar**, ardından **tüm uygulamaları**.

4.  Seçin **bir uygulama eklemek**seçeneğini belirleyip hello **tüm** kategorisi.

5.  Arama **Workday geri yazma**ve bu uygulama hello Galerisi'nden ekleyin.

6.  Merhaba sonra uygulama eklenir ve hello uygulama ayrıntıları ekran gösterilir, seçin **sağlama**

7.  Değişiklik hello **sağlama** **modu** çok**otomatik**

8.  Tam hello **yönetici kimlik bilgileri** gibi bölümünde:

   * **Yönetici kullanıcı adı** – eklenmiş hello Kiracı etki alanı adıyla hello kullanıcı hello Workday entegrasyonu sistem hesabı adını girin. Gibi görünmelidir:username@contoso4

   * **Yönetici parolası –** hello Workday entegrasyonu sistem hesabı, hello parola gir

   * **Kiracı URL –** hello URL toohello Workday web hizmetleri uç kiracınız için girin. Aşağıdaki gibi görünmelidir: https://wd3-impl-services1.workday.com/ccx/service/contoso4, burada contoso4 doğru Kiracı adınız ile değiştirilir ve (gerekirse) wd3 impl hello doğru ortamı dize ile değiştirilir.

   * **Bildirim e-posta –** e-posta adresinizi girin ve "hatası oluşursa, e-posta Gönder" onay kutusunu işaretleyin.

   * Merhaba tıklatın **Bağlantıyı Sına** düğmesi. Merhaba bağlantı testi başarılı olursa, hello tıklatın **kaydetmek** hello üst düğmesini. Başarısız olursa, o hello Workday URL'si iki kez kontrol edin ve kimlik bilgilerini iş günü içinde geçerli.


### <a name="part-2-configure-attribute-mappings"></a>2. Kısım: öznitelik eşlemelerini yapılandırın 


Bu bölümde, kullanıcı verilerini Workday'deki Active Directory ile nasıl akacağını yapılandırır.

1.  Merhaba sağlama sekmesinde altında **eşlemeleri**, tıklatın **eşitleme Azure AD kullanıcıları tooWorkday**.

2.  Merhaba, **kaynak nesne kapsamı** alan, isteğe bağlı olarak filtreleyebilir hangi kullanıcı kümeleri için Azure Active Directory'de e-posta adreslerini yazdığınız geri tooWorkday. "tüm kullanıcılar Azure AD'de" Merhaba varsayılan kapsamıdır. 

3.  Merhaba, **öznitelik eşlemelerini** bölümünde, tek tek nasıl Workday harita tooActive dizin özniteliklerini öznitelikleri tanımlayabilirsiniz. Varsayılan olarak hello e-posta adresi için bir eşleme yoktur. Ancak, eşleşen kimliği hello güncelleştirilmiş toomatch kullanıcılar Azure AD'de Workday bunların karşılık gelen girdilere sahip olması gerekir. Popüler eşleşen yöntemi toosynchronize hello Workday çalışan kimliği veya çalışan Azure AD'de tooextensionAttribute1-15 kimliği ve ardından bu özniteliği Azure AD toomatch kullanıcılar geri iş günü içinde kullanın.

4.  toosave, eşlemeler'e tıklayın **kaydetmek** hello eşleme özniteliği bölüm hello üstünde.

### <a name="part-3-start-hello-service"></a>3. Kısım: Başlangıç hello hizmeti
Bölümleri 1-2 tamamladıktan sonra hizmet sağlama hello başlatabilirsiniz.

1.  Merhaba, **sağlama** sekmesi, kümesi hello **sağlama durumu** için **üzerinde**.

2. **Kaydet** düğmesine tıklayın.

3. Bu değişken sayıda iş günü içinde kaç kullanıcılardır bağlı olarak saatler sürebilir hello ilk eşitlemeyi başlatır.

4. Bireysel eşitleme olayları hello görüntülenebilir **denetim günlüklerini** sekmesi. **[Ayrıntılı yönergeler için raporlama Kılavuzu nasıl tooread hello denetim günlüklerini üzerinde sağlama hello bakın](active-directory-saas-provisioning-reporting.md)**

5. Bir tamamlandı, onu bir denetim özet raporu yazacak **sağlama** sekmesinde, aşağıda gösterildiği gibi.

## <a name="known-issues"></a>Bilinen sorunlar

* **Denetim günlükleri Avrupa yerel ayarlarda** - Bu teknik önizleme hello sürümü olduğundan hello bilinen bir sorun [denetim günlüklerini](active-directory-saas-provisioning-reporting.md) hello görünmeyen hello Workday bağlayıcı uygulamalar için [Azure portal](https://portal.azure.com) hello Azure AD Kiracı Avrupa veri merkezinde bulunuyorsa. Bu sorun için bir düzeltme yeni çıkacak. Lütfen bu alan yeniden hello yakın zaman güncelleştirmeleri denetleyin. 

## <a name="additional-resources"></a>Ek kaynaklar
* [Öğretici: çoklu oturum açma Workday ve Azure Active Directory arasında yapılandırma](active-directory-saas-workday-tutorial.md)
* [İlgili nasıl öğreticiler listesi tooIntegrate Azure Active Directory ile SaaS uygulamaları](active-directory-saas-tutorial-list.md)
* [Uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Sonraki adımlar

* [Tooreview nasıl günlüğe yazacağını öğrenin ve etkinlik sağlama raporları alın](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting)
