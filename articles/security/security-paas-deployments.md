---
title: "aaaSecuring PaaS dağıtımları | Microsoft Docs"
description: " Merhaba güvenlik avantajlarından PaaS diğer bulut hizmet modeli karşılaştırması anlamak ve Azure PaaS dağıtımınızın güvenliğini sağlamaya yönelik önerilen yöntemleri öğrenin. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>PaaS dağıtımları güvenliğini sağlama

Bu makale size yardımcı olacak bilgileri sağlar:

- Merhaba bulut uygulamalarında barındırma hello güvenlik avantajlarından anlama
- Diğer bulut hizmet modeli karşılaştırması (PaaS) hizmet olarak platform Hello güvenlik avantajlarından değerlendir
- Bir ağ merkezli tooan kimlik merkezli çevre güvenlik yaklaşımını güvenlik odağınız değiştirme
- Genel PaaS güvenlik en iyi uygulama önerilerini uygulama

## <a name="cloud-security-advantages"></a>Bulut güvenlik avantajları
Merhaba bulutta güvenlik avantajları toobeing vardır. Kuruluşların büyük olasılıkla bir şirket içi ortamda sahip unmet sorumluluklar ve sınırlı kaynak kullanılabilir tooinvest saldırganlar tüm katmanlar adresindeki mümkün tooexploit güvenlik açıkları olduğu bir ortam oluşturur güvenliği.

![Bulut dönem güvenlik avantajları][1]

Kuruluşların bir sağlayıcının bulut tabanlı güvenlik özellikleri ve bulut Intelligence kullanarak kendi tehdit algılama ve yanıt sürelerini mümkün tooimprove olan.  Sorumlulukları toohello bulut sağlayıcısı değiştirerek, kuruluşların bunları sağlayan daha fazla güvenlik kapsamı tooreallocate güvenlik kaynakları ve bütçe tooother iş önceliklerini elde edebilirsiniz.

## <a name="division-of-responsibility"></a>Sorumluluk bölme
Önemli toounderstand hello bölme sorumluluk ve Microsoft arasında değil. Şirket içi, hello tüm yığın sahipseniz, ancak toohello bulut Taşı gibi bazı sorumlulukları tooMicrosoft aktarım. Merhaba aşağıdaki sorumluluk matrisi hello alanları hello yığınının sorumlu olan bir SaaS, PaaS ve Iaas dağıtımında gösterir ve Microsoft sorumludur.

![Sorumluluk bölgeleri][2]

Tüm bulut dağıtım türleri için veri ve kimlikler sahip. Veri ve kimlikleri, şirket içi kaynakları hello güvenliğini korumak sizin sorumluluğunuzdadır ve denetim bulut bileşenleri hello (hangi hizmet türüne göre değişir).

Her zaman dağıtım, başlangıç türü ne olursa olsun, tarafından korunur sorumlulukları şunlardır:

- Veriler
- Uç Noktalar
- Hesap
- Erişim Yönetimi

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Hizmet modeli bir PaaS güvenlik avantajlarından bulut
Kullanarak hello aynı sorumluluk matrisi, şimdi bir Azure PaaS dağıtımı veya şirket içinde hello güvenlik avantajlarından bakın.

![PaaS güvenlik avantajları][3]

Merhaba yığının hello fiziksel altyapı Hello altındaki başlangıç Microsoft ortak riskleri ve sorumlulukları azaltır. Merhaba Microsoft bulut sürekli olarak Microsoft tarafından izlenen, sabit tooattack demektir. Bir saldırganın toopursue hello Microsoft bulut için hedef olarak anlamlı değil. Merhaba saldırgan para ve kaynakları, hello saldırgan çok sayıda olmadıkça tooanother hedefte büyük olasılıkla toomove olur.  

Merhaba yığını Hello ortadaki bir PaaS dağıtımı ve şirket içi arasında fark yoktur. Merhaba uygulama katmanı ve hello hesabı ve erişim yönetimi katmanı, benzer riskleri de vardır. Merhaba sonraki adımlar bölümünde bu makalede, ortadan kaldırmak veya bu riskleri en aza indirmek için toobest uygulamalar rehberlik ediyoruz.

Merhaba hello yığını, veri yönetimi ve hak yönetimi üst kısmında, Anahtar Yönetimi tarafından azaltılabilir bir riskini alırsınız. (Anahtar yönetimi en iyi yöntemleri ele alınmıştır.) Anahtar Yönetimi ek sorumluluk olsa da, kaynakları tookey Yönetimi kaydırma için artık toomanage elinizde bir PaaS dağıtımı alanlarında sahip.

Hello Azure platformu Ayrıca, güçlü DDoS koruması çeşitli ağ tabanlı teknolojileri kullanılarak sağlar. Ancak, tüm ağ tabanlı DDoS koruması yöntemleri sınırlarının bir bağlantı başına ve veri merkezi başına temelinde vardır. toohelp büyük DDoS saldırıları hello etkisini kaçınmak için Azure'nın çekirdek bulut yeteneğinin, etkinleştirme tooquickly ve otomatik olarak toodefend DDoS saldırılarına karşı genişletme yararlanabilirsiniz. Nasıl yöntemler makaleleri önerilen hello bunu yapabilirsiniz üzerinde size daha fazla ayrıntıya gidersiniz.

## <a name="modernizing-hello-defenders-mindset"></a>Modernizing hello defender'ın bakış
İle PaaS dağıtımları genel yaklaşım toosecurity bir kayma gelir. Her şeyi toocontrol gerek shift kendiniz toosharing sorumluluk Microsoft ile.

Başka bir önemli PaaS geleneksel şirket içi dağıtımlar arasındaki farktır ne hello birincil güvenlik çevre tanımlar, yeni bir görünüm. Tarihsel olarak, hello birincil şirket içi güvenlik çevre ağınızda olan ve en güvenlik tasarımları kullanım hello ağ kendi birincil güvenlik Özet olarak şirket. PaaS dağıtımları için kimlik toobe hello birincil güvenlik çevre dikkate alarak daha iyi sunulur.

## <a name="identity-as-hello-primary-security-perimeter"></a>Merhaba birincil güvenlik çevre olarak kimliği
Merhaba beş temel özellik, ağ merkezli yapar geniş ağ erişimi bulut, biri daha az ilgili düşünüyoruz. Merhaba amacı tooallow kullanıcılar Konum bağımsız olarak tooaccess kaynakları bulut bilgi işlemin çoğunu. Çoğu kullanıcı için konumlarını toobe yere hello Internet üzerinde geçiyor.

Merhaba aşağıdaki şekilde hello güvenlik çevre ağ çevre tooan kimlik çevre nasıl gelişmiştir gösterilmektedir. Güvenlik ağınızın savunma hakkında daha az ve daha fazla hakkında verilerinizi savunma yanı hello güvenlik uygulamaları ve kullanıcıları yönetme olur. Merhaba anahtar toopush güvenlik daha yakından toowhat's önemli tooyour şirket istediğiniz farktır.

![Yeni güvenlik çevre olarak kimliği][4]

Başlangıçta, Azure PaaS Hizmetleri (örneğin, web rolleri ve Azure SQL) çok az kayıpla veya hiç geleneksel ağ çevre savunma sağlanan. Kullanıma sunulan toobe toohello Internet (web rolü) hello öğenin amacı olan ve hello yeni çevre (örneğin, BLOB veya Azure SQL), kimlik doğrulamasının sağlar algılandı.

Modern güvenlik uygulamalarını, o hello etkilemeyi hello ağ çevre İhlale yol varsayalım. Bu nedenle, modern savunma yöntemler tooidentity taşınmış olması. Kuruluşlar, güçlü kimlik doğrulama ve yetkilendirme sağlığı (iyi) ile kimlik tabanlı güvenlik çevre oluşturmanız gerekir.

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Merhaba kimlik çevre yönetme ile ilgili öneriler

İlkeleri ve hello ağ çevre modeller için on yılları kullanılabilir olmuştur. Buna karşılık, hello endüstri görece daha az deneyimi hello birincil güvenlik çevre kimliğine sahip olur. Başka bir deyişle ile yeterli deneyimi tooprovide hello alanında kanıtlanmış bazı genel öneriler birikmiş ve tüm PaaS Hizmetleri tooalmost uygulayın.

Merhaba aşağıdaki genel bir en iyi yöntemler yaklaşım toomanaging kimlik çevre özetler.

- **Anahtarları veya kimlik bilgilerini kaybetmeyin** olan temel toosecure PaaS dağıtımları anahtarlarını ve kimlik bilgilerini güvenli hale getirme. Anahtarları ve kimlik bilgileri kaybetme yaygın görülen bir sorundur. Bir iyi toouse merkezi çözümü anahtarları ve gizli anahtarları donanım güvenlik modülleri (HSM) depolanabileceği çözümdür. Azure ile Merhaba bulutta HSM sağlar [Azure anahtar kasası](../key-vault/key-vault-whatis.md).
- **Kimlik bilgileri ve diğer parolaları kaynak kodu veya GitHub koymayın** toothem anahtarlarını ve kimlik bilgilerini kaybetme elde yetkisiz bir tarafın sahip çok şey daha da kötüsü erişim yalnızca hello. Saldırganlar mümkün tootake avantajlarından bot teknolojileri toofind anahtarları ve gizli anahtarları kod depoları GitHub gibi depolanan ' dir. Bu ortak kaynak kodu depolarına anahtarı ve gizli anahtarları koymayın.
- **Karma PaaS ve Iaas Hizmetleri, VM yönetim arabirimlerindeki korumak** Iaas ve PaaS Hizmetleri sanal makinelerde (VM) çalışır. Hizmet Hello türüne bağlı olarak birkaç yönetim arabirimleri kullanılabilir sağlamak tooremote bu Vm'lere doğrudan yönetme. Uzaktan Yönetim protokolleri gibi [Secure Shell Protokolü (SSH)](https://en.wikipedia.org/wiki/Secure_Shell), [Uzak Masaüstü Protokolü (RDP)](https://support.microsoft.com/kb/186607), ve [uzak PowerShell](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) kullanılabilir. Genel olarak, doğrudan uzaktan erişim tooVMs hello Internet gelen etkinleştirmemeniz önerilir. Mevcut ise, Azure sanal ağda sanal özel ağ kullanarak gibi alternatif yaklaşımlar kullanmanız gerekir. Alternatif yaklaşımlar kullanılabilir değil ve ardından karmaşık parolaları kullandığınızdan emin olun ve varsa, iki öğeli kimlik doğrulama (gibi [Azure çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md)).
- **Güçlü kimlik doğrulama ve yetkilendirme platformları kullanın**

  - Federasyon kimlikleri özel kullanıcı depoları yerine Azure AD kullanın. Federasyon kimlikleri kullandığınızda, platform tabanlı bir yaklaşım yararlanmak ve yetkili kimlikleri tooyour ortakları hello yönetimini atayabilirsiniz. Bir Federasyon kimlik yaklaşım çalışanlar sona erdirilir ve bilgilerin toobe gerekiyor, birden çok kimlik ve yetkilendirme sistemlerinin yansıtılan senaryolarında özellikle önemlidir.
  - Sağlanan platform kimlik doğrulama ve yetkilendirme mekanizmaları yerine özel kod kullanın. Merhaba özel kimlik doğrulama kodu geliştirme hataya olabilir nedenidir. Çoğu, geliştiricilerin güvenlik uzmanları değil ve tahmin edilemez toobe hello subtleties ve kimlik doğrulama ve yetkilendirme son gelişmeleri hello. Ticari (örneğin Microsoft'tan) genellikle kapsamlı bir şekilde gözden güvenlik kodudur.
  - Çok faktörlü kimlik doğrulaması kullanın. Çok faktörlü kimlik doğrulaması hello geçerli olduğu kullanıcı adı ve parola kimlik doğrulaması türlerinde devralınmış hello güvenlik zayıf önler çünkü standart kimlik doğrulama ve yetkilendirme için. Erişim tooboth hello Azure Yönetimi (portal/uzak PowerShell) arabirimleri ve Hizmetleri karşılıklı toocustomer tasarlanması ve toouse yapılandırılmış [Azure çok faktörlü kimlik doğrulama (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - OAuth2 ve Kerberos gibi standart kimlik doğrulama protokolleri kullanır. Bu protokollerin gözden eş yaygın olmuştur ve büyük olasılıkla platform Kitaplıklarınızı kimlik doğrulaması ve yetkilendirme bir parçası olarak uygulanır.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, bir Azure PaaS dağıtımı güvenlik avantajlarından odaklanır. Ardından, PaaS web ve mobil çözümlerinin güvenliğini sağlamaya yönelik önerilen yöntemleri öğrenin. Azure App Service, Azure SQL Database ve Azure SQL Data Warehouse ile başlayacağız. Diğer Azure Hizmetleri için önerilen uygulamaları makalelerini kullanılabilir duruma geldiğinde bağlantılar listesi aşağıdaki hello sağlanacak:

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database ve Azure SQL veri ambarı](security-paas-applications-using-sql.md)
- Azure Storage
- Azure REDIS önbelleği
- Azure Service Bus
- Web uygulaması güvenlik duvarı

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
