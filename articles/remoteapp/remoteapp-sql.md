---
title: Azure RemoteApp ile Azure aaaSQL | Microsoft Docs
description: "Bilgi nasıl toouse Azure RemoteApp ile SQL Azure."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
editor: 
ms.assetid: 35f81d75-bfd7-4980-807e-00339f2cb2a4
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: fec4cb1f1ab3cde03b6ff613650e01bae3552824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-azure-with-azure-remoteapp"></a>Azure RemoteApp ile SQL Azure
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Genellikle müşteriler toohost kendi Windows uygulamalarını Azure RemoteApp ile Merhaba bulutta seçtiğinizde de hello içine SQL sunucuları gibi verilerini bulut toomigrate tüm bulut dağıtımı için isterler. Bu, Azure RemoteApp kullanarak her zaman herhangi bir cihazdan erişilebilir tümü bulutta barındırılan çözüme olanak sağlar. Aşağıdaki bağlantılar ve kılavuz toohelp yanı sıra bu işlemle başvurur.  

## <a name="migrate-your-sql-data"></a>SQL verilerinizi geçirme
İle başlayan [bir SQL Server veritabanı tooAzure SQL veritabanı geçiş](../sql-database/sql-database-cloud-migrate.md). 

## <a name="configure-azure-remoteapp"></a>Azure RemoteApp’i yapılandırma
Windows uygulamanızı Azure RemoteApp’te barındırma Aşağıda çok üst düzey adım adım açıklama bulunmaktadır:

1. Merhaba oluşturma [Azure RemoteApp şablonu VM](remoteapp-imageoptions.md). 
2. Gerekli Merhaba uygulaması hello VM üzerinde yükleyin.
3. Merhaba uygulaması toohello SQL DB'ye bağlanacak şekilde yapılandırın ve çalıştığını doğrulayın.
4. Sysprep ve kapatma hello VM. Azure ile kullanmak için bunu bir görüntü olarak yakalayın. **Not:** Merhaba uygulaması mümkün tooretain hello DB bağlantısı bilgilerini hello sysprep işlemiyle olduğunu tooensure gerekir. Merhaba uygulaması oluşturulamıyor tooretain hello DB bağlantı bilgilerini ise, hello uygulama toocheck tooengage hello satıcısına isteyebilirsiniz nasıl biz hello bağlantı dizesi belirtebilirsiniz.
5. Merhaba özel görüntü SQL Azure dağıtımınızın bulunduğu hello uygun coğrafi konumu seçerek Azure RemoteApp kitaplığınıza aktarın. 
6. Aynı veri şablonu yukarıdaki hello kullanarak SQL Azure dağıtımınız olarak ortalamak ve Merhaba uygulaması yayımlama hello RemoteApp koleksiyonunda dağıtın. Azure RemoteApp hello dağıtma SQL Azure dağıtımınız olarak aynı veri merkezinde hello hızlı bağlantıyı hızını ve gecikme süresini azaltmak yardımcı olur. 

## <a name="app-and-sql-configuration-considerations"></a>Uygulama ve SQL yapılandırmada dikkat edilmesi gerekenler
RemoteApp ile Azure SQL kullanırken, birkaç noktaları tooconsider vardır:

Bilgi [nasıl tooconfigure bir Azure SQL veritabanı Güvenlik Duvarı](../sql-database/sql-database-firewall-configure.md). Bir alıntı Hello makale durumlar, "Başlangıçta, tüm erişim tooyour Azure SQL veritabanı sunucusu hello güvenlik duvarı tarafından engellenir. Azure SQL veritabanı sunucunuzun kullanarak sipariş toobegin içinde toohello Klasik Portal gidin ve erişim tooyour Azure SQL veritabanı sunucusu sağlayan bir veya daha fazla sunucu düzeyinde güvenlik duvarı kuralları belirtin. Merhaba güvenlik duvarı kuralları toospecify Internet izin verilen hello hangi IP adres aralıkları ve Azure uygulamalarını tooconnect tooyour Azure SQL Database sunucusu olsun veya olmasın deneyebilirsiniz kullanın."

Ayrıca, bir bilgisayar tooconnect tooyour veritabanı hello Internet sunucusundan denediğinde hello güvenlik duvarı IP adresi sunucu düzeyi hello kümesini karşı hello isteğinin kaynaklandığı hello denetler ve (gerekliyse) veritabanı düzeyi güvenlik duvarı kuralları. "Hello IP adresi hello isteğinin hello sunucu düzeyinde güvenlik duvarı kurallarında belirtilen hello aralıkları biri içinde ise, hello bağlantı tooyour Azure SQL Database sunucusu verilir." Dolayısıyla, yalnızca IP adresi kaynaklarını değil IP Aralıklarını da kullanabiliriz.

Merhaba adım adım yönergeleri izleyin [nasıl yapılır: hello Azure Portal kullanarak SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](../sql-database/sql-database-configure-firewall-settings.md) toospecify hello IP aralığı. Lütfen hello SQL güvenlik duvarı kurallarını yapılandırırken, belirtilen hello alt ağın IP aralığını hello hello Azure RemoteApp koleksiyonu belirtin. Bunlar dinamik olarak atanan IP adresleri olmasına rağmen bu tooconnect toohello SQL DB hello ARA sunucularının izin vermelidir.

## <a name="troubleshooting"></a>Sorun giderme
Merhaba karşılaşırsanız tooa SQL bağlanan Azure Remoteapp'te barındırılan istemci uygulaması kullanarak Azure üzerinde barındırılan veritabanı veya şirket içi yavaş birkaç nedeni olabilir neden.  

* Aygıt tooAzure gelen ağ gecikmesi yüksektir. Taşıma toohello en iyi ve en hızlı ağ bağlantısı en iyi performans için kullanabilirsiniz. Kullanım [azurespeed.com](http://azurespeed.com/) genel araç tootest, cihazları gecikme tooAzure veri merkezi.  
* Azure RemoteApp’te barındırılan istemci uygulaması gerilim altında. Premium faturalama gibi farklı bir fatura planı seçmek performansı iyileştirir. Başka bir çözüm olan toomonitor hello kaynakları, uygulamanızın: etkin bir oturum sırasında SAS ekran, Görev Yöneticisi'ni seçin ve uygulamanız için kaynak kullanımını gözleyin hello başlatacak ctrl-alt-end anahtar sırası gerçekleştirin.
* SQL server gerilim altından veya en iyi hale getirilmemiş. Sorun giderme için SQL yönergelerini izleyin. 

