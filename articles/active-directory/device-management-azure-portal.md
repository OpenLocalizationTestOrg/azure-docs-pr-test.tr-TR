---
title: "kullanarak aaaManaging cihazları hello Azure portal - Önizleme | Microsoft Docs"
description: "Nasıl toouse hello Azure portal toomanage aygıtlar hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Azure portal hello - Önizleme kullanarak cihazları yönetme

>[!NOTE]
>Bu özellik şu anda genel önizlemede değil. Toorevert hazırlanması veya herhangi bir değişiklik kaldırın. Genel Önizleme sırasında herhangi bir Azure Active Directory (Azure AD) abonelik Hello özelliği kullanılabilir. Ancak, Hello özelliği genel kullanıma sunulduğunda hello özelliği bazı yönlerini bir Azure Active Directory premium aboneliği gerektirebilir.


Azure Active Directory'de (Azure AD) ile cihaz yönetimi, güvenlik ve uyumluluğa yönelik standartlarınızı karşılamak aygıtlardan kullanıcılarınızın kaynaklarınızı eriştiğiniz emin olabilirsiniz. 

Bu konuda:

- Merhaba ile bilgi sahibi olduğunuzu varsayar [giriş toodevice Yönetimi Azure Active Directory'de](device-management-introduction.md)

- Azure portal kullanarak, cihazları yönetme hakkında bilgi ile Merhaba sağlar


toomanage aygıtları hello Azure Portalı'ndaki tooclick ihtiyacınız **aygıtları** hello içinde **Yönet** hello hello bölümünü **Azure Active Directory** dikey.

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Aygıt ayarlarını yapılandır

Hello Azure portal kullanarak aygıtlarınızı toobe ihtiyaç toomanage kayıtlı veya tooAzure AD alanına katılmış. Yönetici olarak, kaydetme ve cihazların Merhaba aygıt ayarları yapılandırarak birleştirme hello işleminde ince ayar yapabilirsiniz.

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/22.png)


Merhaba aygıt ayarları dikey tooconfigure sağlar:

- **Kullanıcıların cihazları tooAzure AD katılma** - bu ayarları, cihazları tooAzure AD katılabilirsiniz tooselect hello kullanıcılar sağlar. Merhaba varsayılandır **tüm**.

- **Ek yerel Yöneticiler Azure AD alanına katılmış aygıtlar** -bir cihazda yerel yönetici haklarına sahip olurlar hello kullanıcılar seçebilir. Buraya eklenen kullanıcılar toohello eklendiğinde *cihaz yöneticileri* Azure AD'de rol. Azure AD'de genel Yöneticiler ve cihaz sahiplerine yerel yönetici hakları varsayılan olarak verilmiştir. Bu seçenek bir premium edition Azure AD Premium veya Enterprise Mobility Suite (EMS) hello gibi ürünler aracılığıyla kullanılabilen bir özelliktir. 

- **Kullanıcıları Azure AD ile cihazlarını kaydetme** -Bu ayar tooallow aygıtları toobe kayıtlı Azure AD ile tooconfigure gerekir. Seçerseniz **hiçbiri**, Azure AD alanına bağlı olmadıkları zaman tooregister ya da karma Azure AD alanına katılmış aygıtlar izin verilmez. Office 365 için Microsoft Intune veya mobil cihaz Yönetimi (MDM) ile kayıt kayıt gerektirir. Bu hizmetlerden birini yapılandırdıysanız **tüm** seçilir ve **NONE** kullanılamıyor...

- **Multi-Factor Auth toojoin cihazları gerektirir** -kullanıcılar gerekli tooprovide olup bir ikinci öğeli kimlik doğrulamasını toojoin kendi cihaz tooAzure AD seçebilirsiniz. Merhaba varsayılandır **Hayır**. Bir cihaz kaydedilirken çok faktörlü kimlik doğrulaması gerektiren öneririz. Bu hizmet için çok faktörlü kimlik doğrulamasını etkinleştirmek için önce bu çok faktörlü kimlik doğrulaması, kullanıcıların aygıtlarını kaydetmesini hello kullanıcılar için yapılandırılmış emin olmalısınız. Farklı Azure çok faktörlü kimlik doğrulama hizmetleri hakkında daha fazla bilgi için bkz: [Azure multi-Factor authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **En fazla cihaz sayısını** -Bu ayar tooselect hello cihaz sayısı üst sınırı bir kullanıcı Azure AD'de sahip olabileceği sağlar. Bir kullanıcı bu kota ulaşırsa, olan değil olmaları mümkün tooadd ek cihazlar kadar veya daha fazla var olan cihazların Merhaba kaldırılır. Merhaba aygıt teklif, Azure AD alanına katılmış ya da Azure AD bugün kayıtlı tüm aygıtlar için sayılır. Merhaba varsayılan değer **20**.

- **Kullanıcıların eşitleme ayarları ve uygulama verileri cihaz üzerinden** -varsayılan olarak, bu çok ayarı**NONE**. Belirli kullanıcıları veya grupları veya tüm seçilmesi hello kullanıcının ayarları ve uygulama veri toosync arasında Windows 10 cihazlarını tanır. Eşitleme Windows 10'da nasıl çalıştığı hakkında daha fazla bilgi edinin.
Bu seçenek bir premium Azure AD Premium veya Enterprise Mobility Suite (EMS) hello gibi ürünler aracılığıyla kullanılabilen bir özelliktir.
 
    ![Bir Intune cihaz yönetme](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Aygıtlar bulunamadı

Bir yönetici olarak hello Azure portal toolocate kayıtlı ve katılmış cihazlarda iki seçeneğiniz vardır:

- **Tüm cihazlar** hello içinde **Yönet** hello bölümünü **aygıtları** dikey penceresi  

    ![Tüm cihazlar](./media/device-management-azure-portal/41.png)


- **Aygıtları** hello içinde **Yönet** bölümünü bir **kullanıcı** dikey penceresi
 
    ![Tüm cihazlar](./media/device-management-azure-portal/43.png)



Her iki seçenek ile tooa görünümü, alabilirsiniz:


- Filtre olarak hello görünen adı kullanarak cihazları için toosearch sağlar.

- Kayıtlı ve birleştirilmiş aygıtları ayrıntılı bakış sağlar

- Tooperform ortak aygıt yönetim görevleri sağlar
   

![Tüm cihazlar](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Aygıt yönetim görevleri

Yönetici olarak, yönettiğiniz hello katılmış cihazlarda veya kayıtlı. Bu bölümde, genel cihaz yönetim görevleri hakkında bilgi sağlar.


**Bir Intune cihaz yönetme** -Intune yöneticisiyseniz, olarak işaretlenmiş cihazlarını yönetebilmeniz için **Microsoft Intune**. Bir yönetici ek aygıt görebilirsiniz 

![Bir Intune cihaz yönetme](./media/device-management-azure-portal/31.png)


**Etkinleştir / devre dışı bir Azure AD cihaz**

tooenable veya devre dışı bir aygıt, Azure AD'de toobe genel yönetici gerekir. Bir aygıtı devre dışı bırakma, bir aygıt, Azure AD kaynaklarını erişmesini engeller.  toodisable hello aygıt yapabilecekleriniz'i *...* Merhaba aygıtı ek ayrıntılar için tıklatın.

 
![Bir Intune cihaz yönetme](./media/device-management-azure-portal/33.png)

Bir aygıtı devre dışı bırakma değişiklikleri hello hello durumda **etkin** sütun çok**Hayır**.

![Bir aygıtı devre dışı](./media/device-management-azure-portal/32.png)


**Bir Azure AD cihaz silme** -toodelete bir aygıtı toobe genel yöneticinin Azure AD içinde gerekir.  
Bir cihazı silme:
 
- Bir aygıt, Azure AD kaynaklarına erişmesini engeller. 

- Tüm iliştirilmiş toohello aygıt, örneğin: ayrıntıları, Windows cihazları için BitLocker anahtarları kaldırır  

- Kurtarılamaz bir etkinliği temsil eder ve gerekli olmadığı sürece önerilmez.

Lütfen bir cihaz başka bir yönetim yetkilisi (örneğin Microsoft Intune) tarafından yönetiliyorsa hello aygıt temizlenmeden / Azure AD'de hello aygıt silmeden önce devre dışı bırakılan emin olun.

Ya da seçebileceğiniz "..." toodelete hello aygıt veya hello cihazda ek ayrıntılar için tıklatın
 
![Bir aygıtı silme](./media/device-management-azure-portal/34.png)


**Görüntüleme veya cihaz kimliği kopyalama** -hello cihazında veya sorun giderme sırasında PowerShell kullanarak bir cihaz kimliği tooverify hello cihaz kimliği ayrıntıları kullanabilirsiniz. tooaccess hello Kopyala seçeneğini, hello cihaz seçeneğine tıklayın.

![Bir cihaz kimliği görüntüleyin](./media/device-management-azure-portal/35.png)
  

**Görüntüleme veya BitLocker anahtarları kopyalama** -bir yönetici görebilir ve kopyalama hello BitLocker anahtarları toohelp kullanıcılar toorecover kendi şifreli sürücüyü. Bu anahtarlar yalnızca şifrelenmiş Windows cihazları için kullanılabilir ve kendi anahtarları Azure AD'de depolanan sahip. Bu anahtarları hello cihaz ayrıntılarını erişirken kopyalayabilirsiniz.
 
![BitLocker anahtarları görüntüleyin](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Denetim günlükleri


Merhaba aygıt etkinlikleri hello etkinlik günlükleri ile kullanılabilir. Merhaba cihaz kayıt hizmeti veya hello kullanıcı tarafından tetiklenen etkinliklerin içerir:

- Cihaz oluşturma ve hello aygıtta sahipleri/kullanıcıları ekleme

- Toodevice ayarlarını değiştirir

- Bir aygıt güncelleştirme veya silme gibi aygıt işlemleri
 
Giriş noktası verileri denetleme toohello olan **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **aygıtları* dikey.

![Denetim günlükleri](./media/device-management-azure-portal/61.png)


Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:

- Başlangıç tarihi ve saati hello oluşum

- Merhaba hedefleri

- Başlatıcı hello / aktör (kimin) etkinliğin

- Merhaba etkinlik (ne)

![Denetim günlükleri](./media/device-management-azure-portal/63.png)

Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.
 
![Denetim günlükleri](./media/device-management-azure-portal/64.png)


Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello denetim verileri filtreleyebilirsiniz bildirdi:

- Catergory
- Etkinlik kaynak türü
- Etkinlik
- Tarih aralığı
- Hedef
- (Aktör) tarafından başlatılan

Ayrıca toohello filtreleri, belirli girişleri için arama yapabilirsiniz.

![Denetim günlükleri](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Active Directory'de giriş toodevice Yönetimi](device-management-introduction.md)



