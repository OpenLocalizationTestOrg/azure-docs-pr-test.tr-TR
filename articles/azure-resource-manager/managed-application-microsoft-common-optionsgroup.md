---
title: "aaaAzure yönetilen uygulama OptionsGroup UI öğesi | Microsoft Docs"
description: "Azure yönetilen uygulamalar için Hello Microsoft.Common.OptionsGroup UI öğesi açıklar"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="2bd49-103">Microsoft.Common.OptionsGroup UI öğesi</span><span class="sxs-lookup"><span data-stu-id="2bd49-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="2bd49-104">Seçim denetim kullanılabilir seçeneklerden bir satır.</span><span class="sxs-lookup"><span data-stu-id="2bd49-104">A selection control with a row of available options.</span></span> <span data-ttu-id="2bd49-105">Bu öğe kullandığınız zaman [yönetilen bir Azure uygulama oluşturmaya](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2bd49-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2bd49-106">Kullanıcı Arabirimi örneği</span><span class="sxs-lookup"><span data-stu-id="2bd49-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="2bd49-108">Şema</span><span class="sxs-lookup"><span data-stu-id="2bd49-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="2bd49-109">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="2bd49-109">Remarks</span></span>
- <span data-ttu-id="2bd49-110">Merhaba etiketi `constraints.allowedValues` öğenin hello görüntüleme metni ve değeri seçildiğinde hello öğesinin hello çıktı değeri.</span><span class="sxs-lookup"><span data-stu-id="2bd49-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="2bd49-111">Belirtilmişse, hello varsayılan değer mevcut bir etiketi olmalıdır `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="2bd49-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="2bd49-112">Belirtilmezse, ilk öğe olarak hello `constraints.allowedValues` varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="2bd49-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="2bd49-113">Merhaba varsayılan değer **null**.</span><span class="sxs-lookup"><span data-stu-id="2bd49-113">hello default value is **null**.</span></span>
- <span data-ttu-id="2bd49-114">`constraints.allowedValues`en az bir öğe içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bd49-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="2bd49-115">Bu öğe hello desteklemiyor `constraints.required` özellik; öğenin seçili toovalidate başarıyla olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bd49-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2bd49-116">Örnek çıktı</span><span class="sxs-lookup"><span data-stu-id="2bd49-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="2bd49-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bd49-117">Next steps</span></span>
* <span data-ttu-id="2bd49-118">Bir giriş toomanaged uygulamalar için bkz [Azure yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bd49-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2bd49-119">Bir giriş toocreating UI tanımları için bkz: [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bd49-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2bd49-120">Kullanıcı Arabirimi öğeleri ortak özellikleri açıklaması için bkz: [CreateUiDefinition öğeleri](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2bd49-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
