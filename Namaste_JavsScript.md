# 🚀 Namaste JavaScript: Master Notebook (Episodes 2 - 26)

> **Course Instructor:** Akshay Saini  
> **Note Type:** Complete Comprehensive Developer Guide (Hinglish)  
> **Status:** 🟢 Complete Knowledge Base

---

## 📌 EPISODE 2: How JavaScript Code is Executed?

Execution Context ka nirmaan hamesha **two phases** mein hota hai. Jab bhi koi JS program run hota hai, engine in do charno se guzarta hai:

### 1. Memory Creation Phase (Phase 1)

Is phase mein JS engine poore code ko scan karta hai aur jitne bhi variables aur functions hain, unke liye memory space reserve karta hai.

* **Variables** ko shuruat mein ek special value di jaati hai: `undefined`.
* **Functions** ke case mein unka poora ka poora source code hi memory mein copy ho jata hai.

### 2. Code Execution Phase (Phase 2)

Is phase mein code ko strictly **line-by-line** top to bottom execute kiya jata hai. Variables ki actual values unhe isi phase mein milti hain.

### 💻 Execution Context Breakdown Simulation

Agar hamare paas yeh code hai:
Jab line 6 par square(n) call hoga, toh JS engine main Global Context ke andar ek naya Local Execution Context banayega:PhaseComponentKeyValuePhase 1MemorynumundefinedPhase 1MemoryansundefinedPhase 2Codenum2 (Argument passed)Phase 2Codeans4 (2 * 2)⚠️ Important: Jaise hi engine return ans; line par pahunchega, yeh value parent execution context ko hand-over kar di jayegi aur yeh local context Call Stack se permanently destroy ho jayega.📌 EPISODE 3: Hoisting in JavaScriptHoisting JavaScript ka ek aisa phenomena hai jisse aap variables aur functions ko unke declaration se pehle hi bina kisi generic crash error ke access kar sakte hain.

```javascript
var n = 2;
function square(num) {
   var ans = num * num;
   return ans;
}
var square2 = square(n);
