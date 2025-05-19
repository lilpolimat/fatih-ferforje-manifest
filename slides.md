# Fatih Ferforje SEO-Adapted Multilingual Landing Manifest
(Klavyenizdeki Space tuşu ile akışa göre devam edebilir, geri dönmek istediğinizde yine klavyenizdeki ok tuşları ile yönlendirebilirsiniz)

Tüm sayfaları inceleyip arasında ok tuşları ile gezinmek için "O" harfine tıklayın. Mobilden erişim sağlıyorsanız, lütfen slide'ı yatay şekilde inceleyin, Touchscreen özellikleri deaktif edildi.
---

## Mevcut SEO

Fatih Ferforje’nin mevcut web uygulaması, geçmişte yapılan SEO çalışmaları ve köklü kod tabanı nedeniyle karmaşık bir yapıya sahip. Görsel ağırlıklı, interaktif kataloglar ve optimize edilmemiş içerikler, uygulamanın performansını ve SEO başarısını ciddi şekilde kısıtlıyor. <span class="highlight-red">Teknik altyapı, modern SEO gereksinimlerini karşılamaktan uzak.</span>
 
***

#### Performans problemleri


Uygulamada Lazy-loading kullanılmıyor. Tüm içerik, end-user herhangi bir sayfayı talep ettiği an yüklenmeye zorlanıyor ve bu sayfalara erişim süresini daraltıyor.
<li class="fragment fade-in">Bu, temel kullanıcı davranışlarına aykırı bir kullanıcı deneyimi yaratıyor zira istatistiklere göre kullanıcı, talep ettiği sayfanın ilk 3 saniye içerisinde tam anlamıyla yüklenmemesi ve ilgisini çekmemesi durumunda sayfayı terk ediyor.</li>

***

Uygulamada kullanılan tasarım, genel tasarım prensiplerine uygun değil. Kullanılan HTML Classlar obfuscation geçirmemiş(kopya ihtimaline karşı karıştırma/karmaşıklaştırma) ve Türkçe yazılmış.

***

#### Tasarım yanlışları

<li class="fragment fade-in">Grid yapısını korumak için boş div classlar ile ortalama yapılmaya çalışılmış. Bu, SEO ve LCP metriği bakımından performansa ket vuran, semantik nitelik barındırmayan ve kullanıcının deneyimine zarar veren bir yaklaşım.</li>

***

Obfuscation geçirmemiş HTML, Page Ripper yazılımlarla doğrudan kopyalanabilir -> Her ne kadar sektörünüzde karşılaşmanız neredeyse imkansız olsa da copy-cat dolandırıcılık yöntemleri için uygulamanız kopyalanabilir ve firmanız adına açılmış sahte, görüntüde aynı fakat arkada kötü niyetler yürütülen yazılımlarla karşılaşabilirsiniz. Bu en çok finans ve telekomünikasyon sektöründe gerçekleşir fakat başınıza kesinlikle gelmeyeceğinin garantisi yok.

***

Obfuscation geçirmiş HTML iskeletleri yine kopyalanabilir ama değişiklik yapmak ya da yeni sayfalar yaratmak zorlaşır, **net bir çözüm değildir lakin faydalıdır, aynı zamanda ilerleyen kısımlarda değineceğim crawling tehlikelerine karşı çok güçlüdür.**
<li class="fragment fade-in">
 Verimli ve ücretsiz CDN çözümleri bulunmasına rağmen, (CloudFlare-daha önce kullanıp güvendiğim ve kesinlikle ideal bir çözüm- ya da ücretli alternatif Vercel vs.) uygulamada herhangi bir CDN barındırılmıyor. Bu, barındırma servisi sağlanan jeolokasyon haricinde(Hostingin bulunduğu vilayet ya da ülke) uygulamadaki içeriklere ulaşmayı zorlaştıran en önemli faktörlerden birisi. Görsel içeriklerin yüklenmesinde hız, lazy-loading ve CDN sayesinde mümkün oluyor. 
</li>

***

CDN, Web sitesinde bulunan ve kullanıcıya yüksek öncelikle ulaştırılması gereken içeriklerin ülke ya da dünya üzerinde dağıtık sunucularda barındırılmasını ve HTTP Request durumunda, yani herhangi bir kullanıcının aplikasyona erişim sağlamak istemesi sonucunda bu içerikleri en yakın sunucudan çekmesini mümkün kılıyor. 
<span class="highlight-red">Modern webte kullanılması elzem ve mevcutta kullanılmaması büyük bir eksiklik.</span>

***

# Teknik bakımdan SEO

Google’ın index kurallarında önde gelen performans kriterleri, mevcut aplikasyon tarafından karşılanmıyor. Domain geçmişi ve mevcut içeriklerin yıllanması sebebiyle yerel markette arama motoru başarısı elde edilse de bu, rakip firmalardan herhangi birinin daha randımanlı çalışma yapmasıyla ekarte edilebilecek bir avantaj. Kısa vadede yerel uygulamada bu durumun çözülmesi, kod tabanı değişmeden imkansız.
***

<li>
<strong>First Contentful Paint</strong> -> 1800ms -> Bu metrik, kullanıcının web sayfasını gördüğü ilk andır. "Sayfa tamamen yüklendi" hissiyatını yaratan metrik budur. Elimizdeki oran, orta kritik.
</li>
<img src="https://wicki.io/posts/2021-07-core-web-vitals/FID-imdb.gif" style="max-width: 500px; display: inline-block;">

***

## FCP problemine sebep olan başlıca faktörler
<li class="fragment fade-in">
    <strong>
    Çok fazla JavaScript, özellikle 3. Parti
    </strong>
    (daha yalın bir JavaScript kullanımıyla çözümleyeceğiz)
</li>
<li class="fragment fade-in">
    <b>
    Dış kaynaktan çekilen iframeler, reklam vb. 3. parti kaynaklar
    </b>
    (Kullanılacak her imaj/kaynak, optimize edilecek)
</li>
<li class="fragment fade-in">
    <b>
    Code-splitting kullanmamak
    </b>
    (SvelteKit gibi modern bir çözümde bu, Vite tarafından yerel olarak hiçbir ek çaba gerektirmeden sağlanır)
</li>

***
<li>
<strong>Largest Contentful Paint</strong> -> 9100ms -> Sayfadaki en büyük içerik ögesinin, fotoğraf/video/başlık vs. yüklendiği andır. Bu metrik, mevcut uygulamamızda haddinden kötü durumda.
</li>
<img src="https://wicki.io/posts/2021-07-core-web-vitals/LCP-techcrunch.gif" style="max-width: 500px; display: inline-block;">

* Örnekte görüleceği üzere kabul gören 1700ms gibi oranlarken, bizde bu 9 saniyeye kadar sıçrayabiliyor.

***

## LCP problemine sebep olan başlıca faktörler
<li class="fragment fade-in">
    <strong>
    Yavaş sunucu cevabı
    </strong>
    (CDN kullanarak ve asıl hostu optimize ederek çözeceğiz)
</li>
<li class="fragment fade-in">
    <b>
    Render-blocking Javascript ve CSS
    </b>
    (Yüklenirken sayfayı donduran CSS ve JS kodları)
</li>
<li class="fragment fade-in">
    <b>
    Yavaş resource load time
    </b>
    (Yine CDN gibi çözümlerin zayıf olması ya da kullanılmaması sonucu oluşur)
</li>
<li class="fragment fade-in">
    <b>
    Client-side rendering
    </b>
    (Biz bunu SvelteKit ile Server-side yapıp ortadan kaldıracağız)
</li>

<span class="highlight-green">Pre-load etiketleri kullanıp, ilk elementin boyutunu ne kadar büyük tutarsak,
    teknik olarak LCP'ye de o kadar mani oluruz.</span>

***

<li>
<strong>Cumulative Layout Shift</strong> -> 1754ms -> Sayfa yüklenirken ögelerin sağa sola kayma ve düzensiz bir görüntü oluşturma miktarı. Uygulamamızda şu an çok kayma olduğunu söylüyor, iyi değil. Tolere edilecek rakamlar 0-200, en ideali 100ms ve altı.
</li>

<img src="https://wicki.io/posts/2021-07-core-web-vitals/CLS-giphy.gif" data-preview-image style="max-width: 500px; display: inline-block;">

***

## CLS problemine sebep olan başlıca faktörler

<li class="fragment fade-in">
    Boyut yani "size" etiketi olmayan imaj bileşenleri
</li>
<li class="fragment fade-in">
    Asenkron kaynak talepleri sonucu bileşenlerin farklı zamanlarda yüklenmesi
</li>
<li class="fragment fade-in">
    <b>Lazy loaded bileşenler</b>
    Her ne kadar lazy-load kategori sayfaları ve devamlı yüklenen içerikler için elzem olsa da yüklenen ilk sayfada kullanılması problemler doğurur.
</li>

***


<li>
<strong>General Speed Index</strong> -> 7700ms -> Sayfanın öncesinde listelenen metrikler dahilinde genel olarak ne kadar hızlı yüklendiğini gösterir. Elimizdeki rakam çok kötü ve düzgün SEO çalışmaları için sonraki uygulamamızda bu oranlara çıkmamak çok önemli.
</li>

***

# Link-Building bakımından SEO

İncelenen en yakın rakipler(arama sonuçları baz alınarak) bizimle aynı miktarda anasayfa backlinklerine sahip. Backlink, kısaca bizden bağımsız lakin otoriter web sayfalarının, özellikle sektörle ilişkiliyse bizden bahsetmesi anlamına geliyor. Sektörle ilişkili web sayfalarından bizim sayfamıza çıkartılan dış bağlantılar, backlink tabanını oluşturur. 

***

Fatih Ferforje’nin belli sayfalarında neredeyse binlerce back-link bulunsa da bunların çoğu Facebook referanslı katalog paylaşımları ve verimli bir link building stratejisi izlediğimiz söylenemez. SEO başarısında en yüksek nitelikli fayda elemanı backlink olduğundan; yeni bir aplikasyon ya da SEO projesinde link building’e önem vermek daha nitelikli ve sonuçları daha gözlemlenebilir bir konsept.

***

# İçerik bakımından SEO

SEO'nun omurgasını oluşturan ilk faktör, düzenli içerik üretimidir. Mevcut uygulamamızda bu, sağlıklı bir biçimde bulundurulmuyor. İyi bir içerik tedarik politikası izlenmeli; <span class="highlight-green">içerik ve backlink SEO performansının başrollerini oynuyor. </span>

***

İçerik ürtiminde de gözetilmesi gereken kurallar var.

En temel örnekler:
<li class="fragment fade-in">
Başlıklar H1 vurgu etiketli, alt başlıklar H2, H3 vs.
</li>
<li class="fragment fade-in">
Paragraflar "p" etiketli, vurgular "strong" içeriyor vb.
</li>
<li class="fragment fade-in">
İçeriğin semantik olması HTML’den bağımsız bir durum. Yayınlayan kişi hata yaparsa HTML de hatalı olur, vurgulamalar doğru olmalı.
</li>

***
SEO için en verimli kelime sayısı 1500 ve üzeri. Google, zengin içeriğe değer veriyor. 1500 kelimede ortalama 30 kez anahtar kelime vurgusu yapılabilir. Bu da çok verimli bir içerikte kullanılacak anahtar kelime havuzunda uygulamanın öne çıkma ihtimalini çok arttırabileceğimiz anlamına gelir. 

***

Dikkat edilecek en önemli nokta, içeriklerin özgün ve kopyalanamamış olması. Google, Duplicate Content için bir çeşit ceza skoru barındırıyor ve cezalı alan isimleri arama sonuçlarında algoritma tarafından geriye itiliyor. Alan adımızın ceza geçmişi mümkün olduğunca incelenmeli ve sorunlar ayıklanmalı.

***

# Kanaat

SEO, üzerinde ne kadar çalışma yapılırsa yapılsın içerik ve link-building olmadan yüksek başarı yakalanacak bir konu değil. Sadece varlığımızı sürdürerek başarı yakalamamız asırlar sürer. Performans sorunları çözüldükten sonra doğruca medyatik bir girişimde bulunulmalı ve marka, kendi sektöründe içerik bakımından yayılmaya başlamalı. <span class="highlight-green">SEO = Düzenli içerik + Backlink + Performans</span>

***

<span class="highlight-red">İzlenen mevcut yol ile başarılı SEO planları ve rekabet düşünülemez.</span>

***

Ben sizin bu sorunu tamamen çözmenizi sağlayacağım.

---

<section data-mask="true" data-background-transition="fade" class="white-text">

## Mevcut Tech-Stack

</section>

---

Web sitenizde kullanılan tüm teknolojileri, teknik bir bilgi sahibi olmadan görüp sıra sıra araştırarak anlayabilirsiniz. https://builtwith.com/
Web sitenizin bağlantısını bırakın, kullanılan teknolojilerin hepsi önünüzde listelenecek.

***

Uygulamamız şu an Vanilla PHP, JQuery gibi eski teknolojiler ile sağlanıyor ve muhafaza ediliyor. Her ne kadar bunlar SEO’ya doğrudan zarar vermiyor olsa da bu kod tabanının güncellenmesi, bakım görmesi ve güvenlik açısından kalibre edilmesi zorlaşır. Kod tabanında inherit edilen, yani her sayfaya yansıyan ve yanlış yapılan tek bir semantik hata; sitede tekrar eden onlarca, belki yüzlerce SEO düşmanı hataya dönüşür. Kendimizi bundan korumak için mümkün olan en yalın tech-stack anlayışını kullanmamız gerekiyor.

---

### Güvenlik Kaygıları
Doğrudan web sitesi hedef alınarak veriler ele geçirilebileceği gibi, SEO çalışmalarında rakip firmalar gray-zone tekniklere başvurarak bizden backlink çalabilir ya da bizi geri düşürmek için başka teknikler kullanabilir. Bir sonraki aşamada bu detaylara daha kapsamlı yaklaşacak olsam da bahsetmek istediğim en büyük endişelerden biri, Vanilla PHP ve JQuery uygulamalarda form içeriklerinin sanitize edilmemesi ve gerekli önlemler alınmaması durumunda XSS(Cross Site Scripting) ya da SQL Injection(Veritabanına yetkisiz isteklerde bulunarak uygulamayı hacklemek) zaafiyetlerine sebep olabilmesi. 

***

**En yaygın web zaafiyetlerini tespit eden OWASP projesine göre XSS ve SQL Injection, dünyanın en yaygın iki zaafiyeti.** Çalışılan firmadan bu konuda herhangi bir uygulama söz konusu mu, söz konusuysa ne gibi teknikler kullanılıyor hususunda bilgi alınmalı. İş planlarımız bir noktada teknik ve SEO odaklı olmaktan çıkmalı ve güvenliğe de yönelmeliyiz.

<span class="highlight-green">İlgi duyarsanız, Burp Suite/OWASP ile güvenlik raporlarını oluşturup size iletebilirim.</span>

***

#### Crawling
Crawling, bir web sitesi üzerinde hedef alınan toplu içerikleri (Örn. fiyat bilgisi, ürün ismi/görseli/tipi) tek bir dedicated-script ile toplamak anlamına gelir. Industrial/Manufacturing klasmanı web uygulamalarında rakip firmalar ya da market araştırması yapmak isteyen Marketing/Startup Agency’ler, bu gibi tekniklere başvurarak iş akışı ve ürün gamı hakkında haksız biçimde bilgi elde edilebilir. 


---

#### Kritik

**Fatih Ferforje’nin robots.txt dosyasında buna mani olmak için koyulmuş kurallar ya da yasal uyarılar yok.** Tüm içeriklerimizi herkese hiçbir yaptırım olmaksızın verebileceğimizi beyan ediyoruz. Arama motoru ve kanun, bu konuda bir koşul taşıyorsak bunu robots.txt metnimize yazmamızı, yazmıyorsak da barındırdığımız her bilginin topluca alınabileceğini belirtiyor.

***

### Hacklink’e sebep olabiliriz.
Hacklink, bir web sitesinden haksız biçimde backlink çıkışı almak için kullanılan yöntemlerdir. Bizim rızamız ya da bilgimiz olmadan sektörden herhangi bir firma ya da kişi çalışma yapmak isterse, hacklink satışı yapan şahıs ve oluşumlar, web sitemize rakip firmalara dair linkler gömebilir. Form submit sanitization ve dış kaynak veri girişleri iyi ayarlandığı sürece kolayca engellenebilir. Ayrıca nadir bir durumdur. Şimdilik main-concern çerçevesinde değerlendirilemez. Zannımca sektördeki kimse, bu gibi tekniklere dair bilgi sahibi değil. Web kaynak kodu kontrol edilerek çok kısa zamanda web sitesi hacklink barındırıyor mu diye kontrol edilebilir.

***

## Mevcut uygulama
Mevcut uygulama multilangual özellik taşıyor lakin .com.tr uzantıda yürütülüyor. Bu, multi-locale SEO yaklaşımının (dizin dil desteği -> /en, /fr, /ru) ccTLD seviyede sadece Türkiye içerisinde uygulanması anlamına geliyor. Bu, uluslararası açılım için yeterli gelemez; siz de bu kaygıyla Multi-site bir yaklaşımda bulunmak istiyorsunuz.

***

Necip Bey, sadece sizin okuduğunuzu varsayarak ya da ben sunmuyorsam diye size ithafen konuşuyorum. İzlediğiniz mimari yanlış ya da sonuçsuz kalacak bir mimari değil. SEO için birden fazla uygulama ile jeolokasyon hedef almak, aslında doğru ve uzun vadede çok fayda sağlayacak bir yaklaşım. Lakin bunun eğer düzenli bir SEO stratejisi kullanacaksak sürdürülebilir olmadığını belirtmem gerekiyor. İlk görüşmemizde bunu yeterli biçimde açıklayamadığımı varsayıyorum, heyecanımı makul görün.

***

Teknik açıdan bir uygulamanın başarılı ve sağlıklı olabilmesi için düzenli bakım görmesi, kontrol edilmesi ve içerik eklenebilmesi adına düzgün bir iş akışına sahip olması gerekir. Bu hedef, başlıca tek bir uygulama için hiçbir çaba gerektirmeden uygulanabilir olsa da birden fazla uygulama kullanılması durumunda düzgün mimari olmadan çok sayıda problem yaratır.

***

### Statükocu yaklaşım, SEO’ya düşmandır.
Mevcut durumu korumak/kurtarmak maksadıyla ileriye dönük SEO hamleleri yapmamak, kısa vadede durumu kotarıp orta ve uzun vadede alınabilecek olanlardan çok daha düşük ve/ya kötü sonuçlar doğurur. Birlikte kuracağımız sistemin akışını beğendiğiniz vakit, yerel uygulamamız dahil markanın tüm dijital kimliğini dönüştürmeyi arzu ediyorum. Sunumumun sonunda, bu konuda bana katılacağınza inanıyorum.

---

<section data-background-transition="fade" data-mask="true">

## Mevcut ilerlemenin dezavantajları

</section>

---

#### 1 - Merkezi olmadan dağıtık uygulamalar, sürdürülemez.

Birden fazla ccTLD (ülkeye göre ayrılmış alan isimli) odaklı uygulama, backlink trafiği ve zamanla kazanılacak yerel alan adı otoritesi için ideal bir yaklaşım. Amazon, kendi hizmetleri için bu yöntemi kullanıyor lakin teknik mimari bakımından sizden farklı yaptığı bir şey var. Amazon, sürekli bakımı ve kataloglamayı sağlamak için merkezi bir back-end mimarisinden faydalanıyor.

***

Sizin fikriniz özünde doğru ve verimli fakat teknik açıdan henüz merkezi bir kontrol mekanizması içermiyor. Bu, ilerleyen süreçte sorunlara sebep olur.


***

#### Amazon, bu yaklaşımdan faydalanabilmek için Headless CMS kullanıyor.

Hayal edelim. 8 ülkede barındığımızı düşünelim ki bu sayı, onlarca olabilir. İngiltere’de, Rusya’da, Nijerya’da, Kenya’da, BAE’de, Türkiye’de, Amerika’da ve Avustralya’da varolmak istiyoruz. 

***

Bulunduğumuz her ülke için optimize edilmiş alan isimleri ve hosting çözümleri kullanıyoruz. Buraya kadar her şey normal ve mantıklı.

***

<span class="highlight-red">Problem, bu uygulamaların hepsinin aynı anda bakımını yapabilmekte, bu uygulamalara içerik eklemekte.</span>


***

Uygulamalarımıza düzenli içerik akışı olmadan, yeni özellikler eklenmeden ve mevcut teknoloji güncellenmeden, SEO konusunda da marka imajımızı, kalitemizi yansıtmakta da başarılı olamayız. Bu sorunun önüne geçmek için her birine ayrı ayrı bakım yapmak, her biri için ayrı bir içerik takvimi yaratmak isteyebilirsiniz. Evet, çözüm bu ama beraberinde yaşanabileceklerden bahsetmek isterim.

***

#### İlk Müdahale
Her ülkede içerik yayınlamak ve her ülke için yazılan uygulamaya bakım sağlamak. <span class="highlight-red">Evet, imkansız değil ama tercih edilebilecek en zahmetli yol.</span>

<li class="fragment fade-in">
Artık her ülke için dependency geliştirdiğimiz bir freelancer yazılımcı ya da yazılım ajansı ve yazılım tabanı var.
</li>
<li class="fragment fade-in">
Uygulamamıza bakım yapmaları için onlara bağımlıyız ve çıkar çatışması durumunda başka insanları bulmak için bürokratik bir kabus yaşayacağız. Teslim edilen yazılımdan anlayacak yeni insan bulma kaygısı, süreci daha da zor hale getirir.
</li>

***

Her ülke için ayrı bir içerik üretim akışı seyretmek, işleri karmaşıklaştırır. Geri dönüşler yakalanıp incelenemez, <span class="highlight-red">yapılan işin kalitesi ve gelişim süreci takip edilemez olur.</span>

***

<li>
İçerik yükü arttıkça redaksiyon, düzenleme ve masraf sıçrama yapacak. İçerikleri eklemesi ve yönetmesi için firmadan bağımsız birden fazla insana bağımlı olacağız. Uzun vadede sürdürülebilir değil ve masraflı.
</li>

***

Sosyal medya hesaplarımız ve izlediğimiz öteki pazarlama/SEO stratejileri ile çatışma doğacak. Bunların arasındaki senkronizasyonu sağlayamaz duruma geleceğiz.

***

## Hakimiyet azalacak, bağımlılık artacak.
Kozmopolitik bir SEO ve marka açılımı stratejisi benimsediğimiz sürece, marka imajına ve yapılanlara hakimiyetimizi kaybedeceğiz çünkü bu, merkezi bir ticari oluşum için fazla merkeziyetsiz bir internet yaklaşımı. Size en başında altdizin fikrini, /en, /fr, /ru stratejisini tavsiye etmemin sebebi bu. Çok daha az masrafla çok daha fazla bütünlük ve avantaj yaratacak başka stratejiler var. 

***

#### Scalability problemleri
Yeni bir modül geliştirdiğimizi varsayalım, artık internet üzerinden sipariş yönetmek istiyoruz ya da yeni bir uygulama fikrimiz var. Bunun entegrasyonunu sağlamak için her bir ülkedeki temsilciler ya da yazılımcılar ile ayrı bürokratik süreç başlar. Her ülkenin farklı çerez politikaları, farklı yazılım kuralları var. Zaman içerisinde istismara açık çerez politikalarıyla, yönetilemez bir sürece adım atacaksınız. 

<span class="highlight-red">Yeni bir modülü her codebase’e ayrıca entegre etmek, tek bir masrafı bulunduğunuz ülke sayısı ile çarpmanız anlamına geliyor. </span>

***

#### Analitiklerin takibi zorlaşır
Her yazılım için ayrı bir analitik çözüm kullanmak ya da her uygulama için ayrı Google Console hesabına bakmak zorunda kalmak, kullanıcı deneyimini ve SEO stratejilerimizi iyileştirmek için ihtiyaç duyduğumuz verilerden mahrum kalmamız anlamına geliyor.
---

<section data-mask="true" data-background-transition="fade" class="white-text">

## Çözüm önerisi: Hibrit Yaklaşım

</section>

---

Altdizin fikri size verimsiz geliyor olabilir ve bu doğal bir kaygı. Birçok marka hala altdizin stratejisini kullansa da siz daha vizyoner bir yaklaşım sergileyip jeolokasyon odaklı ilerlemek istiyorsunuz. Bu, takvimi tersine çeviriyor. Kısa vadede alan adı otoritemizden faydalanamıyoruz ve dağıtık bir gelişim tablosu göreceğimiz anlamına geliyor.

***

Orta vade ve uzun vade hedeflerine olumlu katkısı olduğunu da biliyoruz.

<li class="fragment fade-in">Orta ve uzun vadede her ülkede ayrı bir oluşuma sahip oluyoruz. Bu, otoriteyi paylaşmamak ama kusurlu içerikler doğrultusunda o otoriteye yanlışlıkla zarar vermememek anlamına da gelir. Adil bir risk dağılımı ve avantaj feragatı söz konusu.</li>
<li class="fragment fade-in">Orta ve uzun vadede her biri ayrı web sitesi yaklaşımı, kendi içerisinde link-building stratejisi izlenebilecek bir networking yöntemine dönüşür.</li>

***

Google, otoritesi yüksek ccTLD uzantılara önde yer vermekten hoşlanan bir algoritmaya sahip. Orta ve uzun vadede ülke odaklı alan adı, SEO planınızda zamanla sarsılmaz bir otorite yaratmaya müsait.

***

Jeolokasyon odaklı ccTLD SEO planlamasında, her bir alan adının kendi konumunda otorite geliştirmesi gerekiyor. Her ülke için farklı bir gelişim sergileyeceğimizden eminim çünkü tahminimce sektöre dair arz-talep dengesi her ülkede farklı durumda. Siz bu dengeyi tanıdığınızdan, hangi ülkede ne hızda SEO başarısı yakalayabileceğimizi de kendi mesleki sağduyunuzla tahmin edebilirsiniz. Dilerseniz birlikte çalışmaya karar vermemiz durumunda her ülke özelinde anahtar kelime araştırması da yapabiliriz.

***

Şimdi ikimizin ortak noktada buluşacağı, bu sunumun da asıl amacı olan fikire gelelim. Ben merkezi bir içerik dağıtım yaklaşımını benimsememiz gerektiğini savunuyorum. Siz de dağıtık bir SEO stratejisi izlemek istiyorsunuz. İkisini birleştirdiğimizde, halihazırda Toyota, Mercedes-Benz, Amazon gibi büyük markaların da tercih ettiği Merkezi API Endpoint - Multi-site mimarisi ortaya çıkıyor.

---

<section data-mask="true" data-background-transition="fade" class="white-text">

## Geliştirilecek Uygulama

</section>

---

Size teklif ettiğim mimari, iki ana parçadan oluşuyor. Bunlardan immutable olan kısım; Headless CMS kısmı. Yani asla radikal bir değişiklik olmayacak ve devamında yapılacak her şeyin, atılacak her adımın merkezi olacak.

***

İkinci ve mutable olan parça, kopyalanabilir bir landing uygulaması; brochure page de diyebiliriz. Bu uygulama, gücünü merkezi CMS'ten alarak, dilediğiniz kadar kopyalanabilecek. Yani aslında tek bir uygulama yazıp, bulunmak istediğimiz her ülkede yayına sokacağız.

***

### 1. Parça - Headless CMS
Headless CMS nedir diye aratmak zorunda kalmayın, burada tanımını yapayım. WordPress ve Joomla gibi çözümleri tanıyorsunuz ve dünya üzerindeki web sitelerinin büyük bir kısmını WordPress yürütüyor, bu bakımdan CMS yaklaşımının verimli ve başarılı olduğunu biliyoruz. Yine de dezavantajları söz konusu. 

***

Gerçek hız istiyorsak, bizim WordPress’in gövdesine ihtiyacımız yok, ayrıca her ülkede ayrı bir WordPress altyapısı yürütmek sancılı olabilir. Gövdeden kastım, siteyi açtığınızda gördüğünüz her şey. Content Management, fonksiyonel bakımdan aşikar şekilde ihtiyaç duyduğumuz bir unsur fakat onu gösteren arayüze ve ek middleware ve pluginlere ihtiyacımız yok. Bu yüzden başlıksız, Headless bir CMS tercih edeceğiz. 

***

Headless CMS kullanarak ulaşacağımız hedefler arasında:

<li class="fragment fade-in">Çoklu site ve dil desteği</li>
<li class="fragment fade-in">İnteraktif kataloglama</li>
<li class="fragment fade-in">Düzenli içerik üretimi için altyapı</li>
<li class="fragment fade-in">Tam kapasite SEO otomasyonları</li>
<li class="fragment fade-in">Yüksek hızlı, SSR ve SSG gibi performansa yönelik render paradigmalarına tam destek bulunuyor.</li>

***

#### Çoklu site ve dil desteği

## Müşterinin dilini konuşuyoruz.

<img src="https://payloadcms.com/_next/image?url=https%3A%2F%2Fl4wlsi8vxy8hre4v.public.blob.vercel-storage.com%2Fadmin%20i18n-dark-1.webp&w=3840&q=90" data-preview-image style="max-width: 400px; display: inline-block;">

Uygulama deploy aşamasına geldiğinde, her bir ccTLD(country code top level domain) düzeyinde yayınlanacak olan web sitelerinizin hem arayüzünü, hem içeriğini, hem de SEO kalibrasyonunu otomatik şekilde gerçekleştirebileceksiniz. Aynı masrafı tekrar tekrar her ülke için yapmak yerine, merkezi bir yayın politikasıyla bu sorunların tamamını çözüp; yeni pazarlara açılma hızınızı arttıracak ve SEO konusunda hata yapılması ihtimalini yok edeceksiniz.

***

<span class="highlight-green">Her dil için ayrı kategoride, hangi ülkede ve hangi dilde ne yapıldığını takip edebilecek, her şeyi birbirinden ayırabileceksiniz.</span>

***

#### İnteraktif kataloglama

## Görmek mi istiyorsun? Web sitemizde var.

<img src="https://payloadcms.com/images/docs/admin-dark.jpg" data-preview-image style="max-width: 500px;">

Uygulamayı MVP formuna getirdikten sonra, SEO için de büyük bir katkı yaratacak **Custom Product Page** ayarları aşamasına geçeceğiz. Hem tüm katalog interaktif ve gezilebilir hale gelecek, hem de bu, SEO operasyonunuza yardımcı olmak için metin tabanlı içeriklerle desteklenerek sağlanacak.

***

<span class="highlight-green">Kataloğunuzu çok kolay ve hızlı şekilde değiştirebilecek, üzerinde güncelleme yapabileceksiniz.</span>

***

#### Düzenli içerik üretimi

## Kendi bültenimiz, kendi blog özelliğimiz var. 


<img src="https://api.backlinko.com/app/uploads/2020/05/seo-content.png" data-preview-image style="max-width: 500px;">

SEO'nun omurgasını oluşturan düzenli içerik kuralını yerine getirecek ve bunu büyük bir yetkinlikle yapacak içerik üretim akışını uygulamalarınızın tamamına dahil etmiş olacaksınız. 

***

#### Seo otomasyonları

## SEO için para ödemeye gerek yok. Zaten otomatik yapacağız.

<img src="https://moz.com/images/assets/features/Blog-post-images/What-is-SEO/8-Technical-seo.png?auto=compress%2Cformat&fit=crop&dm=1744396362&s=d2ce3c6d17cd6b97f9b78bea3f873b1a
" data-preview-image style="max-width: 500px;">


Yazacağımız uygulama, üretilen her içeriğin ve web sitesindeki her bir sayfanın SEO uyumlu olduğundan emin olacak. Arama motorunun talep ettiği tüm teknik nitelikleri yaratacağımız her bir sayfaya, her bir içeriğe otomatik olarak ekleyeceğiz. **hreflang, canonicalUrl, metadata, Schema.org için JSON-LD veriler**

***

Artık SEO için ajans aramaya ya da hatanın nerede olduğunu bulmak için zaman kaybetmeye gerek kalmıyor. <span class="highlight-green">SEO'yu bir kere kalibre ettiğimizde, her daim SEO uyumlu bir internet kimliğine sahip olacağız.</span>

***

#### SSR, SSG

## Her çeşit paradigmaya uygun, her biçimde optimize bir uygulama mimarisi.

<img src="https://tsh.io/wp-content/uploads/fly-images/25386/ssr-ssg-overview-559x355.png
" data-preview-image style="max-width: 500px;">

SSR(Server Side Rendering), SSG(Static Site Generating) gibi güncel ve hız için gerekli olan Rendering paradigmalarına tam hakimiyet. SvelteKit'in sade gücü ile hem statik, hem dinamik renderları performans için kalibre edip kullanabileceğiz.

---
<section data-mask="true" data-background-transition="fade" class="white-text">

## Temel optimizasyon hedefleri

</section>

---

#### Tüm ccTLD(ülke odaklı) uzantılar için segmentasyon

country_code, region etiketleri/ülke tanımlama ile her ülke için ayrı marketing ve SEO operasyonları yürütme kabiliyetine kavuşacağız.

***

hreflang, meta-data, canonicalUrl, sitemap otomasyonları ile her şeyin SEO uyumlu olduğundan 7/24 emin olabileceğiz.

***

Merkezi CMS'te locale seçenekleriyle her ülke için ayrı yönetim paneli bulunduracağız.

***

#### Merkezi analitik

Analytics API ve sosyal medya API'ler ile internet üzerinden edindiğimiz tüm etkileşimi mümkün olduğunca merkezi CMS yazılımımızda toplayacak ve yorumlanabilir hale getireceğiz.

***

## Rich Snippet yakalamak için Schema.org JSON-LD çözümleri
Rich Snippet, web sayfası bağlantılarıyla birlikte beliren özel önizlemelerdir(fiyat ya da yayıncı bilgisi, değerlendirme/yıldız sayısı vs.). Bu snippetın yakalanması her açıdan kalite duygusu uyandırır ve arama sonuçlarında kullanıcının markamıza yönlenme ihtimalini arttırır. Bilinen bir SEO taktiğidir.

***

#### Nasıl yakalanır?

| Gereklilik                                    | Açıklama                                                                                                  |
| --------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Şemalara uygun etiket tanımlamaları yapılmalı | price,rating,author gibi etiketlerle içeriğe Rich Snippet yakalamak için kullanılacak verilerin verilmesi |
| JSON-LD veri üretilmesi                       | JSON-LD bir veri çeşididir ve Rich Snippet için gerekir. Landing kısmında üretilebilir.                   |
| Düzenli rich result testi (Schema.org)        | Bu sayede içerikte yanlış var mı yok mu kontrol edilir ve gerekli düzenlemeler yapılır.                   |

**Rich snippet yakalamak, haftalar sürebilir.**

***

##### Opsiyonel - Webhook ile Slack entegrasyonu
İlerleme durumlarına ya da başka sebeplere bağlı olarak çalışmayı yürüten rollere otomatik ileti yollayabilme kabiliyeti, Webhook entegrasyonları ile çeşitli otomasyonlar geliştirebileceğiz. Bu otomasyonlar arasında otomatik sosyal medya paylaşımları, takvimli mailler ve başka hedefler olabilir.

***

### Sosyal medya ile entegrasyon
Tüm sosyal medya hesaplarının, aktivitesinin ve etkileşimlerinin merkezi yönetimi/kontrolü. Web uygulamalarındaki hareketlere dayalı takvimlenmiş yeni paylaşım yaratma, API desteği mevcutsa düzenleme/silme kabiliyeti

***

## Layout as Data

CMS üzerinde implement edilecek bu fonksiyonla, pazarlama birimi ya da teknik bilgisi bulunmayan kişiler, web sayfasının düzeni üzerinde doğrudan değişiklik yapabilir. 

Web sitesi üzerindeki bileşenler, yani görünen metin kutuları, başlıklar, fotoğraflar veri üzerinden döndürülebilir ve akabinde CMS üzerinde modifikasyona uğrayabilir. Bu ilerici, önemli sayılabilecek ve çok verimli bir teknolojidir. İlk aşamada entegrasyonu ehemmi olmasa da sonraki aşamalarda ele alabilir ve geliştirilmesi için adımlar atabiliriz. 

***

## Preview Özelliği
Üretilen içeriklerin yayına sokulmadan önce canlı biçimde incelenebilmesi ve nihai hali hakkında fikir sahibi olunabilmesi, geri dönüşlere göre yayın görmeden tekrar düzenlenebilmesi için Preview özelliği bulunacak.

---

## 2. Parça - Landing

İçeriğini dilediğimiz gibi seçebildiğimiz, üzerine ek özellikler getirebileceğimiz bir uygulama olacak. Kimiz? Ne yapıyoruz? Nasıl yapıyoruz? Ne satıyoruz? Kataloglarımız, tanıtımlarımız, iletişim bilgilerimiz. Bana gösterdiğiniz Rusya portunu ele alabilirsiniz; sabit bir iskelet üzerine yayılmak istediğimiz ülke için eklemeler ve değişiklikler yaparak tekrar tekrar kullanabileceğimiz bir yazılım.

***

Bu yazılımların toplu biçimde kontrolü, bakımı, düzenlenmesi yine ofisinizde dilediğiniz zaman girip inceleyebileceğiniz Headless CMS üzerinden yapılacak.

***

<span class="highlight-green">Dilediğimiz zaman başka bir ülkeye bir saatlik çabayla açılabiliriz,  -> web sitesinin çevirisi ve gerekli API bağlantıları -> sonrası Tek Tık -> Deployment, artık o ülkenin internet pazarındayız.</span>

---
<section data-mask="true" data-background-transition="fade" class="white-text">

#### Landing için kriterlerimiz

</section>

---

## Georouting
Kullanıcının konumunun doğru tespiti ve bu tespit doğrultusunda alakalı uzantıya yönlendirilmesi. Dil/bölge değişimini önce biz tespit edip doğru yere yönlendireceğiz. Sonrasında kullanıcı isterse dilediği dilde arayüzü görüntülemeye devam edebilecek.

Kullanıcının IP adresi ya da tarayıcıda tercih edilen dili ile gerekli yönlendirme yapılıyor.

Bu hizmet, Amazon, Booking, Netflix, Mercedes, Ikea gibi dev markalarda uygulama gören, yaygın, sağlıklı ve SEO dostu bir yaklaşım.


***

Web sitemizde kullanılacak sayfaların ve içeriklerin SEO uyumlu olduğundan emin olmak için kendi iş akışlarımızı yazacağız ve her şeyin SEO uyumlu ilerlediğinden emin olacağız. Sorunları oluşmadan ortadan kaldıracağız ve bir daha SEO çalışmaları için ayrı masraf yapmanıza gerek kalmayacak.

***

## Daha estetik tasarım
Temel CSS animasyonları dışında GSAP kütüphanesi ile zenginleştirilmiş arayüz ve marka kimliği ile bağdaşan tipografi, renkler ve spacing. Kullanılacak menü ve sayfa yapısı componentleri hususunda tasarım aşamasına geçilince daha detaylı incelenip hassas kararlar vereceğiz. <span class="highlight-green">Eski nesil ve çekici olmayan tasarımlar kullanmayacağız.</span>


***

## Gerekirse sosyal medyadan doğrudan içerik alışverişi
Sosyal medya ile web uygulamaları arasında tam senkronizasyon sağlanabilir ve sosyal medya hesaplarından alınacak veri web sitemizde, web sitesinden alınanlar da sosyal medyada kullanılabilir.


***

## ileride kalibre edilmiş yapay zeka ile müşteri desteği
İlerleyen zamanlarda pek çok markanın entegre ettiği özel eğitimli yapay zeka modelleriyle sektöre ve firmaya özel chatbotlarla ekleme yapabilir, web sitesinin Call to Action fonksiyonlarını geliştirebiliriz.

---

<section data-mask="true" data-background-transition="fade" class="white-text">

#### Kullanacağımız teknoloji

</section>

---

Hızlı geliştirme, bakım kolaylığı ve verimlilik bağlamında arayüzü yazmak için SvelteKit kullanabiliriz. Avantajlarını gösterdiğimde sizin de benimseyip kabul edeceğinize inanıyorum. SvelteKit dinamik bir arayüz geliştirme kütüphanesi, yani bu; her bir sayfanın yeni bir HTTP isteği oluşturmadan, dinamik şekilde yükleneceği anlamına geliyor. Kullanıcı bir sayfadan başka bir sayfaya geçerken dönen bir daire görmeyecek ya da beklemeyecek;

***

Seç -> Tıkla -> Arkaplanda oluşturulan sayfa tarayıcıya sunulsun-Beklemeden, sayfa yeniden yüklenmeden, yükleme daireleri çıkmadan.

<li class="fragment fade-in">Bu teknoloji sayesinde sayfanın tamamı değil, sadece değişmesi gereken bileşenler değişip güncellenir. Çok daha hızlı bir deneyim yaratır. SvelteKit gibi frameworklerin kullanılmasındaki başlıca amaç, bu smooth experience'ı yaratmaktır.</li>

<img src="https://blog.openreplay.com/images/single-page-apps-vs-multiple-page-apps/images/GU2qJvu.gif" style="max-width: 720px; display: inline-block;">

***

#### Svelte hızlı mı?

Beklentilerimizi fazlasıyla karşılayacak şekilde hızlı ve SSR(Server Side Rendering) kullanıldığı sürece %100 SEO uyumlu. Güncel teknolojileriniz, bunu sağlamanın kıyısından bile geçemiyor çünkü her sayfa ve talep için yeni bir request yollayıp, statik bir sayfa döndürüyor. Bu SEO’ya her koşulda doğrudan ket vurmasa da kullanıcı deneyimi bakımından tatsız bir görsel oluşturuyor. Size örneklerini gösterdiğimde aradaki farkı ben belirtmeden hissedeceksiniz.

***

Headless CMS stratejisiyle birlikte kullandığımız arayüzde her teknolojiyi gönlümüzce revize edebilir, dilersek tamamen baştan yazabiliriz çünkü içeriğimiz, kataloglarımız ve göstermek istediğimiz her bilgi merkezde güvenli biçimde bekleyecek. Biz, bunların kullanıcıya nasıl iletileceği konusunda tamamen özgürüz. Mevcut uygulamada bunu mümkün kılmak tam anlamıyla imkansız.

***

<span class="highlight-red">Bu konsept yerine dağıtık uygulamalar ve veritabanları mimarisi kullanmamız durumunda yeni bir teknoloji uygulamak istedik diyelim, güncellemeyi her şeye en baştan başlayıp aylar sürecek masraflı bir prosese dönüştürmüş oluruz.</span>

---

### Güvenlik

OWASP 10(En yaygın 10 zaafiyet) için bilgim dahilinde mümkün olduğunca yeni mimarimizin güvenilirliğini, mevcut ya da potansiyel açıkları ve nasıl örtülebilecekleri ile ilgili çalışmaları da yürütebiliriz. Yan disiplinim diyebileceğim kadar tutku beslediğim ve asıl sanat olarak değerlendirilebilecek alan, güvenlik mimarisidir. Bu konuda da kesinlikle dış kaynaklara bağlı kalmadan kendi çapımızda belli bir noktaya kadar faaliyet yürütebiliriz.


***

## Geliştirme aşamasında kaygılar
Geliştirme aşamasında yaşanacak herhangi bir proje terk etme ya da kod tabanı çalma kaygısına karşın, firmaya tahsis edilmiş özel ve tek bir Github hesabında projenin tüm versiyonlama geçmişini inceleyebilir ve yorumlayabiliriz. Kaynak kodu ve ne yapıldığı her an takip edilmiş olur, sürece başkalarını dahil etmek kolaylaşır.


---

## Mimarinin avantajları
En başında altdizin yönetimi yapmak, çok sancılı bir süreç. Siz bunu tek seferde ıskartaya çıkartıyorsunuz; jeolokasyon odaklı SEO gelişiminde bu kaygıya sahip değiliz ve aslına bakılırsa bu, fark etmeden bile olsa dil konusunda hata yapılamayacağı anlamına geliyor. Bu perspektiften stratejiniz, çalışacağınız yazılımcı için mükemmel.

***

#### 1 - Kiminle çalışacağınızı seçmekte özgürsünüz
Benimle çalıştığınızı varsayalım, bir sebepten yollarımızı ayırmak zorunda kaldık ya da artık benimle çalışmak istemiyorsunuz; bu teknolojilerin kullandığı dili ve yöntemleri anlayan herhangi bir insanı IT departmanınızda administrator koltuğuna oturttuğunuz an, her şey devroluyor. Tek bir kod tabanı var ve bakımını Denizli’de yapıp, her ülkeye yarım saat içinde yollayabiliyorsunuz. Her ülkede farklı yazılımcıyla çalışmaya gerek yok. Yapılan her doğru ve yapılan her yanlış, her ülkedeki uygulamaya doğrudan ulaşıyor. Takip etmek, yakalamak, geri dönüşleri inceleyip aksiyon almak çok daha basit. Biz şimdi kimi getireceğiz, bu iş nasıl hallolacak kaygısından kurtuluyorsunuz. **Evrensel ve kuralcı.**

***

#### 2 - Redaktör ve içerik üretici masraflarımız var, biz istediğimiz sürece yazacaklar ve istemediğimiz sürece tüm ilişikleri kesilecek.
Sistemimiz üzerinde kimin yetki ve etki sahibi olduğunu doğrudan takip edebilecek, istenmeyen durumlara tek bir noktadan müdahale edebileceğiz. Tek bir içerik ürettiğimizi varsayalım, mevcut yaklaşımla merkezi API yaklaşımı arasındaki farklardan bahsedeyim.

***

Bir içerik yayınladık, dövme demirin moleküler yapısından ve nasıl şekillendiğinden bahsettik. İçerik 12 farklı dilde 12 farklı ülkede yayına girecek,


<ul class="fragment fade-in">
<li style="text-align: left; color: red;">
<b>Dağıtık Mimaride Nasıl Olacak?</b>
<p>
Her bir içerik farklı ülke için tutulmuş yerel ya da denizaşırı yazara çevriltilecek, ayrıca redaksiyon ve kontrol için de bizden bağımsız bir süreç yürütülmesi gerekecek.
</p>
</li>
<li style="text-align: left; color: green;">
<b>Headless CMS mimarimizde nasıl olacak?</b>
</li>
<p>
Yerel ya da denizaşırı yazar fark etmeksizin, kontrollerini sağlayabileceğimiz içerik oluşturma sürecine merkezi API'mız üzerinden dahil olacak. Süreç bizim müşahedemiz ile tamamen entegre.
</p>
</ul>

***

<ul>
<li style="text-align: left; color: red;">
<b>Dağıtık Mimaride Nasıl Olacak?</b>
</li>
<p>
İçeriğin yayınını sağlayacak olan kim? Yazan kişi çoğu zaman nasıl yayınlanacağı ile ilgilenmez, teknik birilerine ihtiyaç var. Düzenli şekilde ilgilenen birisi varsa metin ona iletilecek ve yayınlanması sağlanacak.
</p>
<li style="text-align: left; color: green;">
<b>Headless CMS mimarimizde nasıl olacak?</b>
</li>
<p>
İçeriğin yayını sizin ya da süreci kontrol eden otoriteye kalmış, tek bir tıkla tüm çeviriler kendi portlarına push edilebilir ya da beğeni kazanamadıysa bekletilebilir/yok edilebilir. Her port için ayrı bir teknik sürece gerek yok, metin yazıldı ve yayın bekliyor.
</p>
</ul>

***

<ul>
<li style="text-align: left; color: red;">
<b>Dağıtık Mimaride Nasıl Olacak?</b>
</li>
<p>
İçeriğin doğru yayınladığından emin olmamız gerekiyor. URL Path ve SEO-Adapted olduğu teyit edilecek, tüm kontrol prosesi firmadan ya da yine remote bir otorite sayesinde mümkün olacak fakat zaman kaybı ya da masraf kaçınılmaz.
</p>
<li style="text-align: left; color: green;">
<b>Headless CMS mimarimizde nasıl olacak?</b>
</li>
<p>
Metnin yayınlanma süreci, zaten standart hale getirdiğimiz kurallar doğrultusunda gerçekleşecek. Her yerde aynı, her yerde standart. Firmanın prensipleri bu konuda da standart ve kaliteli. URL-Path her ülkede standart, arama motoru bunu beğenir. Hiçbir içerik kopya değil, sadece dil farklı. Duplicate Content ihtimali yok, kontrol dilediğimiz noktada sağlanacak. SEO uyumlu olduğundan henüz metin yayınlanmadan eminiz.
</p>
</ul>
***

<ul>
<li style="text-align: left; color: red;">
<b>Dağıtık Mimaride Nasıl Olacak?</b>
</li>
<p>
İçeriğin geri dönüş miktarları takip edilemeyecek ya da çok zorlaşacak, aldığı etkileşim, ne kadar verimli oldu, ne kadar tık aldı, gördüğü etkileşimi sürdürmek için aynı konuda yeni bir içerik yayınlayacak mıyız, bu yol haritasını kim çıkaracak?
</p>
<li style="text-align: left; color: green;">
<b>Headless CMS mimarimizde nasıl olacak?</b>
</li>
<p>
İçeriğin geri dönüşleri standart bir şemada merkeze akacak. Her şeyi detaylı biçimde inceleyip, bir sonraki aksiyonu planlayabileceğiz. Kullanıcı neyi beğendi, hangi bilgiyi yakaladı? Net biçimde biliyoruz. Neyi doğru neyi yanlış yaptığımızı ayırt etmek çok daha kolay.
</p>
</ul>
***

<ul>
<li style="text-align: left; color: red;">
<b>Dağıtık Mimaride Nasıl Olacak?</b>
</li>
<p>
Bu stratejide öznelere karar vermek imkansız ve süreci kimin yöneteceğini bilmek çok zor, aktör sayısı çok fazla; takip edilemeyecek kadar fazla.
</p>
<li style="text-align: left; color: green;">
<b>Headless CMS mimarimizde nasıl olacak?</b>
</li>
<p>
Bu stratejide özneler tanımlanabilir, kimin nerede ne görev alacağı doğrudan seçilebilir ve süreci doğru bir hiyerarşide yönetebiliriz.
</p>
</ul>


---


## Merkezi kontrol
Tüm sürece hakim olmak ve incelemek, tek bir merkezden hareketle operasyon yürütmeniz durumunda ulaşması çok daha kolay bir hedef. Bu yaklaşımla birlikte internetteki tüm varlığımız, her daim kontrol edilebilir ve incelenebilir olur. Firmaya özel bir kontrol ağacı yapısı yarattığımızı varsayabiliriz.

---

## GDPR, KVKK ve robots.txt ile sitemap üzerine net politikalar

Kullanılacak çerez ve robot politikaları, crawling’e ve kullanıcı verisini nasıl işlediğimize dair net kurallar çizip web sitesinin hem yasal, hem sektörel bakımdan meşru olduğunu açıklığa kavuşturacağız. Ayrıca izinsiz ve haksız bilgi elde edilmesi konusunda birtakım prensipler belirleyeceğiz ki bu bence gelişmiş rakip taleplerine/araştırmalarına karşı çok önemli bir adım. 

---

## Dokümantasyon ve özel personel eğitimine uygunluk

Süreci standartlara kavuşturduktan sonra bu alanda çalışacak personelin talimi, tutulması ve çalıştırılması daha mümkün ve daha ucuz hale gelecek. İçerik üretimi ve takibi için outsourcing ya da Türkiye pazarında çözümlere başvurulabilir, gerekli insan kaynağı kolayca sağlanabilir. Dokümantasyon ve eğitim modülleri ile SEO politikası konusunda kendi personelimizin bilinçlenip daha az masrafla daha verimli operasyon yürütmesi hedeflenebilir.

---

## Mikroservis mimarisine dönüşüm şansı
### API-First development yaklaşımı
En başından itibaren API odaklı ilerleyeceğimizden, bunu bu sade ve basit haliyle sürdürebilir ya da gelişimini sağlamak için mikroservis mimarisine geçişi mümkün kılabiliriz. Mikroservis mimarisi kısaca bir uygulamanın fonksiyonlarının mümkün olduğunca parçalanıp birbirinden bağımsız fakat köprü bağlantılarla senkron çalışmasıdır. Bu modele perakende ticaret için modüller eklenebilir ya da daha farklı özellikler geliştirilebilir.

***

## Docker/Kubernetes Swarm
Çaba çok büyüdüğünde, hizmet konteyner havuzuna çevrilebilir ve her fonksiyon parçası için ayrı departman ya da iş akışı yaratılabilir. Bu konu erken ve orta safhada ihtiyaç duyulacak bir şey olmadığından detaylandırma ihtiyacı duymuyorum.

---

## Kullanılabilecek ek stratejiler & Off-page SEO çözümleri

***

### 1 - Mikro siteler ve Subdomain Stratejisi
Ürün yelpazesindeki en başarılı kalemler için ayrı product page’ler üretilebilir ve buraya akacak trafik, asıl web uygulamasına yönlendirilebilir. Bu, teknik zahmeti göze aldığınızda sektör için izlenebilecek verimli yöntemlerden birisi. Sadece marka adına değil, ürün adına da web sayfaları oluşturmak. Çok kısa ve sade olacağından, kendisine bağlı içeriklerle odaklanılan keywordde hızlı başarı elde edilebilir.

***

## 2 - Backlink trafiğini alışverişe çevirmek
Alışveriş yaklaşımıyla farklı web kaynaklarıyla iletişime geçip backlink alışveişi/trafiği yapabiliriz.

***

## 3 - 3. Parti Kaynaklara Yayılma
Video pazarlama(YouTube, TikTok, Instagram), medium.com, LinkedIn gibi sektöre dair veri akışı sağlanabilecek üçüncü kaynaklara yönelebilir, backlink sayısını bu yöntemle arttırabilir ve daha fazla trafik çekebiliriz ki bu mutlaka inceleyip uygulamamız gereken bir yaklaşım çünkü çoğu sektörde sık sık tercih ediliyor.

***

## 4 - Content Gap Analizi
Bizden daha başarılı olduğunu fark ettiğimiz andan itibaren rakibin formülü parçalanır ve içeriği oluşturmakta, kullanıcıya iletmekte ne gibi prensipler incelediği belirlenir. Aynı anahtar kelime grubunda rekabet için aynı içerik prensipleri esas alınarak rakip içerikler üretilir.

***

## 5 - E-Mail Bülteni ve Öteki stratejiler
Bir E-Mail bülteni başlatarak sektörümüzde hobicilere ya da girişimlere bilgi vermek adına çeşitli bültenler düzenleyebiliriz. Bilgiye verilen değer açık olduğundan, insanlara bilgi dağıtımı yoluyla fayda yaratmak en güçlü marketing/SEO stratejilerinden birisi.

## Alan Adı Seçimi
Görüşmemizden sonra ideal alan adı kaydı için neler yapabileceğimizi inceledim.
Domain seçiminde gözetilmesi gereken birkaç kural var, en temel prensip -> hatırlanabilir olması. Bu bağlamda underscore-dash (_ ve -) gibi özel karakterler ve sayılar kullanılmaması tavsiye ediliyor. Anahtar kelimeden yürüyeceğimiz için, birtakım seçeneklerle kısıtlıydık.

1. Forge/Ferforje transkripsiyonu
2. Wrought Iron ya da aynı contexti içeren başka bir kelime/öbek

***

İncelediğim zaman aynı sektörde faaliyet gösteren markaların çoğunlukla Forging ya da Wrought Iron gibi tamlamalar yerine **Iron Works** öbeğini ya da doğruca bir ek olarak **Iron** kelimesini kullandıklarını fark ettim.
Örnekler;

<li class="fragment fade-in">
<b>usaironworks.com</b> - Kullandıkları Header -> Iron Works U.S.A | Iron Doors, Railings,Gates, Fences ...
</li>

<li class="fragment fade-in">
<b>stewartironworks.com</b> - Kullandıkları Header -> Stewart Iron Works | Timeless Custom Iron Works Projects
</li>

<li class="fragment fade-in">
<b>dufferiniron.com</b> - Kullandıkları Header -> Sadece marka ismi -> Dufferin Iron® & Railings
</li>

***

Bu bağlamda, tercihimiz **ironworks** ya da **iron** olabilir. Fikrinizi belirtirseniz müteşekkir kalırım.

---

#### Takvim
İlk 2 haftada tasarım için mock-up ya da yetişmezse Worst Case Scenario olarak UI/UX diyagram paylaşabilirim, uygulamanın hem nasıl görüneceği hem de nasıl çalışacağı konusunda hatrınızda net bir taslak oluşur. Sonrasında uygulamanın tam anlamıyla MVP halini alıp pilot denemelere müsait hale gelebilmesi için 2 aylık bir vade yeterli olur.

***

SEO-Adapted olmanın ne kadar süreceğini tam anlamıya kestiremesem de sürecin 4~6 ay içerisinde tamamlanacağına ve sonrasında da ilk 6 ay içerisinde SEO çalışmamızın geri dönüşlerini toplayacağımıza inanıyorum. Karşılaşabileceğimiz teknik aksaklıkların az olduğunu düşünüyorum. Bu haliyle sürecin hızlı ilerleyeceği kanaatindeyim. MVP uygulamaları ve CMS API’ı birkaç ayda yayına sokabileceğimize eminim, bu süreçte SEO odak konusu olduğundan ciddi bir fine-tuning/cilalama aşaması gerekiyor. Bu fine tuning aşamasının yani SEO kalibrasyonunun ne sürede sağlanacağından emin değilim fakat beklentim en uzun süreyle 6 ayda bu multilingual SEO projesinin tam fonksiyonel olup hızla ivmelenmeye başlayacağı yönünde.

***

Süreci uzun ve sancılı görecek olursanız, bizim yapacağımız şeyin her bakımdan sıfırdan inşa olduğunu ve bunun marka itibarı/yayılma performansı açısından ziyadesiyle ileriye dönük bir yatırım olduğunu lütfen göz önünde bulundurun. Başarılı SEO, yüzbinlerce liralık reklam bütçesinden daha iyidir. Teklif ettiğim şey basit bir SEO planı değil, markanın dijital dönüşümü.

***

#### Sadece Uygulama
SEO aşamasında bulunmamı ve sürekli çalışmayı arzu etmiyorsanız; Uygulamayı Multi-site biçimde kullanılacak hale getirip 3 ayda teslim edebilirim.
Burada karşılaşacağınız tek dezavantaj SEO aşamalarını yürütmesi için Headless CMS mimarisini ve SvelteKit’i tanıyan insan bulmak olur. 

***

SvelteKit ve Headless CMS üzerinde SEO yürütecek bir firmayı ben tanımıyorum, varsa da size yaygın olmayan bir teknoloji kullanmanızı fırsat bilip yüksek fatura çıkarır. Yaygın bir teknoloji kullanmamı isterseniz en yaygınlarını kullanırım, benim için kesinlikle sorun değil. Bu durumda da codebase’in yani uygulamanın kaynak kodunun karmaşıklığı artacak ve tuttuğunuz insanların performansından emin olamayacaksınız, şu an olduğu gibi. **Bu kadar güncel, güzel ve sade teknolojilerle böyle büyük bir operasyon yürütüp başarı sağlayan marka sayısı iki elin parmağını geçmez. Her şeyin ilki olmak istiyorsak, birlikte çalışmamız çok uygun.**

***

#### Firmanızın kendi teknoloji/SEO doktrinini yaratabiliriz

Svelte, nispeten yeni bir teknoloji ve çok sade olmakla birlikte çok verimli. Halef programcılar bulabilir, hatta yetiştirebilirim. İnsan kaynakları masrafını kısmak için firmanın kendi teknoloji prensiplerine ve eğitim programına sahip olması oldukça güzel ve tercih edilebilecek en optimum yaklaşım.

***

Türkiye pazarında yazılım ve arama motoru optimizasyonu gibi konularda ciddi bir yanılsama var. İyi niyetiniz dahilinde rakamlara ve portföylere güvenerek hareket etmiş olabilirsiniz ki bu çok doğal ve doğru bir yaklaşım lakin maalesef bu coğrafyada bu alanlar fazla sanal ve gözlemlenemez olması dolayısıyla manipüle ediliyor. Yaratılan sentetik başarı ve yeterlilik algısıyla müşterinin ikna olması sağlanıyor.

---

# Başarıyı Nasıl Ölçeceğiz?

<li class="fragment fade-in">
Performansı ölçmek için keyword odaklı arama sonuçlarını inceleyecek ve organik trafiği mümkün olduğunca yakalayarak aldığımız geri dönüşü belirleyeceğiz.
    <li class="fragment fade-in">
    Harici keyword toollar dışında, custom eklentiler ile Analytics verileri CMS'e bağlanacak, başarının ölçülmesi ve takip edilmesi kolaylaşacak.
    </li>
</li>

<li class="fragment fade-in">
Bu kaynaklardan kazanılan müşterileri işaretlemek için çeşitli yöntemlere başvurabiliriz.
</li>

<li class="fragment fade-in">
Performans metriklerini düzenli takip edip, yapılan yanlışları rötüşlayarak ilerleyeceğiz.
</li>
    <li class="fragment fade-in">
    Bir hata varsa, temiz kod tabanında düzeltmek zor olmayacak ve tespiti de daha hızlı sağlanacak.
    </li>

<li class="fragment fade-in">
İlerleyen dönemlerde radarımıza girecek kadar trafik çeken bir rakip olursa, shadowing ve detaylı incelemeler ile aynı kelime grubunda hızlı aksiyon alacak, geri dönüşlerin takibiyle aşamalı ve rekabetçi SEO anlayışı uygulayacağız.
</li>

---

<section data-mask="true" data-background-transition="fade" class="white-text">

# Beklenti ve vade

</section>

---

## Beklenti 
Kullanacağımız tech-stack ve içerik/link odaklı SEO stratejisiyle, 6-12 aylık vadede seçtiğimiz kelime havuzlarında hedeflerimizi yakalayacağımızı, başarılı bir açılma süreci geçireceğimizi düşünüyorum. Kullanılabilecek en optimum stratejiyi kurguladığımızdan, teorik olarak başarısızlık imkansız. Sonucun vadesi değişse de ulaşılacak nokta hep aynı, bulunmak istediğimiz ülkelerde aramalara çıkacağız. Elbette bu, eğer orta vade başarı hedefleniyorsa bahsettiğim SEO stratejisi ile mümkün, öteki türlü ne kadar süreceğini öngörmek mümkün değil.

***

Yazılan uygulamanın başarısı, bir bakıma onu kurgulayan vizyonun ne kadar estetik bir yaklaşıma sahip olduğuyla ilgilidir. Ben, sizin markanızın bu vizyonu yaratıp sürdürebilecek yeterliliğe sahip olduğunu gördüm. Siz de aynı potansiyeli umuyorum ki bende yakalamışsınızdır. Kendimden emin biçimde belirteceğim tek husus, birlikte çalışmaya karar verirsek bu vizyonu geliştirmek için tüm bilgi birikimimi ve her seferinde daha ileriye gitmek için tüm çabamı kullanacağımdır.

---

### Recovery 
Kullanılan stratejinin başarısız olması durumunda izlenebilecek alternatif bir stratejiye ihtiyacımız var fakat o stratejiyi kurgulama ihtiyacında değilim zira her şeyi kitabına uygun yaptığımızda başarısız olmanın ihtimali yok, tek fark vade olabilir; o da yakalanan ilk analizlerle hızlıca öngörülebilir. Kaldı ki yapılacak tüm masraftan ve çekilecek tüm zahmetten sonra, bu projeyi geri çekmek akıl karı da değildir. Geriye dönük recovery mümkün olmayacağından, sadece masraf kalemlerinde yeniden kurgu mümkün olabilir:

***

#### Exit Strategy
<li class="fragment fade-in">
Redaksiyon ve yeni içerik üretimi ile reklam çıkışları durdurulur, sürdürülen düzenli masraf kalemi yok edilir ve otoritenin kendi kendine mevcut içerik havuzuyla gelişmesi beklenir.
</li>

<li class="fragment fade-in">
Hostingler mevcut düzende masraf yaratıyorsa, ucuz alternatiflere ya da tavizlere gidilir, barındırma masrafları yok edilir/azaltılır
</li>

<li class="fragment fade-in">
Mevcut uygulama ve içerik altyapısı için inovatif/farklı bir SEO stratejisi geliştirilir ve baştan başlanılır fakat hiçbir SEO stratejisi kapsam bakımından bundan ötesini başaramaz zira bu metni hazırlarken çok doğaçlamacı olmama rağmen değinilebilecek en önemli noktalara değindim ve ötesi için yapılabilecek pek bir şey yok.
</li>

<li class="fragment fade-in">
Exit tercih edileceği vakit, yapılan her şey kar olarak kalır ve yapılmayacak olanlar da kurtarılmış masraf olarak değerlendirilir.
</li>

---

## Çıkış ve Şahsi Mektup
SEO, kavram itibariyle prestijini kaybediyor. Google, arama sonuçlarında ve içerik süzme konusunda AI ithamlarıyla karşı karşıya. SEO uygulamalarının ne kadar verimli olduğu ve eskisi kadar önem arz edip etmediği konusunda hayatını SEO uygulamalarından kazanan mühendislerin dahi endişeleri var. Sektörünüz gereği misilleme babında yapay zeka uygulamalarını kullanmanız çok zor ve orta vade beklentilerinize ne çeşit cevaplar alacağınızı kestirmek mevcut markette/arama motorlarında zor.

***

Google artık içerik değerlemesi için sabit algoritmalar yerine yapay zeka kullanıyor, kendi bağımsız modelleri bulunduğu için bunu ne şekilde modifiye ettikleri ve kıstas olarak hangi parametreleri kullandıkları belirsiz. Bu AI değerlemelerinin SEO uygulamalarını tamamen yok edebileceğine dair fikir yürütenler var. 

***

Yine de şahsi kanaatime göre SEO uygulamalarına uygun stratejiler, AI değerlemelerden de geçer not alabilir zira bilginin esas olduğu bir ortamda parametreler ne kadar değişirse değişsin; bilgiye verilen değerin objektifliği sarsılamaz. Birlikte çalışırsak, bu dönemi de birlikte atlatacağımızı ve gerekli aksiyonu alacağımıza inanıyorum. 

***

Dilerseniz firmanızda bu operasyonla ilgilenen ya da bu operasyonda görevlendirilecek herkese yönelik daha sade, anlaşılabilir ve genel bir bilgilendirici sunum hazırlayabilirim. Lise yıllarımdan beri münazara ve konuşma geçmişi taşıyorum ve bu benim hobim sayılacak kadar tutkulu olduğum bir konu.

***

Hizmet verebileceğim tek alan bu değil. Daha önce bulunduğum firmada daily task automation konusunda çalışmalar yaptım ve stok takibi konusunda birtakım kurallar/metodlar yarattım. Çok verimli ve başarı sağlayan, kritik nitelikte hatalar yakalayan bir yaklaşımdı. Birlikte çalışırsak sadece web geliştirme konusunda değil, siz de dilerseniz iş akışı konusunda inceleme ve geliştirme yapmayı çok isterim.

---

### Şahsi
Necip Bey, beni kendi ofisinizde şahsen ağırlayıp saatlerinizi probleminizi anlatmaya ve beni dinlemeye ayırdığınız için çok teşekkür ederim. Umuyorum ki bu metin, size markanızın gelişmesi konusunda çok şey katacak. Portföyüm olmamasına rağmen uzunca konuşmanız bana benimsenecek, güzel hatırlanacak bir iş görüşmesi anısı yarattı. Mütevaziliğiniz ve şans tanımış olmanızdan mütevellit müteşekkirim.

***

Ülkemizde web geliştirme hala PHP ve JQuery ya da WordPress gibi basite kaçan çözümlerle savsaklanıyor. Bu teknolojiler her ne kadar berbat denecek kadar kötü ya da tamamen verimsiz denecek kadar eski olmasa da artık PHP’nin Laravel ya da Symfony olmadan kullanılması, uygulamada JQuery bulunması saçma. 

***

Ricam, fikir sahibi olmanız için web geliştirmeyle ilgili rastgele makaleler okumanız. Siz, doğrudan orta ya da büyük ölçekli bir işin asli sorumlusu olduğunuz ve bu dönemde markanızın internet varlığı için endişe duyduğunuz için ufkunuzu genişletmekte çok faydası olur. Çok spesifik olmadığı sürece herhangi bir şey okuyabilirsiniz. Sadece 3 gün bu alanda  birkaç genel deneyim ya da geliştirme makaleleri okuduğunuz an muhatap olduğunuz yerel çözümlerin yetersizliğini fark edeceksiniz.

***

Çapraz disiplinlerde gelişme arzusu bulunan alaylı bir programcı olarak, fayda yaratabileceğimden kuşkum yok.

---

Her daim sağlıklı, amacınızda muvaffak olmanız dileği ve en önemlisi,
saygılarla.

***

Hakan Altay Ağyar, 
15 Mayıs 2025

***

# Son
