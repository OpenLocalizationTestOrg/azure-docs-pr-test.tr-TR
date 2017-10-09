---
title: "SQL Server Yedekleme ve geri yükleme için Azure depolama aaaHow toouse | Microsoft Docs"
description: "Bilgi nasıl tooback SQL Server tooAzure depolama ayarlama. SQL veritabanları tooAzure depolama yedekleme hello yararlarını açıklar."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>SQL Server Yedekleme ve geri yükleme için Azure Storage kullanma
## <a name="overview"></a>Genel Bakış
SQL Server 2012 SP1 CU2 ile başlayarak, artık SQL Server yedekleri doğrudan toohello Azure Blob Depolama hizmetinin yazabilirsiniz. Bu işlevselliği tooback tooand yedekten geri hello Azure Blob hizmeti oluşturan bir şirket içi SQL Server veritabanı veya bir Azure sanal makinesinde SQL Server veritabanı ile kullanabilirsiniz. Yedekleme toocloud hello buluttan kullanılabilirlik, coğrafi olarak çoğaltılmış sınırsız şirket dışı depolama ve veri tooand geçişini kolaylığı avantajları sunar. Transact-SQL veya SMO kullanarak yedekleme veya geri yükleme deyimleri verebilir.

SQL Server 2016 yeni özellikleri sunar; kullanabileceğiniz [dosya anlık görüntüsü backup](http://msdn.microsoft.com/library/mt169363.aspx) tooperform neredeyse anlık yedeklemeler ve son derece hızlı geri yükler.

Bu konuda neden toouse SQL yedeklemeler için Azure depolama seçebilir ve ilgili hello bileşenleri açıklar açıklanmaktadır. Sonunda hello hello makale tooaccess izlenecek yollar ve bu hizmet, SQL Server Yedekleme ile kullanarak ek bilgi toostart sağlanan hello kaynakları kullanabilir.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Kullanma hello Azure Blob hizmeti SQL Server yedekleri için avantajları
SQL Server'ı yedeklerken yüz çeşitli zorluklar mevcuttur. Bu zorluklar Depolama Yönetimi, depolama hatası riskini dahil, erişim toooff site depolama alanı ve donanım yapılandırması. Bu zorluklar çoğunu hello Azure Blob Depolama hizmeti için SQL Server Yedekleme kullanarak ele alınmıştır. Aşağıdaki yararları hello göz önünde bulundurun:

* **Kullanım kolaylığı**: Azure BLOB'ları yedekleri depolamak kullanışlı, esnek ve kolay tooaccess site dışındaki bir seçenek olabilir. SQL Server Yedeklemelerinizin varolan değiştirme olarak kadar kolay için şirket dışı depolama oluşturulurken betikleri/işleri toouse hello **yedekleme tooURL** sözdizimi. Şirket dışı depolama, genellikle site dışındaki hello ve üretim veritabanını konumları etkileyebilecek tek bir olağanüstü durum yetecek kadar hello üretim veritabanı konumu tooprevent olmalıdır. Çok seçerek[coğrafi çoğaltılır, Azure BLOB '](../../../storage/common/storage-redundancy.md), hello hello tüm bölge etkileyebilecek bir olağanüstü durumda fazladan bir koruma katmanı vardır.
* **Yedekleme arşiv**: hello Azure Blob Depolama hizmeti daha iyi bir alternatif toohello sık kullanılan bant seçeneği tooarchive yedeklemeler sunar. Bant Depolama fiziksel taşıma tooan site dışındaki tesis ve ölçüleri tooprotect hello medya gerektirebilir. Yedeklemelerinizin Azure Blob Storage'da depolamak, anlık sağlar, yüksek oranda kullanılabilir ve bir dayanıklı arşivleme seçeneği.
* **Yönetilen donanım**: olmamasıdır Azure hizmetleriyle donanım Yönetimi yoktur. Azure Hizmetleri hello donanımını yönetme ve artıklık ve donanım hatalarına karşı koruma için coğrafi çoğaltma sağlayın.
* **Sınırsız depolama**: doğrudan yedekleme tooAzure BLOB'lar etkinleştirerek erişim toovirtually sahip sınırsız depolama. Alternatif olarak, tooan Azure sanal makine diski yedekleme makine boyutuna göre sınırları vardır. Bir sınırı toohello numarası diskleri tooan yedeklemeler için Azure sanal makinesi ekleyebilirsiniz. Bu, çok büyük bir örneği için 16 disk ve daha küçük örnekleri için daha az sınırıdır.
* **Yedekleme kullanılabilirlik**: Azure BLOB'ları depolanan yedekleri her yerden ve herhangi bir zamanda kullanılabilir ve kolayca olabilir hello gerek olmadan bir şirket içi SQL Server veya bir Azure sanal makinede çalışan başka bir SQL Server için geri yüklemeler tooeither erişme Veritabanı ekleme/ayırma veya indiriliyor ve ekleme için VHD hello.
* **Maliyet**: yalnızca kullanılan hello hizmeti için ödeme yaparsınız. Site dışındaki ve yedekleme arşiv isteğe bağlı olarak uygun maliyetli olabilir. Merhaba bkz [Azure fiyatlandırma hesaplayıcısı](http://go.microsoft.com/fwlink/?LinkId=277060 "fiyatlandırma hesaplayıcısı")ve hello [Azure fiyatlandırma makale](http://go.microsoft.com/fwlink/?LinkId=277059 "fiyatlandırma makale") daha fazla bilgi için bilgi.
* **Depolama anlık görüntüleri**: veritabanı dosyalarını bir Azure blob depolanır ve SQL Server 2016 kullanıyorsanız, kullanabileceğiniz [dosya anlık görüntüsü backup](http://msdn.microsoft.com/library/mt169363.aspx) tooperform neredeyse anlık yedeklemeler ve son derece hızlı geri yükler.

Daha fazla ayrıntı için bkz: [SQL Server Yedekleme ve geri yükleme ile Azure Blob Depolama hizmetinin](http://go.microsoft.com/fwlink/?LinkId=271617).

iki bölüm şu hello hello Azure Blob Depolama hizmetinin, gerekli hello SQL Server bileşenleri de dahil olmak üzere tanıtın. Bu önemli toounderstand hello bileşenleri ve etkileşim toosuccessfully kullanımı yedekleme ve geri yükleme hello Azure Blob Depolama hizmetinden olur.

## <a name="azure-blob-storage-service-components"></a>Azure Blob Depolama hizmet bileşenleri
Merhaba aşağıdaki Azure bileşenleri Azure Blob Depolama hizmetinin toohello yedeklerken kullanılır.

| Bileşen | Açıklama |
| --- | --- |
| **Depolama hesabı** |Tüm depolama hizmetleri için başlangıç noktası hello Hello depolama hesabıdır. tooaccess Azure Blob Storage hizmeti, ilk Azure Storage hesabı oluşturun. Azure Blob Depolama hizmeti hakkında daha fazla bilgi için bkz: [nasıl toouse hello Azure Blob Depolama Birimi hizmeti](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Kapsayıcı** |Bir kapsayıcı gruplandırma BLOB'lar kümesinin sağlar ve sınırsız sayıda BLOB depolayabilirsiniz. bir SQL Server Yedekleme tooan Azure Blob hizmeti toowrite, sahip olmanız gerekir en az oluşturulan hello kök kapsayıcı. |
| **BLOB** |Bir dosya türü ve boyutu. BLOB'ları hello şu URL biçimi kullanılarak adreslenebilir: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Sayfa Bloblarını hakkında daha fazla bilgi için bkz: [anlama blok ve sayfa BLOB'ları](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>SQL Server bileşenleri
Merhaba aşağıdaki SQL Server bileşenleri Azure Blob Depolama hizmetinin toohello yedeklerken kullanılır.

| Bileşen | Açıklama |
| --- | --- |
| **URL** |Bir URL bir Tekdüzen Kaynak Tanımlayıcısı (URI) tooa benzersiz yedekleme dosyasını belirtir. Merhaba URL kullanılan tooprovide hello konumu ve hello SQL Server Yedekleme dosyasının adıdır. Merhaba URL tooan gerçek blob, yalnızca bir kapsayıcı işaret etmelidir. Merhaba blob mevcut değilse oluşturulur. Bir blob belirtilirse, yedekleme başarısız olursa, sürece hello > WITH FORMAT seçeneği belirtildi. Merhaba aşağıdadır belirtin hello yedekleme komutu hello URL örneği: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS önerilir ancak gerekli değildir. |
| **Kimlik bilgisi** |gerekli tooconnect ve tooAzure Blob Depolama hizmetinin kimlik doğrulaması hello bilgiler bir kimlik bilgisi olarak depolanır.  SQL Server toowrite yedeklemeleri tooan Azure Blob ya da geri yükleme için sırayla bir SQL Server kimlik bilgisi oluşturulmalıdır. Daha fazla bilgi için bkz: [SQL Server kimlik bilgisi](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Toocopy seçerseniz ve bir yedek dosya toohello Azure Blob Depolama hizmetinin karşıya yükleme, bu dosya geri yükleme işlemleri için toouse planlıyorsanız depolama seçeneği olarak sayfa blob türü kullanmanız gerekir. Bir blok blobu türü geri yükleme, bir hata ile başarısız olur.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
1. Zaten yoksa, bir Azure hesabı oluşturun. Azure değerlendirirken, hello düşünün [ücretsiz deneme sürümü](https://azure.microsoft.com/free/).
2. Ardından, bir depolama hesabı oluşturma ve geri yükleme gerçekleştirme aracılığıyla yol öğreticileri aşağıdaki hello biri aracılığıyla gidin.
   
   * **SQL Server 2014**: [Öğreticisi: SQL Server 2014 yedekleme ve geri yükleme tooMicrosoft Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [Öğreticisi: hello Microsoft Azure Blob Depolama hizmetinin SQL Server 2016 veritabanları ile kullanma](https://msdn.microsoft.com/library/dn466438.aspx)
3. Ek belgeler başlayarak gözden [SQL Server Yedekleme ve geri yükleme ile Microsoft Azure Blob Depolama hizmetinin](https://msdn.microsoft.com/library/jj919148.aspx).

Herhangi bir sorun varsa, hello konusunu gözden geçirmeniz [SQL Server Yedekleme tooURL en iyi yöntemler ve sorun giderme](https://msdn.microsoft.com/library/jj919149.aspx).

Diğer SQL Server için yedekleme ve geri yükleme seçenekleri, bkz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).

