---
title: "aaaAzure işlevleri dış tablo bağlama (Önizleme) | Microsoft Docs"
description: "Dış tablo bağlamaları Azure işlevlerini kullanma"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="5b5f4-103">Azure işlevleri dış tablo bağlama (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="5b5f4-104">Bu makalede gösterilmektedir nasıl toomanipulate tablo veri işlevinizi yerleşik bağlamalarla içinde SaaS sağlayıcıları (örneğin, Sharepoint, Dynamics).</span><span class="sxs-lookup"><span data-stu-id="5b5f4-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="5b5f4-105">Azure işlevleri, harici tablolar için girdi ve çıktı bağlamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="5b5f4-106">API bağlantıları</span><span class="sxs-lookup"><span data-stu-id="5b5f4-106">API Connections</span></span>

<span data-ttu-id="5b5f4-107">Tablo bağlamaları ile 3. taraf SaaS sağlayıcılar dış API bağlantıları tooauthenticate yararlanın.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="5b5f4-108">Bir bağlama atarken, yeni bir API bağlantı oluşturabilir veya var olan bir API bağlantısını hello içinde kullanmak aynı kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="5b5f4-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="5b5f4-109">Desteklenen API bağlantıları (tablo) s</span><span class="sxs-lookup"><span data-stu-id="5b5f4-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="5b5f4-110">Bağlayıcı</span><span class="sxs-lookup"><span data-stu-id="5b5f4-110">Connector</span></span>|<span data-ttu-id="5b5f4-111">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="5b5f4-111">Trigger</span></span>|<span data-ttu-id="5b5f4-112">Girdi</span><span class="sxs-lookup"><span data-stu-id="5b5f4-112">Input</span></span>|<span data-ttu-id="5b5f4-113">Çıktı</span><span class="sxs-lookup"><span data-stu-id="5b5f4-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="5b5f4-114">DB2</span><span class="sxs-lookup"><span data-stu-id="5b5f4-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="5b5f4-115">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-115">x</span></span>|<span data-ttu-id="5b5f4-116">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-116">x</span></span>
|[<span data-ttu-id="5b5f4-117">Dynamics 365 işlemleri için</span><span class="sxs-lookup"><span data-stu-id="5b5f4-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="5b5f4-118">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-118">x</span></span>|<span data-ttu-id="5b5f4-119">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-119">x</span></span>
|[<span data-ttu-id="5b5f4-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="5b5f4-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="5b5f4-121">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-121">x</span></span>|<span data-ttu-id="5b5f4-122">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-122">x</span></span>
|[<span data-ttu-id="5b5f4-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="5b5f4-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="5b5f4-124">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-124">x</span></span>|<span data-ttu-id="5b5f4-125">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-125">x</span></span>
|[<span data-ttu-id="5b5f4-126">Google E-Tablolar</span><span class="sxs-lookup"><span data-stu-id="5b5f4-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="5b5f4-127">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-127">x</span></span>|<span data-ttu-id="5b5f4-128">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-128">x</span></span>
|[<span data-ttu-id="5b5f4-129">Informix</span><span class="sxs-lookup"><span data-stu-id="5b5f4-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="5b5f4-130">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-130">x</span></span>|<span data-ttu-id="5b5f4-131">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-131">x</span></span>
|[<span data-ttu-id="5b5f4-132">Mali Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="5b5f4-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="5b5f4-133">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-133">x</span></span>|<span data-ttu-id="5b5f4-134">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-134">x</span></span>
|[<span data-ttu-id="5b5f4-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="5b5f4-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="5b5f4-136">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-136">x</span></span>|<span data-ttu-id="5b5f4-137">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-137">x</span></span>
|[<span data-ttu-id="5b5f4-138">Oracle Veritabanı</span><span class="sxs-lookup"><span data-stu-id="5b5f4-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="5b5f4-139">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-139">x</span></span>|<span data-ttu-id="5b5f4-140">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-140">x</span></span>
|[<span data-ttu-id="5b5f4-141">Ortak veri hizmeti</span><span class="sxs-lookup"><span data-stu-id="5b5f4-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="5b5f4-142">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-142">x</span></span>|<span data-ttu-id="5b5f4-143">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-143">x</span></span>
|[<span data-ttu-id="5b5f4-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="5b5f4-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="5b5f4-145">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-145">x</span></span>|<span data-ttu-id="5b5f4-146">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-146">x</span></span>
|[<span data-ttu-id="5b5f4-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="5b5f4-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="5b5f4-148">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-148">x</span></span>|<span data-ttu-id="5b5f4-149">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-149">x</span></span>
|[<span data-ttu-id="5b5f4-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b5f4-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="5b5f4-151">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-151">x</span></span>|<span data-ttu-id="5b5f4-152">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-152">x</span></span>
|[<span data-ttu-id="5b5f4-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="5b5f4-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="5b5f4-154">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-154">x</span></span>|<span data-ttu-id="5b5f4-155">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-155">x</span></span>
|<span data-ttu-id="5b5f4-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="5b5f4-156">UserVoice</span></span>||<span data-ttu-id="5b5f4-157">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-157">x</span></span>|<span data-ttu-id="5b5f4-158">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-158">x</span></span>
|<span data-ttu-id="5b5f4-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="5b5f4-159">Zendesk</span></span>||<span data-ttu-id="5b5f4-160">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-160">x</span></span>|<span data-ttu-id="5b5f4-161">x</span><span class="sxs-lookup"><span data-stu-id="5b5f4-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="5b5f4-162">Dış tablo bağlantıları da kullanılabilir [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="5b5f4-163">Bir API bağlantı oluşturma: adım adım</span><span class="sxs-lookup"><span data-stu-id="5b5f4-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="5b5f4-164">Bir işlev oluşturun > Özel işlevi ![özel bir işlev oluşturun](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="5b5f4-165">Senaryo `Experimental`  >  `ExternalTable-CSharp` şablonu > Yeni bir `External Table connection` 
 ![Seç tablo giriş şablonu](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="5b5f4-166">SaaS sağlayıcınızı seçin > bir bağlantı seçin/oluşturmak ![yapılandırma SaaS bağlantı](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="5b5f4-167">API bağlantınızı seçin > merhaba fonksiyon ![Create table işlevi](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="5b5f4-168">seçin`Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="5b5f4-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="5b5f4-169">Merhaba bağlantı toouse hedef tablo yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="5b5f4-170">Bu ayarlar, SaaS sağlayıcılar arasında çok olur.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="5b5f4-171">Aşağıda anahat oldukları [veri kaynağı ayarları](#datasourcesettings)
![yapılandırma tablosu](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="5b5f4-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="5b5f4-172">Kullanım</span><span class="sxs-lookup"><span data-stu-id="5b5f4-172">Usage</span></span>

<span data-ttu-id="5b5f4-173">Bu örnek kimliği, Soyadı ve FirstName sütunlarla "Başvurun" adlı tooa tablo bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="5b5f4-174">hello kişi varlıkları hello tablosundaki Hello kodunu listeler ve günlükleri adları ve soyadları hello.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="5b5f4-175">Bağlamalar</span><span class="sxs-lookup"><span data-stu-id="5b5f4-175">Bindings</span></span>
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
<span data-ttu-id="5b5f4-176">`entityId`Tablo bağlamaları için boş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="5b5f4-177">`ConnectionAppSettingsKey`Merhaba API bağlantı dizesi depolar hello uygulama ayarı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="5b5f4-178">bir API eklediğinizde hello uygulama ayarı otomatik olarak oluşturulan hello bağlantısında UI tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="5b5f4-179">Veri kümeleri tablo Bağlayıcısı sağlar ve her bir veri kümesi tabloları içerir.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="5b5f4-180">"varsayılan" Merhaba hello varsayılan veri kümesinin adıdır</span><span class="sxs-lookup"><span data-stu-id="5b5f4-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="5b5f4-181">Merhaba başlıkları bir veri kümesi ve bir tablo çeşitli SaaS sağlayıcıları için aşağıda listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="5b5f4-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="5b5f4-182">Bağlayıcı</span><span class="sxs-lookup"><span data-stu-id="5b5f4-182">Connector</span></span>|<span data-ttu-id="5b5f4-183">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="5b5f4-183">Dataset</span></span>|<span data-ttu-id="5b5f4-184">Tablo</span><span class="sxs-lookup"><span data-stu-id="5b5f4-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="5b5f4-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="5b5f4-185">**SharePoint**</span></span>|<span data-ttu-id="5b5f4-186">Site</span><span class="sxs-lookup"><span data-stu-id="5b5f4-186">Site</span></span>|<span data-ttu-id="5b5f4-187">SharePoint listesi</span><span class="sxs-lookup"><span data-stu-id="5b5f4-187">SharePoint List</span></span>
|<span data-ttu-id="5b5f4-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5b5f4-188">**SQL**</span></span>|<span data-ttu-id="5b5f4-189">Database</span><span class="sxs-lookup"><span data-stu-id="5b5f4-189">Database</span></span>|<span data-ttu-id="5b5f4-190">Tablo</span><span class="sxs-lookup"><span data-stu-id="5b5f4-190">Table</span></span> 
|<span data-ttu-id="5b5f4-191">**Google sayfası**</span><span class="sxs-lookup"><span data-stu-id="5b5f4-191">**Google Sheet**</span></span>|<span data-ttu-id="5b5f4-192">Elektronik Tablo</span><span class="sxs-lookup"><span data-stu-id="5b5f4-192">Spreadsheet</span></span>|<span data-ttu-id="5b5f4-193">Çalışma sayfası</span><span class="sxs-lookup"><span data-stu-id="5b5f4-193">Worksheet</span></span> 
|<span data-ttu-id="5b5f4-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="5b5f4-194">**Excel**</span></span>|<span data-ttu-id="5b5f4-195">Excel dosyası</span><span class="sxs-lookup"><span data-stu-id="5b5f4-195">Excel file</span></span>|<span data-ttu-id="5b5f4-196">Sayfası</span><span class="sxs-lookup"><span data-stu-id="5b5f4-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="5b5f4-197">C# kullanımı</span><span class="sxs-lookup"><span data-stu-id="5b5f4-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<span data-ttu-id="5b5f4-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
##Veri kaynağı ayarları</span><span class="sxs-lookup"><span data-stu-id="5b5f4-198"><!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="5b5f4-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5b5f4-199">SQL Server</span></span>

<span data-ttu-id="5b5f4-200">komut dosyası toocreate hello ve doldurmak hello kişi tablosu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="5b5f4-201">dataSetName "." varsayılandır</span><span class="sxs-lookup"><span data-stu-id="5b5f4-201">dataSetName is “default.”</span></span>

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a><span data-ttu-id="5b5f4-202">Google E-Tablolar</span><span class="sxs-lookup"><span data-stu-id="5b5f4-202">Google Sheets</span></span>
<span data-ttu-id="5b5f4-203">Google belgeleri elektronik tablo adında bir çalışma sayfasıyla oluşturmak `Contact`.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="5b5f4-204">Merhaba bağlayıcı hello elektronik tablo görünen adı kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="5b5f4-205">Hello iç adını (kalın) dataSetName örneğin kullanılan toobe gerekiyor: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  hello sütun adları eklemek `Id`, `LastName`, `FirstName` toohello ilk satır, ardından üzerinde veri doldurma sonraki satır.</span><span class="sxs-lookup"><span data-stu-id="5b5f4-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="5b5f4-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="5b5f4-206">Salesforce</span></span>
<span data-ttu-id="5b5f4-207">dataSetName "." varsayılandır</span><span class="sxs-lookup"><span data-stu-id="5b5f4-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b5f4-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b5f4-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
