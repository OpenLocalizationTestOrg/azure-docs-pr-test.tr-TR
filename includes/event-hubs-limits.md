Aşağıdaki tabloda kotaları listeler ve Azure Event Hubs'a belirli sınırlar. Event Hubs fiyatlandırması hakkında daha fazla bilgi için bkz: [Event Hubs fiyatlandırması](https://azure.microsoft.com/pricing/details/event-hubs/).

| Sınır | Kapsam | Tür | Aşıldığında davranışı | Değer |
| --- | --- | --- | --- | --- |
| Ad alanı başına olay hub'ları sayısını |Namespace |Statik |Yeni bir ad alanı oluşturmak için sonraki istekleri kabul edilmeyecek. |10 |
| Olay hub'ı başına bölüm sayısı |Varlık |Statik |- |32 |
| Olay hub'ı her tüketici grupları sayısı |Varlık |Statik |- |20 |
| Ad alanı başına AMQP bağlantı sayısı |Namespace |Statik |Sonraki istekleri için ek bağlantıları reddedilir ve arama kodun bir özel durum aldı. |5,000 |
| Event Hubs olay en büyük boyutu|Sistem genelinde |Statik |- |256 KB |
| Bir Event Hub adının en büyük boyutu |Varlık |Statik |- |50 karakter |
| Dönem olmayan alıcılar bir tüketici grubu başına sayısı |Varlık |Statik |- |5 |
| Olay verilerini maksimum bekleme süresi |Varlık |Statik |- |1-7 gün |
| En fazla üretilen iş birimi |Namespace |Statik |Verilerinizi kısıtlanan neden olur ve oluşturur işleme birimi sınırını aşan bir  **[ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception)**. Üretilen iş birimleri için standart bir daha çok sayıda istek katmanı dosyalama tarafından bir [destek isteği](/azure/azure-supportability/how-to-create-azure-support-request). [Ek üretilen iş birimleri](../articles/event-hubs/event-hubs-auto-inflate.md) 20 taahhüt satın alma temelinde bloklarını mevcuttur. |20 |

