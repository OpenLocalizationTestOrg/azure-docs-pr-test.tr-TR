---
title: "aaaLearn hakkında en son Azure konuk işletim sistemi sürümleri hello | Microsoft Docs"
description: "Merhaba en son sürüm Haberler ve SDK uyumluluk Azure bulut Hizmetleri konuk işletim sistemi için."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 6306cafe-1153-44c7-8554-623b03d59a34
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 8/24/2017
ms.author: raiye
ms.openlocfilehash: 7274f5a68a32ce91bdede77e1443cdb8053c07ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-releases-and-sdk-compatibility-matrix"></a>Azure konuk işletim sistemi sürümleri ve SDK uyumluluk matrisi
Bulut Hizmetleri için en son Azure konuk işletim sistemi sürümleri hello hakkında güncel bilgi sağlar. Bu bilgiler, bir konuk işletim sistemi devre dışı önce yükseltme yolunuza planlamanıza yardımcı olur. Rolleri toouse yapılandırırsanız *otomatik* konuk işletim sistemi güncelleştirmeleri açıklandığı gibi [Azure konuk işletim sistemi güncelleştirme ayarları][Azure Guest OS Update Settings], bu sayfayı okuyun önemli değildir.

> [!IMPORTANT]
> Bu sayfa bir konuk işletim sistemi üzerinde çalışan tooCloud Hizmetleri web ve çalışan rolleri, uygulanır. Mevcut **geçerli** tooIaaS sanal makineler.
>
>


> [!NOTE]
> Merhaba RSS akışı son kullanımdan kaldırılmıştır. İzleme yakında yeni bir akış güncelleştirmeleri!
>
>

Konuk işletim sistemi ya da nasıl hello hangi hello değilseniz konuk işletim sistemi iş Yayımları? Okuma [bu](#how-it-works) bölümü.

## <a name="news-updates"></a>Haber güncelleştirmeleri

###### <a name="august-24-2017"></a>**24 Ağustos 2017**
Ağustos konuk işletim sistemi yayımladı.

###### <a name="august-3-2017"></a>**3 Ağustos 2017**
Temmuz konuk işletim sistemi yayımladı.

###### <a name="july-19-2017"></a>**19 Temmuz 2017**
Temmuz konuk işletim sistemi dağıtımı Temmuz 19 başlatıyor ve 8 Ağustos tahmini sürümü vardır.

###### <a name="july-7-2017"></a>**7 Temmuz 2017**
Haziran konuk işletim sistemi yayımladı.

###### <a name="june-16-2017"></a>**16 Haziran 2017**
Haziran konuk işletim sistemi dağıtımı Haziran 16 başlatıyor ve 11 Temmuz tahmini sürümü vardır.

###### <a name="june-5-2017"></a>**5 Haziran 2017**
Konuk işletim sistemi serbest bıraktı.

###### <a name="may-17-2017"></a>**17 May 2017**
Tooa güvenlik hata, biz aralık 2016 ve Ocak 2017 aşağıdaki hello devre dışı hello sahip olmayan bir işletim sistemi sürümleri [düzeltme] hello portalından: WA-KONUK-OS-5.4_201612-01, WA-KONUK-OS-4.39_201612-01, WA-KONUK-OS-3.46_ 201612-01, WA-GUEST-OS-2.59_201701-01

###### <a name="may-12-2017"></a>**12 May 2017**
Mayıs konuk işletim sistemi dağıtımı 12 Mayıs başlatıyor ve 13 Haziran tahmini sürümü vardır.

###### <a name="april-18-2017"></a>**18 Nisan 2017**
Nisan konuk işletim sistemi dağıtımı 18 Nisan başlatıyor ve May 9 Tahmini sürümü vardır.

###### <a name="april-10-2017"></a>**10 Nisan 2017**
Mart konuk işletim sistemi dağıtımı 14 Mart 2017 başlatıldı ve 10 Nisan 2017 yayımlandı.

###### <a name="january-10-2017"></a>**10 Ocak 2017**
Merhaba Ocak konuk işletim sistemi yalnızca işletim sistemi ailesi 2 (Windows 2008 Server R2) etkileyen düzeltme eklerini içerir. Bu nedenle yalnızca hello işletim sistemi ailesi 2 görüntü yayımlandı (WA-GUEST-OS-2.59_201701-01) bu ay için. Diğer tüm işletim sistemi ailesi için aralık OS hello (201612 - 01) kalan son hello.


## <a name="releases"></a>Sürümleri
## <a name="family-5-releases"></a>Aile 5 sürümleri
**Windows Server 2016**

.NET framework yüklü: 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2

> [!NOTE]
> İle tarihleri bir * konu toochange şunlardır.
>
> Merhaba işletim sistemi ailesi 5 için RDP parola en az 10 karakter uzunluğunda olmalıdır.
>

| Yapılandırma dizesi | Sürüm tarihi | Tarih devre dışı bırak | Süresi dolmuş tarih |
| --- | --- | --- | --- |
| WA-GUEST-OS-5.10_201708-01 |24 Ağustos 2017 |POST 5.12 |TBD |
| WA-GUEST-OS-5.9_201707-01 |3 Ağustos 2017 |POST 5.11 |TBD |
| WA-GUEST-OS-5.8_201706-01 |7 Temmuz 2017 |POST 5.10 |TBD |
|~~WA-GUEST-OS-5.7_201705-01~~ |5 Haziran 2017 |24 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-5.6_201704-01~~ |9 May 2017 |3 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-5.5_201703-01~~ |10 Nisan 2017 |7 Temmuz 2017 |TBD |
|~~WA-GUEST-OS-5.4_201612-01~~ |10 Ocak 2017 |5 Haziran 2017|TBD |
|~~WA-GUEST-OS-5.3_201611-01~~ |14 Aralık 2016 |9 May 2017 |TBD |
|~~WA-GUEST-OS-5.2_201610-02~~ |1 Kasım 2016 |10 Nisan 2017 |TBD |

## <a name="family-4-releases"></a>Aile 4 serbest bırakır
**Windows Server 2012 R2**

.NET 4.0, 4.5, 4.5.1, 4.5.2 destekler

> [!NOTE]
> İle tarihleri bir * konu toochange olan
>
>

| Yapılandırma dizesi | Sürüm tarihi | Tarih devre dışı bırak | Süresi dolmuş tarih |
| --- | --- | --- | --- |
| WA-GUEST-OS-4.45_201708-01 |24 Ağustos 2017 |POST 4.47 |TBD |
| WA-GUEST-OS-4.44_201707-01 |3 Ağustos 2017 |POST 4.46 |TBD |
| WA-GUEST-OS-4.43_201706-01 |7 Temmuz 2017 |POST 4,45 |TBD |
|~~WA-GUEST-OS-4.42_201705-01~~ |5 Haziran 2017 |24 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-4.41_201704-01~~ |9 May 2017 |3 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-4.40_201703-01~~ |10 Nisan 2017 |7 Temmuz 2017 |TBD |
|~~WA-GUEST-OS-4.39_201612-01~~ |10 Ocak 2017 |5 Haziran 2017 |TBD |
|~~WA-GUEST-OS-4.38_201611-01~~ |14 Aralık 2016 |9 May 2017 |TBD |
|~~WA-GUEST-OS-4.37_201610-02~~ |16 Kasım 2016 |10 Nisan 2017 |TBD |
|~~WA-GUEST-OS-4.36_201609-01~~ |13 Ekim 2016 |14 Ocak 2017 |TBD |
|~~WA-GUEST-OS-4.35_201608-01~~ |13 Eylül 2016 |16 Aralık 2016 |TBD |
|~~WA-GUEST-OS-4.34_201607-01~~ |8 Ağustos, 2016 |13 Kasım 2016 |TBD |


## <a name="family-3-releases"></a>Aile 3 serbest bırakır
**Windows Server 2012**

.NET 4.0, 4.5, 4.5.1, 4.5.2 destekler

> [!NOTE]
> İle tarihleri bir * konu toochange olan
>
>

| Yapılandırma dizesi | Sürüm tarihi | Tarih devre dışı bırak | Süresi dolmuş tarih |
| --- | --- | --- | --- |
| WA-GUEST-OS-3.52_201708-01 |24 Ağustos 2017 |POST 3.54 |TBD |
| WA-GUEST-OS-3.51_201707-01 |3 Ağustos 2017 |POST 3.53 |TBD |
| WA-GUEST-OS-3.50_201706-01 |7 Temmuz 2017 |POST 3.52 |TBD |
|~~WA-GUEST-OS-3.49_201705-01~~ |5 Haziran 2017 |24 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-3.48_201704-01~~ |9 May 2017 |3 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-3.47_201703-01~~ |10 Nisan 2017 |7 Temmuz 2017 |TBD |
|~~WA-GUEST-OS-3.46_201612-01~~ |10 Ocak 2017 |5 Haziran 2017 |TBD |
|~~WA-GUEST-OS-3.45_201611-01~~ |14 Aralık 2016 |9 May 2017 |TBD |
|~~WA-GUEST-OS-3.44_201610-02~~ |16 Kasım 2016 |1 Mayıs 2017 |TBD |
|~~WA-GUEST-OS-3.43_201609-01~~ |13 Ekim 2016 |14 Ocak 2017 |TBD |
|~~WA-GUEST-OS-3.42_201608-01~~ |13 Eylül 2016 |16 Aralık 2016 |TBD |
|~~WA-GUEST-OS-3.41_201607-01~~ |8 Ağustos, 2016 |13 Kasım 2016 |TBD |


## <a name="family-2-releases"></a>Ailesi 2 sürümleri
**Windows Server 2008 R2 SP1**

.NET 3.5, 4.0, 4.5, 4.5.1, 4.5.2 destekler

> [!NOTE]
> İle tarihleri bir * konu toochange olan
>
>

| Yapılandırma dizesi | Sürüm tarihi | Tarih devre dışı bırak | Süresi dolmuş tarih |
| --- | --- | --- | --- |
| WA-GUEST-OS-2.65_201708-01 |24 Ağustos 2017 |POST 2.67 |TBD |
| WA-GUEST-OS-2.64_201707-01 |3 Ağustos 2017 |POST 2.66 |TBD |
| WA-GUEST-OS-2.63_201706-01 |7 Temmuz 2017 |POST 2.65 |TBD |
|~~WA-GUEST-OS-2.62_201705-01~~ |5 Haziran 2017 |24 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-2.61_201704-01~~ |9 May 2017 |3 Ağustos 2017 |TBD |
|~~WA-GUEST-OS-2.60_201703-01~~ |10 Nisan 2017 |7 Temmuz 2017 |TBD |
|~~WA-GUEST-OS-2.59_201701-01~~ |10 Ocak 2017 |5 Haziran 2017 |TBD |
|~~WA-GUEST-OS-2.58_201612-01~~ |10 Ocak 2017 |9 May 2017|TBD |
|~~WA-GUEST-OS-2.57_201611-01~~ |14 Aralık 2016 |10 Nisan 2017 |TBD |
|~~WA-GUEST-OS-2.56_201610-02~~ |16 Kasım 2016 |10 Şubat 2017 |TBD |
|~~WA-GUEST-OS-2.55_201609-01~~ |13 Ekim 2016 |14 Ocak 2017 |TBD |
|~~WA-GUEST-OS-2.54_201608-01~~ |13 Eylül 2016 |16 Aralık 2016 |TBD |
|~~WA-GUEST-OS-2.53_201607-01~~ |8 Ağustos, 2016 |13 Kasım 2016 |TBD |



## <a name="msrc-patch-updates"></a>MSRC düzeltme eki güncelleştirmeleri
Merhaba her aylık konuk işletim sistemi sürüm ile birlikte gelen düzeltme eklerinin listesini kullanılabilir [burada][patches].

## <a name="sdk-support"></a>SDK'sı desteği
Rağmen hello [hello Azure SDK'sı için devre dışı bırakma İlkesi] [ retire policy sdk] 2.2 yukarıda sürümleri yalnızca desteklenen, belirli konuk işletim sistemi aileleri, toouse izin gösterir önceki sürümleri. Merhaba daima en son desteklenen SDK.

| Konuk işletim sistemi ailesi | Uyumlu SDK sürümleri |
| --- | --- |
| 5 |Sürüm 2.9.5.1+ |
| 4 |Sürüm 2.1 + |
| 3 |Sürüm 1,8 + |
| 2 |Sürüm 1.3 + |
| 1 |Sürüm 1.0 + |

## <a name="guest-os-release-information"></a>Konuk işletim sistemi sürüm bilgileri
TooGuest işletim sistemi sürümleri önemli olan üç tarihleri vardır: **yayın** tarih, **devre dışı** tarihi ve **sona erme** tarih. Merhaba Portal olduğunda ve konuk işletim sistemi hello hedefi olarak seçilen bir konuk işletim sistemi kullanılabilir olarak kabul edilir. Bir konuk işletim sistemi hello ulaştığında **devre dışı** tarih, Azure'dan kaldırılır. Ancak, bu konuk işletim sistemi hedefleme herhangi bir bulut hizmeti hala normal olarak çalışır.

Merhaba penceresinde hello arasında **devre dışı** tarih ve hello **sona erme** tarihi daha yeni bir konuk işletim sistemi tooone bir arabellek tooeasily geçiş ile sağlar. Kullanıyorsanız, *otomatik* , konuk işletim sistemi hello son sürümü her zaman olacaktır ve zaman aşımına uğramak ilgili tooworry yok.

Ne zaman hello **sona erme** geçişleri, o konuk işletim sistemi kullanmaya devam durdurulacak, herhangi bir bulut hizmeti silindi veya zorlanan tooupgrade tarih. Daha fazla bilgiyi hello kullanımdan kaldırma ilkesiyle ilgili [burada][retirepolicy].

## <a name="guest-os-family-version-explanation"></a>Konuk işletim sistemi ailesi sürümlü açıklama
Merhaba konuk işletim sistemi aileleri yayımlanan Microsoft Windows Server sürümlerinde temel alır. Merhaba konuk işletim sistemi hello temel işletim Azure Cloud Services üzerinde çalışan sistemidir. Her konuk işletim sistemi ailesi, sürüm ve sürüm olan sayı.

* **Konuk işletim sistemi ailesi**  
  Bir Windows Server işletim sistemi sürüm konuk işletim sistemi dayanır. Örneğin, *aile 3* Windows Server 2012'de temel alır.
* **Konuk işletim sistemi sürümü**  
  Belirli tooa konuk işletim sistemi ailesi artı ilgili görüntü [Microsoft Güvenlik Yanıt Merkezi (MSRC)] [ msrc] hello tarih hello yeni konuk işletim sistemi sürümünde kullanılabilir düzeltme ekleri oluşturulur. Tüm düzeltme eklerini dahil edilebilir.

    Sayı 0'da başlatın ve güncelleştirmeleri yeni bir dizi eklenen her zaman 1 ile artırın. Sondaki sıfırlar yalnızca gösterilen önemli değilse. Diğer bir deyişle, 2.10 sürüm 2.1 farklı, daha sonraki bir sürümden sürümüdür.
* **Konuk işletim sistemi sürümü**  
  Bir konuk işletim sistemi sürümü sürümündeki. Microsoft Test sırasında sorunları bulursa bir yeniden yayımlama oluşur; değişiklikleri gerektirir. Merhaba en son sürümü her zaman herhangi önceki yerini alır, veya ortak serbest bırakır. Hello Azure portal toopick hello en son sürüm, belirli bir sürümü için kullanıcılar yalnızca izin verecektir. Dağıtımları önceki bir sürümü çalıştıran genellikle hello hata hello önem derecesine bağlı olarak yükseltme zorla değildir.

Merhaba aşağıdaki örnekte, 2 hello ailesi, 12 hello sürümüdür ve "rel2" Merhaba sürüm.

**Konuk işletim sistemi sürüm** - 2,12 rel2

**Bu sürüm için yapılandırma dizesi** -WA-GUEST-OS-2.12_201208-02

Hello yapılandırma dizesi konuk işletim sistemi için bu sürüm için hangi MSRC düzeltme ekleri olarak kabul gösteren bir tarih ile birlikte katıştırılmış aynı bilgiler içeriyor. Bu örnekte, Ağustos 2012 dahil olmak üzere tooand için Windows Server 2008 R2 üretilen MSRC düzeltme ekleri için içerme ele alındı. Yalnızca Windows Server sürümünü toothat özellikle uygulama düzeltme ekleri dahil edilir. MSRC düzeltme eki tooMicrosoft Office geçerliyse, bu ürünü hello Windows Server temel görüntü parçası olmadığından Örneğin, bunu dahil edilmez.

## <a name="guest-os-system-update-process"></a>Konuk işletim sistemi sistem güncelleştirme işlemi
Bu sayfa yakında konuk işletim sistemi sürümleri hakkında bilgi içerir. Müşteriler, "Otomatik" çok güncelleştirme ayarlarsanız bulut hizmeti rollerinin yeniden çünkü bir sürüm olduğunda bunlar tooknow istediğinizi belirttiniz. Konuk işletim sistemi sürümleri genellikle en az beş (5) hello MSRC güncelleştirdikten sonra her ayın ikinci Salı hello üzerinde oluşan sürüm günde bir yapılır. Yeni sürümler tüm hello ilgili MSRC düzeltme eklerinin her konuk işletim sistemi ailesi için içerir.

Microsoft Azure sürekli güncelleştirmeleri yayımladı. Merhaba konuk işletim sistemi yalnızca bir tür hello ardışık düzeninde güncelleştirmesidir. Bir yayın birçok faktörler tarafından etkilenebilir burada çok fazla sayıda toolist. Ayrıca, Azure tam anlamıyla yüz binlerce makineler üzerinde çalışır. Bu tam tarihi ve saati, rollere ne zaman yeniden imkansız toogive olduğu anlamına gelir. Biz planı toolimit üzerinde çalıştığınız veya yeniden başlatma zaman.

Konuk işletim sistemi yayımlanan hello yeni bir sürüm olduğunda, toofully yayılması Azure arasında zaman alabilir. Hizmetleri güncelleştirilmiş toohello gibi yeni konuk işletim sistemi, oldukları yeniden başlatılan uygularken güncelleştirme etki alanları. Bir yayın Hizmetleri kümesi toouse "Otomatik" güncelleştirmeleri ilk alırsınız. Merhaba güncelleştirmeden sonra hello yeni konuk işletim sistemi sürümü hizmetinizi hello için Azure portal listelenen görürsünüz. Yeniden yayımlama, bu süre zarfında ortaya çıkabilir. Bazı sürümler uzun süreler boyunca dağıtılabilir ve Otomatik yükseltme yeniden başlatmalar için birçok hafta sonra hello resmi yayın tarihi gerçekleşmeyebilir. Bir konuk işletim sistemi kullanılabilir olduğunda, daha sonra açıkça sürümünün hello portalından veya yapılandırma dosyanızda seçebilirsiniz.

Post başlıklı hello MSDN blog yeniden başlatılır ve işaretçileri toomore bilgi teknik ayrıntıları Konuk ve ana bilgisayar işletim sistemi güncelleştirmelerinin değerli bilgiler içeren büyük bir bölümünü bakın [rol örneği yeniden son tooOS yükseltmeler] [ restarts].

Konuk işletim sistemi el ile güncelleştirirseniz hello bkz [konuk işletim sistemi devre dışı bırakma İlkesi] [ retirepolicy] ek bilgi için.

## <a name="guest-os-supportability-and-retirement-policy"></a>Konuk işletim sistemi desteklenebilirlik ve kullanımdan kaldırma İlkesi
Merhaba konuk işletim sistemi desteklenebilirlik ve kullanımdan kaldırma İlkesi açıklanmıştır [burada][retirepolicy].

[Install .NET on a Cloud Service Role]: https://azure.microsoft.com/en-us/documentation/articles/cloud-services-dotnet-install-dotnet/?WT.mc_id=azurebg_email_Trans_963_RevisedNET_Update
[Azure Guest OS Update Settings]: cloud-services-how-to-configure.md
[ssl3 announcement]: http://azure.microsoft.com/blog/2014/12/09/azure-security-ssl-3-0-update/
[Microsoft Security Advisory 3009008]: https://technet.microsoft.com/library/security/3009008.aspx
[ssl3-fixit]: http://go.microsoft.com/?linkid=9863266
[MS14-066]: https://technet.microsoft.com/library/security/ms14-066.aspx
[MS14-046]: https://technet.microsoft.com/library/security/ms14-046.aspx
[retire policy sdk]: https://msdn.microsoft.com/library/dn479282.aspx
[server and gos]: https://msdn.microsoft.com/library/dn775043.aspx
[azuresupport]: http://azure.microsoft.com/support/options/
[net install pkg]: http://www.microsoft.com/download/details.aspx?id=42643
[msrc]: http://www.microsoft.com/security/msrc/default.aspx
[update guest os portal]: https://msdn.microsoft.com/library/gg433101.aspx
[update guest os svc]: https://msdn.microsoft.com/library/gg456324.aspx
[restarts]: http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx
[patches]: cloud-services-guestos-msrc-releases.md
[retirepolicy]: cloud-services-guestos-retirement-policy.md
[fam1retire]: cloud-services-guestos-family1-retirement.md
[düzeltme]: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
