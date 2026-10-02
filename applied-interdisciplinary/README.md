# คลังเอกสารสัมมนาการประยุกต์ใช้คอลลัทซ์เชิงสหวิทยาการ (Collatz Applied & Interdisciplinary Topics)

**โครงการสัมมนาและโครงงานคณิตศาสตร์ประยุกต์ ภาคการศึกษา 2569**  
**อาจารย์ที่ปรึกษา:** อาจารย์ ดร.กิตติพงศ์ ทรัพย์วัฒนาชัย  
**ภาควิชาวิทยาการคำนวณและเทคโนโลยีดิจิทัล คณะศิลปศาสตร์และวิทยาศาสตร์ มหาวิทยาลัยเกษตรศาสตร์ กำแพงแสน**

---

## 1. ตารางเปรียบเทียบ 5 เปเปอร์ประยุกต์ที่เข้าถึงได้ง่าย (Accessible Applied Papers Matrix)

| โฟลเดอร์ / หัวข้อ | เปเปอร์และวารสาร | ศาสตร์ที่เชื่อมโยง | ทำไมนิสิตถึงทำได้ง่าย | ชิ้นงานและผลการทดลองที่จับต้องได้ | ไฟล์ในระบบ |
|---|---|---|---|---|---|
| [`01-emmert-streib-2013-networks`](./01-emmert-streib-2013-networks/) | **Frank Emmert-Streib (2013)**<br>*PLoS ONE (Scopus Q1)* | • ทฤษฎีกราฟ (Graph Theory)<br>• วิทยาการเครือข่ายซับซ้อน (Network Science) | ใช้ความรู้ทฤษฎีกราฟเบื้องต้น โค้ด NetworkX สั้น ไม่ติดทฤษฎีซับซ้อน | กราฟิกเครือข่าย CS Graphs สวยงาม, กราฟ Degree Distribution และ Clustering Coefficient | • `paper.pdf` (1.7 MB)<br>• `emmert-streib-2013.qmd`<br>• `emmert-streib-2013.html`<br>• `emmert-streib-2013.pdf` |
| [`02-kontorovich-miller-2005-benford`](./02-kontorovich-miller-2005-benford/) | **Alex Kontorovich & Steven J. Miller (2005)**<br>*Acta Arithmetica (IM PAN)* | • สถิติอนุมาน (Inferential Statistics)<br>• การแจกแจงลอการิทึม | มโนทัศน์เข้าใจง่ายที่สุด (เลขโดดตัวแรก 1-9) ใช้สูตร $\chi^2$-test พื้นฐาน | รันการทดสอบสมมติฐาน $\chi^2$ กับ Big Data และพล็อตเปรียบเทียบกับกฎของเบนฟอร์ด | • `paper.pdf` (354 KB)<br>• `kontorovich-miller-2005.qmd`<br>• `kontorovich-miller-2005.html`<br>• `kontorovich-miller-2005.pdf` |
| [`03-clay-2023-music-acoustics`](./03-clay-2023-music-acoustics/) | **Oliver K. Clay (2023)**<br>*Journal of Humanistic Mathematics (Claremont / MAA)* | • ฟิสิกส์คลื่นเสียงและดนตรี<br>• การประพันธ์เพลงอัลกอริทึม (Algorithmic Music) | ใช้เพียงเลขคณิตมอดุโล 12 (คอร์ด/สเกลดนตรี) และคลื่นเสียง Sine wave | สร้างไฟล์เสียงจริง `.wav` / `.mid` ให้กรรมการและเพื่อนในห้องสัมมนาฟังสด ๆ | • `paper.pdf` (1.1 MB)<br>• `clay-2023.qmd`<br>• `clay-2023.html`<br>• `clay-2023.pdf` |
| [`04-dziala-2023-prng-nist`](./04-dziala-2023-prng-nist/) | **Tomasz R. Dziala (2023)**<br>*arXiv / Elsevier CPC stream* | • ตัวสร้างเลขสุ่มเทียม (PRNG)<br>• ลำดับไวล์ (Weyl Sequences) | โค้ดสั้นระดับ 20 บรรทัด เป็นการเลื่อนบิต (Shift & XOR) เข้าใจกลไกได้ไว | ผลการทดสอบมาตรฐานระดับโลก NIST SP 800-22 และตัวเลขความเร็ว Throughput (GB/s) | • `paper.pdf` (188 KB)<br>• `dziala-2023.qmd`<br>• `dziala-2023.html`<br>• `dziala-2023.pdf` |
| [`05-renza-2020-audio-forensics`](./05-renza-2020-audio-forensics/) | **Diego Renza et al. (2020)**<br>*Applied Sciences (MDPI)* | • นิติวิทยาศาสตร์ดิจิทัล (Audio Forensics)<br>• การตรวจจับการปลอมแปลงเสียง | เห็นโจทย์การประยุกต์ใช้จริงในคดีความ ไม่เสี่ยงเรื่องช่องโหว่รหัสลับพัง | ตรวจจับตำแหน่งที่มีการตัดต่อเสียงได้อย่างแม่นยำ $> 99.8\%$ วัดด้วยค่า BER | • `paper.pdf` (2.2 MB)<br>• `renza-2020.qmd`<br>• `renza-2020.html`<br>• `renza-2020.pdf` |

---

## 2. ยุทธศาสตร์การแนะนำและจัดกลุ่มนิสิตตามความถนัด

1. **กลุ่มชอบงานภาพ/ทฤษฎีกราฟ/วิทยาการข้อมูล:** $\implies$ [`01-emmert-streib-2013-networks`](./01-emmert-streib-2013-networks/)
2. **กลุ่มชอบสถิติและการทดสอบสมมติฐาน:** $\implies$ [`02-kontorovich-miller-2005-benford`](./02-kontorovich-miller-2005-benford/)
3. **กลุ่มสายสร้างสรรค์/ศิลปะคณิตศาสตร์/ดนตรี:** $\implies$ [`03-clay-2023-music-acoustics`](./03-clay-2023-music-acoustics/)
4. **กลุ่มชอบการเขียนโปรแกรมความเร็วสูง/ความปลอดภัย:** $\implies$ [`04-dziala-2023-prng-nist`](./04-dziala-2023-prng-nist/)
5. **กลุ่มนิติวิทยาศาสตร์และมัลติมีเดีย:** $\implies$ [`05-renza-2020-audio-forensics`](./05-renza-2020-audio-forensics/)
