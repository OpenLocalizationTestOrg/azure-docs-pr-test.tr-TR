---
title: "Yönetim hello Azure Active Directory kurumsal uygulamalar için sağlama aaaUser | Microsoft Docs"
description: "Nasıl toomanage kullanıcı hesabı hello Azure Active Directory kullanarak kurumsal uygulamaları için sağlama öğrenin"
services: active-directory
documentationcenter: 
author: asmalser
manager: femila
editor: 
ms.assetid: 34ac4028-a5aa-40d9-a93b-0db4e0abd793
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.openlocfilehash: a613f844c8f51e04b92e62b488313a78ab85f7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-user-account-provisioning-for-enterprise-apps-in-hello-azure-portal"></a>Kullanıcı hesabı hello Azure portal'ın Kurumsal uygulamaları için sağlama yönetme
Bu makalede nasıl toouse hello [Azure portal](https://portal.azure.com) sağlama ve, özellikle olanları hello eklenen destekleyen uygulamalar için sağlamayı kaldırma özelliklerini toomanage otomatik olarak bir kullanıcı hesabı "özel" kategorisi Merhaba [Azure Active Directory Uygulama galerisinde](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery). otomatik olarak bir kullanıcı hesabı sağlama ve nasıl çalıştığı hakkında daha fazla toolearn bkz [otomatikleştirmek kullanıcı hazırlama ve sağlamayı kaldırma işlemlerini tooSaaS Azure Active Directory ile uygulamaları](active-directory-saas-app-provisioning.md).

## <a name="finding-your-apps-in-hello-portal"></a>Uygulamalarınızı hello Portalı'nda bulma
Çoklu oturum açma bir dizinde hello kullanarak bir dizin yönetici tarafından yapılandırılan tüm uygulamaları [Azure Active Directory Uygulama galerisinde](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery), görüntülenebilir ve hello yönetilen [Azure portal](https://portal.azure.com). Merhaba uygulamaları hello bulunabilir **daha Hizmetleri** &gt; **kurumsal uygulamalar** hello portalı bölümü. Kurumsal uygulamalar dağıtılan ve kuruluşunuzda kullanılan uygulamalardır.

![Kurumsal uygulamalar dikey penceresi][0]

Seçme hello **tüm uygulamaları** bağlantıyı hello sol tarafta, hello Galerisi'nden eklenen uygulamalar dahil olmak üzere yapılandırılmış tüm uygulamaların bir listesini gösterir. Bir uygulamayı seçerek hello kaynak dikey burada bu uygulama için raporlar görüntülenebilir ve çeşitli ayarları yönetilebilmesi için bu uygulama için yükler.

Kullanıcı hesabının ayarlarını sağlama seçerek yönetilebilir **sağlama** hello soldaki.

![Uygulama kaynağı dikey][1]

## <a name="provisioning-modes"></a>Sağlama modları
Merhaba **sağlama** dikey başlıyorsa bir **modu** hangi sağlama modları Kurumsal uygulama için desteklenen gösterir ve bunları yapılandırılmış toobe veren menüsü. Merhaba mevcut Seçenekler şunlardır:

* **Otomatik** -bu seçenek, Azure AD API tabanlı otomatik sağlama ve/veya kullanıcı hesapları toothis uygulamasının sağlamayı kaldırma özelliklerini destekliyorsa görünür. Bu mod seçmek, Hesap Eşleştirmeleri ve kullanıcı hesabı veri Azure AD arasında akışı nasıl olmalı tanımlamak iş akışları oluşturma, Azure AD tooconnect toohello uygulamanın kullanıcı yönetimi API yapılandırma yoluyla Yöneticiler kılavuzları bir arabirim görüntüler ve Merhaba uygulama ve yönetme hello Azure AD sağlama hizmeti.
* **El ile** -Azure AD kullanıcı hesapları toothis uygulamasının otomatik sağlamayı desteklemiyor, bu seçenek gösterilir. Bu seçenek hello uygulamada depolanan kullanıcı hesabı kayıtları (içerebilen SAML Just-In-Time sağlama) bu uygulama tarafından sağlanan hello kullanıcı yönetimi ve sağlama yeteneklerine dayalı bir dış işlem kullanarak yönetilmelidir anlamına gelir.

## <a name="configuring-automatic-user-account-provisioning"></a>Otomatik olarak bir kullanıcı hesabı sağlama yapılandırma
Seçme hello **otomatik** seçeneği, dört bölümlerde bölünmüş bir ekran görüntüler:

### <a name="admin-credentials"></a>Yönetici kimlik bilgileri
Azure AD tooconnect toohello uygulamanın kullanıcı yönetim API'si için gerekli olan hello kimlik bilgilerini girildiği budur. gerekli hello giriş hello uygulamaya bağlı olarak değişir. toolearn hello kimlik bilgisi türleri ve belirli uygulamaları için gereksinimleri hakkında bkz hello [, belirli bir uygulama için yapılandırma Öğreticisi](active-directory-saas-app-provisioning.md#list-of-apps-that-support-automated-user-provisioning).

Seçme hello **Bağlantıyı Sına** düğmesi sağlar, Azure AD tooconnect toohello uygulama denemesi sahip tootest hello kimlik bilgilerini hello sağlanan kimlik bilgilerini kullanarak uygulama sağlama.

### <a name="mappings"></a>Eşlemeleri
Burada admins görüntüleyebilir ve Azure AD arasında hangi kullanıcı öznitelikleri akışı Düzenle budur ve hello hedef uygulama, kullanıcı hesaplarını sağlanan veya güncelleştirildiğinde.

Önceden yapılandırılmış bir Azure AD kullanıcı ve her SaaS uygulamanın kullanıcı nesneleri arasındaki eşlemeleri kümesi yok. Bazı uygulamalar, diğer grupların veya kişilerin gibi nesne türlerini yönetin. Bu eşlemeler birini hello tabloda seçerek hello eşleme düzenleyicisini burada bunlar görüntülenebilir ve özelleştirilebilir toohello sağ gösterir.

![Uygulama kaynağı dikey][2]

Desteklenen özelleştirmeler aşağıdakileri içerir:

* Etkinleştirme ve eşlemeleri hello Azure AD kullanıcı nesnesi toohello SaaS uygulamanın kullanıcı nesnesi gibi belirli nesneler için devre dışı bırakma.
* Hangi özniteliklerin hello Azure AD kullanıcı nesnesi toohello uygulamanın kullanıcı nesnesinden akış düzenleme. Özellik eşlemesi hakkında daha fazla bilgi için bkz: [özniteliği eşleme türlerini anlama](active-directory-saas-customizing-attribute-mappings.md#understanding-attribute-mapping-types).
* Azure AD hello üzerinde gerçekleştirdiği eylemleri sağlama filtresi hello uygulamayı hedefledi. Tam eşitleme-nesnelerin Azure AD sahip olmak yerine hello eylemlerin sınırlayabilirsiniz. Örneğin, seçerek yalnızca **güncelleştirme**, var olan kullanıcı hesaplarını bir uygulamada ve yenilerini oluşturmaz Azure AD yalnızca güncelleştirmeler. Yalnızca seçerek **oluşturma**, Azure yalnızca yeni kullanıcı hesapları oluşturur ama var olanları güncelleştirmez. Bu özellik, hesap yöneticileri toocreate farklı eşlemeleri oluşturma ve güncelleştirme iş akışları sağlar.

### <a name="settings"></a>Ayarlar
Bu bölümü admins toostart sağlar ve durdurma hello Azure AD sağlama hizmeti seçili Merhaba uygulaması yanı sıra isteğe bağlı olarak Temizle hello sağlama için önbellek ve hello hizmetini yeniden başlatın.

Sağlama hello için bir uygulama için ilk kez etkinleştiriliyor, hello değiştirerek hello Hizmeti'ni başlatmak **sağlama durumu** çok**üzerinde**. Bu hello Azure AD sağlama hizmeti tooperform hello atanan hello kullanıcılar bunu okuyan burada bir başlangıç eşitlemesi neden olan **kullanıcılar ve gruplar** bölümünde hello hedef uygulama için bunları sorgular ve hello sağlama gerçekleştirir Hello Azure AD tanımlanan Eylemler **eşlemeleri** bölümü. Yönetilmeyen hesapları hiçbir zaman atama kapsamında olan hello hedef uygulamaları içinde işlemleri sağlamayı kaldırma özelliklerini tarafından etkilenmez için bu işlem sırasında hizmet sağlama hello önbelleğe alınan veriler, yönetmekte olduğu, hangi kullanıcı hesapları hakkında depolar. Merhaba sonra ilk eşitleme, hizmet otomatik olarak sağlama hello on dakikalık bir zaman aralığı üzerinde kullanıcı ve Grup nesneleri eşitler.

Değişen hello **sağlama durumu** çok**kapalı** yalnızca duraklatır hello sağlama hizmeti. Bu durumda Azure olmayan oluşturmak, güncelleştirmek veya herhangi bir kullanıcı veya grup nesneleri hello uygulamada kaldırın. Merhaba durumu geri tooon değiştirilmesi, kaldığı yerden yukarı hello hizmet toopick neden olur.

Seçme hello **temizleme geçerli durumu ve eşitlemeyi yeniden başlatma** onay ve durakları kaydetme Merhaba sağlama hizmeti, hangi hesapların Azure AD hakkındaki dökümleri hello önbelleğe alınmış verileri yönetiyor, hello hizmetleri yeniden başlatır ve hello gerçekleştirir yeniden ilk eşitleme. Bu seçenek dağıtım işlemini baştan sağlama admins toostart hello sağlar.

### <a name="synchronization-details"></a>Eşitleme ayrıntıları
Bu bölümde, hizmet sağlama hello hello işlemi hakkında ek ayrıntılar sağlar, hello ilk ve son kez hello sağlama hizmeti de dahil olmak üzere hello uygulama ve kaç kullanıcı ve Grup nesneleri yönetilen karşı verdi.

Bağlantılar toohello sağlanan **Etkinlik Raporu sağlama**, tüm kullanıcıların ve grupların güncelleştirilmiş ve arasında kaldırılan Azure AD oluşturulmuş bir günlük sağlar ve hello hedef uygulama ve toohello **hata sağlama Rapor** daha ayrıntılı hata iletileri için kullanıcı ve Grup nesneleri okumak, oluşturulan, güncelleştirilmiş veya kaldırılamaz, başarısız toobe sağlar. 

##<a name="feedback"></a>Geri Bildirim

Azure AD deneyiminizi gibi umuyoruz. Gelen hello geribildirim unutmayın! Geri bildirim ve fikir geliştirme için hello sonrası **Yönetici portalı** bölümünü bizim [geri bildirim Forumunda](https://feedback.azure.com/forums/169401-azure-active-directory/category/162510-admin-portal).  Biz, her gün harika yeni hizmetler oluşturma hakkında heyecan ve kılavuz tooshape kullanabilir ve sonraki geliştirmemiz ne tanımlayın.


[0]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-blade.PNG
[1]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning.PNG
[2]: ./media/active-directory-enterprise-apps-manage-provisioning/enterprise-apps-provisioning-mapping.PNG
