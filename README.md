# BijayaPerfTest_Jmeter
# 🚀 JMeter Setup and Application Deployment

This repository automates **performance testing with Apache JMeter** using **GitHub Actions**.  
It provisions **HTTPBin** as a mock API service and **cAdvisor** for container metrics, executes JMeter tests, and uploads comprehensive performance reports as workflow artifacts.

---

## 🧩 Workflow Overview

This GitHub Actions workflow performs the following steps manually on every push or pull request to the `main` branch:

1. **Set up environment**
   - Runs on `ubuntu-22.04`
   - Installs JDK 17, JMeter, and required plugins

2. **Start dependent services**
   - 🧱 **HTTPBin** (on port `8088`) — provides sample REST endpoints  
   - 📊 **cAdvisor** (on port `8080`) — exports container-level performance metrics

3. **Run JMeter test**
   - Executes the JMeter test plan:
     ```
     /Bijaya_JMeter/apache-jmeter-5.6.2/bin/jmeter -n -t /Bijaya_JMeter/Bijaya_Scripts/BaseScript.jmx
     /Bijaya_JMeter/apache-jmeter-5.6.2/bin/jmeter -n -t /Bijaya_JMeter/Bijaya_Scripts/HTTPBinAPI_EnduranceTest.jmx
     /Bijaya_JMeter/apache-jmeter-5.6.2/bin/jmeter -n -t /Bijaya_JMeter/Bijaya_Scripts/HTTPBinAPI_LoadTest.jmx
     /Bijaya_JMeter/apache-jmeter-5.6.2/bin/jmeter -n -t /Bijaya_JMeter/Bijaya_Scripts/HTTPBinAPI_SpikeTest.jmx
     /Bijaya_JMeter/apache-jmeter-5.6.2/bin/jmeter -n -t /Bijaya_JMeter/Bijaya_Scripts/HTTPBinAPI_StreeTest.jmx
     ```
   - Generates HTML and JTL reports in `/Bijaya_JMeter/TestResults/HTTPBinAPI_StreeTest`

4. **Collect reports**
   - Copies JMeter HTML report and cAdvisor metrics into:
     ```
     /Bijaya_JMeter/TestResults/HTTPBinAPI_StreeTest
     ```

5. **Upload artifacts**
   - Uploads performance reports as GitHub workflow artifacts for download.

---

## ⚙️ Services Used

| Service    | Purpose                        | Port | Docker Image                             |
|------------|--------------------------------|------|------------------------------------------|
| HTTPBin    | Mock API server for testing    | 8088 | `kennethreitz/httpbin`                    |
| cAdvisor   | Container performance metrics  | 8080 | `gcr.io/cadvisor/cadvisor:latest`        |

---

## 🧰 Installed Components

| Component  | Version / Source                            |
|------------|---------------------------------------------|
| JMeter     | 5.6.3 (from Apache archive)                 |
| Java       | OpenJDK 17                                  |
| JMeter Plugins | Plugins Manager + Ultimate Thread Group |

## Reference urls:
Application_url: http://localhost:88/
Application_url inside container: curl http://localhost:8080/get
Apache Jmeter Download: https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.6.3.zip


---
