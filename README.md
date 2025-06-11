# JMeter Tutorial - Performance Testing & API Testing

![JMeter Logo](https://jmeter.apache.org/images/logo.svg)

## 🎯 Overview

Apache JMeter adalah open-source software untuk performance testing dan load testing yang mendukung berbagai protokol dan platform:

- ✅ Aplikasi Web (HTTP/HTTPS)
- ✅ REST API & SOAP Web Services
- ✅ Database (JDBC)
- ✅ FTP Server
- ✅ Message Queue (JMS)
- ✅ LDAP Server

### Key Features
- 🚀 GUI dan Command Line Interface
- 📊 Real-time hasil testing
- 🔄 Test plan yang dapat digunakan kembali
- 📈 Berbagai format laporan
- 🎯 Simulasi ribuan concurrent users

## 🔧 Prerequisites

Sebelum memulai, pastikan sistem Anda memiliki:

### System Requirements
```
- Java Development Kit (JDK) 8 atau lebih tinggi
- RAM minimal 2GB (disarankan 4GB+)
- Disk space minimal 100MB
- Operating System: Windows, macOS, atau Linux
```

### Check Java Installation
```bash
java -version
```
Expected output:
```
java version "1.8.0_XXX" atau lebih tinggi
```

## 📦 Installation

### Step 1: Download JMeter

1. Kunjungi [Apache JMeter Download Page](https://jmeter.apache.org/download_jmeter.cgi)
2. Download **Binary** (bukan Source) dalam format `.zip` atau `.tgz`
3. Pilih versi terbaru stable release

```bash
# Example download URL
https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-5.6.3.zip
```

### Step 2: Extract dan Setup

#### Windows:
```cmd
# Extract ke direktori pilihan (contoh: C:\jmeter)
# Navigate ke folder bin
cd C:\jmeter\apache-jmeter-5.6.3\bin
# Jalankan JMeter
jmeter.bat
```

#### macOS/Linux:
```bash
# Extract file
tar -xzf apache-jmeter-5.6.3.tgz
# atau unzip apache-jmeter-5.6.3.zip

# Navigate ke folder bin
cd apache-jmeter-5.6.3/bin

# Make executable (if needed)
chmod +x jmeter.sh

# Jalankan JMeter
./jmeter.sh
```

### Step 3: Verify Installation

Jika instalasi berhasil, JMeter GUI akan terbuka dengan tampilan Test Plan kosong.

## 🖥️ JMeter Interface

### Main Components

| Component | Description | Icon |
|-----------|-------------|------|
| **Test Plan** | Root element yang berisi semua test elements | 📋 |
| **Thread Group** | Mengatur jumlah virtual users dan execution | 👥 |
| **Samplers** | Mengirim requests ke target server | 📡 |
| **Listeners** | Menampilkan dan menyimpan test results | 📊 |
| **Assertions** | Memvalidasi response dari server | ✅ |
| **Timers** | Mengatur delay antar requests | ⏱️ |

### Navigation Tree Structure
```
Test Plan
├── Thread Group
│   ├── HTTP Request (Sampler)
│   ├── Response Assertion
│   ├── Constant Timer
│   └── View Results Tree (Listener)
└── HTTP Header Manager
```

## 🚀 Quick Start Guide

### Basic Performance Test dalam 5 Menit

#### Step 1: Create Test Plan
```
File → New → Test Plan
```

#### Step 2: Add Thread Group
```
Right-click Test Plan → Add → Threads (Users) → Thread Group
```

**Configuration:**
- Number of Threads: `10`
- Ramp-Up Period: `5` seconds
- Loop Count: `3`

#### Step 3: Add HTTP Request
```
Right-click Thread Group → Add → Sampler → HTTP Request
```

**Configuration:**
- Server Name: `httpbin.org`
- Path: `/get`
- Method: `GET`

#### Step 4: Add Listener
```
Right-click Thread Group → Add → Listener → View Results Tree
```

#### Step 5: Run Test
```
Click Play button (▶️) atau tekan Ctrl+R
```

#### Step 6: Analyze Results
Check **View Results Tree** untuk melihat:
- ✅ Request details
- ✅ Response data
- ✅ Response time
- ✅ Status codes

## 📈 Performance Testing

Performance Testing mengukur kinerja sistem dalam kondisi normal.

### Complete Step-by-Step Guide

#### 1. Setup Test Plan

```
File → New
```

#### 2. Configure Thread Group

```
Right-click Test Plan → Add → Threads (Users) → Thread Group
```

**Thread Group Settings:**
```yaml
Name: Performance Test Thread Group
Number of Threads (users): 50
Ramp-Up Period (seconds): 30
Loop Count: 5
Action to be taken after a Sampler error: Continue
```

**Penjelasan:**
- **50 users** akan dibuat secara bertahap
- **30 seconds** untuk mencapai 50 users (1.67 users/second)
- **5 iterations** untuk setiap user
- **Continue** jika ada error (tidak stop test)

#### 3. Add HTTP Request Sampler

```
Right-click Thread Group → Add → Sampler → HTTP Request
```

**HTTP Request Configuration:**
```yaml
Name: Homepage Request
Server Name or IP: example.com
Port Number: (kosong - default 80/443)
Protocol: https
Method: GET
Path: /
```

#### 4. Add HTTP Header Manager

```
Right-click HTTP Request → Add → Config Element → HTTP Header Manager
```

**Headers:**
```
User-Agent: Mozilla/5.0 (compatible; JMeter Performance Test)
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
```

#### 5. Add Timer (Realistic User Behavior)

```
Right-click Thread Group → Add → Timer → Constant Timer
```

**Timer Configuration:**
```yaml
Thread Delay: 1000 milliseconds (1 second)
```

#### 6. Add Multiple Listeners

##### Graph Results
```
Right-click Thread Group → Add → Listener → Graph Results
```

##### Summary Report
```
Right-click Thread Group → Add → Listener → Summary Report
```

##### Aggregate Report
```
Right-click Thread Group → Add → Listener → Aggregate Report
```

#### 7. Add Response Assertion

```
Right-click HTTP Request → Add → Assertions → Response Assertion
```

**Assertion Configuration:**
```yaml
Field to Test: Response Code
Pattern Matching Rules: Equals
Patterns to Test: 200
```

#### 8. Save Test Plan

```
File → Save As → performance_test.jmx
```

#### 9. Execute Test

```
Click Play (▶️) button
```

#### 10. Monitor Results

**Graph Results akan menampilkan:**
- 📊 Response times over time
- 📈 Throughput
- 🎯 Active threads

**Summary Report menampilkan:**
- ⏱️ Average response time
- 📊 Min/Max response times
- 🎯 Throughput (requests/second)
- ❌ Error percentage

## 🔥 Load Testing

Load Testing mengevaluasi performa dengan beban normal yang diharapkan.

### E-commerce Load Test Example

#### Scenario:
- **Target:** Online store dapat menangani 500 concurrent users
- **Duration:** 10 menit
- **Activities:** Browse products, add to cart, checkout

#### Step-by-Step Implementation:

#### 1. Thread Group Configuration
```yaml
Name: E-commerce Load Test
Number of Threads: 500
Ramp-Up Period: 300 seconds (5 minutes)
Loop Count: Infinite
Duration: 600 seconds (10 minutes)
```

#### 2. Multiple HTTP Requests

##### Browse Homepage
```
Right-click Thread Group → Add → Sampler → HTTP Request
```
```yaml
Name: Browse Homepage
Server: shop.example.com
Path: /
Method: GET
```

##### Search Products
```yaml
Name: Search Products
Server: shop.example.com
Path: /search
Method: GET
Parameters:
  - q: laptop
  - category: electronics
```

##### View Product Detail
```yaml
Name: Product Detail
Server: shop.example.com
Path: /product/${productId}
Method: GET
```

##### Add to Cart
```yaml
Name: Add to Cart
Server: shop.example.com
Path: /cart/add
Method: POST
Body Data: {"productId": "${productId}", "quantity": 1}
```

#### 3. User Defined Variables

```
Right-click Test Plan → Add → Config Element → User Defined Variables
```

```yaml
Variables:
  - productId: 12345
  - userId: ${__Random(1,1000)}
  - sessionId: ${__UUID()}
```

#### 4. CSV Data Set Config (Realistic Data)

```
Right-click Thread Group → Add → Config Element → CSV Data Set Config
```

**Create products.csv:**
```csv
productId,productName,price
12345,Laptop Dell,15000000
12346,Mouse Wireless,250000
12347,Keyboard Mechanical,750000
```

**Configuration:**
```yaml
Filename: products.csv
Variable Names: productId,productName,price
Delimiter: ,
Recycle on EOF: True
Stop thread on EOF: False
```

#### 5. Think Time (Realistic User Behavior)

```
Right-click Thread Group → Add → Timer → Gaussian Random Timer
```

```yaml
Deviation: 1000 ms
Constant Delay Offset: 2000 ms
```

#### 6. Advanced Listeners

##### Response Time Graph
```
Right-click Thread Group → Add → Listener → Response Time Graph
```

##### Transactions per Second
```
Right-click Thread Group → Add → Listener → Transactions per Second
```

#### 7. Monitoring Server Resources

**JMeter Plugins (Optional):**
- PerfMon Server Agent
- System resource monitoring

#### 8. Success Criteria

**Define acceptable thresholds:**
```yaml
Average Response Time: < 2 seconds
95th Percentile: < 5 seconds
Error Rate: < 0.5%
Throughput: > 50 requests/second
```

## ⚡ Stress Testing

Stress Testing menentukan breaking point sistem dengan beban ekstrem.

### Implementation Guide:

#### 1. Aggressive Thread Group
```yaml
Name: Stress Test
Number of Threads: 2000
Ramp-Up Period: 60 seconds
Loop Count: Infinite
Duration: 1800 seconds (30 minutes)
```

#### 2. Stepping Thread Group (JMeter Plugin)

**Pattern:**
```
0-300s: 0 → 500 users
300-600s: 500 users (steady)
600-900s: 500 → 1000 users  
900-1200s: 1000 users (steady)
1200-1500s: 1000 → 2000 users
1500-1800s: 2000 users (peak stress)
```

#### 3. Minimal Think Time
```yaml
Constant Timer: 100 milliseconds
```

#### 4. Resource Monitoring
- CPU usage
- Memory consumption  
- Database connections
- Network bandwidth

#### 5. Failure Detection
```yaml
Response Assertion:
  - Response Code: 200
  - Response Time < 10000ms (10 seconds)
  
Duration Assertion:
  - Maximum Duration: 10000ms
```

## ✅ Functional Testing

Functional Testing memvalidasi bahwa aplikasi bekerja sesuai spesifikasi.

### Login Functionality Test

#### Step-by-Step:

#### 1. Test Scenario Design
```yaml
Test Case: User Login
Steps:
  1. Navigate to login page
  2. Enter valid credentials
  3. Submit form
  4. Verify successful login
  5. Logout
```

#### 2. Thread Group (Single User)
```yaml
Number of Threads: 1
Ramp-Up Period: 1
Loop Count: 1
```

#### 3. HTTP Requests Sequence

##### Get Login Page
```yaml
Name: Get Login Page
Method: GET
Path: /login
```

##### Submit Login
```yaml
Name: Submit Login
Method: POST
Path: /login
Parameters:
  - username: testuser@example.com
  - password: testpassword123
```

##### Access Protected Page
```yaml
Name: Dashboard Access
Method: GET
Path: /dashboard
```

#### 4. Functional Assertions

##### Login Response Assertion
```yaml
Field to Test: Response Data
Pattern Matching: Contains
Pattern: "Welcome" or "Dashboard"
```

##### Redirect Assertion
```yaml
Field to Test: Response Code
Pattern: 302 (redirect) or 200 (success)
```

##### Cookie Assertion
```yaml
Response Assertion:
Pattern: Set-Cookie
Contains: session_id
```

#### 5. Regular Expression Extractor

Extract session token:
```yaml
Reference Name: sessionToken
Regular Expression: session_token=([^;]+)
Template: $1$
Match No.: 1
```

## 🔌 API Testing

Comprehensive API testing untuk REST services.

### Complete REST API Test Suite

#### Test Scenario: CRUD Operations

#### 1. Test Plan Structure
```
API Test Suite
├── Thread Group (API Tests)
│   ├── Create User (POST)
│   ├── Get User (GET)  
│   ├── Update User (PUT)
│   ├── Delete User (DELETE)
│   └── View Results Tree
└── HTTP Header Manager
```

#### 2. Global HTTP Header Manager
```
Right-click Test Plan → Add → Config Element → HTTP Header Manager
```

**Headers:**
```yaml
Content-Type: application/json
Accept: application/json
Authorization: Bearer ${authToken}
User-Agent: JMeter API Test Suite v1.0
```

#### 3. Base URL Configuration
```
Right-click Test Plan → Add → Config Element → User Defined Variables
```

```yaml
Variables:
  - baseUrl: jsonplaceholder.typicode.com
  - apiVersion: v1
  - userId: ${__Random(1,100)}
```

#### 4. CREATE Operation (POST)

```
Right-click Thread Group → Add → Sampler → HTTP Request
```

**Configuration:**
```yaml
Name: Create User
Server Name: ${baseUrl}
Path: /posts
Method: POST
Body Data:
{
  "title": "JMeter API Test",
  "body": "Testing POST operation with JMeter",
  "userId": ${userId}
}
```

**JSON Extractor untuk Response:**
```
Right-click HTTP Request → Add → Post Processors → JSON Extractor
```

```yaml
Variable Name: createdPostId
JSON Path Expression: $.id
Match No.: 1
Default Value: ERROR
```

**Assertions:**
```yaml
Response Assertion:
  - Field: Response Code
  - Pattern: 201

JSON Assertion:
  - JSON Path: $.title
  - Expected Value: JMeter API Test

Duration Assertion:
  - Duration < 2000ms
```

#### 5. READ Operation (GET)

```yaml
Name: Get User
Server Name: ${baseUrl}
Path: /posts/${createdPostId}
Method: GET
```

**Assertions:**
```yaml
Response Assertion:
  - Field: Response Code  
  - Pattern: 200

JSON Assertion:
  - JSON Path: $.id
  - Expected Value: ${createdPostId}

Size Assertion:
  - Response Size > 100 bytes
```

#### 6. UPDATE Operation (PUT)

```yaml
Name: Update User
Server Name: ${baseUrl}  
Path: /posts/${createdPostId}
Method: PUT
Body Data:
{
  "id": ${createdPostId},
  "title": "Updated JMeter Test",
  "body": "Updated content via JMeter",
  "userId": ${userId}
}
```

#### 7. DELETE Operation (DELETE)

```yaml
Name: Delete User
Server Name: ${baseUrl}
Path: /posts/${createdPostId}  
Method: DELETE
```

**Assertion:**
```yaml
Response Assertion:
  - Field: Response Code
  - Pattern: 200
```

#### 8. Error Handling Tests

##### Invalid Endpoint Test
```yaml
Name: Invalid Endpoint
Path: /invalid-endpoint
Expected Response: 404
```

##### Malformed JSON Test  
```yaml
Name: Malformed JSON
Body Data: {"invalid": json}
Expected Response: 400
```

#### 9. Authentication Testing

##### OAuth 2.0 Flow
```yaml
1. Get Access Token:
   POST /oauth/token
   Body: grant_type=client_credentials&client_id=xxx&client_secret=yyy

2. Extract Token:
   JSON Extractor: $.access_token → authToken

3. Use Token in Headers:
   Authorization: Bearer ${authToken}
```

#### 10. Advanced API Validations

##### Schema Validation
```yaml
JSON Schema Assertion:
Schema:
{
  "type": "object",
  "properties": {
    "id": {"type": "integer"},
    "title": {"type": "string"},
    "body": {"type": "string"}
  },
  "required": ["id", "title", "body"]
}
```

##### Response Time SLA
```yaml
Duration Assertion:
  - GET requests: < 500ms
  - POST requests: < 1000ms  
  - PUT requests: < 800ms
  - DELETE requests: < 300ms
```

#### 11. Data-Driven Testing

**Create test-data.csv:**
```csv
title,body,userId
Test Title 1,Test Body 1,1
Test Title 2,Test Body 2,2
Test Title 3,Test Body 3,3
```

**CSV Data Set Config:**
```yaml
Filename: test-data.csv
Variable Names: title,body,userId
Delimiter: ,
```

**Use in HTTP Request:**
```json
{
  "title": "${title}",
  "body": "${body}",
  "userId": ${userId}
}
```

#### 12. Comprehensive Test Execution

```bash
# Run from command line for CI/CD
jmeter -n -t api_test_suite.jmx -l results.jtl -e -o ./html-report
```

## 🎯 Best Practices

### Performance Testing

#### 1. Environment Setup
```yaml
Test Environment:
  - Isolated from production
  - Similar hardware specs
  - Realistic network conditions
  - Clean state before each test
```

#### 2. Realistic Load Patterns
```yaml
Ramp-up Strategy:
  - Gradual increase (not spike)
  - Monitor breaking points
  - Different user behaviors
  - Think time between actions
```

#### 3. Resource Monitoring
```bash
# Monitor during tests:
- CPU usage
- Memory consumption
- Network I/O
- Database connections
- Application logs
```

### API Testing

#### 1. Test Data Management
```yaml
Strategies:
  - Use test databases
  - Reset data between runs
  - Parameterize test data
  - Handle dependencies
```

#### 2. Response Validation
```yaml
Validation Layers:
  - Status codes
  - Response structure  
  - Business logic
  - Performance SLA
  - Security headers
```

### General Guidelines

#### 1. Test Plan Organization
```
Best Structure:
├── Test Plan
│   ├── User Defined Variables (Global config)
│   ├── HTTP Header Manager (Global headers)
│   ├── Thread Group 1 (Scenario 1)
│   │   ├── HTTP Requests
│   │   ├── Assertions
│   │   ├── Timers
│   │   └── Listeners
│   └── Thread Group 2 (Scenario 2)
```

#### 2. Naming Conventions
```yaml
Examples:
  - Thread Groups: "Load_Test_500_Users"
  - HTTP Requests: "API_POST_CreateUser"
  - Assertions: "Assert_ResponseCode_200"
  - Variables: "baseUrl", "userId", "authToken"
```

#### 3. Version Control
```bash
# Track test plans in Git
git add *.jmx
git commit -m "Add load test for user registration"

# Include test data
git add test-data/
git add properties/
```

## 🐛 Troubleshooting

### Common Issues & Solutions

#### 1. High Memory Usage

**Problem:** JMeter consumes too much memory

**Solutions:**
```bash
# Increase JVM heap size
export JVM_ARGS="-Xms1g -Xmx4g"

# Use non-GUI mode for load tests
jmeter -n -t testplan.jmx -l results.jtl

# Disable unnecessary listeners
# Use Simple Data Writer instead of View Results Tree
```

#### 2. Connection Timeouts

**Problem:** Requests timing out

**Solutions:**
```yaml
HTTP Request Advanced:
  - Connect Timeout: 60000ms
  - Response Timeout: 60000ms
  
System Properties:
  - httpclient.timeout: 60000
```

#### 3. SSL Certificate Issues

**Problem:** HTTPS requests failing

**Solutions:**
```bash
# Ignore SSL certificates (testing only)
System Properties:
  - javax.net.ssl.trustStore: path/to/keystore
  - javax.net.ssl.trustStorePassword: password
```

#### 4. Assertion Failures

**Problem:** Tests failing unexpectedly

**Debug Steps:**
```yaml
1. Check View Results Tree:
   - Request details
   - Response data
   - Response headers

2. Verify Assertions:
   - Correct patterns
   - Case sensitivity
   - Regular expressions

3. Add Debug Samplers:
   - Log variable values
   - Check extracted data
```

#### 5. Performance Issues

**Problem:** JMeter itself is slow

**Optimizations:**
```yaml
JMeter Settings:
  - Disable View Results Tree during load tests
  - Use Summary Report only
  - Increase Java heap size
  - Use distributed testing for high loads
```

### Debugging Tools

#### 1. Debug Sampler
```
Add → Sampler → Debug Sampler
```
Shows all variables and properties.

#### 2. Log Viewer
```
Options → Log Viewer
```
Shows JMeter internal logs.

#### 3. HTTP Mirror Server
```bash
# Start mirror server for request debugging
jmeter-server -Dserver.rmi.ssl.disable=true
```

## 🤝 Contributing

### How to Contribute

1. **Fork** the repository
2. **Create** feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** changes (`git commit -m 'Add amazing feature'`)
4. **Push** to branch (`git push origin feature/amazing-feature`)
5. **Open** Pull Request

### Test Plan Standards

```yaml
Requirements:
  - Clear naming conventions
  - Comprehensive comments
  - Parameterized configurations
  - Proper assertions
  - Documentation updates
```

### Reporting Issues

When reporting issues, include:
- JMeter version
- Java version
- Operating system
- Test plan file (.jmx)
- Error logs
- Steps to reproduce

## 📚 Additional Resources

### Official Documentation
- [Apache JMeter User Manual](https://jmeter.apache.org/usermanual/index.html)
- [JMeter Best Practices](https://jmeter.apache.org/usermanual/best-practices.html)

### Useful Plugins
- [JMeter Plugins Manager](https://jmeter-plugins.org/wiki/PluginsManager/)
- [3 Basic Graphs](https://jmeter-plugins.org/wiki/ResponseTimesOverTime/)
- [PerfMon Server Agent](https://jmeter-plugins.org/wiki/PerfMonAgent/)

### Community
- [JMeter User Mailing List](http://jmeter.apache.org/mail.html)
- [Stack Overflow - JMeter](https://stackoverflow.com/questions/tagged/jmeter)
- [JMeter Reddit Community](https://www.reddit.com/r/jmeter/)

---


**Happy Testing! 🚀**
