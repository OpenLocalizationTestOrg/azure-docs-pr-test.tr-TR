---
title: "aaaEnable Kurumsal durumda Dolaşım Azure Active Directory'de | Microsoft Docs"
description: "Windows cihazları'deki kurumsal durumda Dolaşım ayarları hakkında sık sorulan sorular. Kurumsal durumda dolaşım, kullanıcılar Windows cihazlarını arasında birleştirilmiş bir deneyim sağlar ve yeni bir cihaz yapılandırmak için gereken hello süreyi azaltır."
services: active-directory
keywords: "Kurumsal durumda dolaşımı, windows bulut nasıl tooenable Kurumsal durumda Dolaşım"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Azure Active Directory'de Kurumsal Durumda Dolaşımı etkinleştirme
Kurumsal durumda Dolaşım Premium Azure Active Directory (Azure AD) abonelik kullanılabilir tooany kuruluşla olur. Konusunda daha fazla ayrıntı için tooget bir Azure AD abonelik bkz hello [Azure AD ürün sayfası](https://azure.microsoft.com/services/active-directory).

Kurumsal durumda Dolaşım etkinleştirdiğinizde, kuruluşunuz için ücretsiz, sınırlı kullanım abonelik tooAzure Rights Management lisans otomatik olarak verilir. Bu ücretsiz abonelik sınırlı tooencrypting ve kurumsal ayarları ve uygulama verilerini hello Kurumsal durumda Dolaşım hizmeti tarafından eşitlenen çözme değildir; bir Ücretli abonelik toouse hello özelliklerinin tamamı Azure Rights Management olması gerekir.

Bir Azure AD Premium aboneliği aldıktan sonra bu adımları tooenable Kurumsal durumda Dolaşım izleyin:

1. Oturum açma toohello Klasik Azure portalı.
2. Merhaba solda seçin **ACTIVE DIRECTORY**ve ardından istediğiniz tooenable Kurumsal durumda Dolaşım hello dizini seçin.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Toohello Git **yapılandırma** hello üst sekmesinde.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Başlangıç sayfası ve select aşağı kaydırın **kullanıcılar eşitleme ayarları ve kurumsal uygulama verileri**ve ardından **KAYDETMEK**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Bir Windows 10 cihaz tooroam ayarları için hello Kurumsal durumda Dolaşım hizmeti, bir Azure AD kimlik kullanılarak hello cihaz kimlik doğrulaması gerekir. Birleştirilmiş tooAzure AD cihazlar için hello kullanıcının birincil oturum açma hello Azure AD kimlik olduğundan ek yapılandırma gerekli değildir. Geleneksel şirket içi Active Directory kullanan cihazları hello için BT yöneticisi gerekir [Windows 10 deneyimleri için hello etki alanına katılmış aygıtlar tooAzure AD connect](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Eşitleme veri depolama
Bir veya daha fazla veri Kurumsal durumda Dolaşım barındırılan [Azure bölgeleri](https://azure.microsoft.com/regions/) en iyi hello ülke/bölge değeri hello Azure Active Directory örneğine ayarlanmış hizalar. Kurumsal durumda Dolaşım veri bölümlenmiş üç ana coğrafi bölgelerine bağlı: Kuzey Amerika, EMEA ve APAC. Kurumsal durumda Dolaşım veri hello Kiracı için hello coğrafi bölge ile yerel olarak bulunur ve bölgeler arasında çoğaltılmaz.  Örneğin, "Fransa" veya "Zambiya" verilerine sahip gibi kendi ülke/bölge değer kümesi tooone, EMEA ülkelerin sahip müşteriler birinde veya hello Azure bölgeleri Avrupa içinde barındırılan.  "ABD" veya "Kanada" verilerine sahip gibi Azure AD tooone, Kuzey Amerika ülkelerin ülke/bölge değerlerine ayarlayın müşteriler bir veya daha fazla hello Azure bölgeleri hello ABD içinde barındırılan.  "Avustralya" veya "Yeni Zelanda" verilerine sahip gibi APAC ülkelerde Azure AD tooone ülke/bölge değerlerine ayarlayın müşteriler bir veya daha fazla hello Azure bölgeleri Asya içinde barındırılan.  Güney Amerika ülke ve Antarktika veri hello ABD içinde bir veya daha fazla Azure bölgeleri barındırılacağı.  Merhaba ülke/bölge değeri hello Azure AD dizin oluşturma işleminin bir parçası olarak ayarlayın ve daha sonra değiştirilemez. 

Veri depolama konumu hakkında daha fazla ayrıntı gerekiyorsa, Lütfen bir dosya [Azure Destek](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Kurumsal durumda Dolaşım yönetme
Azure AD genel Yöneticiler etkinleştirmek ve kurumsal durumda Dolaşım hello Klasik Azure portalı devre dışı bırakabilirsiniz.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Genel Yöneticiler ayarları eşitleme toospecific güvenlik grupları sınırlayabilirsiniz.

Genel yöneticiler de bir kullanıcı başına cihaz eşitleme durumu raporu görüntüleyebilirsiniz hello Active Directory örneğinde belirli bir kullanıcı seçerek **kullanıcılar** listesi ve tıklayarak **AYGITLARI** sekmesinde ve Görünüm seçerek**Ayarları ve kurumsal uygulama verileri eşitleniyor aygıtları**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Veri saklama
Kurumsal durumda Dolaşım aracılığıyla eşitlenen veri tooAzure süresiz olarak el ile silme işlemi gerçekleştirilen veya belirlenen toobe eski hello veri söz konusu kaldırılana kadar korunur. 

**Açık silinmesine:** Azure yönetici bir kullanıcı veya bir dizin siler veya bir yönetici veri toobe silinmiş olduğunu açıkça istediğinde hello veriler silinir.

* **Kullanıcı silme**: bir kullanıcı Azure AD'de silindiğinde, veri dolaşımı hello kullanıcı hesabı silinmek üzere işaretlenmiş ve 90 too180 gün arasında silinir. 
* **Dizin silme**: Azure AD içinde tüm dizin silinmesi hemen bir işlem olduğundan. Tüm hello ayarları verileri, dizin silinmek üzere işaretlenmiş ile 90 too180 gün arasında silinecek ilişkili. 
* **İstek silme**: hello Azure AD yönetim istediği toomanually belirli bir kullanıcının veri veya ayar verileri silerseniz, hello Yöneticisi ile bir bilet dosya [Azure Destek](https://azure.microsoft.com/support/). 

**Eski veri silme**: bir yıl ("Merhaba Bekletme dönemi") eski kabul edilir ve Azure'dan silinebilir erişildikten olmayan veriler. Merhaba saklama dönemi konu toochange olmakla birlikte 90 günden olmaz. Merhaba eski veriler Windows/uygulama ayarları veya bir kullanıcı için tüm ayarları belirli bir kümesi olabilir. Örneğin:

* Hiçbir aygıt belirli ayarları koleksiyonu erişirseniz (örneğin, bir uygulama hello CİHAZDAN kaldırılır veya ayarları grubu "Tema" gibi tüm kullanıcı aygıtları için devre dışı bırakılır), o koleksiyona hello saklama döneminden sonra eski haline gelir ve olabilir silindi. 
* Kullanıcı ayarları eşitleme güncelleştirmesini tüm cihazlarda kapalı, hello ayarları verilerin hiçbiri sonra erişilir ve o kullanıcı için tüm hello ayarları veri eski olur ve hello saklama döneminden sonra silinebilir. 
* Hello Azure AD directory Yöneticisi Kurumsal durumda Dolaşım hello tüm dizin için tüm kullanıcılar dizin ayarları eşitleniyor durdurur ve tüm kullanıcılar için tüm ayarları verileri eski haline gelir ve hello saklama döneminden sonra silinebilir kapatırsa. 

**Silinen veri kurtarma**: hello veri bekletme ilkesi yapılandırılabilir değildir. Merhaba veriler kalıcı olarak silinir sonra kurtarılabilir olmaz. Ancak, ayarları veri hello toonote yalnızca Azure'dan hello son kullanıcı cihazı silinecek önemlidir. Herhangi bir aygıt daha sonra toohello Kurumsal durumda Dolaşım hizmet bağlanırsa, hello ayarlarını yeniden eşitlenen ve olması Azure'da depolanır.

## <a name="related-topics"></a>İlgili konular
* [Kurumsal durumda Dolaşım genel bakış](active-directory-windows-enterprise-state-roaming-overview.md)
* [Ayarlar ve veri dolaşımı SSS](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Grup İlkesi ve MDM ayarları ayarları eşitleme](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Windows 10 Dolaşım ayarları başvurusu](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Sorun giderme](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
