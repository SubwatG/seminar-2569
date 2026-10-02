# คู่มือการศึกษาและแผนโครงงานสัมมนา: ระบบเข้ารหัสภาพดิจิทัลด้วยความโกลาหลของคอลลัทซ์ (Collatz Image Encryption)

**ชื่อหัวข้อวิจัย:** Chaos-Based Image Encryption and Scrambling via Collatz Dynamical Systems  
**วรรณกรรมอ้างอิงหลัก:** D. M. Ballesteros et al. (*Entropy*, 2018) / C. Obimbo (*IEEE Access*, 2024) / เอกสารข้อเสนอโครงงาน มก. (`applied-math-project-briefs.md`)  
**กลุ่มเป้าหมาย:** นิสิตปริญญาตรีชั้นปีที่ 3 สาขาคณิตศาสตร์ประยุกต์ / อาจารย์ ดร.กิตติพงศ์ ทรัพย์วัฒนาชัย  
**สถานะ:** เอกสารปูพื้นฐานและข้อเสนอโครงงานสัมมนา (Undergraduate Seminar Briefing)

---

## 1. บทนำและภาพรวมของเปเปอร์ (Executive Summary & Core Intuition)

### 1.1 ปัญหานี้ตอบคำถามอะไร
ภาพดิจิทัล (Digital Images) มีความแตกต่างจากข้อมูลตัวอักษรทั่วไปอย่างยิ่ง เนื่องจากมี **ความซ้ำซ้อนสูงมาก (High Redundancy)** และพิกเซลที่อยู่ติดกันมีความสัมพันธ์กันอย่างแนบแน่น (High Correlation $\approx 0.95$–$0.99$) ขั้นตอนวิธีเข้ารหัสลับมาตรฐานอย่าง AES หรือ RSA ไม่สามารถทำงานได้เร็วพอ และหากเข้ารหัสในโหมด Electronic Codebook (ECB) เค้าโครงภาพเดิมจะยังคงปรากฏให้เห็น

โครงงานนี้ประยุกต์ใช้ **ความโกลาหลและความไม่แน่นอนของฟังก์ชันคอลลัทซ์ ($3x+1$)** มาออกแบบระบบเข้ารหัสภาพแบบ 2 ขั้นตอน (Confusion & Diffusion) ตามสถาปัตยกรรมของแชนนอน (Shannon's Cryptographic Architecture) โดยเปลี่ยนภาพถ่ายต้นฉบับให้กลายเป็นภาพสัญญาณรบกวนคล้ายเม็ดทราย (Noise) ที่ไม่มีเค้าโครงเดิม และสามารถถอดรหัสกลับคืนได้อย่างสมบูรณ์แบบโดยไม่สูญเสียคุณภาพ (Lossless Decryption)

### 1.2 โครงสร้าง 2 ขั้นตอนตามหลักการเข้ารหัสลับ
1. **ขั้นตอนการสับเปลี่ยนตำแหน่งพิกเซล (Permutation / Confusion Phase):**
   ใช้วงโคจรคอลลัทซ์ที่เริ่มจากกุญแจลับ $n_0$ (Seed) มาสร้างลำดับการเรียงสับเปลี่ยนพิกัด $2$ มิติ $(i, j) \mapsto (i', j')$ เพื่อทำลายความสัมพันธ์ระหว่างพิกเซลข้างเคียงให้ลดลงเหลือใกล้ศูนย์ ($r \approx 0.00$)

2. **ขั้นตอนการแพร่กระจายค่าสี (Diffusion Phase):**
   ใช้บิตภาวะคู่คี่หรือค่ามอดุโล $256$ จากวงโคจรมากระทำทางบิต (XOR) หรือการบวกมอดุโล $256$ แบบลูกโซ่ (Cipher Block Chaining) ทำให้การเปลี่ยนแปลงพิกเซลของภาพต้นฉบับเพียง 1 บิต ส่งผลให้ภาพเข้ารหัสเปลี่ยนไปมากกว่า $99.6\%$ (Avalanche Effect)

---

## 2. ความรู้พื้นฐานที่ต้องใช้ (Prerequisites Checklist)

* **คณิตศาสตร์ (Mathematics):**
  - **พีชคณิตเชิงเส้นและเมทริกซ์ (Linear Algebra & 2D Arrays):** การแปลงพิกัดภาพ 2 มิติ $(M \times N)$ เป็นเวกเตอร์ 1 มิติ และการเรียงสับเปลี่ยน (Permutation Matrices)
  - **ทฤษฎีสารสนเทศ (Information Theory):** ค่าเอนโทรปีของแชนนอน (Shannon Entropy):
    $$H(S) = -\sum_{i=0}^{255} P(s_i) \log_2 P(s_i)$$
  - **สถิติสหสัมพันธ์ (Correlation Coefficient):** การวัดความสัมพันธ์ของพิกเซลข้างเคียงในแนวตั้ง แนวนอน และแนวทแยง

* **การเขียนโปรแกรม (Programming):**
  - **Python (NumPy & OpenCV / PIL):** การโหลดภาพ, การเข้าถึงค่าเม็ดสี (Grayscale และ RGB), การกระทำทางบิตระดับอาเรย์
  - **Matplotlib:** การพล็อตฮิสโตแกรมการกระจายตัวของค่าสี (0–255)

---

## 3. เจาะลึกคณิตศาสตร์และตัวชี้วัดความปลอดภัยสากล (Security Metrics)

### 3.1 การป้องกันจุดดักของวัฏจักร (Trivial Cycle Evasion)
ปัญหาของ Collatz ปกติคือจะลู่เข้าสู่วัฏจักร $4 \to 2 \to 1$ เสมอ ในการสร้างลำดับกุญแจที่มีความยาวเท่ากับจำนวนพิกเซลทั้งหมด ($M \times N$) ขั้นตอนวิธีจะต้องใช้กลไก **Re-seeding หรือ Weyl Perturbation**:
$$x_{k+1} = \begin{cases} (x_k // 2) & \text{ถ้า } x_k \text{ เป็นคู่} \\ (3x_k + 1) & \text{ถ้า } x_k \text{ เป็นคี่} \end{cases}$$
เมื่อ $x_k = 1$ ให้ทำการรีซีดด้วยฟังก์ชันกวนบิตเพื่อรักษาสมบัติความสุ่มต่อไป

### 3.2 เกณฑ์ประเมินการต้านทานการโจมตีเชิงผลต่าง (Differential Attack Metrics)
1. **NPCR (Number of Pixels Change Rate):**
   วัดสัดส่วนจำนวนพิกเซลที่เปลี่ยนไปเมื่อภาพต้นฉบับเปลี่ยนไปเพียง 1 บิต:
   $$\text{NPCR} = \frac{\sum_{i,j} D(i,j)}{M \times N} \times 100\% \quad (\text{ค่าอุดมคติ } \approx 99.6094\%)$$

2. **UACI (Unified Average Changing Intensity):**
   วัดความเข้มเฉลี่ยของการเปลี่ยนแปลงระหว่างภาพสองภาพ:
   $$\text{UACI} = \frac{1}{M \times N} \sum_{i,j} \frac{|C_1(i,j) - C_2(i,j)|}{255} \times 100\% \quad (\text{ค่าอุดมคติ } \approx 33.4635\%)$$

---

## 4. แผนการดำเนินงานวิจัย 12 สัปดาห์สำหรับนิสิตสัมมนา (12-Week Roadmap)

| สัปดาห์ | กิจกรรมการศึกษาทางทฤษฎี | การทดลองเชิงตัวเลขและการเขียนโปรแกรม | เอกสารส่งมอบ |
|:---:|---|---|---|
| **สัปดาห์ 1–2** | ศึกษาทฤษฎี Shannon Confusion & Diffusion และสถาปัตยกรรมภาพดิจิทัล | เขียนโปรแกรมโหลดภาพและพล็อตฮิสโตแกรมของภาพก่อนเข้ารหัส | ภาพถ่ายและฮิสโตแกรมสีตั้งต้น |
| **สัปดาห์ 3–4** | ออกแบบขั้นตอนวิธีสับพิกัด (Permutation) ด้วยวงโคจร Collatz | พัฒนาฟังก์ชัน `scramble_image` และ `descramble_image` เพื่อทดสอบการกู้คืนภาพ | ภาพ Scrambled Image และการวัดค่า Correlation |
| **สัปดาห์ 5–6** | ออกแบบขั้นตอนการแพร่กระจาย (Diffusion) ด้วยการ XOR แบบลูกโซ่ | รวมส่วน Permutation + Diffusion เข้าด้วยกันเป็นขั้นตอนวิธีเข้ารหัสสมบูรณ์ | ภาพ Ciphertext Image และผลการวัดค่าเอนโทรปี |
| **สัปดาห์ 7–8** | ศึกษาการทดสอบความทนทานต่อ Differential Attack (NPCR & UACI) | เขียนสคริปต์แก้บิตในภาพต้นฉบับ 1 พิกเซล และคำนวณค่า NPCR และ UACI | ตารางผลการทดสอบ NPCR/UACI เทียบกับค่าอุดมคติ |
| **สัปดาห์ 9–10** | ทดสอบความทนทานต่อสัญญาณรบกวน (Noise Attack & Data Loss) | เพิ่มสัญญาณรบกวน Salt & Pepper และทดสอบว่าภาพถอดรหัสยังพอมองออกหรือไม่ | ภาพการถอดรหัสหลังถูกโจมตีด้วยสัญญาณรบกวน |
| **สัปดาห์ 11–12** | สรุปผลการวิจัยและเตรียมการนำเสนอสัมมนา | จัดทำสไลด์และเล่มรายงานสัมมนา 5 บทฉบับสมบูรณ์ | สไลด์นำเสนอ และเล่มรายงานสัมมนา |

---

## 5. โค้ดตัวอย่างตั้งต้น (Python Starter Code)

```python
"""
collatz_image_encryption.py
ขั้นตอนวิธีเข้ารหัสและถอดรหัสภาพดิจิทัลด้วยความโกลาหลของคอลลัทซ์
"""

import math
import numpy as np


def generate_collatz_stream(seed: int, length: int) -> np.ndarray:
    """สร้างลำดับสุ่มเทียมจากวิถีคอลลัทซ์ความยาวตามจำนวนพิกเซล"""
    stream = np.empty(length, dtype=np.uint64)
    n = np.uint64(seed)
    mask64 = 0xFFFFFFFFFFFFFFFF

    for i in range(length):
        stream[i] = n
        if n % 2 == 0:
            n = n // 2
        else:
            n = (3 * n + 1) & mask64
        # ป้องกันการติดกับดักวัฏจักร 4 -> 2 -> 1
        if n == 1:
            n = np.uint64((seed + i + 0x5DEECE66D) & mask64)
            if n % 2 == 0:
                n += 1
    return stream


def encrypt_image(
    image: np.ndarray, key: int
) -> tuple[np.ndarray, np.ndarray]:
    """เข้ารหัสภาพ 2 มิติ (Grayscale) ด้วยขั้นตอนวิธี Permutation + Diffusion"""
    h, w = image.shape
    total_pixels = h * w
    flat = image.flatten()

    # 1. ขั้นตอน Confusion: เรียงสับเปลี่ยนพิกัดพิกเซล
    collatz_stream = generate_collatz_stream(key, total_pixels)
    perm_indices = np.argsort(collatz_stream)
    scrambled = flat[perm_indices]

    # 2. ขั้นตอน Diffusion: ผสมบิตแบบลูกโซ่ด้วย XOR
    cipher = np.empty_like(scrambled)
    prev = np.uint8(key & 0xFF)
    diff_keys = (collatz_stream % 256).astype(np.uint8)

    for i in range(total_pixels):
        val = scrambled[i] ^ diff_keys[i] ^ prev
        cipher[i] = val
        prev = val

    return cipher.reshape((h, w)), perm_indices


def decrypt_image(
    cipher: np.ndarray, key: int, perm_indices: np.ndarray
) -> np.ndarray:
    """ถอดรหัสภาพกลับสู่ภาพต้นฉบับอย่างสมบูรณ์"""
    h, w = cipher.shape
    total_pixels = h * w
    flat_cipher = cipher.flatten()

    # 1. ย้อนกลับ Diffusion
    scrambled = np.empty_like(flat_cipher)
    collatz_stream = generate_collatz_stream(key, total_pixels)
    diff_keys = (collatz_stream % 256).astype(np.uint8)
    prev = np.uint8(key & 0xFF)

    for i in range(total_pixels):
        val = flat_cipher[i]
        scrambled[i] = val ^ diff_keys[i] ^ prev
        prev = val

    # 2. ย้อนกลับ Confusion
    original_flat = np.empty_like(scrambled)
    original_flat[perm_indices] = scrambled

    return original_flat.reshape((h, w))


def compute_npcr_uaci(c1: np.ndarray, c2: np.ndarray) -> tuple[float, float]:
    """คำนวณค่า NPCR และ UACI เพื่อทดสอบ Differential Attack"""
    diff_mask = c1 != c2
    npcr = np.mean(diff_mask) * 100.0
    uaci = np.mean(np.abs(c1.astype(float) - c2.astype(float)) / 255.0) * 100.0
    return npcr, uaci


if __name__ == "__main__":
    # จำลองภาพทดสอบขนาด 128x128
    np.random.seed(42)
    sample_img = np.random.randint(50, 200, size=(128, 128), dtype=np.uint8)
    secret_key = 987654321012345

    # ดำเนินการเข้ารหัส
    encrypted_img, perm = encrypt_image(sample_img, secret_key)
    decrypted_img = decrypt_image(encrypted_img, secret_key, perm)

    # ตรวจสอบความถูกต้องสมบูรณ์ของการกู้คืน
    is_lossless = np.array_equal(sample_img, decrypted_img)
    print(f"ผลการถอดรหัสตรงกับภาพต้นฉบับ 100%: {is_lossless}")

    # ทดสอบแก้ภาพต้นฉบับ 1 พิกเซลเพื่อวัด NPCR / UACI
    modified_img = sample_img.copy()
    modified_img[0, 0] = (modified_img[0, 0] + 1) % 256
    encrypted_mod, _ = encrypt_image(modified_img, secret_key)

    npcr_val, uaci_val = compute_npcr_uaci(encrypted_img, encrypted_mod)
    print(f"ค่า NPCR: {npcr_val:.4f}% (เกณฑ์มาตรฐาน > 99.60%)")
    print(f"ค่า UACI: {uaci_val:.4f}% (เกณฑ์มาตรฐาน ~ 33.46%)")
```

---

## 6. ตัวชี้วัดและชิ้นงานส่งมอบ (Deliverables & Assessment)

1. **ภาพเปรียบเทียบก่อนและหลังการเข้ารหัส (Visual Comparison):** ภาพต้นฉบับ ภาพที่ผ่านการสับพิกัด ภาพเข้ารหัสสมบูรณ์ และภาพที่กู้คืนได้
2. **ฮิสโตแกรมของค่าสี (Color Histogram):** แสดงว่าฮิสโตแกรมของภาพที่เข้ารหัสแล้วมีการกระจายตัวแบบสม่ำเสมอ (Uniform) ตัดเค้าโครงภาพเดิมออกอย่างสมบูรณ์
3. **ผลการทดสอบความปลอดภัยตามมาตรฐานสากล (Security Scorecard):**
   - ค่าสัมประสิทธิ์สหสัมพันธ์พิกเซลข้างเคียง ($r_{xy} \to 0.00$)
   - ค่าเอนโทรปีของสารสนเทศ ($H \ge 7.99$ บิต จากเต็ม $8.00$)
   - ค่าความทนทานต่อการโจมตีเชิงผลต่าง ($\text{NPCR} > 99.6\%$, $\text{UACI} \approx 33.4\%$)
