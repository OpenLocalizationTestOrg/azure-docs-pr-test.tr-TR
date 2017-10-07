---
title: "aaaCreate ve BizTalk Services bir yedeğini geri | Microsoft Docs"
description: "BizTalk Services yedekleme ve geri yüklemeyi içerir. Bilgi nasıl toocreate bir yedeğini geri yükleyin ve ne yedeklenir belirleyin. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>BizTalk Services: Yedekleme ve Geri Yükleme

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services yedekleme ve geri yükleme özellikleri içerir. Bu konu, Klasik Azure portalı nasıl toobackup ve geri yükleme BizTalk kullanarak Hizmetleri hello açıklar.

BizTalk Services hello kullanarak da yedekleyebilirsiniz [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Karma bağlantılar, Edition hello bağımsız olarak yedeklenmiş değil. Karma bağlantılar yeniden oluşturmanız gerekir.


## <a name="before-you-begin"></a>Başlamadan önce
* Yedekleme ve geri yükleme tüm sürümleri için kullanılamayabilir. Bkz: [BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md).
* Merhaba Klasik Azure portalı kullanarak bir talep üzerine yedekleme oluşturmak veya zamanlanmış yedekleme oluşturmak. 
* Yedekleme içeriği geri yüklenen toohello aynı BizTalk hizmeti veya tooa olabilir yeni BizTalk hizmeti. toorestore hello aynı adı, BizTalk hizmeti varolan hello silinmelidir hello kullanarak BizTalk hizmeti ve hello adı kullanılabilir olması gerekir. BizTalk hizmeti sildikten sonra Merhaba aynı istedik daha uzun zaman alabilir adı toobe kullanılabilir. Merhaba bekleyemiyorsanız aynı toobe kullanılabilir olarak adlandırın ve ardından tooa geri yeni BizTalk hizmeti.
* BizTalk Services, geri yüklenen toohello olabilir aynı sürümü veya daha yüksek bir sürüme. BizTalk Services tooa geri zaman hello yedeğin alındığı, gelen alt sürümü desteklenmiyor.
  
    Örneğin, temel Edition olabilir hello kullanarak bir yedekleme toohello Premium Edition geri. Premium Edition olamaz hello kullanarak bir yedekleme toohello Standard Edition geri.
* Merhaba EDI denetim numaraları hello denetim numaraları toomaintain sürekliliği desteklenir. Merhaba son yedeklemeden sonra işlenen iletileri, bu yedekleme içeriğin geri yinelenen denetim numaraları neden olabilir.
* Bir toplu etkin iletileri varsa, hello toplu işlem **önce** bir yedekleme çalıştırılıyor. Bir yedekleme (gerekli veya zamanlanmış olarak) oluştururken, toplu iletiler hiçbir zaman saklanır. 
  
    **Bir yedekleme toplu etkin iletilerle alınmışsa, bu iletiler yedeklenmez ve bu nedenle kaybolur.**
* İsteğe bağlı: hello BizTalk Services Portalı'da, herhangi bir yönetim işlemini durdurun.

## <a name="create-a-backup"></a>Bir yedekleme oluşturun
Bir yedekleme herhangi bir zamanda alınabilir ve sizin tarafınızdan tamamen denetlenir. Bu bölümde hello Azure Klasik kullanarak hello adımları toocreate yedeklemeler listelenir portal dahil olmak üzere:

[İsteğe bağlı bir yedekleme](#backupnow)

[Yedeklemeyi zamanlama](#backupschedule)

#### <a name="backupnow"></a>İsteğe bağlı bir yedekleme
1. Hello Klasik Azure portalı, seçin **BizTalk Services**, ve ardından BizTalk toobackup istediğiniz hizmetleri seçin hello.
2. Merhaba, **Pano** sekmesine **yedekleme** hello sayfanın hello sonundaki.
3. Yedek bir ad girin. Örneğin *myBizTalkService*BU*tarih*.
4. Bir blob storage hesabı ve select hello onay işareti toostart hello yedeklemeyi seçin.

Hello Yedekleme tamamlandıktan sonra bir kapsayıcı girdiğiniz hello yedek adı ile Merhaba depolama hesabı oluşturulur. Bu kapsayıcı, BizTalk hizmeti yedekleme yapılandırmanızı içerir.

#### <a name="backupschedule"></a>Yedeklemeyi zamanlama
1. Hello Klasik Azure portalı, seçin **BizTalk Services**, select hello tooschedule hello yedekleme istediğiniz ve hello ardından BizTalk hizmeti adını **yapılandırma** sekmesi.
2. Set hello **yedekleme durumu** çok**otomatik**. 
3. Select hello **depolama hesabı** toostore yedekleme Merhaba, hello girin **sıklığı** toocreate hello yedeklemeleri ve ne kadar süreyle tookeep hello yedeklemeleri (**bekletme gün**):
   
    ![][AutomaticBU]
   
    **Notlar**     
   
   * İçinde **bekletme gün**, hello saklama dönemi hello yedekleme sıklığı büyük olmalıdır.
   * Seçin **her zaman en az bir yedekleme tutun**, hello saklama süresi olsa bile.
4. **Kaydet**’i seçin.

Zamanlanmış bir yedekleme işini çalıştırdığında, girdiğiniz hello depolama hesabında bir kapsayıcı (toostore yedekleme verilerini) oluşturur. Merhaba hello kapsayıcının adını adlandırılan *BizTalk hizmeti adı-tarih-saat*. 

Merhaba BizTalk hizmeti Pano gösterirse bir **başarısız** durumu:

![Zamanlanan son yedekleme durumu][BackupStatus] 

Merhaba bağlantı hello Yönetim Hizmetleri işlem günlükleri toohelp sorun giderme açar. Bkz: [BizTalk Services: işlem günlükleri kullanarak sorun giderme](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Geri Yükleme
Merhaba Klasik Azure portalı veya hello yedeklerini geri [geri BizTalk hizmeti REST API'si](http://go.microsoft.com/fwlink/p/?LinkID=325582). Bu bölümde hello Klasik portalı kullanarak hello adımları toorestore listelenir.

#### <a name="before-restoring-a-backup"></a>Bir yedeği geri yüklemeden önce
* Yeni izleme, arşivleme ve depoları izleme BizTalk hizmeti geri yüklenirken girilebilir.
* Merhaba aynı EDI çalışma zamanı verileri geri yüklenir. Merhaba EDI çalışma zamanı yedekleme hello denetim numaraları depolar. geri hello denetim hello yedekleme hello saati sırayla numaralarıdır. Merhaba son yedeklemeden sonra işlenen iletileri, bu yedekleme içeriğin geri yinelenen denetim numaraları neden olabilir.

#### <a name="restore-a-backup"></a>Yedeği geri yükleme
1. Hello Klasik Azure portalı, seçin **yeni** > **uygulama hizmetleri** > **BizTalk hizmeti** > **geri yükleme** :
   
    ![Yedeği geri yükleme][Restore]
2. İçinde **yedekleme URL**hello klasör simgesini seçin ve depoları BizTalk hizmeti yapılandırma yedeği hello hello Azure depolama hesabı'nı genişletin. Merhaba kapsayıcısını genişletin ve geri .txt dosyasının yedeğini karşılık gelen hello hello sağ bölmede seçin. 
   <br/><br/>
   Seçin **açık**.
3. Merhaba üzerinde **geri yükleme BizTalk hizmeti** want bir **BizTalk hizmeti adı** ve hello doğrulayın **etki alanı URL'si**, **Edition**ve **Bölge** hello BizTalk hizmeti geri için. **Yeni bir SQL veritabanı oluştur** veritabanı izleme hello için:
   
    ![][RestoreBizTalkService]
   
    Merhaba İleri okunu seçin.
4. Merhaba hello SQL veritabanı adını doğrulayın, bu sunucu için hello fiziksel sunucu hello SQL veritabanının oluşturulacağı ve bir kullanıcı adı/parola girin.

    Tooconfigure hello SQL veritabanı sürümü, boyutu ve diğer özellikleri istiyorsanız seçin **Gelişmiş veritabanı ayarlarını yapılandır**. 

    Merhaba İleri okunu seçin.

1. Yeni bir depolama hesabı oluşturun veya hello BizTalk hizmeti için mevcut bir depolama hesabını girin.
2. Merhaba onay işareti toostart hello geri seçin.

Merhaba geri yükleme başarıyla tamamlandıktan sonra yeni bir BizTalk hizmeti askıya alınmış durumda hello Klasik Azure Portalı'ndaki hello BizTalk Services sayfasında listelenir.

### <a name="postrestore"></a>Bir yedekleme geri yükledikten sonra
Merhaba BizTalk hizmeti her zaman içinde geri bir **askıya** durumu. Bu durumda, önce Hello yeni ortam işlevsel dahil olmak üzere yapılandırma değişiklikleri yapabilirsiniz:

* BizTalk hizmeti uygulamalarını hello Azure BizTalk Services SDK'sını kullanarak oluşturduysanız, bu uygulamaları toowork geri hello ortamıyla tootooupdate hello erişim denetimi (ACS) kimlik bilgileri gerekebilir.
* BizTalk hizmeti tooreplicate mevcut bir BizTalk hizmeti ortamına geri yükleyin. Bir kaynak FTP klasörü kullanmak hello özgün BizTalk Services Portalı'nda yapılandırılmış anlaşmaları varsa, bu durumda, yeni geri hello ortamı toouse farklı kaynak FTP klasörü tooupdate hello sözleşmelerde gerekebilir. Aksi takdirde olabilir toopull çalışırken iki farklı anlaşmaları hello aynı ileti.
* Birden çok BizTalk hizmeti ortamları toohave geri yüklediyseniz, hello Visual Studio uygulamaları, PowerShell cmdlet'leri, REST API'leri veya ticari ortak Yönetimi OM API'leri doğru ortamında hello hedef emin olun.
* İyi bir uygulama tooconfigure otomatik yedeklemeler yeni geri hello BizTalk hizmeti ortamda olur.

Merhaba Klasik Azure portalı select hello toostart hello BizTalk hizmeti geri BizTalk hizmeti ve select **Sürdür** hello görev çubuğunda. 

## <a name="what-gets-backed-up"></a>Ne yedeklenir
Bir yedek oluşturulduğunda hello aşağıdaki öğeleri yedeklenir:

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Yedeklenecek öğe</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Azure BizTalk Services portalı</strong></td>
</tr> 
<tr>
<td>Yapılandırma ve çalışma zamanı</td> 
<td>
<ul>
<li>İş ortakları ve profili ayrıntıları</li>
<li>Ortak sözleşmeleri</li>
<li>Dağıtılan özel derlemeler</li>
<li>Dağıtılan köprüleri</li>
<li>Sertifikalar</li>
<li>Dağıtılan dönüşümler</li>
<li>İşlem hatları</li>
<li>Oluşturulan ve hello BizTalk Services portalı kaydedilen şablonları</li>
<li>X12 ST01 ve GS01 eşlemeleri</li>
<li>Denetim numaraları (EDI)</li>
<li>AS2 ileti MIC değerleri</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Azure BizTalk hizmeti</strong></td>
</tr> 
<tr>
<td>SSL sertifikası</td> 
<td>
<ul>
<li>SSL sertifikası verileri</li>
<li>SSL sertifika parolası</li>
</ul>
</td>
</tr> 
<tr>
<td>BizTalk hizmeti ayarları</td> 
<td>
<ul>
<li>Ölçek birimi sayısı</li>
<li>Sürüm</li>
<li>Ürün sürümü:</li>
<li>Bölge/veri merkezi</li>
<li>Erişim denetimi Hizmeti'nden (ACS) ad alanı ve anahtarı</li>
<li>Veritabanı bağlantı dizesi izleme</li>
<li>Depolama hesabı bağlantı dizesi arşivleme</li>
<li>Depolama hesabı bağlantı dizesi izleme</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Ek öğeler</strong></td>
</tr> 
<tr>
<td>Veritabanı izleme</td> 
<td>Merhaba BizTalk hizmeti oluşturulduğunda, hello Azure SQL veritabanı sunucusu ve hello izleme veritabanı adı dahil olmak üzere hello izleme veritabanı ayrıntıları girilir. Merhaba izleme veritabanı otomatik olarak yedeklenmez.
<br/><br/>
<strong>Önemli</strong><br/>
Merhaba izleme veritabanı silinir ve kurtarılan veritabanının gereksinimlerine Merhaba, önceki bir yedekleme mevcut olması gerekir. Bir yedek yoksa, hello izleme veritabanı ve veri kurtarılabilir değildir. Bu durumda, yeni bir izleme veritabanı ile Merhaba oluşturmak aynı veritabanı adı. Coğrafi çoğaltma önerilir.</td>
</tr> 
</table>

## <a name="next"></a>Sonraki
toocreate Azure BizTalk Services hello Azure Klasik portal, Git çok[BizTalk Services: sağlama kullanarak Azure Klasik portalı](http://go.microsoft.com/fwlink/p/?LinkID=302280). uygulamaları, Git çok oluşturma toostart[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Ayrıca Bkz.
* [BizTalk hizmeti yedekleme](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [BizTalk hizmeti yedekten geri yükleyin](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services: Klasik portalı kullanarak Azure hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [BizTalk Services: Durum Grafiğini hazırlama](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [BizTalk Services: Azaltma](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [BizTalk Services: Verenin Adı ve Verenin Anahtarı](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

