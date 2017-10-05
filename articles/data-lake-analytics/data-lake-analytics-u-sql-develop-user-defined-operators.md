---
title: "U-SQL kullanıcı tanımlı işleçler (Udo'lar) geliştirme | Microsoft Docs"
description: "Kullanıcı tanımlı işleçler kullanılan ve Data Lake Analytics işleri yeniden için geliştirmeyi öğrenin. "
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
ms.openlocfilehash: fdee02fb60b633c26704fc1774dfc3a7825b5e0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-u-sql-user-defined-operators-udos"></a><span data-ttu-id="6e075-103">U-SQL kullanıcı tanımlı işleçler (Udo'lar) geliştirin</span><span class="sxs-lookup"><span data-stu-id="6e075-103">Develop U-SQL user-defined operators (UDOs)</span></span>
<span data-ttu-id="6e075-104">Kullanıcı tanımlı işleçler bir U-SQL işi verileri işlemek için geliştirmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6e075-104">Learn how to develop user-defined operators to process data in a U-SQL job.</span></span>

<span data-ttu-id="6e075-105">U-SQL için genel amaçlı derlemeleri geliştirme ile ilgili yönergeler için bkz: [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md)</span><span class="sxs-lookup"><span data-stu-id="6e075-105">For instructions on developing general-purpose assemblies for U-SQL, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md)</span></span>

## <a name="define-and-use-a-user-defined-operator-in-u-sql"></a><span data-ttu-id="6e075-106">Tanımlama ve U-SQL kullanıcı tanımlı bir işleç kullanma</span><span class="sxs-lookup"><span data-stu-id="6e075-106">Define and use a user-defined operator in U-SQL</span></span>
<span data-ttu-id="6e075-107">**Oluşturmak ve U-SQL işi göndermek için**</span><span class="sxs-lookup"><span data-stu-id="6e075-107">**To create and submit a U-SQL job**</span></span>

1. <span data-ttu-id="6e075-108">Visual Studio seçin gelen **Dosya > Yeni > Proje > U-SQL projesi**.</span><span class="sxs-lookup"><span data-stu-id="6e075-108">From the Visual Studio select **File > New > Project > U-SQL Project**.</span></span>
2. <span data-ttu-id="6e075-109">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e075-109">Click **OK**.</span></span> <span data-ttu-id="6e075-110">Visual Studio Script.usql dosyası ile çözüm oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6e075-110">Visual Studio creates a solution with a Script.usql file.</span></span>
3. <span data-ttu-id="6e075-111">Gelen **Çözüm Gezgini**Script.usql genişletin ve ardından **Script.usql.cs**.</span><span class="sxs-lookup"><span data-stu-id="6e075-111">From **Solution Explorer**, expand Script.usql, and then double-click **Script.usql.cs**.</span></span>
4. <span data-ttu-id="6e075-112">Dosyasına aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="6e075-112">Paste the following code into the file:</span></span>

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
6. <span data-ttu-id="6e075-113">Açık **Script.usql**, aşağıdaki U-SQL betiğini yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="6e075-113">Open **Script.usql**, and paste the following U-SQL script:</span></span>

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
            TO "/Samples/Outputs/Drivers.csv"
            USING Outputters.Csv(Encoding.Unicode);
7. <span data-ttu-id="6e075-114">Data Lake Analytics hesabını, Veritabanı'nı ve Şema'yı belirtin.</span><span class="sxs-lookup"><span data-stu-id="6e075-114">Specify the Data Lake Analytics account, Database, and Schema.</span></span>
8. <span data-ttu-id="6e075-115">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betik Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e075-115">From **Solution Explorer**, right-click **Script.usql**, and then click **Build Script**.</span></span>
9. <span data-ttu-id="6e075-116">**Çözüm Gezgini**'nden, **Script.usql** öğesine sağ tıklayın ve ardından **Betiği Gönder**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6e075-116">From **Solution Explorer**, right-click **Script.usql**, and then click **Submit Script**.</span></span>
10. <span data-ttu-id="6e075-117">Azure aboneliğinize bağlanmadıysanız, Azure hesabı kimlik bilgilerinizi girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="6e075-117">If you haven't connected to your Azure subscription, you will be prompted to enter your Azure account credentials.</span></span>
11. <span data-ttu-id="6e075-118">Tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="6e075-118">Click **Submit**.</span></span> <span data-ttu-id="6e075-119">Gönderim tamamlandığında Sonuçları penceresinde, gönderme işleminin sonuçları ve iş bağlantısı da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6e075-119">Submission results and job link are available in the Results window when the submission is completed.</span></span>
12. <span data-ttu-id="6e075-120">Tıklatın **yenileme** en son iş durumu ve ekranı yenilemek görmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="6e075-120">Click the **Refresh** button to see the latest job status and refresh the screen.</span></span>

<span data-ttu-id="6e075-121">**Çıkışı görmek için**</span><span class="sxs-lookup"><span data-stu-id="6e075-121">**To see the output**</span></span>

1. <span data-ttu-id="6e075-122">Gelen **Sunucu Gezgini**, genişletin **Azure**, genişletin **Data Lake Analytics**, Data Lake Analytics hesabınızı genişletin, **depolama hesapları**, varsayılan depolama sağ tıklayın ve ardından **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6e075-122">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the Default Storage, and then click **Explorer**.</span></span>
2. <span data-ttu-id="6e075-123">Örnekleri genişletin, çıkışları genişletin ve ardından **sürücüler.csv**.</span><span class="sxs-lookup"><span data-stu-id="6e075-123">Expand Samples, expand Outputs, and then double-click **Drivers.csv**.</span></span>

## <a name="see-also"></a><span data-ttu-id="6e075-124">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="6e075-124">See also</span></span>
* [<span data-ttu-id="6e075-125">PowerShell kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6e075-125">Get started with Data Lake Analytics using PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="6e075-126">Azure Portalı'nı kullanarak Data Lake Analytics ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6e075-126">Get started with Data Lake Analytics using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6e075-127">U-SQL uygulamalarını geliştirmek için Visual Studio için Data Lake araçları kullanın</span><span class="sxs-lookup"><span data-stu-id="6e075-127">Use Data Lake Tools for Visual Studio for developing U-SQL applications</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
