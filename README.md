# GlobalAIHub
Global AI Hub - Sürücüsüz Metro Simülasyonu (Rota Optimizasyonu)
Bu projede, bir metro ağında; iki istasyon arasındaki en hızlı ve en az aktarmalı rotayı bulan bir simülasyon geliştirilmeye çalışılmıştır.
Elbette, kodda kullanılan Python kütüphanelerini ve amaçlarını açıklayabilirim:

Kullanılan Modüller:
1. collections Modülü:
defaultdict:
Bu, bir sözlük (dictionary) benzeri veri yapısıdır. Ancak, bir anahtar (key) bulunmadığında, varsayılan bir değer döndürür.
Kodda, hatlar sözlüğünü oluşturmak için kullanılmıştır. Bu, her hat için istasyon listelerini saklamak için kullanılmıştır. Bir hata yeni bir hat adı ile çağrıldığında, hata ait boş bir liste otomatik olarak oluşturulur.
Bu, kodun daha temiz ve okunabilir olmasını sağlar, çünkü her yeni hat için manuel olarak boş bir liste oluşturmaya gerek kalmaz.

deque:
Bu, çift uçlu bir kuyruk (double-ended queue) veri yapısıdır. Hem baştan hem de sondan eleman ekleme ve çıkarma işlemlerini verimli bir şekilde gerçekleştirir.
en_az_aktarma_bul fonksiyonunda BFS (Genişlik Öncelikli Arama) algoritmasını uygulamak için kullanılmıştır. BFS algoritmasında, ziyaret edilecek istasyonları saklamak ve sırayla işlemek için bir kuyruğa ihtiyaç vardır. deque, bu amaç için idealdir.

2. heapq Modülü:
Bu modül, yığın (heap) veri yapısını uygular. Yığınlar, öncelik kuyrukları olarak da bilinir ve en küçük (veya en büyük) elemanı hızlı bir şekilde bulmak için kullanılır.
en_hizli_rota_bul fonksiyonunda A* arama algoritmasını uygulamak için kullanılmıştır. A* algoritmasında, keşfedilecek istasyonları maliyetlerine göre sıralamak ve en düşük maliyetli istasyonu seçmek için bir öncelik kuyruğuna ihtiyaç vardır. heapq, bu amaç için verimli bir yol sağlar.

3. typing Modülü:
Bu modül, Python'da tip ipuçları sağlamak için kullanılır. Tip ipuçları, fonksiyonların ve değişkenlerin beklenen tiplerini belirtmeye yardımcı olur.
Kodda, fonksiyonların girdi ve çıktı tiplerini belirtmek için kullanılmıştır. Bu, kodun daha okunabilir ve anlaşılır olmasını sağlar, ayrıca hataları erken yakalamaya yardımcı olur.
Dict, List, Set, Tuple, Optional gibi tipler kullanılmıştır.

Kullanılan Algoritmalar:
1. BFS (Genişlik Öncelikli Arama) Algoritması:
BFS, bir labirentte veya haritada yol bulmaya benzer. Başlangıç noktasından başlar ve adım adım ilerler.
İlk önce başlangıç noktasının tüm komşularını (yanındaki istasyonları) ziyaret eder. Sonra, bu komşuların komşularını ziyaret eder ve bu şekilde devam eder. Yani, önce en yakındaki yerleri, sonra daha uzaktaki yerleri ziyaret eder. Bu işlem sırasında, ziyaret edilen yerleri bir "kuyruk" (liste) içinde saklar. Hedef noktaya ulaştığında, izlediği yolu (rotayı) döndürür.
Neden Kullanıldı?
Bu uygulamada, en az aktarmalı rotayı bulmak için kullanıldı.
BFS, her adımda en yakın komşuları ziyaret ettiği için, en kısa yolu (en az aktarma ile) bulmada etkilidir.

2. A* Arama Algoritması:
A*, BFS'ye benzer, ancak daha akıllı bir şekilde çalışır. Her adımda, sadece en yakın komşuları değil, aynı zamanda hedefe olan tahmini uzaklığı da dikkate alır. Bu tahmini uzaklığa "sezgisel" denir. A*, hem mevcut yolun maliyetini (seyahat süresi) hem de sezgisel değeri birleştirerek en iyi yolu seçer. Bu sayede, hedefe daha hızlı ulaşır.
Neden Kullanıldı?
Bu uygulamada, en hızlı rotayı bulmak için kullanıldı.
A*, seyahat süresini ve tahmini hedef uzaklığını dikkate alarak, en kısa sürede varılacak rotayı bulmada etkilidir.

Örnek Kullanım:
# Senaryo 4: Kızılay'dan Keçiören'e
    print("\n3. Kızılay'dan Keçiören'e:")
    rota = metro.en_az_aktarma_bul("K1", "T4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("K1", "T4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))

Test sonucu: 
4. Kızılay'dan Keçiören'e:
En az aktarmalı rota: Kızılay -> Ulus -> Demetevler -> Demetevler -> Gar -> Keçiören
En hızlı rota (16 dakika): Kızılay -> Kızılay -> Sıhhiye -> Gar -> Gar -> Keçiören

Örnek Kullanım:
# Senaryo 5: AŞTİ'den Gar'a
    print("\n5. AŞTİ'den Gar'a:")
    rota = metro.en_az_aktarma_bul("M1", "T3")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
        
    sonuc = metro.en_hizli_rota_bul("M1", "T3")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))

Test Sonucu:
5. AŞTİ'den Gar'a:
En az aktarmalı rota: AŞTİ -> Kızılay -> Sıhhiye -> Gar -> Gar
En hızlı rota (14 dakika): AŞTİ -> Kızılay -> Sıhhiye -> Gar -> Gar
