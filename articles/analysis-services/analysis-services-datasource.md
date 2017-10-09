---
title: "Azure Analysis Services içinde desteklenen aaaData kaynakları | Microsoft Docs"
description: "Azure Analysis Services veri modelleri için desteklenen veri kaynakları açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Azure Analysis Services içinde desteklenen veri kaynakları
Azure Analysis Services sunucuları bağlanan toodata kaynaklarını hello Bulut ve şirket içi kuruluşunuzdaki destekler. Ek desteklenen veri kaynakları hello zaman eklenir. Geri sık sık kontrol edin. 

şu anda aşağıdaki veri kaynaklar hello desteklenir:

| Bulut  |
|---|
| Azure Blob Depolama *  |
| Azure SQL Database  |
| Azure veri ambarı |


| Şirket içi  |   |   |   |
|---|---|---|---|
| Access veritabanı  | Klasör * | Oracle Veritabanı  | Teradata Database |
| Active Directory *  | JSON belgesini *  | Postgre SQL veritabanı *  |XML tablo * |
| Analysis Services  | Satırlarından ikili *  | SAP HANA *  |
| Analiz platformu sistemi  | MySQL Veritabanı  | SAP Business Warehouse *  | |
| Dynamics CRM *  | OData akışı *  | SharePoint *  |
| Excel çalışma kitabı  | ODBC sorgu  | SQL Database  |
| Exchange *  | OLE DB  | Sybase veritabanı  |

\*Yalnızca tablolu 1400 modeller için. 

> [!IMPORTANT]
> Tooon içi veri kaynaklarının gerektirdiği bağlanan bir [şirket içi veri ağ geçidi](analysis-services-gateway.md) ortamınızdaki bir bilgisayara yüklenmiş.

## <a name="data-providers"></a>Veri sağlayıcıları

Azure Analysis Services veri modelleri farklı veri sağlayıcıları toocertain veri kaynaklarına bağlanırken gerektirebilir. Bazı durumlarda, tablolu modeller toodata kaynakları SQL Server Native Client (SQLNCLI11) gibi yerel sağlayıcılarını kullanarak bağlanırken bir hata döndürebilir.

Tooa bulut verilerini bağlanan veri modelleri için kaynak gibi Azure SQL veritabanı, yerel sağlayıcıları SQLOLEDB dışında kullanırsanız, hata iletisi görebilirsiniz: **"Merhaba Sağlayıcı 'SQLNCLI11.1' kayıtlı değil."** Ya da yerel sağlayıcıları kullanırsanız bağlantı tooon içi veri kaynakları, model DirectQuery varsa hata iletisi görebilirsiniz: **"OLE DB satır kümesi oluşturulurken hata oluştu. 'Sınırı' yakınındaki sözdizimi yanlış "**.

veri kaynağı sağlayıcıları aşağıdaki hello bağlanan toodata hello Bulut veya şirket içi kaynakları bellek içi veya DirectQuery veri modelleri için desteklenmez:

### <a name="cloud"></a>Bulut
| **Veri kaynağı** | **Bellek içi** | **DirectQuery** |
|  --- | --- | --- |
| Azure SQL Veri Ambarı |SQL Server için .NET framework veri sağlayıcısı |SQL Server için .NET framework veri sağlayıcısı |
| Azure SQL Database |SQL Server için .NET framework veri sağlayıcısı |SQL Server için .NET framework veri sağlayıcısı | |

### <a name="on-premises-via-gateway"></a>Şirket içi (yoluyla ağ geçidi)
|**Veri kaynağı** | **Bellek içi** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |SQL Server için .NET framework veri sağlayıcısı |
| SQL Server |SQL Server için Microsoft OLE DB sağlayıcısı |SQL Server için .NET framework veri sağlayıcısı | |
| SQL Server |SQL Server için .NET framework veri sağlayıcısı |SQL Server için .NET framework veri sağlayıcısı | |
| Oracle |Oracle için Microsoft OLE DB sağlayıcısı |.NET için Oracle veri sağlayıcısı | |
| Oracle |.NET için Oracle veri sağlayıcısı |.NET için Oracle veri sağlayıcısı | |
| Teradata |Teradata için OLE DB sağlayıcısı |.NET için Teradata veri sağlayıcısı | |
| Teradata |.NET için Teradata veri sağlayıcısı |.NET için Teradata veri sağlayıcısı | |
| Analiz platformu sistemi |SQL Server için .NET framework veri sağlayıcısı |SQL Server için .NET framework veri sağlayıcısı | |

> [!NOTE]
> 64-bit sağlayıcıları, şirket içi ağ geçidi kullanırken yüklü olduğundan emin olun.
> 
> 

Bir şirket içi SQL Server Analysis Services tablolu model tooAzure Analysis Services geçirirken, gerekli toochange hello sağlayıcısı olabilir.

**toospecify bir veri kaynağı sağlayıcısı**

1. Ssdt'de > **tablolu Model Gezgini** > **veri kaynakları**, bir veri kaynağı bağlantısı sağ tıklayın ve ardından **veri kaynağını Düzenle**.
2. İçinde **bağlantı Düzenle**, tıklatın **Gelişmiş** tooopen hello Gelişmiş Özellikler penceresi.
3. İçinde **gelişmiş özelliklerini ayarla** > **sağlayıcıları**, uygun sağlayıcıyı seçin hello sonra.

## <a name="impersonation"></a>Kimliğe bürünme
Bazı durumlarda, gerekli toospecify farklı kimliğe bürünme hesabı olabilir. Kimliğe bürünme hesabı SSDT veya SSMS belirtilebilir.

Şirket içi veri kaynakları için:

* SQL kimlik doğrulamasını kullanıyorsanız, kimliğe bürünme hizmet hesabı olması gerekir.
* Windows kimlik doğrulamasını kullanıyorsanız, Windows kullanıcı/parola ayarlayın. SQL Server için Windows kimlik doğrulaması belirli kimliğe bürünme hesabı ile yalnızca bellek içi veri modelleri için desteklenir.

Bulut veri kaynakları için:

* SQL kimlik doğrulamasını kullanıyorsanız, kimliğe bürünme hizmet hesabı olması gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Şirket içi veri kaynakları varsa emin tooinstall hello olması [şirket içi ağ geçidi](analysis-services-gateway.md).   
SSDT veya SSMS, sunucunuzu yönetme hakkında daha fazla toolearn bkz [sunucunuzu yönetin](analysis-services-manage.md).

