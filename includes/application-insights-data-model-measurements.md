<span data-ttu-id="4b303-101">Özel ölçüler koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="4b303-101">Collection of custom measurements.</span></span> <span data-ttu-id="4b303-102">Merhaba telemetri öğeyle ilişkili ölçüm adlı bu koleksiyonu tooreport kullanın.</span><span class="sxs-lookup"><span data-stu-id="4b303-102">Use this collection tooreport named measurement associated with hello telemetry item.</span></span> <span data-ttu-id="4b303-103">Genel kullanım örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4b303-103">Typical use cases are:</span></span>
- <span data-ttu-id="4b303-104">Bağımlılık Telemetrisi yükü Hello boyutu</span><span class="sxs-lookup"><span data-stu-id="4b303-104">hello size of Dependency Telemetry payload</span></span>
- <span data-ttu-id="4b303-105">Merhaba isteği Telemetri tarafından işlenen sıra öğe sayısı</span><span class="sxs-lookup"><span data-stu-id="4b303-105">hello number of queue items processed by Request Telemetry</span></span>
- <span data-ttu-id="4b303-106">zaman o müşteri Sihirbazı Adım tamamlama olayı Telemetri toocomplete hello adım sürdü.</span><span class="sxs-lookup"><span data-stu-id="4b303-106">time that customer took toocomplete hello step in wizard step completion Event Telemetry.</span></span>

<span data-ttu-id="4b303-107">Sorgulayabileceğiniz [özel ölçümleri](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) uygulama analytics'te:</span><span class="sxs-lookup"><span data-stu-id="4b303-107">You can query [custom measurements](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) in Application Analytics:</span></span>

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > <span data-ttu-id="4b303-108">Özel ölçümler, ait oldukları hello telemetri öğesi ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="4b303-108">Custom measurements are associated with hello telemetry item they belong to.</span></span> <span data-ttu-id="4b303-109">Bu ölçümler içeren hello telemetri öğeyle konu toosampling oldukları.</span><span class="sxs-lookup"><span data-stu-id="4b303-109">They are subject toosampling with hello telemetry item containing those measurements.</span></span> <span data-ttu-id="4b303-110">tootrack kullanım diğer telemetri türlerinden bağımsız bir değere sahip bir ölçü [ölçüm telemetri](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4b303-110">tootrack a measurement that has a value independent from other telemetry types, use [Metric telemetry](../articles/application-insights/app-insights-api-custom-events-metrics.md).</span></span>

<span data-ttu-id="4b303-111">En fazla anahtar uzunluğu: 150</span><span class="sxs-lookup"><span data-stu-id="4b303-111">Max key length: 150</span></span>
