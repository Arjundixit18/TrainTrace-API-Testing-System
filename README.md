# 🚄 TrainTrace API Testing System
_Automated PNR Enquiry Testing Framework using Java, RestAssured & JSON Server_

TrainTrace API Testing System is a Java-based project built to automate and validate Railway PNR enquiry responses.  
It uses **RestAssured** to test a mock train status API created using **JSON Server**, ensuring high accuracy, fast responses, and correct passenger status validation.

---

## 🎯 Project Objective
This project automates verification of:

✅ PNR number search results  
✅ Passenger booking & current status (Confirmed / RAC / Waiting)  
✅ API response code and headers  
✅ Response performance (time < 2000 ms)  
✅ Accurate JSON data extraction  

---

## 🛠️ Tech Stack
| Technology | Purpose |
|-----------|----------|
| **Java** | Core programming |
| **RestAssured** | API test automation |
| **JSON Server** | Mock REST API |
| **IntelliJ / Eclipse** | IDE |
| **Git & GitHub** | Version control |

---

## 📁 Project Files
```

TrainTrace/
│
├── PNR_STATUS.java     → Test automation script using RestAssured
├── Pnr_api.json        → Mock API dataset for train & passenger status
└── README.md           → Project documentation

```

---

## 🚀 How the System Works

### ✅ 1. API Request Triggered  
The script sends:
```

GET /trainStatus?pnrNumber=2468013579

````

### ✅ 2. JSON Response Extracted  
Using RestAssured + JsonPath:
- Train Name  
- Train Number  
- Travel Date  
- Passenger Details  
- Booking & Current Status  

### ✅ 3. Automated Validations  
✔ Status Code = **200 OK**  
✔ Response Time < **2000 ms**  
✔ Content-Type = **application/json**  
✔ Passenger Status ∈ {Confirmed, RAC, Waiting}

Any invalid status → **Assertion Error**

---

## 📌 Code Overview: `PNR_STATUS.java`

Key features of the script:

- Sends GET request using RestAssured  
- Validates headers & response time  
- Extracts JSON response  
- Iterates all passengers  
- Ensures valid status values  
- Prints results neatly  

---

## 🧪 Sample Test Snippet

```java
given()
    .baseUri(baseURI)
    .pathParam("pnrNumber", pnrNumber)
.when()
    .get("/trainStatus?pnrNumber={pnrNumber}")
.then()
    .statusCode(200)
    .time(lessThan(2000L))
    .header("Content-Type", containsString("application/json"))
    .extract().response();
````

---

## 🗂 Mock API: `Pnr_api.json`

The mock API contains:

* PNR Number
* Train Name & Number
* Travel Date
* List of Passengers
* Seat & Status → Confirmed / RAC / Waiting

This allows real PNR-style validation without any live railway API.

---

## ▶️ How to Run

### 1️⃣ Start JSON Server

```bash
json-server --watch Pnr_api.json --port 3000
```

### 2️⃣ Run the Java Test

```bash
javac PNR_STATUS.java
java PNR_STATUS
```

(Or run via IntelliJ/Eclipse)

---

## ✅ Sample Output

```
PNR Search Results:
Train Name: Himgiri Express
Prince Singh | Seat: A1-11 | Status: Confirmed
Gautam Chandra | Seat: A1-12 | Status: Confirmed
```

---

## ⭐ Future Enhancements

* POST request for adding new passengers
* PUT/PATCH to update statuses
* JUnit/TestNG integration
* Detailed HTML report (Allure Report)

---

## 📜 License

Open-source under the MIT License.

---

## 💙 Support

If this project helped you, consider giving a ⭐ on GitHub!

