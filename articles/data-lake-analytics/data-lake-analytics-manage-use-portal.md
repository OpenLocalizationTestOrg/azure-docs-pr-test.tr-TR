---
title: Azure portal kullanarak Azure Data Lake Analytics aaaManage hello | Microsoft Docs
description: "Bilgi nasıl toomanage Data Lake Analytics sayılarının, veri kaynakları, kullanıcılar ve işler."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak Azure Data Lake Analytics'i yönetme
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Azure portal toomanage Azure Data Lake Analytics hesapları, hesap veri kaynakları, kullanıcılar ve kullanarak işleri nasıl hello öğrenin. diğer araçları kullanarak hakkında toosee yönetimi konuları hello sayfanın üst kısmındaki hello bir sekmesini tıklatın.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Data Lake Analytics hesaplarını yönetme

### <a name="create-an-account"></a>Bir hesap oluşturun

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **Yeni** > **Zeka + analiz** > **Data Lake Analytics**'e tıklayın.
3. Aşağıdaki öğelerindeki hello için değerleri seçin: 
   1. **Ad**: hello Data Lake Analytics hesabı hello adı.
   2. **Abonelik**: hello hesabı için kullanılan Azure aboneliği hello.
   3. **Kaynak grubu**: hello Azure kaynak grubu toocreate hello hesap. 
   4. **Konum**: hello Data Lake Analytics hesabı için Azure veri merkezi hello. 
   5. **Data Lake Store**: hello Data Lake Analytics hesabı için kullanılan varsayılan deposu toobe hello. Hello Azure Data Lake Store hesabı ve hello Data Lake Analytics hesabı olmalıdır aynı konuma hello.
4. **Oluştur**'a tıklayın. 

### <a name="delete-a-data-lake-analytics-account"></a>Bir Data Lake Analytics hesabı silme

Bir Data Lake Analytics hesabı silmeden önce varsayılan Data Lake Store hesabını silin.

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Sil**'e tıklayın.
3. Tür hello hesap adı.
4. **Sil**'e tıklayın.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Veri kaynaklarını yönet

Data Lake Analytics veri kaynakları aşağıdaki hello destekler:

* Data Lake Store
* Azure Storage

Veri Gezgini toobrowse veri kaynakları ve temel dosya yönetimi işlemleri kullanabilirsiniz. 

### <a name="add-a-data-source"></a>Veri kaynağı ekleme

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. Tıklatın **veri kaynakları**.
3. Tıklatın **veri kaynağı ekleme**.
    
   * tooadd bir Data Lake Store hesabı, gereksinim duyduğunuz hello hesap adı ve erişim toohello hesap toobe mümkün tooquery onu.
   * Azure Blob Depolama tooadd hello depolama hesabı ve hello hesap anahtarı gerekir. toofind hello Portal'da bunları, Git toohello depolama hesabı.

## <a name="set-up-firewall-rules"></a>Güvenlik duvarı kuralları ayarlamak

Data Lake Analytics toofurther erişim tooyour Data Lake Analytics hesabı kilitleme hello ağ düzeyinde kullanabilirsiniz. Bir güvenlik duvarını etkinleştir, bir IP adresi belirtin veya güvenilen istemcileriniz için bir IP adresi aralığı tanımlayın. Bu ölçüleri etkinleştirdikten sonra tanımlanan hello aralıkta hello IP adresine sahip yalnızca istemcileri toohello deposu bağlanabilir.

Azure Data Factory veya VM gibi diğer Azure hizmetleriyle toohello Data Lake Analytics hesabı bağlanıyorsanız, emin olun **izin Azure Hizmetleri** açık **üzerinde**. 

### <a name="set-up-a-firewall-rule"></a>Bir güvenlik duvarı kuralı ayarlamak

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. Merhaba hello soldaki menüsünde **Güvenlik Duvarı**.

## <a name="add-a-new-user"></a>Yeni kullanıcı ekleme

Merhaba kullanabilirsiniz **Kullanıcı Ekleme Sihirbazı** tooeasily yeni Data Lake kullanıcı sağlama.

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. Sol, altında hello üzerinde **Başlarken**, tıklatın **Kullanıcı Ekleme Sihirbazı**.
3. Bir kullanıcı seçin ve ardından **seçin**.
4. Bir rol seçin ve ardından **seçin**. Yeni bir geliştirici toouse Azure Data Lake, select hello yukarı tooset **Data Lake Analytics Geliştirici** rol.
5. Merhaba U-SQL veritabanları için Hello erişim denetim listelerini (ACL'ler) seçin. Seçimlerinizi yaptıktan sonra tıklatın **seçin**.
6. Merhaba ACL'ler dosyaları için seçin. Merhaba varsayılan deposu için hello kök klasör için hello ACL'ler değişmez "/" ve hello/sistem klasörü için. **Seç**'e tıklayın.
7. Tüm seçili değişikliklerinizi gözden geçirin ve ardından **çalıştırmak**.
8. Merhaba sihirbaz tamamlandığında tıklatın **Bitti**.

## <a name="manage-role-based-access-control"></a>Rol tabanlı erişim denetimini yönetmek

Diğer Azure hizmetleriyle gibi hello hizmeti ile kullanıcıların nasıl etkileşim rol tabanlı erişim denetimi (RBAC) toocontrol kullanabilirsiniz.

Hello standart RBAC rolleri, özellikleri aşağıdaki hello sahiptir:
* **Sahibi**: iş göndermek, izleyebilir işleri, herhangi bir kullanıcı işlerini iptal edin ve hello hesabı yapılandırın.
* **Katkıda bulunan**: iş göndermek, izleyebilir işleri, herhangi bir kullanıcı işlerini iptal edin ve hello hesabı yapılandırın.
* **Okuyucu**: işleri izleyebilirsiniz.

Merhaba Data Lake Analytics geliştirici, rol, tooenable, U-SQL, geliştiriciler, toouse, Merhaba, Data Lake Analytics, hizmeti kullanın. Merhaba Data Lake Analytics Geliştirici rolüne kullanabilirsiniz:
* İşlerini gönderin.
* Herhangi bir kullanıcı tarafından gönderilen işlerin iş durumunu ve hello ilerleme izleyin.
* Merhaba U-SQL betikleri herhangi bir kullanıcı tarafından gönderilen işlerine bakın.
* Yalnızca kendi işlerini iptal edin.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Kullanıcı veya güvenlik grupları tooa Data Lake Analytics hesabı ekleme

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. Tıklatın **erişim denetimi (IAM)** > **Ekle**.
3. Bir rol seçin.
4. Bir kullanıcı ekleyin.
5. **Tamam** düğmesine tıklayın.

>[!NOTE]
>Bir kullanıcı veya güvenlik grubu toosubmit işleri gerekiyorsa, bunlar da hello depolama hesabındaki izni gerekir. Daha fazla bilgi için bkz: [güvenli Data Lake Store içinde depolanan verileri](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>İşleri yönetme

### <a name="submit-a-job"></a>Bir işi gönderin

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.

2. Tıklatın **yeni iş**. Her bir iş yapılandırın:

    1. **İş adı**: hello işinin hello adı.
    2. **Öncelik**: alt numaraları yüksek önceliği vardır. İki işi sıraya alınmışsa, düşük öncelik değerine sahip hello ilk çalışır.
    3. **Paralellik**: hello en fazla işlem sayısı bu işin tooreserve işler.

3. **İşi Gönder**'e tıklayın.

### <a name="monitor-jobs"></a>İşleri izleme

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. Tıklatın **tüm işleri görüntüleyin**. Merhaba hesaptaki tüm hello etkin ve en son bitmiş işlerin bir listesini gösterilir.
3. İsteğe bağlı olarak, tıklayın **filtre** hello işleri tarafından bulduğunuz toohelp **zaman aralığı**, **iş adı**, ve **Yazar** değerleri. 

### <a name="monitoring-pipeline-jobs"></a>Ardışık Düzen işlerini izleme
Bir işlem hattı parçası olan birlikte, genellikle bir sırayla tooaccomplish belirli bir senaryoyu işler. Örneğin, temizler, ayıklar, dönüşümleri, müşteri Öngörüler için kullanım toplayan bir ardışık düzen olabilir. Ardışık Düzen işleri hello iş gönderildiğinde hello "Ardışık düzen" özelliği kullanılarak tanımlanır. ADF V2 kullanılarak zamanlanan işleri otomatik olarak doldurulmuş bu özelliğe sahip. 

Ardışık Düzen parçası olan U-SQL işlerin bir listesini tooview: 

1. Hello Azure portal, tooyour Data Lake Analytics hesapları gidin.
2. Tıklatın **iş Öngörüler**. "Tüm işleri" sekmesi, çalışan, listesini gösteren varsayılan olacak hello sıraya ve işleri sona erdi.
3. Merhaba tıklatın **ardışık düzen işleri** sekmesi. Ardışık Düzen işlerin bir listesini her ardışık düzeni için toplu istatistikler birlikte gösterilir.

### <a name="monitoring-recurring-jobs"></a>Yinelenen işlerini izleme
Yinelenen bir işi hello sahip biridir aynı iş mantığı her çalıştığında farklı giriş verisi ancak kullanır. İdeal olarak, yinelenen işleri her zaman başarılı ve göreceli olarak tutarlı yürütme süresi vardır; Bu davranışların izleme hello iş sağlıklı olduğundan emin olun yardımcı olur. Yinelenen işleri hello "Recurrence" özelliği kullanılarak tanımlanır. ADF V2 kullanılarak zamanlanan işleri otomatik olarak doldurulmuş bu özelliğe sahip.

tooview yinelenen U-SQL işleri listesi: 

1. Hello Azure portal, tooyour Data Lake Analytics hesapları gidin.
2. Tıklatın **iş Öngörüler**. "Tüm işleri" sekmesi, çalışan, listesini gösteren varsayılan olacak hello sıraya ve işleri sona erdi.
3. Merhaba tıklatın **yinelenen işleri** sekmesi. Yinelenen işlerin bir listesini, yinelenen her iş için toplu istatistikler birlikte gösterilir.

## <a name="manage-policies"></a>İlkeleri yönetme

### <a name="account-level-policies"></a>Hesap düzeyinde ilkeleri

Bu ilkeler, bir Data Lake Analytics hesabı tooall işleri geçerlidir.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>En fazla Avustralya numarasında Data Lake Analytics hesabı
Bir ilke hello Analytics Data Lake Analytics hesabınızı kullanabilirsiniz birimlerin (Avustralya) toplam sayısını denetler. Varsayılan olarak, too250 hello değer ayarlanır. Bu değer too250 Avustralya ayarlanırsa, örneğin, 250 atanan Avustralya tooit ile çalışan bir iş ya da 25 ile çalışan 10 işleri olabilir Avustralya her. Hello çalışan işler tamamlanana kadar gönderilen ek işler kuyruğa alınır. Çalışan işleri tamamlandığında, Avustralya kaydınızı hello kurtulurlar işleri toorun sıraya alındı.

toochange hello sayısı Avustralya, Data Lake Analytics hesabı için:

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Özellikler**'e tıklayın.
3. Altında **maksimum Avustralya**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin. 
4. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> Size gereken birden çok hello varsayılan (250) Avustralya, hello Portalı'nda tıklatın **Yardım + Destek** toosubmit bir destek isteği. Avustralya Data Lake Analytics hesabınızı kullanılabilir Hello sayısı artırılabilir.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Aynı anda çalışabilir işi sayısı üst sınırı
Bir ilke kaç işleri hello çalıştırabilirsiniz denetimleri aynı anda. Varsayılan olarak, bu değer too20 ayarlanır. Data Lake Analytics Avustralya kullanılabilir olan yeni işleri hemen işleri çalıştırma hello toplam sayısı bu ilkenin hello değere ulaşana kadar zamanlanmış toorun demektir. Merhaba iş sayısı üst sınırını aynı anda çalışabilecek ulaştığında, sonraki işleri (AU kullanılabilirliğine bağlı olarak) bir veya daha fazla çalışan iş tamamlanana kadar öncelik sırasına göre sıralanır.

aynı anda çalışabilecek iş toochange hello sayısı:

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Özellikler**'e tıklayın.
3. Altında **en büyük sayı, çalışan işleri**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin. 
4. **Kaydet** düğmesine tıklayın.

> [!NOTE]
> Daha fazla varsayılan (20) hello portalında, iş sayısı hello daha tıklatın toorun gerekiyorsa **Yardım + Destek** toosubmit bir destek isteği. Data Lake Analytics hesabınızı eşzamanlı olarak çalışabilecek iş Hello sayısı artırılabilir.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>Ne kadar süreyle tookeep işi meta verileri ve kaynaklar 
Kullanıcılarınızın U-SQL işleri çalıştırdığınızda, hello Data Lake Analytics hizmeti ilişkili tüm dosyaları korur. İlgili dosyalar hello U-SQL komut dosyası, hello U-SQL komut dosyası, derlenmiş kaynaklar ve İstatistikler başvurulan hello DLL dosyaları içerir. Merhaba, hello /system/ klasöründe hello varsayılan Azure Data Lake Store hesabına dosyalarıdır. Bu ilke, bu kaynakları otomatik olarak silinmeden önce ne kadar süreyle depolanır denetler (Merhaba varsayılan olarak 30 gün). Hata ayıklama ve hello gelecekteki yeniden işleri için performans ayarlama, bu dosyaları kullanabilirsiniz.

toochange ne kadar süreyle tookeep işi meta verileri ve kaynaklar:

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Özellikler**'e tıklayın.
3. Altında **gün tooRetain iş sorguları**hello kaydırıcı tooselect bir değer taşımak veya hello değeri hello metin kutusuna girin.  
4. **Kaydet** düğmesine tıklayın.

### <a name="job-level-policies"></a>Proje düzeyi ilkeleri
İş düzeyinde ilkeleriyle kontrol edebilirsiniz maksimum Avustralya hello ve hello bireysel kullanıcılar (veya belirli güvenlik gruplarının üyeleri) bunlar gönderme işlere ayarlayabilirsiniz en yüksek öncelik. Bu kullanıcılar tarafından hello maliyetleri kontrol etmenizi sağlar. Ayrıca sağlar zamanlanmış iş denetim hello etkisi, yüksek öncelikli olabilir çalışmakta olan üretim işlerini hello aynı Data Lake Analytics hesabı.

Data Lake Analytics hello iş düzeyinde ayarlayabilirsiniz iki ilke vardır:

* **İş başına AU sınırı**: kullanıcılar yalnızca Avustralya toothis sayıda işleri gönderme. Varsayılan olarak, bu sınır olan hello hello AU sınırını hello hesabı ile aynı.
* **Öncelik**: kullanıcıların yalnızca bir öncelik eşit veya değerinden daha düşük toothis değerine sahip işlerin gönderin. Daha yüksek bir sayı daha düşük bir öncelik anlamına gelir. Varsayılan olarak, bu too1, hello olası en yüksek öncelikli olduğu ayarlanır.

Varsayılan ilke her hesabında kümesi yok. Merhaba varsayılan ilke tooall kullanıcılar hello hesabının geçerlidir. Ek ilkeler belirli kullanıcılar ve gruplar için ayarlayabilirsiniz. 

> [!NOTE]
> Hesap düzeyinde ilkeler ve iş düzeyinde ilkeleri aynı anda uygulayın.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Belirli bir kullanıcı veya grup için bir ilke ekleme

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Özellikler**'e tıklayın.
3. Altında **iş gönderim sınırları**, hello tıklatın **ilke Ekle** düğmesi. Ardından, seçin veya ayarları aşağıdaki hello girin:
    1. **İlke adı işlem**: tooremind İlkesi bir ad girin, hello İlkesi hello amacı.
    2. **Kullanıcı veya Grup Seç**: hello kullanıcı veya bu ilkenin uygulandığı grup seçin.
    3. **Merhaba iş AU sınırını ayarlama**: toohello geçerlidir hello AU sınırını ayarlama seçili kullanıcı veya grup.
    4. **Merhaba öncelik sınırı ayarlama**: toohello geçerlidir hello öncelik sınırını ayarlama seçili kullanıcı veya grup.

4. **Tamam**’a tıklayın.

5. Merhaba yeni ilke hello listelenen **varsayılan** altında İlkesi tablo **iş gönderim sınırları**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Silin veya mevcut bir ilkeyi Düzenle

1. Hello Azure portal, tooyour Data Lake Analytics hesabı gidin.
2. **Özellikler**'e tıklayın.
3. Altında **iş gönderim sınırları**, tooedit istediğiniz Bul hello ilkesi.
4.  toosee hello **silmek** ve **Düzenle** Merhaba tablonun hello en sağdaki sütundaki seçenekleri **...** .

### <a name="additional-resources-for-job-policies"></a>İş ilkeleri için ek kaynaklar
* [İlke genel bakış blog gönderisi](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Hesap düzeyinde ilkeler blog gönderisi](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Proje düzeyi ilkeleri blog gönderisi](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Sonraki adımlar

* [Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md)
* [Azure PowerShell kullanarak Azure Data Lake Analytics'i yönetme](data-lake-analytics-manage-use-powershell.md)

