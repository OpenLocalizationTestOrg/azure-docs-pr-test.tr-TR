---
title: "aaaDevelop U-SQL kullanıcı tanımlı işleçler (Udo'lar) | Microsoft Docs"
description: "Nasıl toodevelop kullanıcı tanımlı işleçler toobe kullanılan ve Data Lake Analytics işleri yeniden öğrenin. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: e5189e4e-9438-46d1-8686-ed4836bf3356
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 6b86618efd3751cd9a5e91875879d7dd6d6a7b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a>U-SQL kullanıcı tanımlı işleçler (Udo'lar) geliştirin
Bilgi nasıl toodevelop kullanıcı tanımlı işleçler tooprocess veri U-SQL işi.

U-SQL için genel amaçlı derlemeleri geliştirme ile ilgili yönergeler için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md)

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a>Tanımlama ve U-SQL kullanıcı tanımlı bir işleç kullanma
**toocreate ve U-SQL işi gönderin**

1. Visual Studio Hello seçin **Dosya > Yeni > Proje > U-SQL projesi**.
2. **Tamam** düğmesine tıklayın. Visual Studio Script.usql dosyası ile çözüm oluşturur.
3. Gelen **Çözüm Gezgini**Script.usql genişletin ve ardından **Script.usql.cs**.
4. Merhaba dosyasına koddan hello yapıştırın:

        using Microsoft.Analytics.Interfaces;
        using System.Collections.Generic;

        namespace USQL_UDO
        {
            public class CountryName : IProcessor
            {
                private static IDictionary<string, string> CountryTranslation = new Dictionary<string, string>
                {
                    {
                        "Deutschland", "Germany"
                    },
                    {
                        "Suisse", "Switzerland"
                    },
                    {
                        "UK", "United Kingdom"
                    },
                    {
                        "USA", "United States of America"
                    },
                    {
                        "中国", "PR China"
                    }
                };

                public override IRow Process(IRow input, IUpdatableRow output)
                {

                    string UserID = input.Get<string>("UserID");
                    string Name = input.Get<string>("Name");
                    string Address = input.Get<string>("Address");
                    string City = input.Get<string>("City");
                    string State = input.Get<string>("State");
                    string PostalCode = input.Get<string>("PostalCode");
                    string Country = input.Get<string>("Country");
                    string Phone = input.Get<string>("Phone");

                    if (CountryTranslation.Keys.Contains(Country))
                    {
                        Country = CountryTranslation[Country];
                    }
                    output.Set<string>(0, UserID);
                    output.Set<string>(1, Name);
                    output.Set<string>(2, Address);
                    output.Set<string>(3, City);
                    output.Set<string>(4, State);
                    output.Set<string>(5, PostalCode);
                    output.Set<string>(6, Country);
                    output.Set<string>(7, Phone);

                    return output.AsReadOnly();
                }
            }
        }
6. Açık **Script.usql**, ve Yapıştır hello aşağıdaki U-SQL betiği:

        @drivers =
            EXTRACT UserID      string,
                    Name        string,
                    Address     string,
                    City        string,
                    State       string,
                    PostalCode  string,
                    Country     string,
                    Phone       string
            FROM "/Samples/Data/AmbulanceData/Drivers.txt"
            USING Extractors.Tsv(Encoding.Unicode);

        @drivers_CountryName =
            PROCESS @drivers
            PRODUCE UserID string,
                    Name string,
                    Address string,
                    City string,
                    State string,
                    PostalCode string,
                    Country string,
                    Phone string
            USING new USQL_UDO.CountryName();    

        OUTPUT @drivers_CountryName
            too"/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. Merhaba Data Lake Analytics hesabı, veritabanını ve şemayı belirtin.
8. **Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betik Oluştur**'a tıklayın.
9. **Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betiği Gönder**'e tıklayın.
10. Azure aboneliği tooyour bağlanmadıysanız, şunları yapacaksınız Azure hesabı kimlik bilgileriniz istendiğinde tooenter olabilir.
11. Tıklatın **gönderme**. Merhaba gönderim tamamlandığında gönderme işleminin sonuçları ve iş bağlantısı hello sonuçları penceresi için kullanılabilir.
12. Merhaba tıklatın **yenileme** düğmesini toosee hello en son iş durumunu ve yenileme hello ekran.

**toosee hello çıktı**

1. Gelen **Sunucu Gezgini**, genişletin **Azure**, genişletin **Data Lake Analytics**, Data Lake Analytics hesabınızı genişletin, **depolama hesapları**hello varsayılan depolama sağ tıklayın ve ardından **Explorer**.
2. Örnekleri genişletin, çıkışları genişletin ve ardından **sürücüler.csv**.

## <a name="see-also"></a>Ayrıca bkz.
* [PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-powershell.md)
* [Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md)
* [U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın](data-lake-analytics-data-lake-tools-get-started.md)
