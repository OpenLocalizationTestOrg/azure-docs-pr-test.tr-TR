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
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="ff639-103">U-SQL kullanıcı tanımlı işleçler (Udo'lar) geliştirin</span><span class="sxs-lookup"><span data-stu-id="ff639-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="ff639-104">Bilgi nasıl toodevelop kullanıcı tanımlı işleçler tooprocess veri U-SQL işi.</span><span class="sxs-lookup"><span data-stu-id="ff639-104">Learn how toodevelop user-defined operators tooprocess data in a U-SQL job.</span></span>

<span data-ttu-id="ff639-105">U-SQL için genel amaçlı derlemeleri geliştirme ile ilgili yönergeler için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="ff639-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="ff639-106">Tanımlama ve U-SQL kullanıcı tanımlı bir işleç kullanma</span><span class="sxs-lookup"><span data-stu-id="ff639-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="ff639-107">**toocreate ve U-SQL işi gönderin**</span><span class="sxs-lookup"><span data-stu-id="ff639-107">**toocreate and submit a U-SQL job**</span></span>

1. <span data-ttu-id="ff639-108">Visual Studio Hello seçin **Dosya > Yeni > Proje > U-SQL projesi**.</span><span class="sxs-lookup"><span data-stu-id="ff639-108">From hello Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="ff639-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff639-109">Click **OK**.</span></span> <span data-ttu-id="ff639-110">Visual Studio Script.usql dosyası ile çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff639-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="ff639-111">Gelen **Çözüm Gezgini**Script.usql genişletin ve ardından **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="ff639-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="ff639-112">Merhaba dosyasına koddan hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="ff639-112">Paste hello following code into hello file:</span></span>

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
6. <span data-ttu-id="ff639-113">Açık **Script.usql**, ve Yapıştır hello aşağıdaki U-SQL betiği:</span><span class="sxs-lookup"><span data-stu-id="ff639-113">Open **Script.usql**, and paste hello following U-SQL script:</span></span>

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
7. <span data-ttu-id="ff639-114">Merhaba Data Lake Analytics hesabı, veritabanını ve şemayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="ff639-114">Specify hello Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="ff639-115">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betik Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff639-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="ff639-116">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betiği Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ff639-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="ff639-117">Azure aboneliği tooyour bağlanmadıysanız, şunları yapacaksınız Azure hesabı kimlik bilgileriniz istendiğinde tooenter olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff639-117">If you haven't connected tooyour Azure subscription, you will be prompted tooenter your Azure account credentials.</span></span>
11. <span data-ttu-id="ff639-118">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="ff639-118">Click **Submit**.</span></span> <span data-ttu-id="ff639-119">Merhaba gönderim tamamlandığında gönderme işleminin sonuçları ve iş bağlantısı hello sonuçları penceresi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff639-119">Submission results and job link are available in hello Results window when hello submission is completed.</span></span>
12. <span data-ttu-id="ff639-120">Merhaba tıklatın **yenileme** düğmesini toosee hello en son iş durumunu ve yenileme hello ekran.</span><span class="sxs-lookup"><span data-stu-id="ff639-120">Click hello **Refresh** button toosee hello latest job status and refresh hello screen.</span></span>

<span data-ttu-id="ff639-121">**toosee hello çıktı**</span><span class="sxs-lookup"><span data-stu-id="ff639-121">**toosee hello output**</span></span>

1. <span data-ttu-id="ff639-122">Gelen **Sunucu Gezgini**, genişletin **Azure**, genişletin **Data Lake Analytics**, Data Lake Analytics hesabınızı genişletin, **depolama hesapları**hello varsayılan depolama sağ tıklayın ve ardından **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ff639-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="ff639-123">Örnekleri genişletin, çıkışları genişletin ve ardından **sürücüler.csv**.</span><span class="sxs-lookup"><span data-stu-id="ff639-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="ff639-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ff639-124">See also</span></span>
* [<span data-ttu-id="ff639-125">PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff639-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="ff639-126">Hello Azure portal kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ff639-126">Get started with Data Lake Analytics using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ff639-127">U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="ff639-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
