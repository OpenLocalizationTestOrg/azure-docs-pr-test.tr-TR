---
title: "blob depolama biriminden aaaUsing Azure içeri/dışarı aktarma tootransfer veri tooand | Microsoft Docs"
description: "Nasıl toocreate alma ve işler hello blob depolama alanından veri tooand aktarmak için Azure portal'verme öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Merhaba Microsoft Azure içeri/dışarı aktarma hizmeti tootransfer veri tooblob depolama kullanın
Hello Azure içeri/dışarı aktarma hizmeti toosecurely aktarımı büyük miktarlarda veri tooAzure blob depolama sevkiyat sabit disk sürücülerinin tooan Azure veri merkezi tarafından sağlar. Ayrıca, bu hizmet tootransfer verileri Azure blob depolama toohard disk sürücüleri kullanan ve tooyour şirket içi site sevk. Bu hizmet durumlarda uygundur burada birkaç terabayta (TB) veri tooor azure'dan tootransfer istiyor, ancak karşıya yükleme veya hello ağ üzerinden indirme toolimited bant genişliği nedeniyle uyuşmazlığa veya yüksek ağ maliyetlerini.

sabit disk sürücüleri BitLocker verilerinizi hello güvenlik amacıyla şifrelenmiş olması gerektiğini Hello hizmetini gerektirir. Merhaba hizmeti hem hello Klasik ve Azure Resource Manager depolama hesapları (standart ve seyrek erişimli katman) ortak Azure tüm hello bölgelerde mevcut destekler. Bu makalenin sonraki bölümlerinde belirtilen hello desteklenen konumların sabit disk sürücülerinin tooone birlikte gerekir.

Bu makalede, hello Azure içeri/dışarı aktarma hizmeti ve Azure Blob depolama alanından veri tooand kopyalamak için tooship nasıl sürücüler hakkında bilgi edinin.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Hello Azure içeri/dışarı aktarma hizmeti ne zaman kullanmalıyım?
Azure içeri/dışarı aktarma hizmeti karşıya yüklenirken kullanmayı düşünün hello ağ üzerinden veri indirme çok yavaşsa veya ek ağ bant genişliği alma maliyetli olabilir.

Bu hizmet gibi senaryolarda kullanabilirsiniz:

* Geçirme verilerini toohello bulut: büyük miktarlarda veri tooAzure hızlıca taşımak ve düşük maliyetle.
* İçerik dağıtım: veri tooyour müşteri sitelerini hızlı bir şekilde gönderin.
* Yedekleme: Azure blob depolama alanına, şirket içi veri toostore yedeğini alın.
* Veri kurtarma: kurtarmak büyük miktarda veri blob depolama alanına depolanır ve tooyour şirket içi konumunuz teslim sahip.

## <a name="prerequisites"></a>Ön koşullar
Bu bölümde Biz bu hizmet hello önkoşullar gerekli toouse listeleyin. Lütfen dikkatle sürücülerinizin göndermeden önce gözden geçirin.

### <a name="storage-account"></a>Depolama hesabı
Var olan bir Azure aboneliği ve bir veya daha fazla depolama hesapları toouse hello içeri/dışarı aktarma hizmeti olması gerekir. Her iş yalnızca bir depolama hesabından kullanılan tootransfer veri tooor olabilir. Diğer bir deyişle, bir tek içeri/dışarı aktarma işi birden çok depolama hesaplarında yayılamaz. Yeni bir depolama hesabı oluşturma hakkında daha fazla bilgi için bkz: [nasıl tooCreate bir depolama hesabı](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>BLOB türleri
Azure içeri/dışarı aktarma hizmeti toocopy verilerini kullanabileceğine**blok** BLOB'lar veya **sayfa** BLOB'lar. Buna karşılık, yalnızca verebilirsiniz **blok** BLOB'lar, **sayfa** BLOB'lar veya **Append** bu hizmeti kullanarak Azure storage bloblarından.

### <a name="job"></a>İş
Blob depolama alanından verme tooor alma hello işlem toobegin, önce bir iş oluşturun. Bir iş, bir içeri aktarma işi veya bir dışarı aktarma işinin olabilir:

* Azure depolama hesabınızdaki şirket içi tooblobs sahip tootransfer verileri istediğinizde bir alma işi oluşturun.
* Bir dışarı aktarma işi oluşturma bir proje oluşturduğunuzda, depolama hesabı toohard sürücülerinizin blobları tooyou.s sevk edilmiş olarak şu anda depolanan tootransfer veri istediğinizde hello alma/verme, bir sevkiyat olmalıdır, hizmet ya da daha fazla sabit sürücüler tooan Azure bildir Veri Merkezi.

* Bir içeri aktarma işi için verilerinizi içeren sabit sürücüler sevkiyat.
* Bir dışarı aktarma işi için boş sabit disk sürücüler sevkiyat.
* Too10 sabit disk sürücülerinin (job) başına yukarı gönderebilirsiniz.

Alma oluşturmak veya hello Azure portal veya hello kullanarak iş verme [Azure depolama içeri/dışarı aktarma REST API](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>WAImportExport aracı
Merhaba oluşturmanın ilk adımı bir **alma** iş tooprepare alma için gönderilen sürücülerinizin olduğu. tooprepare sürücülerinizin, tooa yerel sunucuya ve çalışma hello WAImportExport aracı hello yerel sunucuda bağlanmalısınız. Bu WAImportExport aracı veri toohello sürücünüze kopyalama, hello sürücüde BitLocker ile Merhaba verileri şifrelemek ve hello sürücü günlük dosyaları oluşturma kolaylaştırır.

Hello günlük dosyaları, iş ve sürücü sürücü seri numarası ve depolama hesabı adı gibi ilgili temel bilgileri saklar. Bu günlük dosyası hello sürücüsünde depolanmaz. İçeri aktarma işi oluşturma sırasında kullanılır. Adım adım iş oluşturma hakkındaki ayrıntıları bu makalenin sonraki bölümlerinde sağlanır.

Merhaba WAImportExport aracı yalnızca 64-bit Windows işletim sistemiyle uyumlu değil. Merhaba bkz [işletim sistemi](#operating-system) desteklenen belirli işletim sistemi sürümleri için bölüm.

Hello hello en son sürümünü indirme [WAImportExport aracı](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Merhaba WAImportExport aracını kullanma hakkında daha fazla ayrıntı hello için bkz: [kullanma hello WAImportExport aracı](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Önceki sürümü:** yapabilecekleriniz [WAImportExpot V1 karşıdan](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) hello sürümü çok bakın ve aracı[WAImportExpot V1 kullanım kılavuzda](storage-import-export-tool-how-to-v1.md). Merhaba aracı WAImportExpot V1 sürümü için destek sağlar **veri zaten toohello disk önceden yazıldığında diskleri hazırlama**. Ayrıca Hello yalnızca anahtar kullanılabilir SAS anahtarı ise toouse WAImportExpot V1 Aracı gerekir.

>

### <a name="hard-disk-drives"></a>Sabit disk sürücüleri
Yalnızca 2,5 inç SSD veya 2,5" veya 3,5" SATA II veya III iç HDD hello içeri/dışarı aktarma hizmeti ile kullanım için desteklenir. Bir tek içeri/dışarı aktarma işi en fazla 10 HDD/SSD olabilir ve tek tek her HDD/SSD herhangi bir boyutta olabilir. Büyük sayıda sürücüsü birden çok iş arasında yayılabilir ve hello oluşturulabilen iş sayısı sınırı yoktur. 

İçeri aktarma işi için yalnızca hello ilk veri birimi hello sürücüde işlenir. Merhaba veri birimi NTFS ile biçimlendirilmiş olması gerekir.

> [!IMPORTANT]
> Yerleşik bir USB bağdaştırıcısı ile gelen dış sabit disk sürücülerinin, bu hizmet tarafından desteklenmiyor. Ayrıca, bir dış HDD, hello büyük/küçük harf içinde hello disk kullanılamaz; Lütfen dış HDD göndermeyin.
> 
> 

Aşağıda dış USB bağdaştırıcıları listesini toocopy veri toointernal HDD kullanılır. Anker 68UPSATAA - 02BU Anker 68UPSHHDS BU Startech SATADOCK22UE Orico 6628SUS3 C SİY (6628 serisi) Thermaltake BlacX etkin takas SATA dış sabit sürücü yerleştirme istasyon (USB 2.0 & eSATA)

### <a name="encryption"></a>Şifreleme
BitLocker Sürücü Şifrelemesi'ni kullanarak hello sürücüdeki Hello verilerin şifrelenmesi gerekir. Bunu esnasında bu verilerinizi korur.

İçeri aktarma işi için iki yol tooperform hello şifreleme vardır. Merhaba ilk yol toospecify hello veri kümesi CSV dosyası sürücü hazırlanması sırasında hello WAImportExport Aracı çalıştırırken kullanırken bir seçenektir. Merhaba ikinci yol tooenable BitLocker şifrelemesi hello sürücüsünde el ile ve WAImportExport aracı komut satırı sürücü hazırlanması sırasında çalıştırırken hello driveset CSV hello şifreleme anahtarını belirtin.

Kopyalanan toohello sürücüleri, verilerinizi olduktan sonra dışarı aktarma işleri için hello hizmeti geri tooyou göndermeden önce BitLocker'ı kullanarak hello sürücüsünü şifrelemek. Merhaba şifreleme anahtarı tooyou hello Azure portal aracılığıyla sağlanır.  

### <a name="operating-system"></a>İşletim Sistemi
64-bit işletim sistemleri tooprepare hello sabit sürücü hello sürücü tooAzure göndermeden önce hello WAImportExport aracını kullanarak aşağıdaki hello birini kullanabilirsiniz:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. BitLocker Sürücü Şifrelemesi bu işletim sistemlerini desteklemez.

### <a name="locations"></a>Konumlar
Hello Azure içeri/dışarı aktarma hizmeti tüm ortak Azure depolama hesapları arasından kopyalama veri tooand destekler. Aşağıdaki konumlardan Merhaba, sabit disk sürücülerinin tooone gönderebilirsiniz. Depolama hesabınız, burada, oluştururken bir alternatif sevkiyat konumu sağlanan belirtilmemiş bir ortak Azure konumdaysa iş hello kullanarak Azure portalında hello veya içeri/dışarı aktarma REST API hello.

Sevkiyat konumlar desteklenir:

* Doğu ABD
* Batı ABD
* Doğu ABD 2
* Batı ABD 2
* Orta ABD
* Orta Kuzey ABD
* Orta Güney ABD
* Batı Orta ABD
* Kuzey Avrupa
* Batı Avrupa
* Doğu Asya
* Güneydoğu Asya
* Avustralya Doğu
* Avustralya Güneydoğu
* Japonya Batı
* Japonya Doğu
* Orta Hindistan
* Güney Hindistan
* Batı Hindistan
* Orta Kanada
* Doğu Kanada
* Güney Brezilya
* Kore Orta
* ABD Devleti Virginia
* ABD Devleti Iowa
* US DoD Doğu
* US DoD Orta
* Çin Doğu
* Çin Kuzey
* Birleşik Krallık Güney

### <a name="shipping"></a>Aktarma
**Sevkiyat toohello veri merkezi sürücüler:**

Bir içe veya dışa aktarma işi oluştururken, teslimat adresi hello birinin konumları tooship sürücülerinizin desteklenen sağlanacaktır. sağlanan adresi sevkiyat hello depolama hesabınızın hello konumuna bağlıdır, ancak aynı depolama hesabı konumu olarak hello olmayabilir.

Hizmet sağlayıcılar FedEx, DHL, UPS veya hello ABD posta hizmeti tooship gibi sevkiyat adresini, sürücüler toohello kullanabilirsiniz.

**Sevkiyat hello veri merkezinden sürücüler:**

İşinizi tamamlandıktan sonra sevkiyat hello sürücüleri yedeklediğinizde içe veya dışa aktarma işi oluştururken, Microsoft toouse için bir dönüş adresi sağlamanız gerekir. Lütfen geçerli bir dönüş adresi işleme tooavoid gecikme sağladığınızdan emin olun.

Tercih ettiğiniz bir taşıyıcı sipariş tooforward sevk hello sabit disk kullanabilirsiniz. Merhaba taşıyıcı uygun izleme sırası toomaintain zincirini içinde olması gerekir. Microsoft tarafından geri hello sürücüleri aktarma için kullanılan hesap numarası toobe geçerli FedEx veya DHL operatör de sağlamanız gerekir. FedEx hesap numarası, geri hello ABD ve Avrupa konumlardan sürücüleri sevkiyat için gereklidir. DHL hesap numarası, sürücüler geri Asya ve Avustralya'da konumlardan sevkiyat için gereklidir. Oluşturabileceğiniz bir [FedEx](http://www.fedex.com/us/oadr/) (için ABD ve Avrupa) veya [DHL](http://www.dhl.com/) bir yoksa (Asya ve Avustralya) taşıyıcı hesap. Bir taşıyıcı hesap numarası zaten varsa, Lütfen geçerli olduğunu doğrulayın.

Paketlerinizi sevkiyat içinde hello koşulların en izlemelisiniz [Microsoft Azure Hizmet Koşulları'nı](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Lütfen, yayımlayan hello fiziksel ortam toocross uluslararası sınırların gerekebileceğini unutmayın. Fiziksel ortam ve veri içe aktarılan ve/veya hello ilgili yasalarına uygun olarak dışarı olduğunu sağlamaktan sorumludur. Merhaba fiziksel ortam göndermeden önce medya ve veri sevk edilen toohello tanımlanan veri merkezi yasal olabilir, advisers tooverify ile denetleyin. Bu, Microsoft zamanında ulaştığında tooensure yardımcı olur. Örneğin, uluslararası sınırların arası herhangi bir paket (dışında Kenarlıklar Avrupa Birliği içinde çapraz) hello paketiyle eşlik ticari fatura toobe gerekir. Merhaba ticari fatura taşıyıcı Web sitesinden doldurulmuş bir kopyasını yazdırmak. Ticari faturalar örnektir [DHL ticari fatura](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) ve [FedEx ticari fatura](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Microsoft hello verici belirtmedi olduğundan emin olun.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Hello Azure içeri/dışarı aktarma hizmeti nasıl çalışır?
İşleri oluşturma ve sabit disk sürücülerinin tooan Azure veri merkezine sevkiyat hello Azure içeri/dışarı aktarma hizmetini kullanarak Azure blob storage ve şirket içi site arasında veri aktarımı. Sevk her sabit diskin tek bir iş ile ilişkilidir. Her bir iş, tek bir depolama hesabıyla ilişkilendirilir. Gözden geçirme hello [önkoşullar bölümünde](#pre-requisites) dikkatle toolearn hello ayrıntılarını bu gibi desteklenen hizmet blob türleri, disk türlerini, konumlarını ve aktarma hakkında.

Bu bölümde, içeri aktarma bir yüksek düzey hello adımları sırasında açıklamak ve işleri verin. Merhaba devamındaki [Hızlı Başlat bölümünde](#quick-start), bir içeri aktarma hakkında adım adım yönergeler toocreate sağlar ve iş dışarı aktarma.

### <a name="inside-an-import-job"></a>İçe aktarma işi
Yüksek bir düzeyde bir alma işi hello aşağıdaki adımları içerir:

* Size gereken sürücü sayısı hello ve içeri hello veri toobe belirler.
* Blob storage verilerinizin Hello hedef blob konum belirleyin.
* BitLocker ile şifrelemek ve Hello WAImportExport aracı toocopy veri tooone ya da daha fazla sabit disk sürücüsü kullanın.
* Hedef depolama hesabınızı hello Azure portal kullanarak bir içeri aktarma işi oluşturma veya içeri/dışarı aktarma REST API hello. Hello Azure portalını kullanıyorsanız, hello sürücü günlük dosyalarını karşıya yükleyin.
* Merhaba dönüş adresi ve taşıyıcı hesap numarası toobe hello sürücüleri geri tooyou aktarma için kullanılan sağlar.
* Proje oluşturma sırasında sağlanan adresi sevkiyat sevk hello sabit disk sürücülerinin toohello.
* İzleme numarası hello alma işi ayrıntıları hello teslim güncelleştirin ve hello alma işi göndermek.
* Sürücüleri alınan ve hello Azure veri merkezinde işlenebilir.
* Sürücüleri hello alma işi sağlanan, taşıyıcı hesap toohello dönüş adresi kullanılarak aktarılır.
  
    ![Şekil 1:Import iş akışı](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>İçinde bir dışarı aktarma işinin
Yüksek bir düzeyde bir dışarı aktarma işinin hello aşağıdaki adımları içerir:

* Hello veri toobe dışa aktarılan ve sürücü ihtiyacınız olacak hello belirler.
* Merhaba kaynak BLOB veya verilerinizi Blob depolamada kapsayıcı yollarını belirleyin.
* Kaynak depolama hesabınızı hello Azure portal kullanarak bir dışa aktarma işi oluşturma veya içeri/dışarı aktarma REST API hello.
* Kaynak BLOB'ları hello veya iş verilerinizin hello kapsayıcısı yollarının verme belirtin.
* Merhaba sürücüleri geri tooyou aktarma için kullanılan toobe için Hello dönüş adresi ve taşıyıcı hesap numarası sağlayın.
* Proje oluşturma sırasında sağlanan adresi sevkiyat sevk hello sabit disk sürücülerinin toohello.
* İzleme numarası hello dışa aktarma işi ayrıntıları hello teslim güncelleştirin ve hello dışa aktarma işi göndermek.
* Merhaba sürücüleri alınan ve hello Azure veri merkezinde işlenebilir.
* BitLocker ile şifrelenmiş Hello sürücüleri; Merhaba anahtarları hello Azure portal kullanılabilir.  
* Merhaba sürücüleri hello alma işi sağlanan, taşıyıcı hesap toohello dönüş adresi kullanılarak aktarılır.
  
    ![Şekil 2:Export iş akışı](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>İş ve sürücü durumunu görüntüleme
Alma hello durumunu izlemek veya işleri hello Azure portal ' dışa aktarın. Merhaba tıklatın **içeri/dışarı aktarma** sekmesi. İşleriniz listesini hello sayfasında görüntülenir.

![Görünüm iş durumu](./media/storage-import-export-service/jobstate.png)

İş durumları sürücünüze hello işleminde olduğu bağlı olarak aşağıdaki hello birini görürsünüz.

| İş durumu | Açıklama |
|:--- |:--- |
| Oluşturma | Bir işi oluşturulduktan sonra durumu tooCreating ayarlanır. Merhaba iş hello oluşturma durumu olsa da, hello içeri/dışarı aktarma hizmeti hello sürücüleri sevk edilen toohello veri merkezi edilmemiş varsayar. Bir işi daha sonra otomatik olarak hello hizmeti tarafından silinir tootwo hafta yedeklemek için hello oluşturma durumunda kalabilir. |
| Aktarma | Paketinizi sevk sonra izleme bilgilerini hello Azure portal'ın hello güncelleştirmeniz gerekir.  Bu hello iş "İçine aktarma" açın. Merhaba iş tootwo hafta yedeklemek için hello sevkiyat durumunda kalır. 
| Alınan | Tüm sürücüler hello veri merkezinde alınmış olan sonra hello iş durumu toohello alınan ayarlanır. |
| Aktarma | En az bir sürücü işleme başladıktan sonra hello iş durumu toohello ayarlanacak aktarma. Merhaba sürücü durumları görmek için ayrıntılı bilgi bölümü altında. |
| Paketleme | Tüm sürücüler işlemeyi tamamladıktan sonra sevk edilen geri tooyou hello sürücülerdir kadar hello iş hello paketleme durumda yerleştirilir. |
| tamamlandı | Merhaba iş hatasız tamamladıysa tüm sürücüler sevk edilen geri toohello müşteri eklendikten sonra hello iş toohello tamamlandı durumuna ayarlanır. Merhaba iş hello tamamlandı durumu 90 gün sonra otomatik olarak silinir. |
| Kapalı | Hello iş hello işleme sırasında hataları olmuştur, tüm sürücüleri sevk edilen geri toohello müşteri eklendikten sonra hello iş toohello kapalı duruma ayarlanır. Merhaba iş hello kapalı durumda otomatik olarak 90 gün sonra silinir. |

bir içe veya dışa aktarma işi ile geçiş yapıldığı gibi ayrı ayrı bir sürücü hello yaşam döngüsünü hello tabloda açıklanmaktadır. bir işi her sürücüde geçerli durumunu Hello şimdi Azure portal hello görünür olur.
Merhaba aşağıdaki tabloda her bir iş sürücüde geçirir her durum açıklanmaktadır.

| Sürücü durumu | Açıklama |
|:--- |:--- |
| Belirtilen | Merhaba iş hello Azure portal, oluşturulduğunda bir içeri aktarma işi için bir sürücü için hello ilk durumu hello belirtilen durumudur. Hiçbir sürücü Hello iş oluşturulduğunda, belirtilen bu yana bir dışa aktarma işi için hello ilk sürücü durumu hello alınan durumudur. |
| Alınan | Merhaba içeri/dışarı aktarma hizmeti işleci şirket içe aktarma işi için sevkiyat hello öğesinden alınan hello sürücüleri işlendiğinde hello sürücü toohello alınan durumuna geçiş yapar. Bir dışarı aktarma işi için hello ilk sürücü durumu hello alınan durumudur. |
| NeverReceived | Merhaba sürücü toohello NeverReceived durumu bir iş için başlangıç paketi ulaşır ancak hello paket hello sürücü içermiyor taşınır. İki hafta hello hizmeti hello Sevkiyat bilgileri aldı, ancak hello paket henüz hello veri merkezinde geldi değil bu yana olması durumunda bir sürücü de bu duruma taşıyabilirsiniz. |
| Aktarma | Merhaba sürücü tooWindows Azure Storage tootransfer verileri Hello hizmeti başladığında, bir sürücü toohello aktarma durumu taşınır. |
| tamamlandı | Merhaba hizmeti başarıyla hatasız tüm hello veri aktarıldığında bir sürücü toohello tamamlandı durumu taşınır.
| CompletedMoreInfo | Bir sürücü toohello hello hizmeti bazı sorunlar veri kopyalanırken herhangi birinden karşılaştığında CompletedMoreInfo durumu veya toohello sürücü taşınır. Merhaba bilgi hataları, uyarıları veya BLOB üzerine hakkında bilgilendirici iletileri ekleyebilirsiniz.
| ShippedBack | Merhaba veri merkezi geri toohello dönüş adresinden gönderilen zaman hello sürücü toohello ShippedBack durumu taşınır. |

Hello Azure portal bu görüntüden hello sürücü bir örnek iş durumunu görüntüler:

![Sürücü durumunu görüntüle](./media/storage-import-export-service/drivestate.png)

Merhaba aşağıdaki tabloda hello sürücü hata durumları ve her durum için yapılan hello eylemler açıklanmaktadır.

| Sürücü durumu | Olay | Çözümleme / sonraki adım |
|:--- |:--- |:--- |
| NeverReceived | (Merhaba işin sevkiyat bir parçası olarak alınmadı çünkü) başka bir sevkiyat NeverReceived ulaşan olarak işaretlenmiş bir sürücü. | Merhaba işletim ekibi hello sürücü toohello alınan durum taşınır. |
| Yok | Başka bir iş parçası olarak hello veri merkezindeki herhangi bir işi parçası olmayan bir sürücü ulaşır. | Merhaba sürücü fazladan bir sürücü olarak işaretlenir ve hello özgün paket ile ilişkili hello iş tamamlandığında toohello müşteri döndürülür. |

### <a name="time-tooprocess-job"></a>Süresi tooprocess işi
içeri/dışarı aktarma işi değişir sevkiyat zaman, proje türü gibi farklı etkenlere bağlı olarak tooprocess geçen süre hello miktarı yazın ve hello kopyalanan verileri ve hello sağlanan hello disk boyutu boyutu. Merhaba içeri/dışarı aktarma hizmeti bir SLA yok ancak hello diskleri alındıktan sonra hello hizmet toocomplete hello kopyalama 7 too10 gün içinde çalışır.. Merhaba REST API tootrack hello ilerleyişini daha yakından kullanabilirsiniz. Merhaba kopyalama devam eden bir gösterge sağlayan listesi işleri işlemi yüzde tam parametresi yok. Tahmin toocomplete süresi kritik içeri/dışarı aktarma işi gerekiyorsa toous ulaşın.

### <a name="pricing"></a>Fiyatlandırma
**İşleme ücret sürücü**

Alma işleminizin bir parçası olarak işlenen her bir sürücü için bir sürücü işleme ücret yoktur veya iş dışa aktarın. Merhaba üzerinde Hello ayrıntıları görmek [Azure içeri/dışarı aktarma fiyatlandırma](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Sevkiyat maliyetleri**

Sürücüleri tooAzure sevk ettiğinizde, maliyet toohello Sevkiyat taşıyıcı sevkiyat hello ücret ödersiniz. Microsoft hello sürücüleri tooyou geri döndüğünde, maliyet sevkiyat hello hello işi oluşturma sırasında sağlanan toohello taşıyıcı hesap ücretlendirilir.

**İşlem maliyetleri**

Blob depolama alanına veri içe aktarırken hiçbir işlem maliyetleri vardır. blob depolama alanından verileri verildiğinde hello standart çıkış ücretleri uygulanabilir. İşlem maliyetleri hakkında daha fazla bilgi için bkz: [veri aktarımı fiyatlandırmasını.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Hızlı Başlangıç
Bu bölümde, bir içeri aktarma ve dışarı aktarma işini oluşturmak için adım adım yönergeler sağlar. Lütfen tüm hello karşıladığından emin olun [ön koşullar](#pre-requisites) ilerleyen önce.

> [!IMPORTANT]
> Merhaba hizmet alma başına bir standart depolama hesabı destekler veya iş dışarı aktarın ve premium depolama hesaplarını desteklemiyor. 
> 
> 
## <a name="create-an-import-job"></a>Bir içeri aktarma işi oluşturma
Veri toohello belirtilen veri merkezi içeren bir veya daha fazla sürücüler sevkiyat tarafından sabit sürücülerden bir içeri aktarma işi toocopy veri tooyour Azure depolama hesabı oluşturun. Merhaba alma işi iletir sabit disk sürücüleriyle ilgili ayrıntıları, veri toobe kopyalanır, hedef depolama hesabı ve bilgi toohello Azure içeri/dışarı aktarma hizmeti aktarma. İçe aktarma işi oluşturma üç adımlık bir işlemdir. İlk olarak, hello WAImportExport aracını kullanarak sürücülerinizin hazırlayın. İkinci olarak, hello Azure portal kullanarak bir içeri aktarma işi gönderin. Üçüncü iş oluşturma ve güncelleştirme hello bilgileri, iş ayrıntılarını aktarma sırasında sağlanan adresi sevkiyat hello sürücüleri toohello birlikte.   

### <a name="prepare-your-drives"></a>Sürücülerinizin hazırlama
Hello Azure içeri/dışarı aktarma hizmeti kullanarak veriyi içeri aktarma tooprepare olduğunda ilk adımı hello WAImportExport aracını kullanarak sürücülerinizin hello. Tooprepare Hello adımları sürücülerinizin izleyin.

1. İçeri aktarılan hello veri toobe tanımlayın. Bu, dizinleri ve tek başına dosya hello yerel sunucuda veya bir ağ paylaşımı olabilir.  
2. Merhaba verilerin toplam boyutu bağlı olarak gerekir sürücüleri Hello sayısını belirler. Gerekli hello sayısı 2,5 inç SSD veya 2,5" ya da 3,5" SATA II veya III sabit disk sürücüsü temin edin.
3. Merhaba hedef depolama hesabı, kapsayıcı, sanal dizinleri ve blobları tanımlayın.
4.  Merhaba dizinler ve/veya kopyalanan tooeach sabit disk sürücüsü olacaktır bağımsız dosyaları belirler.
5.  Merhaba, veri kümesi ve driveset için CSV dosyaları oluşturun.
    
    **Veri kümesi CSV dosyası**
    
    Aşağıda bir örnek veri kümesi CSV dosyası örneği verilmiştir:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    Yukarıdaki örnek Hello 100M_1.csv.txt kopyalanan toohello kök "containername" adlı hello kapsayıcısının olacaktır. Merhaba kapsayıcı adı "containername" mevcut değilse tane oluşturulur. Tüm dosya ve klasörlerin 50M_original altında kopyalanan yinelemeli olarak toocontainername olacaktır. Klasör yapısı korunur.

    Daha fazla bilgi edinmek [hello veri kümesi CSV dosyası hazırlama](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Unutmayın**: varsayılan olarak, blok Blobları hello veriler alınır. Sayfa Blobları hello BlobType alan değeri tooimport verileri kullanabilirsiniz. Örneğin, bir Azure VM diskleri olarak bağlanacaktır VHD dosyaları alıyorsanız, bunları sayfa BLOB olarak aktarmalısınız.

    **Driveset CSV dosyası**

    diskleri toowhich hello sürücü harflerini hello listesini içeren bir CSV dosyası hello aracı toocorrectly sırada eşlendi bayrağı olan hello driveset Hello değeri hazır diskler toobe hello listesini seçin. 

    Merhaba driveset CSV dosyası örneği aşağıdadır:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    Yukarıdaki örnek Hello iki diskleri bağlı ve temel NTFS birimleri birim harfi G:\ ve H:\ ile oluşturulan varsayılır. Merhaba aracı biçimlendirmek ve H:\ barındıran değil biçimlendirmek ve hello disk birimi G:\ barındırma şifrelemek hello disk şifreleyebilirsiniz.

    Daha fazla bilgi edinmek [hello driveset CSV dosyası hazırlama](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Kullanım hello [WAImportExport aracı](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy veri tooone ya da daha fazla sabit disk sürücüler.
7.  Şifreleme alanda drivset CSV tooenable BitLocker şifrelemesi hello sabit disk sürücüsünde, "Şifrele" belirtebilirsiniz. Alternatif olarak, de el ile Merhaba sabit disk sürücüsünde BitLocker şifrelemesini etkinleştirmek "AlreadyEncrypted" belirtin ve hello Aracı çalıştırırken hello driveset CSV hello anahtarında sağlayın.

8. Merhaba veri hello sabit disk sürücülerini veya hello günlük dosyası disk hazırlığı tamamladıktan sonra değişiklik yapmayın.

> [!IMPORTANT]
> Hazırlık her sabit disk sürücüsü bir günlük dosyasında neden olur. Hello Azure portal kullanarak hello alma işi oluştururken bu içeri aktarma işinin bir parçası olan hello sürücüleri tüm hello günlük dosyalarını yüklemeniz gerekir. Günlük dosyaları işlenmeyecek sürücüleri.
> 
>

Aşağıda hello komutlar ve hello sabit disk sürücüsü hazırlamaya yönelik örnekler WAImportExport aracı kullanıyorsunuz.

WAImportExport aracı PrepImport komutu hello için oturumu toocopy dizinler ve/veya yeni bir kopya oturum dosyalarıyla ilk kopyalayın:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**İçeri aktarma örnek 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Sırayla çok**daha fazla sürücü ekleme**, bir yeni bir driveset dosyası oluşturun ve hello komutu aşağıdaki gibi çalıştırın. Sonraki kopyalama oturumları toohello farklı sabit sürücüler için belirtilenden InitialDriveset .csv dosyasında, yeni bir driveset CSV dosyası belirtin ve bir değer toohello parametresi "AdditionalDriveSet" sağlayın. Kullanım hello **aynı günlük dosyası** adlandırın ve sağlayan bir **yeni oturum kimliği**. Merhaba AdditionalDriveset CSV dosyasının InitialDriveSet biçimi olarak aynı biçimidir.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Örnek 2 alma**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

Sipariş tooadd ek veri toohello içinde aynı driveset WAImportExport aracı PrepImport komut sonraki kopyalama oturumları toocopy ek dosyalar/dizin için çağrılabilir: aynı sabit disk sürücüleri sonraki kopyalama oturumları toohello belirtildiği için InitialDriveset .csv dosya, hello belirtin **aynı günlük dosyası** adlandırın ve sağlayan bir **yeni oturum kimliği**; gerek tooprovide hello depolama hesabı anahtarı yok.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Örnek 3 alma**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Merhaba WAImportExport aracını kullanma hakkında daha fazla ayrıntı görmek [sabit sürücüler alma işlemi için hazırlanıyor](storage-import-export-tool-preparing-hard-drives-import.md).

Ayrıca, toohello başvuru [örnek iş akışı tooprepare sabit sürücülerini içeri aktarma işi](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) daha ayrıntılı adım adım yönergeler için.  

### <a name="create-hello-import-job"></a>Merhaba alma işi oluşturma
1. Sürücünüzün hazır olduktan sonra tooyour depolama hesabında hello Azure portalına gidin ve hello Pano görüntüleyin. Altında **Hızlı Bakış**, tıklatın **bir içeri aktarma işi oluşturma**. Merhaba adımlarını gözden geçirin ve hello onay kutusunu tooindicate sürücünüze hazırladıktan ve hello sürücü günlük dosyasının kullanılabilir olduğunu seçin.
2. Adım 1'de, bu alma işi ve geçerli bir dönüş adresi sorumlu hello kişi için kişi bilgilerini sağlayın. Hello içe aktarma işi için ayrıntılı günlük verileri toosave istiyorsanız hello seçeneği çok denetleyin**Kaydet hello ayrıntılı günlük my 'waimportexport' blob kapsayıcısında**.
3. 2. adımda hello sürücü hazırlık adımında elde ettiğiniz hello sürücü günlük dosyalarını karşıya yükleyin. Hazırladığınız her bir sürücü için bir dosya tooupload gerekir.
   
   ![Adım 3 - içe aktarma işi oluşturma](./media/storage-import-export-service/import-job-03.png)
4. Adım 3'te hello içe aktarma işi için açıklayıcı bir ad girin. Girdiğiniz hello adı içerebilir yalnızca küçük harfler, sayılar, tire ve alt çizgi, bir harf ile başlamalı ve boşluk içeremez unutmayın. Devam eden ve bunlar tamamlandığında durumdayken işleriniz tootrack seçin hello adını kullanacaksınız.
   
   Ardından, veri merkezi bölgenizi hello listeden seçin. Merhaba veri merkezi bölgesi hello veri merkezi ve paketinizi hazırlamalısınız toowhich adresini belirtir. Daha fazla bilgi için aşağıda Hello SSS bakın.
5. 4. adım, dönüş taşıyıcı hello listeden seçin ve taşıyıcı hesap numaranızı girin. Microsoft, içe aktarma işi tamamlandıktan sonra bu hesabı tooship hello sürücüleri geri tooyou kullanır.
   
   İzleme numaranız varsa, teslim taşıyıcı hello listeden seçin ve izleme numaranızı girin.
   
   Sayı henüz seçin izleme yoksa **my paket sevk olan sonra bu içeri aktarma işi için sevkiyat bilgilerimi sağlayacak**, hello alma işlemini tamamlamak.
6. paketinizin gönderilen sonra izleme numaranızı tooenter dönmek toohello **içeri/dışarı aktarma** sayfasında hello Azure portalı içinde depolama hesabınız için işinizi hello listeden seçin ve Seç **Sevkiyat bilgisi**. Merhaba sihirbazda gidin ve 2. adımda izleme numaranızı girin.
   
    İzleme numarası hello hello iş oluşturma 2 hafta içinde güncelleştirilmezse hello işin süresi dolar.
   
    Merhaba iş hello oluşturma, sevkiyat veya aktarma durumda ise, taşıyıcı hesap numaranızı adım 2'deki hello Sihirbazı'nın da güncelleştirebilirsiniz. Merhaba iş hello paketleme durumda olduğunda, taşıyıcı hesap numaranızı iş güncelleştirilemiyor.
7. Merhaba portal panosunda, işin ilerleme durumunu izleyebilirsiniz. Her iş durumu hello önceki bölümdeki tarafından anlamı bkz [işi durumunu görüntüleme](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Bir dışarı aktarma işi oluşturma
Bir dışarı aktarma işi toonotify Merhaba, bir sevkiyat veya veri depolama hesabı toohello sürücülerden aktarılabilir ve ardından sevk edilen tooyou hello sürücüleri böylece daha fazla boş sürücüleri toohello veri merkezi içeri/dışarı aktarma hizmeti oluşturun.

### <a name="prepare-your-drives"></a>Sürücülerinizin hazırlama
Aşağıdaki ön denetimleri sürücülerinizin dışa aktarma işi için hazırlamak için önerilir:

1. Merhaba WAImportExport aracın PreviewExport komutunu kullanarak gerekli disk Hello sayısını denetleyin. Daha fazla bilgi için bkz: [bir dışarı aktarma işi için sürücü kullanımı Önizleme](https://msdn.microsoft.com/library/azure/dn722414.aspx). Seçtiğiniz hello BLOB'lar için sürücü kullanımı önizlemesini yardımcı olur, hello hello sürücüleri boyutuna göre toouse adımıdır.
2. Okuma/hello dışa aktarma işi için gönderilen toohello sabit sürücü yazabilir olduğunu denetleyin.

### <a name="create-hello-export-job"></a>Merhaba dışa aktarma işi oluşturma
1. toocreate bir dışarı aktarma işinin tooyour depolama hesabında hello Azure portalına gidin ve hello Pano görüntüleyin. Altında **Hızlı Bakış**, tıklatın **bir dışarı aktarma işi oluşturma** ve hello sihirbazdaki adımları izleyin.
2. Adım 2'de bu dışarı aktarma işi için hello sorumlu için kişi bilgilerini sağlayın. Merhaba dışa aktarma işi için toosave ayrıntılı günlük verileri istiyorsanız hello seçeneği çok denetleyin**Kaydet hello ayrıntılı günlük my 'waimportexport' blob kapsayıcısında**.
3. Adım 3'te hangi blob depolama hesabı tooyour boş iken tooexport istediğiniz verileri sürücü veya sürücüler belirtin. Merhaba depolama hesabında tüm blob verilerini tooexport seçebilirsiniz veya BLOB veya BLOB tooexport ayarlar belirtebilirsiniz.
   
   toospecify bir blob tooexport kullanmak hello **eşit** Seçicisi ve hello kapsayıcı adı ile başlayan, hello göreli yol toohello blob belirtin. Kullanım *$root* toospecify hello kök kapsayıcı.
   
   toospecify tüm BLOB'ların kullanımı hello bir önek ile başlayan **ile başlar** Seçicisi ve eğik çizgiyle başlayan hello öneki belirtin '/'. Merhaba önek hello önek hello kapsayıcı adı, hello tam kapsayıcı adı veya hello blob adı hello öneki tarafından izlenen hello tam kapsayıcı adı olabilir.
   
   Aşağıdaki tablonun hello geçerli blob yolu örnekleri gösterilmektedir:
   
   | Seçici | BLOB yolu | Açıklama |
   | --- | --- | --- |
   | İle başlar |/ |Merhaba depolama hesabındaki tüm BLOB'lar verir |
   | İle başlar |/$root / |Merhaba kök kapsayıcıdaki tüm blob'lara verir |
   | İle başlar |/Book |Önek ile başlayan tüm kapsayıcıdaki tüm blob'lara aktarır **rehberi** |
   | İle başlar |/Music/ |Kapsayıcıdaki tüm blob'lara aktarır **müzik** |
   | İle başlar |/ Müzik/love |Kapsayıcıdaki tüm blob'lara aktarır **müzik** önek ile başlayan **memnuniyet** |
   | Çok eşit|$root/logo.bmp |Dışarı aktarma blob **logo.bmp** hello kök kapsayıcısında |
   | Çok eşit|Videos/Story.mp4 |Dışarı aktarma blob **story.mp4** kapsayıcısında **videolar** |
   
   Merhaba blob geçerli biçimler yollarında tooavoid hataları işleme sırasında bu ekran görüntüsünde gösterildiği gibi sağlamalısınız.
   
   ![Adım 3 dışa aktarma işi - oluşturma](./media/storage-import-export-service/export-job-03.png)
4. Adım 4'te hello dışa aktarma işi için açıklayıcı bir ad girin. Girdiğiniz hello adı içerebilir yalnızca küçük harfler, sayılar, tire ve alt çizgi, bir harf ile başlamalı ve boşluk içeremez.
   
   Merhaba veri merkezi bölgesi paketinizi hazırlamalısınız hello veri merkezi toowhich belirtir. Daha fazla bilgi için aşağıda Hello SSS bakın.
5. 5. adım, dönüş taşıyıcı hello listeden seçin ve taşıyıcı hesap numaranızı girin. Microsoft, bu hesabı tooship kullanacak, dışa aktarma işi tamamlandıktan sonra sürücülerinizin tooyou yedekleyin.
   
   İzleme numaranız varsa, teslim taşıyıcı hello listeden seçin ve izleme numaranızı girin.
   
   Sayı henüz seçin izleme yoksa **my paket sevk olan sonra bu dışarı aktarma işi için sevkiyat bilgilerimi sağlayacak**, hello dışarı aktarma işlemini tamamlamak.
6. paketinizin gönderilen sonra izleme numaranızı tooenter dönmek toohello **içeri/dışarı aktarma** sayfasında hello Azure portalı içinde depolama hesabınız için işinizi hello listeden seçin ve Seç **Sevkiyat bilgisi**. Merhaba sihirbazda gidin ve 2. adımda izleme numaranızı girin.
   
    İzleme numarası hello hello iş oluşturma 2 hafta içinde güncelleştirilmezse hello işin süresi dolar.
   
    Merhaba iş hello oluşturma, sevkiyat veya aktarma durumda ise, taşıyıcı hesap numaranızı adım 2'deki hello Sihirbazı'nın da güncelleştirebilirsiniz. Merhaba iş hello paketleme durumda olduğunda, taşıyıcı hesap numaranızı iş güncelleştirilemiyor.
   
   > [!NOTE]
   > Merhaba blob toobe dışarı toohard sürücü kopyalama hello zaman kullanılıyorsa, Azure içeri/dışarı aktarma hizmeti hello blob ve kopyalama hello anlık görüntüsünü alın.
   > 
   > 
7. Merhaba Panoda hello Azure portal, işin ilerleme durumunu izleyebilirsiniz. Her iş durumu hello önceki bölümde anlamı bkz üzerinde "görüntüleme, iş durumunu".
8. Merhaba sürücüler, dışarı aktarılan verilerle aldıktan sonra görüntülemek ve sürücünüzün hello hizmeti tarafından oluşturulan hello BitLocker anahtarları kopyalayın. Tooyour depolama hesabında hello Azure portalına gidin ve hello içeri/dışarı aktarma sekmesini tıklatın. Dışarı aktarma işini hello listeden seçin ve hello görünümü anahtarlarını düğmesine tıklayın. Merhaba BitLocker anahtarları, aşağıda gösterildiği gibi görünür:
   
   ![BitLocker anahtarları dışa aktarma işi için görüntüleme](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Müşterilere işbu hizmeti kullanırken karşılaştığınız hello en yaygın soruları kapsar Lütfen aracılığıyla aşağıdaki hello SSS bölümüne gidin.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

**Hello Azure içeri/dışarı aktarma hizmetini kullanarak Azure File storage kopyalayabilir miyim?**

Hayır, hello Azure içeri/dışarı aktarma hizmeti yalnızca blok Blobları ve sayfa Bloblarını destekler. Azure File storage, Table Storage ve kuyruk depolama dahil diğer tüm depolama türleri desteklenmez.

**Hello Azure içeri/dışarı aktarma hizmeti için CSP abonelikler var mı?**

Azure içeri/dışarı aktarma hizmeti CSP abonelikleri desteklemiyor.

**İçe aktarma işi için hello sürücü hazırlık adımı atlayabilirsiniz veya kopyalamadan t bir sürücü hazırlayabilirsiniz?**

Hello Azure WAImportExport aracını kullanarak verileri almak için tooship istediğiniz herhangi bir sürücü hazırlanması gerekir. Merhaba WAImportExport aracı toocopy veri toohello sürücüsü kullanmanız gerekir.

**Tooperform tüm disk hazırlığı bir dışarı aktarma işinin oluştururken ihtiyacım var mı?**

Yoktur, ancak bazı ön denetimleri önerilir. Merhaba WAImportExport aracın PreviewExport komutunu kullanarak gerekli disk Hello sayısını denetleyin. Daha fazla bilgi için bkz: [bir dışarı aktarma işi için sürücü kullanımı Önizleme](https://msdn.microsoft.com/library/azure/dn722414.aspx). Seçtiğiniz hello BLOB'lar için sürücü kullanımı önizlemesini yardımcı olur, hello hello sürücüleri boyutuna göre toouse adımıdır. Ayrıca, okuyabileceği onay ve Merhaba sevk yazma toohello sabit sürücü iş verin.

**I yanlışlıkla toohello uymuyor bir HDD gönderirseniz olanlar gereksinimleri destekleniyor mu?**

Hello Azure veri merkezi desteklenen toohello gereksinimleri tooyou uymuyor hello sürücü döndürür. Yalnızca bazı hello sürücüleri hello paketindeki hello destek gereksinimlerini karşılayan bu sürücüleri işlenir ve hello gereksinimleri karşılamayan hello sürücüleri tooyou döndürülür.

**İşim iptal edebilir miyim?**

Durumunu oluştururken veya sevkiyat bir işi iptal edebilirsiniz.

**Ne kadar süreyle hello tamamlanmış işlerin durumunu hello Azure portalında görebilir miyim?**

Too90 gün için tamamlanan işler hello durumunu görüntüleyebilirsiniz. Tamamlanan İşler 90 gün sonra silinir.

**Tooimport istediğiniz veya 10'dan fazla sürücüleri dışarı aktarma, ne yapmalıyım?**

Bir içeri aktarma veya dışarı aktarma işini hello içeri/dışarı aktarma hizmeti için tek bir işi yalnızca 10 sürücüleri başvuru. 10'dan fazla sürücüleri tooship istiyorsanız, birden çok işleri oluşturabilirsiniz. Aynı iş birlikte içinde sevk edilmesi hello ilişkilendirilmiş sürücüleri aynı paketin hello.
Microsoft, işler Kılavuzu ve veri kapasitesi birden çok disk yayıldığında Yardım alma sunar. Temasa bulkimport@microsoft.com daha fazla bilgi için

**Bunları dönmeden önce hizmet biçimindeki hello sürücüleri hello mu?**

Hayır. Tüm sürücüler BitLocker ile şifrelenmiş.

**Sürücüleri içeri/dışarı aktarma işleri için Microsoft'tan satın alabilir?**

Hayır. Her ikisi için de kendi sürücüler içeri ve işleri dışarı aktarma tooship gerekir.

** Bu hizmet ** tarafından alınan veri nasıl erişebilir mi

Merhaba verileri Azure depolama hesabınızın altında hello Azure Portal erişilebilir veya ayrı bir araç kullanarak Depolama Gezgini çağrılır. https://docs.microsoft.com/en-us/Azure/VS-Azure-Tools-Storage-Manage-With-Storage-Explorer 

**Merhaba alma işi tamamlandıktan sonra ne hello depolama hesabında my veri görünümü ister? Belgelerim dizini hiyerarşi korunur?**

Bir sabit sürücü içeri aktarma işi için hazırlarken hello hedef veri kümesi CSV hello DstBlobPathOrPrefix alanında belirtilir. Merhaba hedef hello sabit sürücüsünden veri kopyalanır hello depolama hesabı toowhich kapsayıcısında budur. Bu hedef kapsayıcı içindeki hello sabit sürücüden klasörler için oluşturulan sanal dizinleri ve blobları dosyaları için oluşturulur. 

**Merhaba hizmet Hello sürücüsünde depolama Hesabımı zaten mevcut dosyaların varsa, varolan depolama Hesabımı blobları üzerine mi Yazar?**

Merhaba sürücü hazırlanırken hello hedef dosyaların üzerine yazılacağını veya değerlendirme adlı veri kümesini CSV dosyasında hello alanını kullanarak göz ardı belirtebilirsiniz: < yeniden adlandırma | Hayır üzerine | üzerine >. Varsayılan olarak, hello hello yeni dosyaları yeniden adlandırmak yerine hizmetini mevcut bloblarının üzerine yazmayı.

**Merhaba WAImportExport aracının 32-bit işletim sistemleriyle uyumlu mu?**
Hayır. Merhaba WAImportExport aracı yalnızca 64-bit Windows işletim sistemleriyle uyumlu değil. Lütfen hello toohello işletim sistemleri bölümüne başvurun [ön koşullar](#pre-requisites) desteklenen işletim sistemi sürümleri tam bir listesi.

**My paketinde hello sabit disk sürücüsü dışında her şey eklemeliyim?**

Lütfen yalnızca sabit sürücülerinizin birlikte. Güç kaynağı kabloları veya USB kablosu gibi öğeleri dahil etmeyin.

**Tooship FedEx veya DHL kullanarak my sürücüleri var mı?**

Sürücüleri toohello veri merkezi FedEx, DHL, UPS veya ABD posta hizmeti gibi bilinen bir taşıyıcı kullanarak gönderebilirsiniz. Ancak, sevkiyat hello sürücüleri geri tooyou için hello veri merkezi, ABD ve AB hello FedEx hesap numarasındaki ya da hello Asya ve Avustralya bölgeler DHL hesap numarası sağlamalısınız.

**Sürücümün uluslararası sevkiyat ile herhangi bir kısıtlama var mı?**

Lütfen, yayımlayan hello fiziksel ortam toocross uluslararası sınırların gerekebileceğini unutmayın. Fiziksel ortam ve veri içe aktarılan ve/veya hello ilgili yasalarına uygun olarak dışarı olduğunu sağlamaktan sorumludur. Merhaba fiziksel ortam göndermeden önce medya ve veri sevk edilen toohello tanımlanan veri merkezi yasal olabilir, danışmanlar tooverify ile denetleyin. Bu, Microsoft zamanında ulaştığında tooensure yardımcı olur.

**Bir işi oluştururken, sevkiyat adresini hello my depolama hesabı konumdan farklı bir konumdur. Ne yapmalıyım?**

Bazı depolama hesabı konumları sevkiyat eşlenen tooalternate konumlardır. Daha önce kullanılabilir sevkiyat konumları geçici olarak eşlenmiş tooalternate konumları da olabilir. Her zaman sürücülerinizin teslim etmeden önce işi oluşturma sırasında sağlanan adresi sevkiyat hello denetleyin.

**Sürücümün sevkiyat yapılırken hello taşıyıcı hello veri merkezi iletişim adresi ve telefon numarası için sorar. Ne ı sağlamanız gerekir?**

Merhaba telefon numarası ve DC adresi iş oluşturmanın bir parçası sağlanır.

**Hello Azure içeri/dışarı aktarma hizmeti toocopy PST posta kutuları ve SharePoint veri tooO365 kullanabilir miyim?**

Lütfen çok başvurun[alma PST dosyaları veya SharePoint veri tooOffice 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**My yedeklemeleri çevrimdışı toohello Azure Backup hizmeti hello Azure içeri/dışarı aktarma hizmeti toocopy kullanabilir miyim?**

Lütfen çok başvurun[Çevrimdışı Yedekleme iş akışı Azure Yedekleme'de](../../backup/backup-azure-backup-import-export.md).

**Merhaba en fazla sayıda HDD için bir sevkiyat içinde nedir?**

Herhangi bir sayıda HDD bir sevkiyat olabilir ve hello diskleri toomultiple işleri aitse önerilen çok bir) hello karşılık gelen iş adlarıyla etiketli hello diske sahip. b) -1 ile sonekine izleme numarası olan güncelleştirme hello işleri-2 vb..
  
**Merhaba en fazla blok blobu ve sayfa Blob Disk içeri/dışarı aktarma tarafından desteklenen boyutu nedir?**

En fazla blok blobu boyutudur yaklaşık 4.768TB veya 5,000,000 MB.
En fazla sayfa Blob boyutu 1 TB'tır.

**Disk içeri/dışarı aktarma AES 256 şifrelenmesini destekliyor mu?**

AES 128 bitlocker şifrelemesi ile Azure içeri/dışarı aktarma hizmeti varsayılan olarak şifreler, ancak veri kopyalamadan önce el ile bitlocker ile şifreleyerek bu artan tooAES 256 olabilir. 

Kullanıyorsanız [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), aşağıda bir örnek komut verilmiştir
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Kullanıyorsanız [WAImportExport aracı](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) "AlreadyEncrypted" belirtin ve hello driveset CSV hello anahtarında sağlayın.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba WAImportExport aracı ayarlama](storage-import-export-tool-how-to.md)
* [Merhaba AzCopy komut satırı yardımcı programı ile veri aktarımı](storage-use-azcopy.md)
* [Azure alma verme REST API örnek](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

