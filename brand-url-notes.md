# Brand URL Patterns — สำหรับเพิ่มสินค้าใหม่ในเว็บเปรียบเทียบราคา

โน้ตนี้เก็บ pattern URL ที่ยืนยันแล้วว่าใช้ได้จริง เพื่อให้ครั้งต่อไปที่เพิ่มสินค้าแบรนด์เดิม ไม่ต้องเสียเวลา/token เดาโดเมนใหม่ทุกครั้ง

## วิธีที่เร็วที่สุดในการเพิ่มสินค้าใหม่

**ส่งลิงก์สินค้าจากเว็บทางการมาให้สัก 1 ประเทศ** (ประเทศไหนก็ได้) — จะได้รหัสสินค้า (product code) ทันที แล้วเดา URL ประเทศอื่นจาก pattern ด้านล่างได้เลยโดยไม่ต้อง WebSearch หาโดเมนใหม่

ถ้าไม่มีลิงก์ ก็บอกแค่ชื่อแบรนด์ + ชื่อสินค้า ผมจะ WebSearch หาให้ แต่จะช้ากว่า (โดยเฉพาะแบรนด์ที่ยังไม่เคยทำ)

---

## Chanel — chanel.com

โดเมนกลางเดียว ใช้ country-path แยกกันตามนี้ (ยืนยันแล้วจากสินค้า Chance Eau Tendre, Coco Mademoiselle):

```
https://www.chanel.com/th/fragrance/p/{PRODUCT_CODE}/{slug}/
https://www.chanel.com/jp/fragrance/p/{PRODUCT_CODE}/{slug}/
https://www.chanel.com/kr/fragrance/p/{PRODUCT_CODE}/{slug}/
https://www.chanel.com/fr/parfums/p/{PRODUCT_CODE}/{slug}/        ← หมวดฝรั่งเศสใช้คำว่า parfums ไม่ใช่ fragrance
https://www.chanel.com/us/fragrance/p/{PRODUCT_CODE}/{slug}/
```

- แต่ละไซส์ (35ml/50ml/100ml/150ml/200ml) มีรหัสสินค้า (PRODUCT_CODE) แยกกันคนละหน้า — ต้องเปิดทีละไซส์
- หน้าสินค้าจริงจะมี meta price + sibling-size list ให้เห็นในหน้าเดียว (บางครั้งไม่ครบทุกไซส์ ต้องเช็กว่าประเทศนั้นๆ ขายไซส์นั้นจริงไหม)
- ลิงก์ chanel.com จะ **auto-redirect ตาม IP ผู้เข้าดู** ไม่ว่าจะใส่ /th/ /jp/ /us/ /kr/ /fr/ หรือไม่ — เปิดจากไทยจะเด้งไปหน้าไทยเสมอ (แต่ราคาที่ดึงมาถูกต้องแล้ว แค่ลิงก์คลิกดูจะเด้ง)

## Dior — dior.com

โดเมนกลางเดียว ใช้ locale-path แบบ `{lang}_{COUNTRY}` (ยืนยันแล้วจาก Sauvage EDT, Forever Skin Glow):

```
https://www.dior.com/en_th/beauty/products/{slug}-{PRODUCT_CODE}.html   ← ไทย ใช้ en_th (มี th_th ด้วยแต่ en_th ใช้ slug อังกฤษ fetch ง่ายกว่า)
https://www.dior.com/ja_jp/beauty/products/{slug}-{PRODUCT_CODE}.html   ← ญี่ปุ่น (ใส่ slug อังกฤษก็ redirect ไปหน้าจริงได้ ไม่ต้องเข้ารหัสภาษาญี่ปุ่นเอง)
https://www.dior.com/ko_kr/beauty/products/{slug}-{PRODUCT_CODE}.html   ← เกาหลีใต้ (ต้องใช้ slug ภาษาเกาหลีจริง ไม่งั้น fetch ไม่เจอ — เอา slug จากลิสต์ "Choose your Country" ท้ายหน้า en_us)
https://www.dior.com/fr_fr/beauty/products/{slug}-{PRODUCT_CODE}.html   ← ฝรั่งเศส
https://www.dior.com/en_us/beauty/products/{slug}-{PRODUCT_CODE}.html   ← สหรัฐฯ
```

- PRODUCT_CODE เดียวกันทุกประเทศ (เช่น Y0000149) ไม่เหมือน YSL ที่สหรัฐฯ ใช้รหัสแยก
- ทุกหน้ามีลิสต์ "Choose your Country or Region & Language" ท้ายหน้า ให้ URL ที่ถูกต้องของทุกประเทศ (รวม slug ภาษานั้นๆ) — เปิดหน้า en_us ก่อนแล้วเลื่อนไปดูลิสต์นี้เพื่อเอา URL ประเทศอื่นแบบชัวร์ๆ ในการ fetch ครั้งเดียว จะเร็วกว่าเดา
- ระวัง: URL ที่มีอักษรภาษาเอเชียเข้ารหัส (%E3%82...) ยาวมากอาจโดน error "URL exceeds maximum length" — ให้ลองใช้ slug อังกฤษแทนก่อน (มักจะ redirect ไปหน้าเดียวกันได้เอง โดยเฉพาะ ja_jp), ถ้าไม่ได้ค่อยย้อนไปใช้ slug ภาษานั้นจากลิสต์ท้ายหน้า
- ลิงก์ dior.com **ไม่เด้งตาม IP** กดดูได้ตรงๆ ไม่ต้องมีลิงก์สำรอง
- บางช่วงมีโปรลดราคาชั่วคราว (เช่น "7.7 Sale", "SOLDES D'ÉTÉ") — ให้ใช้ราคาปกติ/ราคาเดิม ไม่ใช้ราคาลด

## YSL — โดเมนแยกตามประเทศ (ไม่ใช้ dior.com/chanel.com pattern)

**ข้อควรระวัง:** yslbeauty.com/int/... หรือ /{locale}/... เป็นหน้า catalog ระดับสากล **ไม่มีราคาจริง** (price:amount=0, currency:N/A) ห้ามใช้เป็นแหล่งราคา

โดเมนจริงที่ใช้ได้ (ยืนยันแล้วจาก Y EDP):

```
https://www.yslbeautyth.com/en_TH/...      ← ไทย
https://www.yslbeautykr.com/ko_KR/...      ← เกาหลีใต้
https://www.yslb.jp/...                     ← ญี่ปุ่น (ไม่ใช่ yslbeauty.jp หรือ yslbeautyjp.com — ทั้งคู่ใช้ไม่ได้)
https://www.yslbeauty.fr/...                 ← ฝรั่งเศส (ไม่ใช่ yslbeautyfr.com — ใช้ไม่ได้)
https://www.yslbeautyus.com/...              ← สหรัฐฯ (ใช้รหัสสินค้าคนละชุดกับประเทศอื่น! เช่น "727YSL" แทน "WW-50194YSL")
```

- รหัสสินค้าสากล (ไทย/เกาหลี/ญี่ปุ่น/ฝรั่งเศส) มักขึ้นต้น `WW-` เช่น `WW-50194YSL.html` — สหรัฐฯ ใช้รหัสแยกต่างหาก
- ไทย/เกาหลี/สหรัฐฯ **ไม่โชว์ราคาไซส์อื่นในหน้าเดียว** ต้อง fetch ทีละไซส์ผ่าน query param `?dwvar_{PRODUCTCODE}_size={value}` (หา value จาก href ของปุ่มเลือกไซส์ในหน้าแรก) — ฝรั่งเศสเป็นข้อยกเว้นที่โชว์ราคาทุกไซส์ในหน้าเดียว (เหมือน Chanel)
- แพลตฟอร์มเบื้องหลังเป็น Demandware/Salesforce Commerce Cloud เหมือน dior.com/chanel.com เลยใช้ query param pattern เดียวกันได้

---

## Workflow ที่ประหยัดสุด (สรุป)

1. มีลิงก์สินค้า 1 ประเทศ → เอารหัสสินค้า → ลอง pattern โดเมนของแบรนด์นั้นจากโน้ตนี้กับอีก 4 ประเทศ (fetch พร้อมกันในคำสั่งเดียว ไม่ทยอยทำทีละอัน)
2. ไม่มีลิงก์ → WebSearch หาโดเมน/รหัสสินค้าก่อน 1 ครั้ง แล้วค่อยทำตามข้อ 1
3. เจอ URL ยาวเกิน/error → ลองสลับเป็น slug ภาษาอังกฤษ หรือใช้ locale path แบบสั้นกว่าก่อนเดาใหม่
4. ราคาที่มีโปรลดชั่วคราว → ใช้ราคาปกติเสมอ ระบุใน sizeNote ถ้าจำเป็น
5. ไซส์ไหนของประเทศไหนตรวจสอบไม่ได้ → ไม่ใส่ ไม่เดา ระบุใน sizeNote ว่าไม่ยืนยัน
