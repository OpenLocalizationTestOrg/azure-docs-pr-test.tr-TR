---
title: "aaaAzure veri Kataloğu sürüm notları | Microsoft Docs"
description: "Azure veri kataloğu için sürüm notları."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Azure veri Kataloğu sürüm notları
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Azure veri Kataloğu'nun hello 20 Kasım 2015 sürüm notları
### <a name="opening-data-sources-in-power-bi-desktop"></a>Power BI Desktop'ta açılış veri kaynakları
Merhaba "Açık olarak Power BI Desktop" Merhaba seçeneğinden kullanırken **Azure veri Kataloğu** portalı, kullanıcıların hello Power BI Desktop uygulama içinde iki sorunlardan biri karşılaşabilirsiniz:

* Merhaba başlığı "Oluşturulamıyor tooOpen belge" içeren bir iletişim kutusu görüntülenir
* Merhaba Power BI Desktop uygulamasını açar ancak hello dosya toobe boş görünür

Her durum için Power BI Desktop'hello en son sürümünü indirip hello sorun çözülebilir [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Azure veri Kataloğu'nun hello 13 Kasım 2015 sürüm notları
### <a name="registering-and-connecting-tooteradata"></a>Kaydetme ve tooTeradata bağlanma
Kullanılan hello yazılımların hello verileri (32 bit veya 64 bit) eşleşen kullanıcıları hello doğru Teradata ODBC sürücüsü yüklü olmalıdır tooTeradata veri kaynaklarına bağlanırken.

Bu ADC itibariyle, yayın tarihi, en son hello [windows (sürüm 15.10) için Teradata ODBC sürücüsü](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) uyumlu Office 2013, ancak Office 2016 ile değil.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Azure veri Kataloğu'nun hello 13 Temmuz 2015 sürüm notları
### <a name="registering-and-connecting-toooracle-database"></a>Kaydetme ve tooOracle veritabanına bağlanma
Ne zaman tooOracle veritabanı veri kaynakları kullanıcılara bağlanan kullanılmakta hello yazılımların hello verileri (32 bit veya 64 bit) eşleşen hello doğru Oracle sürücüleri yüklü olmalıdır.

* 32 bit Windows çalıştıran bir bilgisayarda Oracle veri kaynaklarını kaydederek yüklerken hello 32-bit Oracle sürücüler kullanılır
* 64 bit Windows çalıştıran bir bilgisayarda Oracle veri kaynaklarını kaydederek yüklerken hello 64-bit Oracle sürücüler kullanılır
* Microsoft Office hello 32-bit sürümünü çalıştıran bir bilgisayarda Excel kullanarak tooOracle veri kaynaklarına bağlanırken, 64 bit Windows'ta dahil olmak üzere hello 32-bit Oracle sürücüler kullanılır
* Microsoft Office hello 64-bit sürümünü çalıştıran bir bilgisayarda Excel kullanarak tooOracle veri kaynaklarına bağlanırken hello 64-bit Oracle sürücüler kullanılır

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>Kaydetme ve tooSQL Server Reporting Services bağlanma
SQL Server Reporting Services (SSRS) veri kaynakları için destek, yalnızca şu anda sınırlı tooNative modu sunucuları içindir. SSRS desteği SharePoint modunda daha sonraki bir sürümde eklenecek.

### <a name="opening-data-assets-in-excel"></a>Excel açılırken veri varlıklarını
Veri varlıklarını hello Microsoft Excel'de açarken **Azure veri Kataloğu** portal, kullanıcılar ile istenebilir bir **Microsoft Excel Güvenlik Bildirimi** iletişim kutusu. Bu standart, beklenen davranıştır ve kullanıcılar seçebilir **etkinleştirmek** toocontinue.

Daha fazla bilgi için bkz: [etkinleştirmek veya devre dışı bağlantılar ve şüpheli Web sitelerine dosyalarından ilgili güvenlik uyarıları](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Proxy ve ilke yapılandırması ve veri kaynağı kaydı
Kullanıcılar nerede toohello Azure veri Kataloğu portalındaki, ancak bunları oturum açmasını engelleyen bir hata iletisi karşılaştıkları toohello veri kaynağı kayıt aracını üzerinde toolog çalıştığınızda oturum durumlar yaşayabilirsiniz.

Bu sorunu davranış iki olası nedenleri şunlardır:

**1. neden: Active Directory Federasyon Hizmetleri Yapılandırma** hello veri kaynağı kayıt aracını form kimlik doğrulaması toovalidate kullanıcı oturumları Active Directory karşı kullanır. Başarılı oturum açma işlemi için form kimlik doğrulaması Active Directory Yöneticisi tarafından hello genel kimlik doğrulama ilkesini etkinleştirilmesi gerekir.

Bazı durumlarda, bu hata davranış yalnızca hello kullanıcı hello şirket ağında olmadığında veya yalnızca dış hello şirket ağdan hello kullanıcı bağlanırken ortaya çıkabilir. Merhaba genel kimlik doğrulama ilkesini intranet ve extranet bağlantıları için ayrı ayrı etkin kimlik doğrulama yöntemleri toobe sağlar. Hangi hello kullanıcı bağlanıyor hello ağ için form kimlik doğrulaması etkin değilse oturum açma hataları oluşabilir.

Daha fazla bilgi için bkz: [kimlik doğrulaması ilkelerini yapılandırma](https://technet.microsoft.com/library/dn486781.aspx).

**2. neden: Ağ proxy yapılandırmasını** hello kurumsal ağ proxy sunucusu kullanıyorsa, hello kayıt aracı hello proxy üzerinden mümkün tooconnect tooAzure Active Directory olmayabilir. Kullanıcılar bu hello kayıt aracı hello aracın yapılandırma dosyasını düzenleyerek bu bölüm toohello dosyasını ekleme sağlayabilirsiniz:

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


toolocate hello RegistrationTool.exe.config dosya hello kayıt aracını başlatmak ve hello Windows Görev Yöneticisi yardımcı programını açın. Görev Yöneticisi'nde hello Ayrıntılar sekmesinde, üzerinde RegistrationTool.exe sağ tıklayın ve hello açılır menüsünden dosya konumunu Aç'ı seçin.
