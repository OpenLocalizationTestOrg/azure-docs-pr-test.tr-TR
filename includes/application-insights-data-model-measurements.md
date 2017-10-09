Özel ölçüler koleksiyonu. Merhaba telemetri öğeyle ilişkili ölçüm adlı bu koleksiyonu tooreport kullanın. Genel kullanım örnekleri şunlardır:
- Bağımlılık Telemetrisi yükü Hello boyutu
- Merhaba isteği Telemetri tarafından işlenen sıra öğe sayısı
- zaman o müşteri Sihirbazı Adım tamamlama olayı Telemetri toocomplete hello adım sürdü.

Sorgulayabileceğiniz [özel ölçümleri](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA2WLOw6DMAyGd07hZoLeoRPqyMaGGAL8aiPhGCV2kKoeHsHK%2Bj1myyr8LoiaqfrT%2FkUCzRft4LMl8OUeL3LuLLIx%2BxR%2BIF8%2BtcoiNq2o78vgWuFthQaJ1AeGGxt6UlBwKxa1qQ6EpLhAfQAAAA%3D%3D&timespan=PT24H) uygulama analytics'te:

```
customEvents
| where customMeasurements != ""
| summarize avg(todouble(customMeasurements["Completion Time"]) * itemCount)
```

 > [!NOTE]
 > Özel ölçümler, ait oldukları hello telemetri öğesi ile ilişkilendirilmiş. Bu ölçümler içeren hello telemetri öğeyle konu toosampling oldukları. tootrack kullanım diğer telemetri türlerinden bağımsız bir değere sahip bir ölçü [ölçüm telemetri](../articles/application-insights/app-insights-api-custom-events-metrics.md).

En fazla anahtar uzunluğu: 150
