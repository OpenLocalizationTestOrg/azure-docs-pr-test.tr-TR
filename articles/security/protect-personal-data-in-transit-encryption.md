---
title: "aaaProtect kişisel Aktarımdaki verileri şifreleme Azure ile | Microsoft Docs"
description: "Azure tooprotect kişisel verileri şifreleme kullanma"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Azure şifreleme teknolojilerini: şifrelemesi ile Aktarım kişisel verileri koruma

Bu makalede anlamak ve Azure şifreleme teknolojileri toosecure veri aktarım sırasında kullanmanıza yardımcı olur. 

Kişisel veri koruma hello gizliliğini hello ağ üzerinden geçen çok katmanlı savunma güvenlik stratejisinin önemli bir parçası aynıdır. Şifreleme Aktarımdaki tasarlanmış tooprevent engeller mümkün tooview veya kullanım hello veri aktarımları karşılar bir saldırgan ' dir.

## <a name="scenario"></a>Senaryo

Merhaba Amerika Birleşik Devletleri'nde yönetim büyük seyahat şirket, kendi işlemleri toooffer programlarıyla hello Akdeniz, Adriatic ve Baltık seas yanı sıra hello İngiliz Adaları arasında içinde genişletmektedir. toosupport bu çaba İtalya, dayanarak birkaç küçük seyahat satırları geçirmiş Almanya, Danimarka ve hello İngiltere 

Merhaba şirket hello bulutta Microsoft Azure toostore şirket verileri kullanır. Bu ad, adres, telefon numaraları gibi kişisel olarak tanımlanabilir bilgileri ve genel müşteri tabanı, kredi kartı bilgilerini içerir. Ayrıca tüm konumlarda adresleri, telefon numaralarını, vergi kimlik numaraları ve şirket çalışanlarının tıbbi bilgi gibi geleneksel İnsan Kaynakları bilgileri içerir. Merhaba seyahat satır Ayrıca, kişisel bilgi tootrack ilişkileri geçerli ve geçmiş müşterilerle içeren büyük bir veritabanını ödül ve bağlılık programı üyeleri korur.

Kişisel veriler müşterilerin hello veritabanında hello şirketin şubelere ve seyahat Merhaba Dünya bulunan aracılardan gelen girilir. Müşteri bilgilerini içeren belgeleri hello ağ tooAzure depolama aktarılır.

## <a name="problem-statement"></a>Sorun bildirimi

Merhaba şirket müşterilerin hello gizliliğini korumak gerekir ve çalışanların kişisel veriler, Azure hizmetlerinden geçiş tooand içinde.

## <a name="company-goal"></a>Şirket hedefi

Şirket hedef tooensure hello disk zaman devre dışı kişisel veriler şifrelenir. Yetkisiz kişilerin hello disk kapalı kişisel verilere müdahale okunamaz kılacak bir formda olması gerekir. Şifreleme uygulama kolay ya da kullanıcılar ve Yöneticiler için tamamen saydam olmalıdır.

## <a name="solutions"></a>Çözümler

Azure hizmetleri sağlayan birden çok Araçlar ve teknolojiler toohelp kişisel Aktarımdaki verileri korumak.

### <a name="azure-storage"></a>Azure Storage

Merhaba bulutta depolanan veriler toohello Azure veri merkezi, hello world fiziksel olarak herhangi bir yerde bulunabilir hello istemciden gitmeniz gerekir. Bu verileri kullanıcılar tarafından alındığında, onu yeniden hello geçen yönü ters. Aktarım sırasında veriler üzerinde hello genel Internet saldırganlar tarafından riskinin her zaman altındadır. Bu önemli tooprotect hello gizlilik kişisel veri aktarım düzeyinde şifreleme toosecure gibi konumlar arasında taşır kullanmaktır.

Merhaba HTTPS protokolünü hello Internet güvenli, şifrelenmiş iletişim kanalı sağlar. HTTPS, REST API'leri çağrılırken Azure Storage ve kullanılan tooaccess nesneleri olması gerekir. Kullanırken hello HTTPS protokolünü kullanılmasını zorunlu [paylaşılan erişim imzaları](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate erişim tooAzure depolama nesneleri. SAS iki tür vardır: hizmet SAS ve hesap SAS.

#### <a name="how-do-i-construct-a-service-sas"></a>Hizmet SAS nasıl oluşturmak?

Bir hizmet SAS temsilciler erişim tooa kaynak yalnızca bir hello depolama hizmetleri (blob, kuyruk, tablo veya dosya hizmeti). bir hizmet SAS tooconstruct hello aşağıdaki:

1. Merhaba imzalandı sürüm alanını belirtin

2. Merhaba imzalandı kaynak (Blob ve sadece dosya hizmeti) belirtin

3. Sorgu parametreleri tooOverride yanıt üstbilgilerini (Blob hizmeti ve sadece dosya hizmeti) belirtin

4. Merhaba (yalnızca tablo hizmeti) tablo adı belirtin

5. Merhaba erişim ilkesini belirtin

6. Merhaba imza geçerlilik aralığı belirtin

8. İzinleri belirtin

9. IP adresi veya IP aralığını belirtin

10. Merhaba HTTP protokolü belirtin

11. Tablo erişim aralıkları belirtin

12. Merhaba imzalandı tanımlayıcısını belirtin

13. Merhaba imza belirtin

Daha ayrıntılı yönergeler için bkz: [hizmet SAS oluşturma](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>Bir hesap SAS nasıl oluşturmak?

Bir hesap SAS bir veya daha fazla hello depolama hizmet erişim tooresources atar. Ayrıca, erişim tooread, yazma ve silme işlemleri blob kapsayıcılar, tablolar, kuyruklar ve hizmet SAS ile izin verilmiyor dosya paylaşımları üzerinde devredebilirsiniz. Bir hesap SAS yapımı hizmet SAS, benzer toothat ' dir. Ayrıntılı yönergeler için bkz: [bir hesap SAS oluşturma.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>HTTPS nasıl REST API'leri çağrılırken zorunlu?

REST API'leri tooaccess nesneleri depolama hesaplarında çağrılırken HTTPS tooenforce hello kullanımı, hello depolama hesabı için güvenli aktarım gerekli etkinleştirebilirsiniz. 

1. Hello Azure portal, seçin **depolama hesabı oluştur**, veya mevcut bir depolama hesabını seçin **ayarları** ve ardından **yapılandırma**.

2. Altında **güvenli aktarım gerekli**seçin **etkin**.

![Bir depolama hesabı oluşturma](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Daha ayrıntılı yönergeler için de dahil olmak üzere tooenable güvenli aktarım gerekli programlı olarak bkz nasıl [gerektiren güvenli aktarım](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Nasıl Azure dosya depolama birimindeki verileri şifreliyor mu?

Aktarım ile tooencrypt verileri [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), SMB kullanabilirsiniz 3.x Windows 8, 8.1 ve 10 ve Windows Server 2012 R2 ve Windows Server 2016 ile. Hello Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur. Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve bazı özellikleri hello Linux SMB istemcisi kullanarak senaryolar içerir.

#### <a name="azure-client-side-encryption"></a>Azure istemci tarafı şifreleme

Bir istemci uygulaması ve Azure Storage arasında aktarıldığı sırada kişisel verileri korumak için başka bir seçenek [istemci tarafı şifreleme](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Azure depolama alanına aktarılmadan önce Hello veri şifrelenir ve Azure depolama biriminden hello veri aldığınızda hello istemci tarafında alındıktan sonra hello veri şifresi çözülür.

### <a name="azure-site-to-site-vpn"></a>Azure siteden siteye VPN

Etkili şekilde bir tooprotect kişisel verileri şirket ağı veya kullanıcı ve hello Azure sanal ağı arasında aktarımda toouse olan bir [siteden siteye](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) veya [noktası site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) sanal özel ağ (VPN). Bir VPN bağlantısı hello Internet şifrelenmiş güvenli bir tünel oluşturur.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Siteden siteye VPN bağlantısı nasıl oluşturulur?

Siteden siteye VPN hello şirket ağı tooAzure birden fazla kullanıcı bağlanır. toocreate hello Azure portal'ın bir siteden siteye bağlantı hello aşağıdaki:

1. Bir sanal ağ oluşturun.

2. Bir DNS sunucusu belirtin.

3. Merhaba ağ geçidi alt ağı oluşturun.

4. Merhaba VPN ağ geçidi oluşturun. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Merhaba yerel ağ geçidi oluşturun.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. VPN Cihazınızı yapılandırın.

7. Merhaba VPN bağlantısı oluşturun.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Merhaba VPN bağlantısını doğrulayın.

Daha fazla hakkında ayrıntılı yönergeler için nasıl toocreate bir site siteye bağlantı hello Azure portal, bkz: [Create bir Site siteye bağlantı hello Azure Portal'ın.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Bir noktadan siteye VPN bağlantısı nasıl oluşturulur?

Bir noktadan siteye VPN bir tek bir istemci bilgisayar tooa sanal ağdan güvenli bir bağlantı oluşturur. Uzak bir konumdan tooconnect tooAzure gibi giriş veya bir otel veya konferans Merkezi'nden istediğinizde kullanışlıdır. bir noktadan siteye bağlantı hello Azure portal'ın toocreate,

1. Bir sanal ağ oluşturun.

2. Bir ağ geçidi alt ağı ekleyin.

3. Bir DNS sunucusu belirtin. (isteğe bağlı)

4. Bir sanal ağ geçidi oluşturun.

5. Sertifikaları oluşturur.

6. Merhaba istemcisi adres havuzunu ekleyin.

7. Merhaba kök sertifika ortak sertifikası verileri karşıya yükleyin.

8. Oluştur ve hello VPN istemcisi yapılandırma paketini yükleyin.

9. Dışarı aktarılan istemci sertifikası yükleyin.

10. TooAzure bağlanın.

11. Bağlantınızı doğrulayın.

Daha ayrıntılı yönergeler için bkz: [bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Microsoft, her zaman farklı konumlar arasında SSL/TLS protokolleri tooexchange veri kullanmanızı önerir. Toouse seçin kuruluşlar [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove büyük veri kümeleri ayrılmış bir yüksek hızlı WAN bağlantısı üzerinden de hello SSL/TLS veya diğer protokoller için ek koruma kullanarak uygulama düzeyi hello verileri şifrelemek.

### <a name="encryption-by-default"></a>Varsayılan şifreleme

Microsoft, müşteriler ve Azure bulut hizmetleri arasında aktarımda şifreleme tooprotect verileri kullanır. Hello Azure portalı Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur.

[Aktarım Katmanı Güvenliği](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) protokolüdür Microsoft veri merkezleri toonegotiate tooMicrosoft bulut hizmetlerine bağlanacak istemci sistemleriyle çalışacak hello. TLS, güçlü kimlik doğrulaması, ileti gizliliği ve bütünlük (ileti oynama, kişiler tarafından ele ve sahtekarlığı saptama etkinleştirir), birlikte çalışabilirlik, algoritma esnekliği, dağıtım ve kullanım kolaylığı sağlar.

[Kusursuz iletme gizliliği](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) de işe benzersiz anahtarlar böylece müşterilerin istemci sistemleri ve Microsoft'un bulut hizmetleri arasında her bağlantı kullanır. Bağlantıları tooMicrosoft bulut hizmetleri de dayalı RSA 2.048 bit şifreleme anahtar uzunluklarını yararlanın. Merhaba TLS, RSA 2.048 bit anahtar uzunluğu, birleşimi ve PFS kılar çok daha zor birisi için Microsoft bulut hizmetlerine ve müşterileri arasında aktarımda toointercept ve erişim veriler.

Aktarımdaki verileri [Data Lake Store'da] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview) her zaman şifrelenir. Ayrıca tooencrypting veri önceki toostoring toopersistent medya hello veri ayrıca her zaman aktarım sırasında HTTPS kullanılarak korunmaktadır. HTTPS için Data Lake Store REST arabirimleri hello desteklenir hello tek protokoldür.

## <a name="summary"></a>Özet

Merhaba şirket HTTPS bağlantıları tooAzure depolama zorlama, paylaşılan erişim imzaları kullanarak ve güvenli aktarım gerekli hello depolama hesaplarında etkinleştirme kişisel veri ve hello gizlilik bu tür veri korumanın amacı gerçekleştirebilirsiniz. Bunlar aynı zamanda kişisel verileri SMB 3.0 bağlantıları kullanarak ve istemci tarafı şifreleme uygulama koruyabilirsiniz. Siteden siteye VPN bağlantılarından şirket ağı toohello Azure sanal ağı hello ve bireysel kullanıcılardan noktadan siteye VPN bağlantıları üzerinden güvenli bir şekilde kişisel veriler seyahat güvenli bir tünel oluşturur. Microsoft'un varsayılan şifreleme yöntemler kişisel verilerin hello gizliliği daha fazla koruma sağlar.

## <a name="next-steps"></a>Sonraki adımlar

- [Azure veri güvenliği ve şifreleme en iyi uygulamalar](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [VPN Gateway için planlama ve tasarım](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [VPN Gateway ile ilgili SSS](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Satın alma ve Azure uygulama hizmetiniz için bir SSL sertifikası yapılandırma](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
