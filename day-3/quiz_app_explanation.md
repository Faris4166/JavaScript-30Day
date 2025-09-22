# 📘 อธิบายการทำงานของ Quiz App (scripts.js)

โค้ดนี้คือ **Quiz Application** แบบตัวเลือก (Multiple Choice)
ที่เขียนด้วย JavaScript\
ต่อไปนี้คือคำอธิบายทีละส่วนอย่างละเอียด

------------------------------------------------------------------------

## 🔹 โครงสร้างข้อมูลคำถาม

``` js
const questions = [
  {
    question: "What does hardware refer to?",
    answers: [
      { text: "Software", correct: false },
      { text: "The physical components of a computer", correct: true },
      { text: "Operating system", correct: false },
      { text: "Application programs", correct: false },
    ],
  },
  ...
];
```

-   เก็บคำถามทั้งหมดไว้ใน **array `questions`**
-   แต่ละคำถามเป็น **object** ที่มี:
    -   `question` → ข้อความคำถาม
    -   `answers` → คำตอบหลายตัวเลือก (array) แต่ละคำตอบมี
        `{ text: "คำตอบ", correct: true/false }`

------------------------------------------------------------------------

## 🔹 การเชื่อมกับ HTML

``` js
const questionElement = document.getElementById("question");
const answerButtons = document.getElementById("answer-buttons");
const nextButton = document.getElementById("next-btn");
```

-   `questionElement` → แสดงคำถาม
-   `answerButtons` → ใส่ปุ่มคำตอบ
-   `nextButton` → ปุ่ม Next

------------------------------------------------------------------------

## 🔹 ตัวแปรสถานะของเกม

``` js
let currentQuestionIndex = 0;
let score = 0;
```

-   `currentQuestionIndex` → เก็บว่าอยู่ข้อที่เท่าไหร่
-   `score` → เก็บคะแนนที่ตอบถูก

------------------------------------------------------------------------

## 🔹 ฟังก์ชันหลัก

### 1. `startQuiz()` → เริ่มเกม

รีเซ็ตค่าต่าง ๆ และแสดงคำถามข้อแรก

### 2. `showQuestion()` → แสดงคำถาม

-   ล้างปุ่มเก่า (`resetState()`)
-   แสดงคำถามปัจจุบัน
-   สร้างปุ่มคำตอบใหม่ และตรวจว่าถูก/ผิด

### 3. `resetState()` → ล้างปุ่มเก่า

ซ่อนปุ่ม Next และลบปุ่มคำตอบทั้งหมดก่อนแสดงคำถามใหม่

### 4. `selectAnswer()` → เมื่อผู้ใช้เลือกคำตอบ

-   ตรวจว่าถูกหรือผิด
-   ถ้าถูก → ใส่ class `correct` และเพิ่มคะแนน
-   ถ้าผิด → ใส่ class `incorrect`
-   เฉลยคำตอบที่ถูกเสมอ
-   ปิดปุ่มคำตอบ และแสดงปุ่ม Next

### 5. `showScore()` → แสดงคะแนน

-   ล้างปุ่มเก่า
-   แสดงข้อความ "You scored X out of Y"
-   เปลี่ยนปุ่มเป็น "Play Again"

### 6. `handleNextButton()` → ไปยังข้อถัดไป

-   เพิ่มเลขข้อ
-   ถ้ามีคำถามเหลือ → แสดงต่อ
-   ถ้าหมดแล้ว → แสดงคะแนน

------------------------------------------------------------------------

## 🔹 การทำงานของปุ่ม Next

``` js
nextButton.addEventListener("click", () => {
  if (currentQuestionIndex < questions.length) {
    handleNextButton();
  } else {
    startQuiz();
  }
});
```

-   ถ้ายังเหลือข้อ → ไปข้อถัดไป
-   ถ้าหมดแล้ว → เริ่มเกมใหม่

------------------------------------------------------------------------

## 🔹 เริ่มทำงาน

``` js
startQuiz();
```

-   สั่งเริ่มเกมทันทีเมื่อโหลดหน้าเว็บ

------------------------------------------------------------------------

## 📌 Flow การทำงานโดยสรุป

1.  เริ่มจาก `startQuiz()` → รีเซ็ต → แสดงคำถามแรก
2.  `showQuestion()` → สร้างปุ่มตัวเลือกใหม่
3.  ผู้ใช้กดคำตอบ → `selectAnswer()` → ตรวจถูก/ผิด → เฉลย
4.  กดปุ่ม Next → `handleNextButton()`
    -   ถ้ามีคำถามเหลือ → ไปต่อ
    -   ถ้าไม่เหลือ → `showScore()` แสดงคะแนน
5.  ถ้ากด "Play Again" → `startQuiz()` วนใหม่

------------------------------------------------------------------------
