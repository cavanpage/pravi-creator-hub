# Pravi Creator Hub - High-Throughput Media Ingestion and Observability

Pravi Creator Hub is a professional grade desktop ingestion engine and creative utility designed for photographers and videographers who manage high volumes of data across multiple physical drives. It replaces manual file shuffling with a high-concurrency pipeline, automated triage, and real-time observability.

### The Mission
To provide a one-click workflow that handles the heavy lifting of media organization while giving the user deep visibility into the system performance and creative tools for rapid content generation.

* **Kotlin (Desktop):** Orchestrates multi-threaded IO, manages complex UI states, and provides a hardware-accelerated preview interface for collage creation.
* **Python (Sidecar):** Executes the brain logic, including metadata-based triage (EXIF), AI-driven aesthetic scoring, and automated image composition for collages.

---

### System Architecture

#### High-Performance Ingestion (Kotlin)
* **Multi-Lane Pipelines:** Uses Kotlin Coroutines with LimitedParallelism to saturate hardware IO without UI blocking.
* **State Management:** Implements a strict MVI (Model-View-Intent) pattern to handle hardware mount and unmount events.
* **Observability Dashboard:** Real-time canvas-based graphs for throughput (MB/s), IO wait times, and hash-based integrity verification.

#### Intelligent Triage and Composition (Python)
* **Automated Sorting:** Maps files to a structured hierarchy for Videos, RAW photos, and JPEGs.
* **Collage Engine:** A Python-based processing module using Pillow or OpenCV to automatically arrange selected JPEGs into optimized grid layouts or social media ready collages.
* **AI Culling:** Lightweight CLIP or OpenCV implementation to identify junk shots before they waste cloud storage.
* **Headless Ingestion:** Uses Playwright to automate the Amazon Photos web-client for JPEG backups.

---

### Targeted Data Pipeline
Pravi Creator Hub automatically enforces organizational standards upon mounting a source:

1. **Source SD**
2. **.ARW (RAW)** targets /Volumes/Photo_Drive/2026/03-11_Project/RAW/
3. **.JPG (JPEG)** targets /Volumes/Photo_Drive/2026/03-11_Project/JPEG/ and Amazon Photos
4. **.MP4 (Video)** targets /Volumes/Video_Drive/2026/03-11_Project/

---

### Roadmap and Timeline

#### Phase 1: The Core Skeleton
* **Kotlin:** Initialize Compose Desktop app with a Source and Destination configuration UI.
* **Python:** Create a FastAPI sidecar service to handle file system indexing.
* **Connectivity:** Establish gRPC or Ktor communication between the UI and the Logic service.

#### Phase 2: The High-Throughput Pipeline
* **Concurrency:** Implement parallel copy lanes for RAW, JPEG, and Video.
* **Observability:** Build the real-time throughput dashboard using Compose Canvas.
* **Triage Logic:** Implement the Python metadata-triage script using ExifRead.

#### Phase 3: The Creative Suite
* **Collage Logic:** Develop Python functions to generate dynamic grid layouts based on image aspect ratios.
* **Live Preview:** Implement a Kotlin-based canvas to allow users to drag, drop, and reorder images before final collage rendering.
* **Export Engine:** One-click export of processed collages to the JPEG archive and Amazon Photos.

#### Phase 4: The Intelligence Layer
* **AI Scoring:** Integrate a culling model to flag low-quality images.
* **Cloud Bridge:** Implement the Amazon Photos automation via Playwright or Selenium.
* **Integrity Checks:** Add MD5 or SHA-256 verification after every transfer.

---

### Installation and Setup

1. **Environment:**
    * JDK 17+ (for Kotlin/JVM)
    * Python 3.10+
2. **Run Service:**
    ```bash
    cd service/
    pip install -r requirements.txt
    python main.py
    ```
3. **Run Desktop App:**
    ```bash
    ./gradlew run
    ```

---
