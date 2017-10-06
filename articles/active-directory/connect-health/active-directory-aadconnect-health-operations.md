---
title: "aaaAzure Active Directory Connect Health işlemleri"
description: "Bu makalede, Azure AD Connect Health dağıttıktan sonra gerçekleştirilebilir ek işlemleri açıklanır."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 86cc3840-60fb-43f9-8b2a-8598a9df5c94
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 1dddcee0bca3150ce08621c045a92a1b3ad9df30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-connect-health-operations"></a>Azure Active Directory Connect Health işlemleri
Bu konu, hello açıklar çeşitli işlemler Azure Active Directory (Azure AD) Connect Health kullanarak gerçekleştirebilirsiniz.

## <a name="enable-email-notifications"></a>E-posta bildirimlerini etkinleştir
Uyarıları kimlik altyapınızı sağlıklı değil belirttiğinizde hello Azure AD Connect Health hizmeti toosend e-posta bildirimleri yapılandırabilirsiniz. Bu, bir uyarı oluşturulduğunda ve giderildikten sonra oluşur.

![Ekran Azure AD Connect Health e-posta bildirim ayarları](./media/active-directory-aadconnect-health/email_noti_discover.png)

> [!NOTE]
> E-posta bildirimleri varsayılan olarak etkinleştirilir.
>
>

### <a name="tooenable-azure-ad-connect-health-email-notifications"></a>tooenable Azure AD Connect Health e-posta bildirimleri
1. Açık hello **uyarıları** dikey tooreceive e-posta bildirimi istediğiniz hello hizmeti.
2. Merhaba eylem çubuğundaki **bildirim ayarlarını**.
3. Merhaba e-posta bildirim anahtarında seçin **ON**.
4. Tüm genel Yöneticiler tooreceive e-posta bildirimleri istiyorsanız hello onay kutusunu seçin.
5. Başka bir e-posta adreslerini tooreceive e-posta bildirimleri istiyorsanız, bunları hello belirtin **ek e-posta alıcılarını** kutusu. tooremove bu listeden bir e-posta adresi hello girişi sağ tıklatın ve seçin **silmek**.
6. toofinalize hello değişikliklerinin **kaydetmek**. Yalnızca kaydettikten sonra değişiklikler etkili olur.

## <a name="delete-a-server-or-service-instance"></a>Bir sunucu veya hizmet örneğini silin

Bazı durumlarda, tooremove izlenmekte olan bir sunucunun isteyebilirsiniz. İşte gerekenler tooknow tooremove hello Azure AD Connect Health hizmetine bir sunucudan.

Bir sunucu silmekte olduğunuz zaman hello aşağıdakilere dikkat edin:

* Bu eylem bu sunucudan daha fazla veri toplamayı durdurur. Bu sunucu izleme hizmeti hello kaldırılır. Bu işlemin ardından, mümkün tooview yeni uyarıları, izleme veya bu sunucu için kullanım analizi verilerini olup olmadığı.
* Bu eylemin hello sistem durumu aracısı sunucunuzdan kaldırmaz. Merhaba sistem durumu aracısı, bu adımı uygulamadan önce kaldırmadıysanız, hataları ilgili toohello sistem durumu aracısı hello sunucuda görebilirsiniz.
* Bu eylem bu sunucudan zaten toplanmış hello verileri silmez. Bu verileri Azure veri bekletme ilkesi hello uygun olarak silinir.
* Bu eylemi gerçekleştirdikten sonra isterseniz toostart izleme hello aynı sunucuya yeniden, kaldırıp hello sistem durumu aracısı bu sunucuya yeniden yüklemeniz gerekir.

### <a name="toodelete-a-server-from-hello-azure-ad-connect-health-service"></a>toodelete bir sunucudan hello Azure AD Connect Health hizmeti
Azure AD Connect Health için Active Directory Federasyon Hizmetleri (AD FS) ve Azure AD Connect (eşitleme):

1. Açık hello **Server** dikey penceresinden hello **sunucu listesi** hello sunucu adı toobe seçerek dikey kaldırıldı.
2. Merhaba üzerinde **Server** hello eylem çubuğundan dikey tıklayın **silmek**.
3. Merhaba onay kutusuna Hello sunucu adını yazarak onaylayın.
4. **Sil**'e tıklayın.

Azure AD Connect Health için Azure Active Directory etki alanı Hizmetleri:

1. Açık hello **etki alanı denetleyicileri** Pano.
2. Select hello etki alanı denetleyicisi toobe kaldırıldı.
3. Merhaba eylem çubuğundaki **Sil Seçili**.
4. Merhaba eylem toodelete hello sunucusu onaylayın.
5. **Sil**'e tıklayın.

### <a name="delete-a-service-instance-from-azure-ad-connect-health-service"></a>Bir hizmet örneği Azure AD Connect Health hizmetinden Sil
Bazı durumlarda, bir hizmet örneği tooremove isteyebilirsiniz. İşte ne tooknow tooremove bir hizmet örneği hello Azure AD Connect Health hizmetinden.

Bir hizmet örneği silmekte olduğunuz zaman hello aşağıdakilere dikkat edin:

* Bu eylem hello geçerli hizmet örneği izleme hizmeti hello kaldırır.
* Bu eylem bırakmaz kaldırın veya bu hizmet örneği bir parçası olarak izlenmekte hello sunuculardan herhangi biri hello sistem durumu aracısını kaldırın. Merhaba sistem durumu aracısı, bu adımı uygulamadan önce kaldırmadıysanız, hataları ilgili toohello sistem durumu aracısı hello sunucularda görebilirsiniz.
* Azure veri bekletme ilkesi hello uygun olarak bu hizmete ait tüm veriler silinir.
* Bu eylemi gerçekleştirdikten sonra toostart hello hizmetini izlemek isterseniz, kaldırın ve tüm hello sunucularında hello sistem durumu aracısı yükleyin. Bu eylemi gerçekleştirdikten sonra aynı sunucuya yeniden kaldırmak, yeniden yükleyin ve kayıt hello izleme toostart istiyorsanız sistem durumu aracısı, bu sunucu üzerinde hello.

#### <a name="toodelete-a-service-instance-from-hello-azure-ad-connect-health-service"></a>toodelete hello Azure AD Connect Health hizmetinden bir hizmet örneği
1. Açık hello **hizmet** dikey penceresinden hello **hizmet listesi** tooremove istediğiniz hello hizmet tanımlayıcısını (grup adı) seçerek dikey.
2. Merhaba üzerinde **Server** hello eylem çubuğundan dikey tıklayın **silmek**.
3. Merhaba onay kutusuna Hello hizmet adını yazarak onaylayın (örneğin: sts.contoso.com).
4. **Sil**'e tıklayın.
   <br><br>

[//]: # (Start of RBAC section)
## <a name="manage-access-with-role-based-access-control"></a>Rol tabanlı erişim denetimi ile erişimi yönetme
[Rol tabanlı erişim denetimi (RBAC)](../role-based-access-control-configure.md) Azure AD Connect Health erişim toousers ve genel Yöneticiler başka gruplar sağlar. RBAC rolleri toohello hedeflenen kullanıcılar ve gruplar atar ve toolimit hello genel Yöneticiler, dizininizde bir mekanizma sağlar.

### <a name="roles"></a>Roller
Azure AD Connect Health yerleşik roller aşağıdaki hello destekler:

| Rol | İzinler |
| --- | --- |
| Sahip |Sahipleri olabilir *erişimini yönetme* (örneğin, bir rol tooa kullanıcı veya Grup Ata), *tüm bilgileri görüntüleyebilir* (örneğin, uyarıları görüntüleme) hello portalından ve *ayarlarını değiştirmek* () Örneğin, e-posta bildirimleri) Azure AD Connect Health içinde. <br>Varsayılan olarak, Azure AD genel Yöneticiler bu role atanmış ve bu değiştirilemez. |
| Katılımcı |Katkıda Bulunanlar yapabilirsiniz *tüm bilgileri görüntüleyebilir* (örneğin, uyarıları görüntüleme) hello portalından ve *ayarlarını değiştirme* (örneğin, e-posta bildirimleri) Azure AD Connect Health içinde. |
| Okuyucu |Okuyucuların *tüm bilgileri görüntüleyebilir* (örneğin, uyarıları görüntüleme) Azure AD Connect Health içinde hello portalından. |

Merhaba rolleri hello portal deneyimi kullanılabilir olsa bile diğer tüm rolleri (örneğin, kullanıcı erişim yöneticileri veya DevTest Labs kullanıcıların) Azure AD Connect Health içinde hiçbir etkisi tooaccess sahip.

### <a name="access-scope"></a>Erişim kapsamı
Azure AD Connect Health, iki düzeyde erişimi yönetme destekler:

* **Tüm hizmet örnekleri**: hello çoğu durumda yolu önerilen budur. Azure AD Connect Health tarafından izlenen tüm rol türleri arasındaki tüm hizmet örnekleri (örneğin, bir AD FS grubunu) erişimi denetler.
* **Hizmet örneği**: Bazı durumlarda, rol türleri veya bir hizmet örneği tarafından temel toosegregate erişimi gerekebilir. Bu durumda, hello hizmeti örnek düzeyinde erişimi yönetebilirsiniz.  

Bir son kullanıcı erişimi hello dizin veya hizmet düzeyinde varsa izin verilir örnek düzeyi.

### <a name="allow-users-or-groups-access-tooazure-ad-connect-health"></a>İzin kullanıcılara veya gruplara erişim tooAzure AD Connect Health
Merhaba aşağıdaki adımlar nasıl tooallow erişim gösterir.
#### <a name="step-1-select-hello-appropriate-access-scope"></a>1. adım: hello uygun erişim kapsamını seçin
tooallow hello bir kullanıcının erişim *tüm hizmet örnekleri* Azure AD Connect Health, açık hello ana dikey penceresinde Azure AD Connect Health içinde düzeyi.<br>

#### <a name="step-2-add-users-and-groups-and-assign-roles"></a>2. adım: Kullanıcıları ve grupları ekleyin ve Rolleri Ata
1. Merhaba gelen **yapılandırma** 'yi tıklatın **kullanıcılar**.<br>
   ![Ekran Azure AD Connect sistem durumu RBAC ana dikey, vurgulanmış kullanıcılarla](./media/active-directory-aadconnect-health/RBAC_main_blade.png)
2. **Add (Ekle)** seçeneğini belirleyin.
3. Merhaba, **bir rol seçin** bölmesinde, bir rol seçin (örneğin, **sahibi**).<br>
   ![Azure ekran AD sistem durumu RBAC kullanıcıların bağlanmasına penceresi](./media/active-directory-aadconnect-health/RBAC_add.png)
4. Merhaba adı yazın veya hedeflenen hello kullanıcı veya grup tanıtıcısı. Bir veya daha fazla kullanıcı veya grup hello adresindeki seçebileceğiniz aynı anda. **Seç**'e tıklayın.
   ![Azure ekran AD sistem durumu RBAC kullanıcıların bağlanmasına penceresi](./media/active-directory-aadconnect-health/RBAC_select_users.png)
5. **Tamam**’ı seçin.<br>
6. Hello rol ataması tamamlandıktan sonra hello kullanıcılar ve gruplar hello listesinde görünür.<br>
   ![Vurgulanan yeni kullanıcılar ile Azure ekran AD sistem durumu RBAC kullanıcıların bağlanmasına penceresi](./media/active-directory-aadconnect-health/RBAC_user_list.png)

Merhaba kullanıcılar listelenmiş ve gruplar, roller atanmış tootheir göre erişebilir.

> [!NOTE]
> * Genel yöneticiler her zaman tam erişim tooall hello işlemleri sahip, ancak genel yönetici hesapları listesi önceki hello mevcut değildir.
> * Merhaba kullanıcıları davet Özelliği Azure AD Connect Health içinde desteklenmez.
>
>

#### <a name="step-3-share-hello-blade-location-with-users-or-groups"></a>3. adım: Paylaşımı hello dikey konumu olan kullanıcıları veya grupları
1. İzinleri atadıktan sonra bir kullanıcı Azure AD Connect Health giderek erişebilir [burada](http://aka.ms/aadconnecthealth).
2. Merhaba dikey penceresinde hello kullanıcı hello dikey ya da farklı bölümleri, toohello Pano sabitleyebilirsiniz. Merhaba tıklamanız yeterlidir **PIN toodashboard** simgesi.<br>
   ![Vurgulanan PIN simgesiyle ekran Azure AD Connect sistem durumu RBAC PIN dikey](./media/active-directory-aadconnect-health/RBAC_pin_blade.png)

> [!NOTE]
> Merhaba okuyucu rolüne atanmış olan bir kullanıcı hello Azure Marketi mümkün tooget Azure AD Connect Health uzantı değil. Merhaba kullanıcı hello gerekli "Oluştur" işlemi toodo bu nedenle gerçekleştirilemiyor. Merhaba kullanıcı tarafından giderek toohello bağlantı önceki toohello dikey hala elde edebilirsiniz. Sonraki kullanım için hello kullanıcı hello dikey toohello Pano sabitleyebilirsiniz.
>
>

### <a name="remove-users-or-groups"></a>Kullanıcıları veya grupları kaldırın
Bir kullanıcıya veya gruba eklenen kaldırabilirsiniz tooAzure AD Connect sistem durumu RBAC. Sadece hello kullanıcı veya grubu sağ tıklatın ve seçin **kaldırmak**.<br>
![Vurgulanan Kaldır ile Azure ekran AD sistem durumu RBAC kullanıcıların bağlanmasına penceresi](./media/active-directory-aadconnect-health/RBAC_remove.png)

[//]: # (End of RBAC section)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Aracısı yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health sürüm geçmişi](active-directory-aadconnect-health-version-history.md)
