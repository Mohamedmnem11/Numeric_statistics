# 🚀 HPC Task 2 - MPI Statistics

![MPI](https://img.shields.io/badge/MPI-Parallel_Computing-blue)
![C](https://img.shields.io/badge/C-99-green)
![Docker](https://img.shields.io/badge/Docker-Ready-blue)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Overview

A **high-performance parallel system** for computing statistical metrics on extremely large integer datasets using **MPI (Message Passing Interface)**.

💡 Designed for **distributed memory systems** with focus on:

* Performance ⚡
* Scalability 📈
* Memory efficiency 🧠

---

## ✨ Key Features

* 🔹 Parallel processing باستخدام MPI
* 🔹 Load balancing ذكي باستخدام `MPI_Scatterv`
* 🔹 Dynamic Hash Table (rehashing عند 0.75 load factor)
* 🔹 يدعم أرقام ضخمة (`int64_t`)
* 🔹 Efficient memory usage (stores unique values only)
* 🔹 يتعامل مع ملفات أكبر من **1GB**
* 🔹 Docker support لتشغيل سهل

---

## 📊 Computed Statistics

| Metric       | Description       |
| ------------ | ----------------- |
| 🔽 Minimum   | أقل قيمة          |
| 🔼 Maximum   | أكبر قيمة         |
| ➕ Sum        | مجموع القيم       |
| 📈 Mean      | المتوسط الحسابي   |
| 🔁 Frequency | عدد تكرار كل قيمة |

---

## 🏗️ Project Structure

```bash
hpc-task2-statistics/
│
├── src/
│   ├── main.c
│   ├── mpi_distributor.c
│   ├── stats_calculator.c
│   ├── frequency_tracker.c
│   └── data_loader.c
│
├── include/
│
├── data/
├── output/
├── bin/
│
├── Makefile
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## ⚙️ Installation

### 🐧 Linux / WSL

```bash
sudo apt update
sudo apt install -y mpich gcc make
```

### 🐳 Docker (Recommended)

```bash
docker build -t mpi-stats .
```

---

## 🔨 Build

```bash
make clean
make
```

---

## ▶️ Run

### باستخدام MPI

```bash
mpirun -np 4 ./bin/stats data/input.txt
```

### باستخدام Docker

```bash
docker run --rm -v $(pwd):/app mpi-stats mpirun -np 4 /app/bin/stats /app/data/input.txt
```

---

## 🧪 Generate Test Data

### Small

```bash
for i in {1..10000}; do echo $((RANDOM % 1000)); done > data/input.txt
```

### Large

```bash
python3 generate_text.py
```

---

## 📊 Sample Output

```text
Total elements: 145,400,000
Minimum: -1000000
Maximum: 1000000
Mean: 8.49

=== Frequency Table ===
Unique values: 2,000,001
```

---

## 📈 Performance

| Dataset | Time  | Speed         |
| ------- | ----- | ------------- |
| 100KB   | 0.01s | 1M nums/sec   |
| 100MB   | 27s   | 540K nums/sec |
| 1GB     | 222s  | 654K nums/sec |

✔ Scaling شبه Linear
✔ أفضل أداء عند 4 processes

---

## ⚡ How It Works

### 1️⃣ Data Distribution

```c
MPI_Scatterv(...)
```

### 2️⃣ Local Computation

* Min / Max / Sum
* Frequency باستخدام Hash Table

### 3️⃣ Result Aggregation

```c
MPI_Reduce(...)
```

---

## 🧠 Core Idea

بدل ما نخزن كل البيانات:
✔ بنخزن **القيم unique فقط**
✔ مع عدد التكرار

➡️ ده بيقلل الذاكرة بشكل ضخم جدًا

---

## 🐳 Docker Support

```bash
docker build -t mpi-stats .
docker-compose up
```

---

## 🛠️ Requirements

* MPI (MPICH / OpenMPI)
* GCC
* Linux / WSL / Docker
* ≥ 2GB RAM

---

## 🐛 Troubleshooting

| Problem         | Solution              |
| --------------- | --------------------- |
| mpicc not found | install mpich         |
| slots error     | use `--oversubscribe` |
| memory issue    | reduce dataset        |

---

## 🚀 Future Work

* Streaming for huge files
* GPU acceleration (CUDA)
* Binary file processing
* Real-time progress bar

---

## 👨‍💻 Author

**Mohamed Abdelmonem**
HPC Course - 2026

---

## 📄 License

MIT License

---

## ⭐ Final Note

This project demonstrates:

* Parallel Computing باستخدام MPI
* Efficient Data Structures
* Real-world large-scale processing

🔥 مناسب جدًا كمشروع HPC قوي
