# Timmomatic_tool
Use of Timmomatic tool for the removal of poor-quality reads

# Software Requirements
*Ubuntu (WSL)
*Java
*FastQC
*Trimmomatic v0.39

Raw FASTQ
     │
     ▼
FastQC (Quality Check)
     │
     ▼
Trimmomatic
(Remove low-quality bases)
     │
     ▼
Trimmed FASTQ
     │
     ▼
FastQC
(Post-trimming Quality Check)
     │
     ▼
Compare Raw vs Trimmed Reports



# Step 1: Check the Raw Data

Move to the directory containing the FASTQ file.


cd /mnt/c
ls

Example output

```
test_udemy.fastq
```

Run FastQC

```bash
fastqc test_udemy.fastq
```

Files generated

```
test_udemy_fastqc.html
test_udemy_fastqc.zip
```

Open the HTML report

```bash
explorer.exe .
```

---

# Step 2: Copy FASTQ File to Home Directory

Copy the FASTQ file from Windows to the Linux home directory.

```bash
cp /mnt/c/test_udemy.fastq ~/
```

Go to the home directory.

```bash
cd ~
```

Verify the file.

```bash
ls
```

---

# Step 3: Run Trimmomatic

For **Single-End (SE)** sequencing:

```bash
TrimmomaticSE -phred33 test_udemy.fastq test_trimmed.fastq TRAILING:10
```

### Explanation of Parameters

| Parameter          | Description                                                 |
| ------------------ | ----------------------------------------------------------- |
| TrimmomaticSE      | Single-end trimming                                         |
| -phred33           | Input quality encoding (Phred+33)                           |
| test_udemy.fastq   | Input FASTQ file                                            |
| test_trimmed.fastq | Output trimmed FASTQ file                                   |
| TRAILING:10        | Remove low-quality bases from the 3' end with quality < Q10 |

---

# Single-End vs Paired-End Sequencing

### Single-End (SE)

* DNA fragment is sequenced from one end only.
* Lower cost.
* Simpler analysis.
* Higher probability of mapping errors compared to paired-end sequencing.

### Paired-End (PE)

* DNA fragment is sequenced from both ends.
* Higher accuracy.
* Better alignment.
* Preferred for RNA-Seq studies.

---

# Step 4: Trimming Output

Successful execution produces output similar to:

```
Input Reads: 305
Surviving: 305 (100.00%)
Dropped: 0 (0.00%)

TrimmomaticSE: Completed successfully
```

### Interpretation

* Input reads = **305**
* Surviving reads = **305**
* Dropped reads = **0**
* No poor-quality reads were removed because the dataset already had good sequencing quality.

---

# Step 5: Run FastQC on Trimmed Reads

```bash
fastqc test_trimmed.fastq
```

Generated files

```
test_trimmed_fastqc.html
test_trimmed_fastqc.zip
```

---

# Step 6: Compare FastQC Reports

Compare the following reports:

* Raw FASTQ FastQC Report
* Trimmed FASTQ FastQC Report

Important modules to compare:

* Basic Statistics
* Per Base Sequence Quality
* Per Sequence Quality Scores
* Per Base Sequence Content
* Per Sequence GC Content
* Sequence Length Distribution
* Sequence Duplication Levels
* Adapter Content

---

# Viewing the HTML Report in Windows

```bash
explorer.exe .
```

---

# Copy Report to Windows Desktop

```bash
cp test_trimmed_fastqc.html /mnt/c/Users/HP/Desktop/
```

---

# Copy Report to Windows Downloads Folder

```bash
cp test_trimmed_fastqc.html /mnt/c/Users/HP/Downloads/
```

> **Note:** Replace `HP` with your Windows username if it is different.

---

# Results

| Parameter             | Value        |
| --------------------- | ------------ |
| Total Reads           | 305          |
| Sequence Length       | 100 bp       |
| Average Read Quality  | ~Q37         |
| Adapter Contamination | Not detected |
| Reads Dropped         | 0            |
| Surviving Reads       | 305 (100%)   |
| Quality Encoding      | Phred+33     |

<img width="1787" height="853" alt="image" src="https://github.com/user-attachments/assets/0ea3dc45-9f64-4c53-85c8-b7881c9bb0a2" />
