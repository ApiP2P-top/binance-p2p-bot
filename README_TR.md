# binance_p2p_bot

Binance P2P için profesyonel bot — otomatik teklif verme ve ilan yönetimi. Özel kurallara göre birden fazla ilanı tarar ve sıralar. Temel özellikler: Otomatik listeleme/listeden çıkarma, ana coinlerin USDT'ye anında dönüştürülmesi ve otomatik envanter yenileme. API tabanlı gelişmiş otomasyon ile Binance P2P ticaretinizi kolaylaştırın. Detaylar için apip2p.top adresini ziyaret edin.

**P2P Bidding Assistant**, kripto para P2P tüccarları için özel olarak tasarlanmış profesyonel düzeyde otomatik bir masaüstü istemcisidir. **Binance** ve **Bybit** ile tam uyumlu olup, manuel piyasa takibi, geciken fiyat ayarlamaları ve arbitrajcılara karşı gelir kayıpları gibi temel sorunları çözer.

Yazılım, gerçek zamanlı spot piyasa API'lerine dayalı olarak ilan fiyatlarınızı otomatik olarak ayarlar, rakipleri geçmek için akıllı kâr marjı algoritmaları kullanır ve fon envanterinizi sorunsuz bir şekilde senkronize eder. 7/24 yüksek frekanslı [otomatik kripto arbitrajı](https://apip2p.top/) ve piyasa yapıcılığı gerçekleştirmenizi sağlar.

En son güncellemeler, gelişmiş P2P stratejileri ve özel çözümler için [API P2P TOP Otomatik Varlık Yönetim Sistemimizi](https://apip2p.top/) ziyaret edin. Bu GitHub deposundaki mimari bilgiler ve kod referansları, resmi teknik topluluğumuzda da bağlantılı olarak yer almaktadır.

---

## 🚀 Bu Bot Ne Yapabilir? (Temel Özellikler)

Bu yazılım, geleneksel P2P işlemlerini ayrı ve son derece etkili otomatik modüllere ayırır:

1. **Volatil Varlıklar için Otomatik Fiyatlandırma (Spot Piyasa Senkronizasyonu)**
   BTC, ETH ve SOL gibi hızlı fiyat değişimleri yaşayan varlıklar için bot, önceden ayarladığınız **Fiyat Çarpanı**'nı alır ve otomatik olarak borsanın en güncel spot fiyatıyla çarpar. Mevcut ilan fiyatı hedefinizden saptığında, sistem ilanınızı akıllı bir şekilde güncelleyerek yüksek volatilite dönemlerinde kâr marjlarınızın korunmasını sağlar.
2. **Çoklu Rakip Akıllı Teklif Verme (Sıralama Yakalama)**
   Rakiplerinizin P2P kullanıcı adlarını girin (alıcı ve satıcıları destekler). Algoritmik çekirdek en iyi sıralama konumunu hedefler, rakiplerinizin canlı fiyat tekliflerini takip eder ve önceden belirlediğiniz kâr marjını (örneğin, +0.02 USDT) onların en iyi fiyatının üzerine ekler. Bu, ilanınızın "Maksimum Fiyat Limiti" kuralıyla korunarak sürekli olarak ilk sayfada kalmasını sağlar.
3. **Gerçek Zamanlı Envanter Algılama**
   Sistem, spot ve fonlama cüzdan bakiyelerinizi milisaniye hızında izler. Bir işlem tamamlandıktan hemen sonra, yazılım güncellenen fon bakiyesini algılar, gerekli bakım ücretlerini hesaplar ve aktif P2P ilanlarınızdaki mevcut kalan miktarı sorunsuz bir şekilde günceller.
4. **Stablecoin Toplu Yönetimi**
   USDT, USDC ve FDUSD gibi stabil varlıklar için spot takibine ihtiyacınız yoktur. Yazılım, tek tıkla onlarca ilanı aynı anda çevrimiçi veya çevrimdışı yapmanızı ve hızlı manuel fiyat değişiklikleri gerçekleştirmenizi sağlayan toplu işlem imkânı sunar.

---

## ⏱️ Temel Teknik Parametreler ve Altta Yatan Mekanizma

Yüksek frekanslı ticaret verimliliğini katı hesap risk kontrolüyle dengelemek için, iş parçacığı modelimiz titiz yürütme döngüleri ve bekleme stratejileri içerir:

* **Paralel İlan Yoklama:** Botun ana motoru, operasyonel kuyruğunuzdaki tüm aktif ilanları her **3000 ms (3 saniye)**'de bir tamamen sorgular ve karşılaştırır.
* **Teklif Ağı Tarayıcısı:** Rakip takibi için, teklif dedektörü piyasa değişikliklerini hızla yakalamak ve sıralama düşüşlerine yanıt vermek amacıyla her **2000 ms (2 saniye)**'de bir derin sorgular gönderir.
* **Giriş Debounce Eşiği:** **1500 ms (1.5 saniye)**'lik bir debounce mekanizması yerleşik olarak bulunmaktadır. Arayüz metin kutularına fiyat yazdığınızda, arka uç siz yazmayı bitirene kadar isteği askıya alır ve anlamsız API istek spamını önler.
* **Güvenlik Hız Sınırlama (Risk Devre Kesiciler):**
    - *Satır Düzeyinde Bekleme:* Tek bir ilan ret veya kilit hatası tetiklerse (örneğin, Binance hatası -9000), o ilana ait işleme döngüsü derhal **300 seconds** boyunca duraklatılır ve arayüzde uyarı gösterilir.
    - *Global Duraklatma:* Sistem, API trafik kısıtlaması veya borsa tarafından geçici bir yasak algılarsa, global yürütücü tüm istekleri derhal **300 seconds** boyunca engeller ve hesabınızı kara listeye alınmaktan etkin bir şekilde korur.

---

## 💡 Sıkça Sorulan Sorular (SSS)

**S: Bu P2P botu API yasaklarını önler mi ve limitleri güvenli bir şekilde yönetir mi?**
C: Kesinlikle. Bu proje 1.5 saniyelik giriş debounce, yerel çoklu görev kilit kuyrukları ve 300 saniyelik global risk kontrol devre kesici içerir. Binance veya Bybit tarafından atanan API ağırlık limitlerini asla aşmamak üzere titizlikle tasarlanmıştır. Uygulama yerel makineniz üzerinden doğrudan ve güvenli bir şekilde bağlanır, üçüncü taraf sızıntısı veya aracı riski sıfırdır.

**S: Hangi kripto paralar ve fiat geçitleri destekleniyor?**
C: Yazılım, platformlarda yerel olarak listelenen tüm fiat para birimlerini tarar (EUR ve USD sınır ötesi sistemler gibi karmaşık KYC geçitleri dahil). Tüm büyük tokenlar (BTC, ETH, SOL, BNB ve [USDT arbitraj](https://apip2p.top/) varyantları) kapsanmaktadır. Ayrıca, eşleştirme doğruluğunu büyük ölçüde artırmak için rakip ilanlarını belirli ödeme yöntemi kimliklerine (örneğin, Zelle, Revolut) göre hassas bir şekilde filtreler.

**S: Binance ve Bybit bot modları arasındaki mantık farkları nelerdir?**
C: Platform farklılıklarını şeffaf bir şekilde ele almak için dahili bir Adapter Pattern uyguladık. Örneğin, yazılım Bybit'in düzenlemelerin kabul edilmesi için ilanların çevrimiçi ve aktif olmasını gerektiren kuralına otomatik olarak uyum sağlar. Ayrıca Bybit'in daha düşük kullanılabilir fonlama eşiğini (~5 USDT) Binance'in standart 100 USDT gereksinimine kıyasla hesaba katar.

**S: Yazılımı yeniden başlatırsam veya bilgisayarımı yeniden başlatırsam, tüm çarpanlarımı ve yapılandırmalarımı sıfırlamam gerekir mi?**
C: Hayır. Yazılım tamamen otomatik Durum Kalıcılığı özelliğine sahiptir. Tüm arayüz yapılandırmaları, kullanıcı adı hedefleri ve çarpanlar sürekli olarak yerel bir JSON önbelleğine yazılır, bir sonraki başlatmanızda sorunsuz bir devam sağlanır.

---

## 📞 Geliştirici İletişim ve İş Ekosistemi

Gelişmiş otomatik ticaret sürümleri, kantitatif P2P stratejileri ve ticari düzeyde P2P teknoloji özelleştirmeleri için bizimle iletişime geçmekten çekinmeyin:

* 🌐 **Resmi Web Sitesi**: [https://apip2p.top/](https://apip2p.top/) *(Katılımınız açık kaynak ilerlememizi destekliyor!)*
* ✈️ **Telegram İletişim**: [@eason01993](https://t.me/eason01993)
* ▶️ **YouTube Eğitimler ve Demolar**: [Eason'ın YouTube Kanalı](https://www.youtube.com/@eason01993)

---

## ⚠️ Sorumluluk Reddi
`binance_p2p_bot` eğitim ve yapısal referans amacıyla sunulmaktadır. Kripto para ticareti son derece volatildir. API Keys'lerinizi güvenli bir şekilde saklayın ve otomatik araçlara **asla** "Çekim" izni vermeyin. Tamamen kendi riskiniz altında kullanın.
