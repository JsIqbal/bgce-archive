### 🐳 Go Debugging Playground – Docker-এর মাধ্যমে ইন্টার‍্যাকটিভ GDB

এই Docker ইমেজটি দিয়ে তুমি খুব সহজেই Go প্রোগ্রাম কম্পাইল এবং `gdb` দিয়ে স্টেপ-বাই-স্টেপ ডিবাগ করতে পারবে।

---

### 🚀 শুরু করার নিয়ম

#### ১. Docker Hub থেকে ইমেজ ডাউনলোড করো:

```bash
docker pull jsiqbal/go-debug-ready
```

---

#### ২. কন্টেইনার রান করাও:

```bash
docker run -it --name go-debug jsiqbal/go-debug-ready
```

---

### 🧠 কন্টেইনারের ভিতরে যা করতে হবে

কন্টেইনারে ঢুকে এই ধাপগুলো অনুসরণ করো:

#### ৩. Go প্রোগ্রামের ফোল্ডারে যাও:

```bash
cd /app
```

#### ৪. কোড দেখো বা এডিট করো:

```bash
nano add.go
```

কোডটা দেখতে এরকম:

```go
package main

import "fmt"

func add(a, b int) int {
	return a + b
}

func main() {
	result := add(3, 5)
	fmt.Println("Result:", result)
}
```

---

#### ৫. Go বাইনারি ডিবাগিং ইনফো সহ বানাও:

```bash
go build -gcflags="all=-N -l" -o add add.go
```

🛠️ ব্যাখ্যা:

-   `-N`: অপটিমাইজেশন বন্ধ
-   `-l`: ইনলাইনের মত টেকনিক বন্ধ

---

#### ৬. GDB চালাও এবং ডিবাগ শুরু করো:

```bash
gdb ./add
```

GDB চালু হলে লিখো:

```gdb
break main.main     # main ফাংশনে ব্রেকপয়েন্ট দাও
run                 # প্রোগ্রাম চালাও
n                   # পরের লাইনে যাও
info locals         # লোকাল ভেরিয়েবলগুলো দেখো
info registers      # CPU রেজিস্টারগুলো দেখো
x/1i $pc            # বর্তমান ইনস্ট্রাকশনটা কী দেখো
```

---

### 🔁 আবার চালু করতে চাইলে:

```bash
docker start -ai go-debug
```

না চাইলে পুরো নতুন করে চালাও:

```bash
docker rm -f go-debug
docker run -it --name go-debug jsiqbal/go-debug-ready
```
