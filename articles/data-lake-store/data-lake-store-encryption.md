---
title: Azure Data Lake Store'da aaaEncryption | Microsoft Docs
description: "Şifreleme ve anahtar döndürmenin Azure Data Lake Store'da nasıl çalıştığını anlama"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Azure Data Lake Store'da veri şifreleme

Azure Data Lake Store’da şifreleme; verilerinizi koruma, kurumsal güvenlik ilkeleri uygulama ve yasal uyumluluk gereksinimlerini karşılamaya yardımcı olur. Bu makalede hello tasarım genel bir bakış sağlar ve bazı uygulama teknik yönlerini hello ele alır.

Data Lake Store, hem bekleyen hem de aktarımdaki verilerin şifrelenmesini destekler. Bekleyen veriler için Data Lake Store, "varsayılan olarak etkin" saydam şifrelemeyi destekler. Bu terimlerin biraz daha ayrıntılı olarak anlamı şudur:

* **Üzerinde varsayılan olarak**: yeni bir Data Lake Store hesabı oluşturduğunuzda, hello varsayılan ayar şifrelemeyi etkinleştirir. Bundan sonra Data Lake Store içinde depolanan verileri her zaman şifreli önceki toostoring kalıcı medyada gerçekleşir. Bu tüm veriler için hello davranıştır ve bir hesabı oluşturulduktan sonra değiştirilemez.
* **Saydam**: Data Lake Store otomatik olarak veri önceki toopersisting şifreler ve veri önceki tooretrieval şifresini çözer. Hello şifreleme yapılandırılıp hello Data Lake Store düzeyi bir yönetici tarafından yönetilebilir. Toohello veri yapılan hiçbir değişiklik API'lere erişim. Bu nedenle, Data Lake Store ile etkileşimde bulunan uygulamalarda ve hizmetlerde şifreleme için herhangi bir değişiklik yapılması gerekmez.

Data Lake Store'da aktarımdaki (diğer adıyla hareket halindeki) veriler de her zaman şifrelenir. Ayrıca tooencrypting veri önceki toostoring toopersistent medya hello veri ayrıca her zaman aktarım sırasında HTTPS kullanılarak korunmaktadır. HTTPS için Data Lake Store REST arabirimleri hello desteklenir hello tek protokoldür. Merhaba Aşağıdaki diyagramda nasıl Data Lake Store'da şifreli veriler hale gösterilmektedir:

![Data Lake Store'da veri şifreleme diyagramı](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Data Lake Store ile şifrelemeyi ayarlama

Data Lake Store için Şifreleme, hesap oluşturma sırasında ayarlanır ve her zaman varsayılan olarak etkindir. Merhaba anahtarları kendiniz yönetmek veya Data Lake Store toomanage izin ver (Bu, hello varsayılan), bunları.

Daha fazla bilgi için [Başlarken](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal) bölümüne bakın.

## <a name="how-encryption-works-in-data-lake-store"></a>Data Lake Store'da şifreleme nasıl çalışır

Merhaba aşağıdaki bilgileri nasıl toomanage ana şifreleme anahtarları açıklar hello üç farklı türde Data Lake Store için veri şifrelemeyi kullanabilirsiniz anahtarları kapsar.

### <a name="master-encryption-keys"></a>Ana şifreleme anahtarları

Data Lake Store, ana şifreleme anahtarlarının (MEK’ler) yönetimi için iki mod sağlar. Şu an için bu hello ana şifreleme anahtarı hello en üst düzey anahtardır varsayalım. Data Lake Store içinde depolanan tüm verileri gerekli toodecrypt erişim toohello ana şifreleme anahtarıdır.

Merhaba iki modları hello ana şifreleme anahtarı yönetmek için aşağıdaki gibidir:

*   Hizmet tarafından yönetilen anahtarlar
*   Müşteri tarafından yönetilen anahtarlar

Her iki modda Azure anahtar kasası depolayarak hello ana şifreleme anahtarı güvenlik altına alınır. Anahtar kasası, kullanılan toosafeguard şifreleme anahtarları olabilir Azure üzerinde tam olarak yönetilen, yüksek güvenlikli bir hizmettir. Daha fazla bilgi için bkz. [Key Vault](https://azure.microsoft.com/services/key-vault).

Burada, kısa bir hello MEKs yönetme hello iki moddan tarafından sağlanan özellikleri karşılaştırması verilmiştir.

|  | Hizmet tarafından yönetilen anahtarlar | Müşteri tarafından yönetilen anahtarlar |
| --- | --- | --- |
|Veriler nasıl depolanır?|Her zaman şifreli önceki toobeing depolanır.|Her zaman şifreli önceki toobeing depolanır.|
|Merhaba ana şifreleme anahtarı nerede depolanır?|Anahtar Kasası|Anahtar Kasası|
|Hello depolanan anahtarlar temizleyin şifreleme anahtar kasası dışında misiniz? |Hayır|Hayır|
|Merhaba MEK anahtar kasası tarafından alınabilir?|Hayır. MEK anahtar kasasında depolanan hello sonra onu yalnızca şifreleme ve şifre çözme için kullanılabilir.|Hayır. MEK anahtar kasasında depolanan hello sonra onu yalnızca şifreleme ve şifre çözme için kullanılabilir.|
|Merhaba anahtar kasası örneği ve hello MEK Kime ait?|Merhaba Data Lake Store hizmeti|Kendi Azure aboneliğinizde ait hello anahtar kasası örnek sahip. Merhaba MEK anahtar Kasası'nda, yazılım veya donanım tarafından yönetilebilir.|
|Itanium tabanlı sistemler için erişim toohello MEK hello Data Lake Store hizmeti için geçersiz kılabilir mi?|Hayır|Evet. Anahtar kasasına erişim denetim listelerini yönetmek ve erişim denetimi girdileri toohello hizmet kimliği hello Data Lake Store hizmetini için kaldırın.|
|Merhaba MEK kalıcı olarak silebilir?|Hayır|Evet. Anahtar Kasası'hello MEK silerseniz, herkes tarafından hello Data Lake Store hizmeti dahil olmak üzere hello verileri hello Data Lake Store hesabı şifresi çözülemiyor. <br><br> Siz açıkça hello MEK önceki toodeleting, anahtar Kasası'nı yedeklediyseniz hello MEK geri yüklenebilir ve hello veri ardından kurtarılabilir. Hello MEK önceki toodeleting, anahtar Kasası'nı yedeklemediyseniz, ancak hello Data Lake Store hesabı hello verilerde hiçbir zaman bundan sonra şifresi çözülebilir.|


Bu farkı yanı sıra hello MEK yöneten ve içinde bulunduğu, hello anahtar kasası örnek hello tasarım hello kalan olduğu hello aynı her iki mod için.

Ana şifreleme anahtarları hello için hello modu seçtiğinizde önemli tooremember hello aşağıda verilmiştir:

*   Bir Data Lake Store hesabı sağladığınızda toouse müşteri anahtarları ve yönetilen hizmeti anahtarlar yönetilen olup olmadığını seçebilirsiniz.
*   Bir Data Lake Store hesabı sağlandıktan sonra başlangıç modu değiştirilemez.

### <a name="encryption-and-decryption-of-data"></a>Verilerin şifrelenmesi ve şifresinin çözülmesi

Veri şifreleme hello tasarımında kullanılan anahtarların üç tür vardır. Aşağıdaki tablonun hello bir Özet sağlar:

| Anahtar                   | Kısaltma | İlişkili olduğu yer: | Depolama konumu                             | Tür       | Notlar                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Ana Şifreleme Anahtarı | MEK          | Bir Data Lake Store hesabı | Anahtar Kasası                              | Asimetrik | Data Lake Store veya sizin tarafınızdan yönetilebilir.                                                              |
| Veri Şifreleme Anahtarı   | DEK          | Bir Data Lake Store hesabı | Kalıcı depolama, Data Lake Store hizmeti tarafından yönetilir | Simetrik  | Merhaba DEK MEK hello tarafından şifrelenir. Merhaba şifrelenmiş DEK ne kalıcı medyada depolanır. |
| Blok Şifreleme Anahtarı  | BEK          | Bir veri bloğu | None                                         | Simetrik  | Merhaba BEK hello DEK ve hello veri bloğu türetilir.                                                      |

Aşağıdaki diyagramda hello bu kavramları göstermektedir:

![Veri şifrelemesindeki anahtarlar](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Bir dosya şifresi toobe olduğunda sözde algoritması:
1.  Merhaba DEK hello Data Lake Store hesabı için önbelleğe alınmış ve kullanıma hazır olup olmadığını denetleyin.
    - Aksi durumda, hello DEK kalıcı depolama biriminden şifrelenmiş okuma ve şifresi tooKey kasa toobe gönderebilirsiniz. Önbellek hello DEK bellekte şifresi. Bu hazır toouse sunulmuştur.
2.  Her hello dosyasındaki veri bloğu için:
    - Merhaba şifrelenmiş veri bloğunu kalıcı depolama alanından okuyun.
    - Merhaba BEK hello DEK gelen ve hello şifrelenmiş veri bloğunu oluşturur.
    - Merhaba BEK toodecrypt verileri kullanın.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Bir veri bloğunun toobe şifreli olduğunda sözde algoritması:
1.  Merhaba DEK hello Data Lake Store hesabı için önbelleğe alınmış ve kullanıma hazır olup olmadığını denetleyin.
    - Aksi durumda, hello DEK kalıcı depolama biriminden şifrelenmiş okuma ve şifresi tooKey kasa toobe gönderebilirsiniz. Önbellek hello DEK bellekte şifresi. Bu hazır toouse sunulmuştur.
2.  Veri hello bloğu için benzersiz bir BEK hello DEK oluşturur.
3.  Merhaba veri bloğu ile Merhaba BEK, AES 256 şifreleme kullanarak şifreler.
4.  Veri Hello şifrelenmiş veri bloğunu kalıcı depolama alanında depolar.

> [!NOTE] 
> Performans nedenleriyle hello DEK temizleyin hello kısa bir süre için bellekte önbelleğe alınır ve hemen sonra silinir. Kalıcı bir ortama MEK hello tarafından şifrelenmiş her zaman depolanır.

## <a name="key-rotation"></a>Anahtar döndürme

Müşteri tarafından yönetilen anahtarlarını kullanırken hello MEK döndürebilirsiniz. Müşteri tarafından yönetilen anahtarlarla Data Lake Store hesabı tooset nasıl görürüm toolearn [Başlarken](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Ön koşullar

Data Lake Store hesabı hello ayarladığınızda, kendi anahtarları toouse seçtiniz. Bu seçenek Hello hesabı oluşturulduktan sonra değiştirilemez. Merhaba aşağıdaki adımlarda müşteri tarafından yönetilen anahtarları kullandığınız varsayılmaktadır (diğer bir deyişle, kendi anahtarları anahtar Kasası'nı seçmiş olduğunuz).

Şifreleme için hello varsayılan seçenekleri kullanırsanız, verileriniz her zaman Data Lake Store tarafından yönetilen anahtarlar kullanılarak şifrelenmiş olduğunu unutmayın. Bu seçenekte, Data Lake Store tarafından yönetilen gibi hello özelliği toorotate anahtarları yok.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Nasıl toorotate hello Data Lake Store'da MEK

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Data Lake Store hesabınızla ilişkili anahtarlarınızı depolar toohello anahtar kasası örnek göz atın. **Anahtarlar**’ı seçin.

    ![Key Vault ekran görüntüsü](./media/data-lake-store-encryption/keyvault.png)

3.  Data Lake Store hesabınızla ilişkili hello anahtarı seçin ve bu anahtar yeni bir sürümünü oluşturur. Data Lake Store şu anda yalnızca bir anahtarı'nın anahtar döndürme tooa yeni sürümü desteklediğini unutmayın. Döndürme tooa farklı anahtarı desteklemiyor.

   ![Yeni Sürümün vurgulandığı Anahtarlar penceresi ekran görüntüsü](./media/data-lake-store-encryption/keynewversion.png)

4.  Toohello Data Lake Store depolama hesabını bulun ve seçin **şifreleme**.

    ![Şifreleme’nin vurgulandığı Data Lake Store depolama hesabı penceresinin ekran görüntüsü](./media/data-lake-store-encryption/select-encryption.png)

5.  Bir ileti hello anahtarı yeni bir anahtar sürümü kullanılabilir olduğunu bildirir. Tıklatın **döndürme anahtar** tooupdate hello anahtar toohello yeni sürümü.

    ![İleti ve Anahtarı Döndür seçenekleri vurgulanmış Data Lake Store penceresinin ekran görüntüsü](./media/data-lake-store-encryption/rotatekey.png)

Bu işlem iki dakikadan kısa sürer ve tookey dönüş son beklenen kapalı kalma süresi yok. Merhaba işlemi tamamlandıktan sonra hello hello anahtarı'nın yeni sürümü kullanılıyor.
