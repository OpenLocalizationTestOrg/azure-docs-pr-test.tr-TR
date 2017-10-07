---
title: "Azure Traffic Manager ile azure'da aaaHigh kullanılabilirlik çapraz coğrafi AD FS dağıtımı | Microsoft Docs"
description: "Bu belgede, öğreneceksiniz nasıl toodeploy AD FS azure'da yüksek kullanılabilirlik için."
keywords: "Ad fs ile Azure trafik Yöneticisi, adfs Azure trafik Yöneticisi, coğrafi, birden çok veri merkezi, coğrafi veri merkezleri, çoklu coğrafi veri merkezleri, azure'da AD FS dağıtmak, dağıtımını azure adfs, azure adfs, azure ad fs, adfs dağıtımı, ad fs, adfs azure'da dağıtmak, ADFS dağıtımı azure üzerinde adfs tooazure taşıma azure, adfs azure, Azure, Azure, ıaas, ADFS, AD FS'de giriş tooAD FS, AD FS dağıtma"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Azure Traffic Manager ile Azure’da yüksek kullanılabilirliğe sahip çapraz coğrafi AD FS dağıtımı
[Azure AD FS dağıtım](active-directory-aadconnect-azure-adfs.md) adım adım kılavuz sağlar toohow Azure içinde kuruluşunuz için basit bir AD FS altyapısını dağıtabilirsiniz. Bu makalede, Azure kullanarak AD FS dağıtımını toocreate bir çapraz coğrafi hello sonraki adımlar sağlanmaktadır [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Azure trafik Yöneticisi yardımcı yaparak coğrafi olarak forma yüksek kullanılabilirlik ve yüksek performanslı, kuruluşunuz için AD FS altyapısını oluşturmak yönlendirme yöntemleri kullanılabilir toosuit farklı gereken hello altyapısından aralığının kullanın.

Çapraz coğrafi yüksek kullanılabilirliğe sahip AD FS altyapısı şunları sağlar:

* **Tek hata noktası ortadan kaldırılması:** ile yük devretme yetenekleri Azure trafik Yöneticisi'nin, hatta hello Merhaba Dünya bir parçası olan veri merkezlerinde birini devre dışı kaldığında yüksek oranda kullanılabilir bir AD FS altyapısını elde edebilirsiniz
* **Geliştirilmiş performans:** kullanabileceğiniz hello önerilen Bu makale tooprovide dağıtımda daha hızlı kimlik doğrulaması kullanıcıların yardımcı olabilecek yüksek performanslı AD FS altyapısı. 

## <a name="design-principles"></a>Tasarım ilkeleri
![Genel tasarım](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Merhaba temel tasarım ilkeleri tasarım ilkeleri AD FS dağıtımı azure'da hello makalesinde listelenen aynı olacaktır. Yukarıdaki diyagramda Hello hello temel dağıtımı tooanother coğrafi bölge için bir basit uzantısı gösterir. Bazı noktaları tooconsider dağıtım toonew Coğrafi bölgenize genişletirken altındadır

* **Sanal ağ:** yeni bir sanal ağ oluşturmanız gerekir hello coğrafi bölgede toodeploy ek AD FS altyapınızın istiyor. Yukarıdaki Hello diyagramda, Geo1 VNET ve Geo2 VNET her coğrafi bölgedeki iki sanal ağ hello gibi görürsünüz.
* **Etki alanı denetleyicilerinin ve AD FS sunucularına yeni coğrafi VNET:** hello AD FS sunucuları hello yeni bölgede toocontact bir etki alanı denetleyicisi başka bir programda kadar değil böylece toodeploy etki alanı denetleyicileri hello yeni coğrafi bölgede önerilir dışarıda ağ toocomplete bir kimlik doğrulama ve böylece iyileştirme hello performans.
* **Depolama hesapları:** Depolama hesapları bir bölge ile ilişkilidir. Yeni bir coğrafi bölge içindeki makineler dağıtma olduğundan, toocreate toobe hello bölgede kullanılan yeni depolama hesaplarına sahip olur.  
* **Ağ Güvenlik Grupları:** Bir bölgede oluşturulan Ağ Güvenlik Grupları başka bir coğrafi bölgede depolama hesabı olarak kullanılamaz. Bu nedenle, INT ve DMZ alt hello yeni coğrafi bölgede toocreate yeni ağ güvenlik grupları benzer toothose hello ilk coğrafi bölgede gerekir.
* **Genel IP adresleri için DNS etiketleri:** Azure Traffic Manager tooendpoints başvurabilir yalnızca DNS etiketleri aracılığıyla. Bu nedenle, hello dış yük dengeleyici ortak IP adresleri için DNS etiketleri gerekli toocreate altındadır.
* **Azure Traffic Manager:** Microsoft Azure trafik Yöneticisi toocontrol hello dağıtım Merhaba Dünya farklı veri merkezlerinde çalışan kullanıcı trafiği tooyour hizmet uç noktaları sağlar. Azure trafik Yöneticisi DNS düzeyi hello çalışır. DNS yanıtları toodirect son kullanıcı trafiği tooglobally dağıtılmış uç noktaları kullanır. İstemciler daha sonra toothose uç noktaları doğrudan bağlanır. Farklı yönlendirme seçeneklerle performans, Weighted ve öncelik, kuruluşunuzun gereksinimlerine en uygun hello yönlendirme seçeneği kolayca seçebilirsiniz. 
* **İki bölgeler arasında V net tooV net bağlantısı:** , hello sanal ağlar arasında toohave bağlantı kendisini gerekmez. Her sanal ağ erişim toodomain denetleyicilerinin ve AD FS ve WAP sunucusu kendisini sahip olduğundan, farklı bölgelerdeki hello sanal ağlar arasında herhangi bir bağlantı olmadan çalışabilir. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Adımları toointegrate Azure trafik Yöneticisi
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Merhaba yeni coğrafi bölge'de AD FS dağıtma
Merhaba adımları ve yönergeleri izleyin [azure'da AD FS dağıtımı](active-directory-aadconnect-azure-adfs.md) toodeploy hello hello yeni coğrafi bölgede aynı topolojisi.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Merhaba Internet'e yönelik (Genel) yük dengeleyici genel IP adresi için DNS etiketleri
Yukarıda belirtildiği gibi hello Azure trafik Yöneticisi uç noktalar olarak tooDNS etiketleri yalnızca başvuruda bulunabilir ve bu nedenle önemli toocreate DNS etiketleri hello dış yük dengeleyici ortak IP adresleri için oluşur. Merhaba ortak IP adresi için DNS etiketi nasıl yapılandırabileceğiniz ekran görüntüsü gösterilmektedir. 

![DNS Etiketi](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager’ı dağıtma
Trafik Yöneticisi profili toocreate Hello adımları izleyin. Daha fazla bilgi için aynı zamanda çok başvurabilir[bir Azure Traffic Manager profilini yönetme](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Traffic Manager profili oluşturun:** Traffic manager profilinize benzersiz bir ad verin. Bu hello profilinin adını hello DNS adı bir parçasıdır ve hello trafik yöneticisi etki alanı adı etiketi için bir önek olarak görev yapar. Merhaba adı / önek trafik Yöneticisi için too.trafficmanager.net toocreate bir DNS etiketi eklenir. Merhaba ekran görüntüsü aşağıda hello trafik Yöneticisi DNS ön ekini mysts.trafficmanager.net mysts ve sonuçta elde edilen DNS etiketi olarak ayarlanan gösterir. 
   
    ![Traffic Manager profili oluşturma](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Trafik yönlendirme yöntemi:** Traffic manager’da üç yönlendirme seçeneği vardır:
   
   * Öncelik 
   * Performans
   * Ağırlıklı
     
     **Performans** hello seçeneği tooachieve hızlı yanıt veren AD FS altyapınızın önerilir. Ancak, dağıtım ihtiyaçlarınıza en uygun yönlendirme yöntemini seçebilirsiniz. Merhaba AD FS işlevselliğine hello yönlendirme seçeneği seçili tarafından etkilenmez. Daha fazla bilgi için bkz. [Traffic Manager trafik yönlendirme yöntemleri](../traffic-manager/traffic-manager-routing-methods.md). Hello hello Yukarıdaki örnek ekran görebilirsiniz **performans** seçilen yöntemi.
3. **Uç noktalarını yapılandırma:** hello trafik Yöneticisi sayfası, uç noktalarda tıklayın ve Ekle'yi seçin. Bu bir Ekle uç nokta sayfa benzer toohello aşağıdaki ekran görüntüsünde açar
   
   ![Uç noktaları yapılandırma](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Merhaba farklı girdileri hello kılavuz aşağıdaki izleyin:
   
   **Tür:** biz tooan Azure genel IP adresine işaret şekilde Azure uç noktası seçin.
   
   **Ad:** tooassociate hello uç noktası ile istediğiniz bir ad oluşturun. Bu hello DNS adı değil ve şifrelemeyle DNS kayıtları vardır.
   
   **Hedef kaynak türü:** hello değeri toothis özelliği olarak seçin genel IP adresi. 
   
   **Hedef kaynak:** bu seçeneği toochoose verecektir hello farklı DNS etiketlerden sahip olduğunuz kullanılabilir abonelik altında. Merhaba yapılandırmakta olduğunuz karşılık gelen toohello endpoint DNS etiketi seçin.
   
   Hello Azure Traffic Manager tooroute trafiği istediğiniz her coğrafi bölge için uç nokta ekleyin.
   Daha fazla bilgi ve ayrıntılı adımları tooadd / traffic Manager'da uç yapılandırın, çok bakın[ekleme, devre dışı bırakma, etkinleştirme veya silme uç noktaları](../traffic-manager/traffic-manager-endpoints.md)
4. **Araştırmasını yapılandırma:** hello trafik Yöneticisi sayfasında, yapılandırma'ya tıklayın. Merhaba yapılandırma sayfasında, toochange hello İzleyici ayarlarını tooprobe HTTP bağlantı noktası 80 ve göreli yol /adfs/probe gerekir
   
    ![Araştırmayı yapılandırma](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Merhaba yapılandırması tamamlandıktan sonra hello uç noktaları hello durumunu çevrimiçi olduğundan emin olun**. Tüm uç noktaları 'düzeyi düşürülmüş' durumunda ise, Azure Traffic Manager hello tanılama yanlış ve tüm uç noktaları ulaşılabilen varsayarak bir en iyi girişim tooroute hello trafiği yapın.
   > 
   > 
5. **Azure trafik Yöneticisi için DNS kayıtlarını değiştirme:** Federasyon hizmetinize bir CNAME toohello Azure trafik Yöneticisi DNS adı olmalıdır. Böylece aktaranın tooreach hello Federasyon hizmeti çalışıyor gerçekte hello Azure Traffic Manager ulaştığında bir CNAME hello Genel DNS kayıtlarını oluşturun.
   
    Örneğin, toopoint hello Federasyon Hizmeti fs.fabidentity.com toohello trafik Yöneticisi aşağıdaki, DNS kaynak kaydı toobe hello tooupdate gerekir:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Test Hello Yönlendirme ve AD FS oturum açma
### <a name="routing-test"></a>Yönlendirme testi
Merhaba yönlendirme çok basit bir sınama tootry ping hello Federasyon Hizmeti DNS adı her coğrafi bölgede bulunan bir makineden olacaktır. Seçilen hello yönlendirme yöntemine bağlı olarak, aslında ping hello endpoint hello ping görüntüde yansıtılır. Merhaba performans seçtiyseniz, örneğin, yönlendirme, ardından toohello en yakın hello bitiş hello istemci bölgesi ulaşılacak. İki farklı bir bölgeye istemci makinelerden iki ping hello görüntüsünü, EastAsia bölgede diğeri Batı ABD aşağıdadır. 

![Yönlendirme testi](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS oturum açma testi
Merhaba en kolay yolu tootest AD FS hello Idpınitiatedsignon.aspx sayfasının kullanmaktır. Gerekli tooenable olduğundan, sipariş toobe mümkün toodo içinde IdpInitiatedSignOn hello AD FS özellikleri hello. AD FS kurulumunuzu tooverify Hello adımları izleyin

1. Çalışma hello aşağıdaki cmdlet'i hello AD FS sunucusunda PowerShell, tooset kullanarak, onu tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Herhangi bir dış makineden https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx sayfasına erişin
3. Merhaba AD FS sayfasını görmelisiniz aşağıdaki gibi:
   
    ![ADFS testi - kimlik doğrulama sınaması](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    oturum açma başarılı olduğunda aşağıdaki gibi bir başarı iletisi gösterilir:
   
    ![ADFS testi - kimlik doğrulama başarılı](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>İlgili bağlantılar
* [Azure’da temel AD FS dağıtımı](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [Traffic Manager trafik yönlendirme yöntemleri](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure Traffic Manager profilini yönetme](../traffic-manager/traffic-manager-manage-profiles.md)
* [Uç noktaları ekleme, devre dışı bırakma, etkinleştirme veya silme](../traffic-manager/traffic-manager-endpoints.md) 

