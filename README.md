# คู่มือการติดตั้ง PySpark บน Windows และ Mac OS

## สารบัญ
1. [การติดตั้ง Conda](#การติดตั้ง-conda)
2. [การติดตั้ง Java Development Kit (JDK)](#การติดตั้ง-java-development-kit-jdk)
3. [การติดตั้ง Apache Spark](#การติดตั้ง-apache-spark)
4. [การตั้งค่า Environment Variables](#การตั้งค่า-environment-variables)
5. [การติดตั้ง Python และ PySpark ผ่าน conda](#การติดตั้ง-python-และ-pyspark-ผ่าน-conda)

## การติดตั้ง Conda

### Windows
1. ดาวน์โหลด Miniconda จาก: https://docs.conda.io/en/latest/miniconda.html
2. เลือก Miniconda3 Windows 64-bit
3. เปิดไฟล์ติดตั้งและทำตามขั้นตอน
4. ตรวจสอบการติดตั้งโดยเปิด Command Prompt และพิมพ์:
   ```bash
   conda --version
   ```

### Mac OS
1. ดาวน์โหลด Miniconda จาก: https://docs.conda.io/en/latest/miniconda.html
2. เลือก Miniconda3 macOS 64-bit
3. เปิด Terminal และไปยังโฟลเดอร์ที่ดาวน์โหลด
4. รันคำสั่ง:
   ```bash
   bash Miniconda3-latest-MacOSX-x86_64.sh
   ```
5. ทำตามขั้นตอนการติดตั้ง
6. ตรวจสอบการติดตั้ง:
   ```bash
   conda --version
   ```

## การติดตั้ง Java Development Kit (JDK)

### Windows
1. ดาวน์โหลด OpenJDK จาก: https://adoptium.net/
2. เลือกเวอร์ชัน 8 LTS ขึ้นไป (เช่น JDK 8 LTS)
3. ดาวน์โหลดและติดตั้งตามขั้นตอน
4. ตรวจสอบการติดตั้ง:
   ```bash
   java -version
   ```

### Mac OS
1. เปิด Terminal
2. ติดตั้ง OpenJDK ผ่าน Homebrew:
   ```bash
   brew install --cask temurin11
   ```
3. ตรวจสอบการติดตั้ง:
   ```bash
   java -version
   ```

## การติดตั้ง Apache Spark

### Windows
1. ดาวน์โหลด Apache Spark จาก: https://spark.apache.org/downloads.html
2. เลือกเวอร์ชันล่าสุดและ package type: Pre-built for Apache Hadoop
3. แตกไฟล์ zip ไปยังตำแหน่งที่ต้องการ (เช่น C:\spark)

### Mac OS
1. ติดตั้งผ่าน Homebrew:
   ```bash
   brew install apache-spark
   ```

## Download winutils.exe

### Windows
1. ดาวน์โหลด winutils จาก: https://github.com/cdarlint/winutils/tree/master/hadoop-3.3.6
2. สร้างโฟลเดอร์ชื่อ "hadoop\bin" ของไดรฟ์ C:
3. คัดลอกไฟล์ winutils.exe ที่ดาวน์โหลดมาไปยังไดรฟ์ "C:\hadoop\bin"

## การตั้งค่า Environment Variables

### Windows
1. เปิด System Properties > Advanced > Environment Variables
2. เพิ่ม System Variables:
   - JAVA_HOME: ตำแหน่งที่ติดตั้ง JDK
   - SPARK_HOME: ตำแหน่งที่ติดตั้ง Spark
   - PATH: เพิ่ม %SPARK_HOME%\bin และ %JAVA_HOME%\bin

### Mac OS
1. เปิดไฟล์ ~/.zshrc หรือ ~/.bash_profile:
   ```bash
   nano ~/.zshrc
   ```
2. เพิ่มบรรทัดต่อไปนี้:
   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home)
   export SPARK_HOME=/usr/local/Cellar/apache-spark/[version]/libexec
   export PATH=$PATH:$SPARK_HOME/bin
   ```
3. บันทึกและรีโหลด:
   ```bash
   source ~/.zshrc
   ```

## การติดตั้ง Python และ PySpark ผ่าน conda

### Windows และ Mac OS (ขั้นตอนเหมือนกัน)
1. สร้าง conda environment ใหม่:
   ```bash
   conda create -n pyspark python=3.9
   ```
2. เปิดใช้งาน environment:
   ```bash
   conda activate pyspark
   ```
3. ติดตั้ง PySpark:
   ```bash
   conda install pyspark
   ```
4. ตรวจสอบการติดตั้ง:
   ```python
   python
   >>> import pyspark
   >>> print(pyspark.__version__)
   ```

## การทดสอบการติดตั้ง

ทดสอบ PySpark โดยรันโค้ดต่อไปนี้:
```python
from pyspark.sql import SparkSession

# สร้าง SparkSession
spark = SparkSession.builder \
    .appName("Test") \
    .getOrCreate()

# ทดสอบสร้าง DataFrame
df = spark.createDataFrame([("test",)], ["col1"])
df.show()

# ปิด SparkSession
spark.stop()
```

หากไม่มี error แสดงว่าการติดตั้งสำเร็จ

## การแก้ไขปัญหาทั่วไป

1. หากพบ error เกี่ยวกับ Java:
   - ตรวจสอบการตั้งค่า JAVA_HOME
   - ตรวจสอบเวอร์ชัน Java ที่ติดตั้ง

2. หากพบ error เกี่ยวกับ Spark:
   - ตรวจสอบการตั้งค่า SPARK_HOME
   - ตรวจสอบว่า PATH มีการเพิ่ม Spark bin directory

3. หากพบ error เกี่ยวกับ PySpark:
   - ลองติดตั้ง PySpark ใหม่ด้วย pip:
     ```bash
     pip install pyspark
     ```
   - ตรวจสอบเวอร์ชัน Python ที่ใช้
