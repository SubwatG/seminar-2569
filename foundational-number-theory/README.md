# คลังเอกสารวิจัยทฤษฎีจำนวนและระบบพลวัตคอลลัทซ์ (Foundational Number Theory & Collatz Dynamics)

**โครงการสัมมนาและโครงงานคณิตศาสตร์ประยุกต์ ภาคการศึกษา 2569**  
**อาจารย์ที่ปรึกษา:** อาจารย์ ดร.กิตติพงศ์ ทรัพย์วัฒนาชัย  
**ภาควิชาวิทยาการคำนวณและเทคโนโลยีดิจิทัล คณะศิลปศาสตร์และวิทยาศาสตร์ มหาวิทยาลัยเกษตรศาสตร์ กำแพงแสน**

---

## 1. ตารางเปรียบเทียบ 4 เปเปอร์เสาหลักทางทฤษฎีจำนวน (Foundational Papers Matrix)

| หมวดหมู่ / โฟลเดอร์ | เปเปอร์และวารสาร | แกนคณิตศาสตร์หลัก | ระดับความยาก | เหมาะสำหรับนิสิตกลุ่มใด | ผลงานส่งมอบและเอกสารในระบบ |
|---|---|---|:---:|---|---|
| [`01-lagarias-1985-amm`](./01-lagarias-1985-amm/) | **Jeffrey C. Lagarias (1985)**<br>*The American Mathematical Monthly (MAA)* | • ภาพรวมทฤษฎีจำนวนทั้งระบบ<br>• Parity Vectors mod $2^k$<br>• ความน่าจะเป็นและ Brownian drift $\frac{3}{4}$<br>• Conway's Undecidability | ★★★☆☆<br>(ปานกลาง - ภาษาอ่านง่ายมาก) | นิสิตที่ต้องการภาพกว้างทางคณิตศาสตร์ เห็นความเชื่อมโยงหลายสาขา | • `paper.pdf`<br>• `lagarias-1985.qmd`<br>• `lagarias-1985.html`<br>• `lagarias-1985.pdf` |
| [`02-terras-1976-acta-arithmetica`](./02-terras-1976-acta-arithmetica/) | **Riho Terras (1976)**<br>*Acta Arithmetica (IM PAN)* | • บทตั้ง Parity Vector Bijection<br>• การหารลงตัวและคอนกรูเอนซ์ mod $2^k$<br>• การพิสูจน์ความหนาแน่นเวลาหยุด $= 1$ | ★★☆☆☆<br>(เหมาะกับเด็ก ป.ตรี มากที่สุด) | นิสิตที่ชอบการพิสูจน์แบบ Elementary Number Theory และอยากแกะ Proof ทีละบรรทัด | • `paper.pdf` (สแกน 1976 ต้นฉบับ)<br>• `terras-1976.qmd`<br>• `terras-1976.html`<br>• `terras-1976.pdf` |
| [`03-chamberland-2003-survey`](./03-chamberland-2003-survey/) | **Marc Chamberland (2003)**<br>*Grinnell College / AMS Survey* | • กราฟต้นไม้ย้อนกลับ (Predecessor Trees)<br>• 3 วัฏจักรบนจำนวนเต็มลบ $\mathbb{Z}^-$<br>• ฟังก์ชันต่อเนื่อง $f(x)$ บน $\mathbb{R}$ | ★★☆☆☆<br>(เห็นภาพชัดเจนที่สุด) | นิสิตที่ชอบทฤษฎีกราฟ ระบบพลวัต และการเขียนโค้ดวาดกราฟิก NetworkX | • `paper.pdf`<br>• `chamberland-2003.qmd`<br>• `chamberland-2003.html`<br>• `chamberland-2003.pdf` |
| [`04-simons-deweger-2005-acta-arithmetica`](./04-simons-deweger-2005-acta-arithmetica/) | **John Simons & Benne de Weger (2005)**<br>*Acta Arithmetica (IM PAN)* | • สมการไดโอแฟนไทน์ของวัฏจักร<br>• เศษส่วนต่อเนื่องของ $\log_2 3$<br>• รูปแบบเชิงเส้นของลอการิทึม (Baker's Method)<br>• การพิสูจน์ว่าไม่มี $m$-cycles สำหรับ $m \le 68$ | ★★★★☆<br>(ทฤษฎีจำนวนเข้มข้น) | นิสิตที่สนใจสมการไดโอแฟนไทน์และการคำนวณขั้นสูง (ตรงสายวิจัยอาจารย์) | • `paper.pdf`<br>• `simons-deweger-2005.qmd`<br>• `simons-deweger-2005.html`<br>• `simons-deweger-2005.pdf` |

---

## 2. ยุทธศาสตร์การแนะนำนิสิต (Advising Roadmap)

1. **สัปดาห์ที่ 1–2 (เริ่มต้นอ่าน):**  
   ให้นิสิตเริ่มต้นจาก [`03-chamberland-2003-survey`](./03-chamberland-2003-survey/) หรือ [`01-lagarias-1985-amm`](./01-lagarias-1985-amm/) เพื่อทำความเข้าใจภาพรวม ปัญหา $3x+1$ และลองเขียนโค้ดทดลองด้วยตนเอง

2. **สัปดาห์ที่ 3–6 (แกะบทพิสูจน์จริง):**  
   ให้นิสิตศึกษา [`02-terras-1976-acta-arithmetica`](./02-terras-1976-acta-arithmetica/) เพื่อฝึกพิสูจน์บทตั้ง **Parity Vector Bijection Lemma** ด้วยการอุปนัยเชิงคณิตศาสตร์ และเขียนโปรแกรมตรวจสอบบน $\mathbb{Z} / 2^k \mathbb{Z}$

3. **สัปดาห์ที่ 7–10 (ต่อยอดขั้นสูง):**  
   สำหรับนิสิตที่มีศักยภาพสูง ให้ลงลึกใน [`04-simons-deweger-2005-acta-arithmetica`](./04-simons-deweger-2005-acta-arithmetica/) เพื่อศึกษาความเชื่อมโยงกับสมการไดโอแฟนไทน์และเศษส่วนต่อเนื่องของ $\log_2 3$ สู่การทำเล่มโครงงานปริญญาตรี (01417499)
