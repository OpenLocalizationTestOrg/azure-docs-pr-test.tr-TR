---
title: "Şirket içi kimlik altyapınızın hello aaaMonitor bulut."
description: "Bu nedir açıklayan hello Azure AD Connect Health sayfasıdır ve kullanacağınızı neden."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Şirket içi kimlik altyapınızı ve eşitleme hizmetlerinizi hello bulutta izleyin
Azure Active Directory (Azure AD) Connect Health, izlemek ve şirket içi kimlik altyapınızı ve hello Eşitleme hizmetlerini erişim sahibi yardımcı olur. Toomaintain güvenilir bağlantı tooOffice 365 ve Microsoft Online Services Active Directory Federasyon Hizmetleri (AD FS) sunucuları, Azure AD Connect sunucuları (da bilinen gibi anahtar kimlik bileşenlerinizi izleme işlevleri sağlayarak sağlar Eşitleme altyapısı), olarak Active Directory etki alanı denetleyicileri, vs. Ayrıca hello bu bileşenler hakkındaki anahtar veri noktalarını kolayca erişilebilir böylece kullanım alabilir ve diğer önemli kılar Öngörüler toomake kararları bilgilendirildi.

Merhaba bilgi hello sunulan [Azure AD Connect Health portalı](https://aka.ms/aadconnecthealth). Hello Azure AD Connect Health Portalı'nda, uyarıları, performans izlemeyi, kullanım analizi ve diğer bilgileri görüntüleyebilirsiniz. Azure AD Connect Health hello tek sistem durumu tek bir yerde anahtar kimlik bileşenleriniz için odağı sağlar.

![Azure AD Connect Health nedir?](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Azure AD Connect Health Hello özelliklerinde arttıkça, hello portal kimlik hello odağı aracılığıyla tek bir Pano sağlar. Daha sağlam, sağlıklı ve tümleşik bir ortam, kullanıcıların tooincrease için kendi yeteneği tooget hallolmasını.

## <a name="why-use-azure-ad-connect-health"></a>Azure AD Connect Health neden kullanılır?
Şirket içi dizinlerinizi Azure AD ile tümleştirdiğinizde, ortak bir kimlik tooaccess hem Bulut ve şirket içi kaynaklar olduğundan, kullanıcılarınızın daha üretken. Ancak, bu tümleştirme, kullanıcıların güvenilir bir şekilde hem şirket içinde ve hello bulut kaynaklarına herhangi bir aygıttan erişebilmesi için bu ortamın sağlıklı olup sağlamaya hello sınama oluşturur. Azure AD Connect Health, izleme ve kullanılan tooaccess Office 365 veya diğer Azure AD uygulamaları şirket içi kimlik altyapınızı Öngörüler elde yardımcı olur. Her bir şirket içi kimlik sunucunuza bir aracı yüklemek kadar basittir.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[AD FS için Azure AD Connect Health](active-directory-aadconnect-health-adfs.md)
AD FS'ye ilişkin Azure AD Connect Health Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 üzerinde AD FS 2.0'ı destekler. Ayrıca izleme hello AD FS proxy destekler veya extranet erişimi için kimlik doğrulaması sağlayan web uygulama proxy sunucuları destekler. Bir kolay ve düşük maliyetli yüklemesiyle hello sistem durumu aracısı, Azure AD Connect Health AD FS için hello aşağıdaki temel işlevler kümesini sağlar:

* AD FS ile AD FS proxy sunucuları sağlam olmadığında uyarı tooknow ile izleme
* Kritik uyarılar için e-posta bildirimleri
* AD FS kapasite planlaması için yararlı olan performans verilerindeki eğilimler
* AD FS oturum açma işlemleri ile AD FS kullanımını nasıl yararlı toounderstand olan özetlere (uygulamalar, kullanıcılar, ağ konumu vb.) için kullanım analizi
* Son IP adresi ile hatalı kullanıcı adı/parola denemesi yapan ilk 50 kullanıcı gibi AD FS raporları

Merhaba aşağıdaki video Azure AD Connect Health genel bir bakış için AD FS sağlar.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Eşitleme için Azure AD Connect Health](active-directory-aadconnect-health-sync.md)
Azure AD Connect Health eşitleme izler ve şirket içi Active Directory ve Azure AD arasında oluşan hello eşitlemeler hakkında bilgi sağlar. Azure AD Connect Health eşitleme hello aşağıdaki temel işlevler kümesini sağlar:

* Bir Azure AD Connect sunucusu olduğunda uyarıları tooknow ile izleme, olarak da bilinen eşitleme altyapısı hello iyi durumda değil
* Kritik uyarılar için e-posta bildirimleri
* Ekleme, güncelleştirme, silme gibi farklı işlemlerdeki eğilimlere ve eşitleme işlemlerine ilişkin gecikme süresi grafikleri de dahil olmak üzere, eşitlemeyle ilgili operasyonel öngörüler
* Hızlı bakış bilgileri eşitleme özelliklerine ve son başarılı tooAzure AD dışarı aktarma
* Nesne düzeyinde eşitleme hatalarıyla ilgili raporlar için \(Azure AD Premium gerekli değildir\)

Merhaba aşağıdaki video Azure AD Connect Health genel bir bakış için eşitleme sağlar.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[AD DS için Azure AD Connect Health](active-directory-aadconnect-health-adds.md)
Active Directory Domain Services (AD DS) için Azure AD Connect Health, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016'da yüklü etki alanı denetleyicileri için izleme olanağı sağlar. Merhaba Sistem Durumu Aracısı yükleme sağlar, toomonitor şirket içi AD DS ortamında hello buluttan. Azure AD Connect Health AD DS'nin hello aşağıdaki temel işlevler kümesini sağlar:

* Etki alanı denetleyicileri sağlıksız ve e-posta bildirimleri kritik uyarılar için uyarılar toodetect izleme
* Merhaba sistem durumu hızlı bir görünümünü ve etki alanı denetleyicileriniz işletimsel durumunu sağlar hello etki alanı denetleyicileri Panosu
* Merhaba son çoğaltma bilgileri ve hatalar algılandığında tootroubleshooting kılavuzları bağlantılar hello çoğaltma durumu Panosu
* Sorun giderme ve izleme amacıyla için gerekli olan popüler performans sayaçları tooperformance veri grafikleri her yerden erişim hızlı

Merhaba aşağıdaki video Azure AD Connect Health genel bir bakış için AD DS sağlar.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Azure AD Connect Health ile çalışmaya başlama
Azure AD Connect Health ile aşağıdaki adımları kullanın hello tooget başlatıldı:

1. [Azure AD Premium alın](../active-directory-get-started-premium.md) veya [deneme sürümünü başlatın](https://azure.microsoft.com/trial/get-started-active-directory/).
2. Kimlik sunucularınıza [Azure AD Connect Health Aracılarını indirin ve yükleyin](#download-and-install-azure-ad-connect-health-agent).
3. Görünüm hello Azure AD Connect Health Panosu'nda [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Azure AD Connect Health Panonuzda veri görmeden önce hedeflenen sunucularınıza tooinstall hello Azure AD Connect Health aracılarını gereksinim unutmayın.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Azure AD Connect Health Aracısını indirme ve yükleme
* Olduğundan emin olun, [hello gereksinimleri karşılaması](active-directory-aadconnect-health-agent-install.md#requirements) Azure AD Connect Health için.
* AD FS için Azure AD Connect Health kullanmaya başlama
    * [AD FS için Azure AD Connect Health Aracısını indirin.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Merhaba yükleme yönergelerine bakın](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Eşitleme için Azure AD Connect Health kullanmaya başlama
    * [Hello Azure AD Connect'in en son sürümünü karşıdan yükleyip](http://go.microsoft.com/fwlink/?linkid=615771). Eşitleme için sistem durumu aracısı Hello hello Azure AD Connect yüklemesinin bir parçası yüklenir (sürüm 1.0.9125.0 veya daha yüksek).
* AD DS için Azure AD Connect Health kullanmaya başlama
    * [AD DS için Azure AD Connect Health Aracısını indirin](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Merhaba yükleme yönergelerine bakın](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Azure AD Connect Health portalı
Hello Azure AD Connect Health portalı uyarıları, performans ve kullanım analizi görünümleri gösterir. Merhaba https://aka.ms/aadconnecthealth URL Azure AD Connect Health'in ana dikey toohello alır. Dikey pencereyi bir pencere olarak düşünebilirsiniz. Merhaba ana dikey penceresinde, gördüğünüz **Hızlı Başlangıç**, Azure AD Connect Health ve ek yapılandırma seçeneklerini içindeki Hizmetler. Merhaba bkz ekran ve hello ekran izleyin kısa açıklamaları. Merhaba aracıları dağıttıktan sonra hello sistem durumu hizmeti otomatik olarak Azure AD Connect Health izleme hello hizmetleri tanımlar.

> [!NOTE]
> Lisans bilgileri için bkz: Merhaba [Azure AD Connect ile ilgili SSS](active-directory-aadconnect-health-faq.md) veya hello [Azure AD fiyatlandırma sayfası](https://aka.ms/aadpricing).
    
![Azure AD Connect Health Portalı](./media/active-directory-aadconnect-health/portal4.png)

* **Hızlı Başlangıç**: Bu seçeneği belirlediğinizde, hello **Hızlı Başlangıç** dikey pencere açılır. Seçerek hello Azure AD Connect Health Aracısı indirebilirsiniz **araçları alma**. Ayrıca, belgelere erişebilir ve geri bildirim gönderebilirsiniz.
* **Active Directory Federasyon Hizmetleri**: Bu seçenek Azure AD Connect Health şu anda izlediği tüm AD FS hello hizmetleri gösterir. Bir örnek seçin, açılır hello dikey o hizmet örneği hakkında bilgi gösterir. Bu bilgiler; genel bakışı, özellikleri, uyarıları, izlemeyi ve kullanım analizlerini içerir. Merhaba özellikler hakkında daha fazla bilgiyi [kullanarak Azure AD Connect Health AD FS ile](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (eşitleme)**: Bu seçenek, Azure AD Connect Health'in o anda izlediği Azure AD Connect sunucularınızı gösterir. Hello girdisini seçtiğinizde açar hello dikey Azure AD Connect sunucularınız hakkında bilgi gösterir. Merhaba özellikler hakkında daha fazla bilgiyi [kullanarak Azure AD Connect Health eşitleme](active-directory-aadconnect-health-sync.md).
* **Active Directory etki alanı Hizmetleri**: Bu seçenek Azure AD Connect Health şu anda izlediği tüm AD DS hello ormanlar gösterir. Bir orman seçin, açılır hello dikey o ormana hakkında bilgi gösterir. Bu bilgiler, önemli bilgiler, hello etki alanı denetleyicileri Pano, hello çoğaltma durumu Panosu, uyarılar ve izleme hakkında genel bir bakış içerir. Merhaba özellikler hakkında daha fazla bilgiyi [kullanarak Azure AD Connect Health AD DS ile](active-directory-aadconnect-health-adds.md).
* **Yapılandırma**: Bu bölümde açıp kapatma seçenekleri tooturn hello aşağıdakileri içerir:

  - Otomatik güncelleştirme tooautomatically güncelleştirme hello Azure AD Connect Health Aracısı toohello en son sürümü: mevcut olduklarında hello Azure AD Connect Health Aracısı en son sürümlerini otomatik olarak güncelleştirilen toohello olacaktır. Bu, varsayılan olarak etkindir.
  - Sorun giderme amacıyla yalnızca Microsoft access tooyour Azure AD directory durum verilerine izin ver: Bu etkinleştirildiğinde Microsoft görebilirsiniz hello gördüğünüz aynı veri. Bu bilgiler sorun giderme konusunda yardımcı olabilir. Bu, varsayılan olarak devre dışıdır.

## <a name="related-links"></a>İlgili bağlantılar
* [Azure AD Connect Health Aracısı yüklemesi](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health işlemleri](active-directory-aadconnect-health-operations.md)
* [Azure AD Connect Health'i AD FS ile Kullanma](active-directory-aadconnect-health-adfs.md)
* [Eşitleme için Azure AD Connect Health'i kullanma](active-directory-aadconnect-health-sync.md)
* [Azure AD Connect Health'i AD DS ile Kullanma](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health ile ilgili SSS](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health sürüm geçmişi](active-directory-aadconnect-health-version-history.md)
