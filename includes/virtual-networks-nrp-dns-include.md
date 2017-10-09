## <a name="azure-dns"></a><span data-ttu-id="4ff69-101">Azure DNS</span><span class="sxs-lookup"><span data-stu-id="4ff69-101">Azure DNS</span></span>
<span data-ttu-id="4ff69-102">Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="4ff69-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="4ff69-103">Özellik</span><span class="sxs-lookup"><span data-stu-id="4ff69-103">Property</span></span> | <span data-ttu-id="4ff69-104">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ff69-104">Description</span></span> | <span data-ttu-id="4ff69-105">Örnek değer</span><span class="sxs-lookup"><span data-stu-id="4ff69-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ff69-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="4ff69-106">**DNSzones**</span></span> |<span data-ttu-id="4ff69-107">Etki alanı bölgesi bilgi toohost DNS kayıtlarını belirli bir etki alanı</span><span class="sxs-lookup"><span data-stu-id="4ff69-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="4ff69-108">/ subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com "</span><span class="sxs-lookup"><span data-stu-id="4ff69-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="4ff69-109">DNS kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="4ff69-109">DNS record sets</span></span>
<span data-ttu-id="4ff69-110">DNS bölgeleri kayıt kümesi adında bir alt nesne vardır.</span><span class="sxs-lookup"><span data-stu-id="4ff69-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="4ff69-111">Kayıt kümeleri, ana bilgisayar kayıtları bir DNS bölgesi için türüne göre koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="4ff69-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="4ff69-112">Kayıt türleri: A, AAAA, CNAME, MX, NS, SOA, SRV ve TXT.</span><span class="sxs-lookup"><span data-stu-id="4ff69-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="4ff69-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="4ff69-113">Property</span></span> | <span data-ttu-id="4ff69-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ff69-114">Description</span></span> | <span data-ttu-id="4ff69-115">Örnek değer</span><span class="sxs-lookup"><span data-stu-id="4ff69-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4ff69-116">A</span><span class="sxs-lookup"><span data-stu-id="4ff69-116">A</span></span> |<span data-ttu-id="4ff69-117">IPv4 kayıt türü</span><span class="sxs-lookup"><span data-stu-id="4ff69-117">IPv4 record type</span></span> |<span data-ttu-id="4ff69-118">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="4ff69-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="4ff69-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="4ff69-119">AAAA</span></span> |<span data-ttu-id="4ff69-120">IPv6 kayıt türü</span><span class="sxs-lookup"><span data-stu-id="4ff69-120">IPv6 record type</span></span> |<span data-ttu-id="4ff69-121">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="4ff69-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="4ff69-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="4ff69-122">CNAME</span></span> |<span data-ttu-id="4ff69-123">kurallı ad kayıt türü <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4ff69-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="4ff69-124">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="4ff69-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="4ff69-125">MX</span><span class="sxs-lookup"><span data-stu-id="4ff69-125">MX</span></span> |<span data-ttu-id="4ff69-126">posta kayıt türü</span><span class="sxs-lookup"><span data-stu-id="4ff69-126">mail record type</span></span> |<span data-ttu-id="4ff69-127">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/Mail</span><span class="sxs-lookup"><span data-stu-id="4ff69-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="4ff69-128">NS</span><span class="sxs-lookup"><span data-stu-id="4ff69-128">NS</span></span> |<span data-ttu-id="4ff69-129">ad sunucusu kaydı türü</span><span class="sxs-lookup"><span data-stu-id="4ff69-129">name server record type</span></span> |<span data-ttu-id="4ff69-130">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="4ff69-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="4ff69-131">SOA</span><span class="sxs-lookup"><span data-stu-id="4ff69-131">SOA</span></span> |<span data-ttu-id="4ff69-132">Başlangıç yetkilisi kayıt türünün <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="4ff69-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="4ff69-133">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="4ff69-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="4ff69-134">SRV</span><span class="sxs-lookup"><span data-stu-id="4ff69-134">SRV</span></span> |<span data-ttu-id="4ff69-135">Hizmet kayıt türü</span><span class="sxs-lookup"><span data-stu-id="4ff69-135">service record type</span></span> |<span data-ttu-id="4ff69-136">/Subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="4ff69-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="4ff69-137"><sup>1</sup> yalnızca kayıt kümesi başına bir değer verir.</span><span class="sxs-lookup"><span data-stu-id="4ff69-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="4ff69-138"><sup>2</sup> yalnızca bir kayıt türü SOA DNS bölgesi başına izin verir.</span><span class="sxs-lookup"><span data-stu-id="4ff69-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="4ff69-139">Json biçimindeki DNS bölgesini örneği:</span><span class="sxs-lookup"><span data-stu-id="4ff69-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="4ff69-140">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4ff69-140">Additional resources</span></span>
<span data-ttu-id="4ff69-141">Okuma hello [DNS bölgeleri için REST API belgeleri ](https://msdn.microsoft.com/library/azure/mt130626.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4ff69-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="4ff69-142">Okuma hello [DNS kayıt kümelerini için REST API belgeleri](https://msdn.microsoft.com/library/azure/mt130627.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4ff69-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

