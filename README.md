# Patient Management System API

This is a FastAPI-based application to manage patient records, including creating, viewing, and sorting patient data.

## Setup Instructions

### 1. Create and Activate a Virtual Environment

#### Create a Virtual Environment
Run the following command to create a virtual environment:
```bash
python3 -m venv venv
```
#### Activate Env

```bash
source venv/bin/activate
```

#### 2. Install Required Libraries
After activating the virtual environment, install the required libraries:

```bash
pip install fastapi uvicorn pydantic
```

#### 3. Run the API
Start the FastAPI server using uvicorn:

```bash
uvicorn main:app --reload
```

### main refers to the filename (main.py).
### app refers to the FastAPI instance in the file.
### The API will be available at: http://127.0.0.1:8000

#### 4. API Endpoints

### 1. **Welcome Endpoint**
- **URL**: `/`
- **Method**: `GET`
- **Description**: Returns a welcome message.
- **Response**:
  ```json
  {
    "message": "Patient Management System API"
  }
  ```

---

### 2. **About Endpoint**
- **URL**: `/about`
- **Method**: `GET`
- **Description**: Provides information about the API.
- **Response**:
  ```json
  {
    "message": "A fully functional API to manage your patient records"
  }
  ```

---

### 3. **View All Patients**
- **URL**: `/view`
- **Method**: `GET`
- **Description**: Retrieves all patient records.
- **Response**:
  ```json
  {
    "P001": {
      "name": "John Doe",
      "city": "New York",
      "age": 30,
      "gender": "male",
      "height": 1.75,
      "weight": 70,
      "bmi": 22.86,
      "verdict": "Normal"
    }
  }
  ```

---

### 4. **View a Specific Patient**
- **URL**: `/patient/{patient_id}`
- **Method**: `GET`
- **Description**: Retrieves a specific patient record by their ID.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient.
- **Response**:
  - **200 OK**: Returns the patient record.
  - **404 Not Found**: Patient not found.

---

### 5. **Sort Patients**
- **URL**: `/sort`
- **Method**: `GET`
- **Description**: Sorts patient records by height, weight, or BMI.
- **Query Parameters**:
  - `sort_by` (string): The field to sort by (`height`, `weight`, or `bmi`).
  - `order` (string): The sort order (`asc` for ascending, `desc` for descending).
- **Response**:
  - **200 OK**: Returns the sorted list of patients.
  - **400 Bad Request**: Invalid field or order specified.

---

### 6. **Create a New Patient**
- **URL**: `/create`
- **Method**: `POST`
- **Description**: Adds a new patient record.
- **Request Body**:
  ```json
  {
    "id": "P001",
    "name": "John Doe",
    "city": "New York",
    "age": 30,
    "gender": "male",
    "height": 1.75,
    "weight": 70
  }
  ```
- **Response**:
  - **201 Created**: Patient created successfully.
  - **400 Bad Request**: Patient with the same ID already exists.

---

### 7. **Update a Patient**
- **URL**: `/edit/{patient_id}`
- **Method**: `PUT`
- **Description**: Updates an existing patient record.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient to update.
- **Request Body**:
  ```json
  {
    "name": "Jane Doe",
    "city": "Los Angeles",
    "age": 28,
    "height": 1.65,
    "weight": 60
  }
  ```
- **Response**:
  - **200 OK**: Patient updated successfully.
  - **404 Not Found**: Patient not found.

---

### 8. **Delete a Patient**
- **URL**: `/delete/{patient_id}`
- **Method**: `DELETE`
- **Description**: Deletes a patient record.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient to delete.
- **Response**:
  - **200 OK**: Patient deleted successfully.
  - **404 Not Found**: Patient not found.


### 5. Deactivate the Virtual Environment
When you're done, deactivate the virtual environment:

```bash
deactivate
```


## CRUD Operations in the API

This API supports the following CRUD (Create, Read, Update, Delete) operations for managing patient records:

---

### 1. **Create a New Patient**
- **Endpoint**: `POST /create`
- **Description**: Adds a new patient record to the database.
- **Request Body**:
  ```json
  {
    "id": "P001",
    "name": "John Doe",
    "city": "New York",
    "age": 30,
    "gender": "male",
    "height": 1.75,
    "weight": 70
  }
  ```
- **Response**:
  - **201 Created**: Patient created successfully.
  - **400 Bad Request**: Patient with the same ID already exists.

---

### 2. **Read Patient Records**
#### a. View All Patients
- **Endpoint**: `GET /view`
- **Description**: Retrieves all patient records.
- **Response**:
  ```json
  {
    "P001": {
      "name": "John Doe",
      "city": "New York",
      "age": 30,
      "gender": "male",
      "height": 1.75,
      "weight": 70,
      "bmi": 22.86,
      "verdict": "Normal"
    }
  }
  ```

#### b. View a Specific Patient
- **Endpoint**: `GET /patient/{patient_id}`
- **Description**: Retrieves a specific patient record by ID.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient (e.g., `P001`).
- **Response**:
  - **200 OK**: Returns the patient record.
  - **404 Not Found**: Patient not found.

---

### 3. **Update a Patient**
- **Endpoint**: `PUT /edit/{patient_id}`
- **Description**: Updates an existing patient record.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient to update.
- **Request Body**:
  ```json
  {
    "name": "Jane Doe",
    "city": "Los Angeles",
    "age": 28,
    "height": 1.65,
    "weight": 60
  }
  ```
- **Response**:
  - **200 OK**: Patient updated successfully.
  - **404 Not Found**: Patient not found.

---

### 4. **Delete a Patient**
- **Endpoint**: `DELETE /delete/{patient_id}`
- **Description**: Deletes a patient record.
- **Path Parameter**:
  - `patient_id` (string): The ID of the patient to delete.
- **Response**:
  - **200 OK**: Patient deleted successfully.
  - **404 Not Found**: Patient not found.

---

### 5. **Sort**
- **Endpoint**: `GET /sort`
- **Description**: Sorts patient records by height, weight, or BMI.
- **Query Parameters**:
  - `sort_by`: The field to sort by (`height`, `weight`, or `bmi`).
  - `order`: The sort order (`asc` for ascending, `desc` for descending).
- **Response**:
  - **200 OK**: Returns the sorted list of patients.
  - **400 Bad Request**: Invalid field or order specified.

---

### Notes
- **Validation**: The API validates input data using Pydantic models.
- **Error Handling**: Returns appropriate HTTP status codes and error messages for invalid requests.
- **Data Storage**: Patient records are stored in a JSON file (`patients.json`).

---

## Common HTTP Response Status Codes

### **2xx Success**
- **200 OK**: The request was successful, and the server returned the requested data.
- **201 Created**: The request was successful, and a new resource was created.
- **202 Accepted**: The request has been accepted for processing, but the processing is not yet complete.
- **204 No Content**: The request was successful, but there is no content to return.

---

### **3xx Redirection**
- **301 Moved Permanently**: The resource has been permanently moved to a new URL.
- **302 Found**: The resource is temporarily located at a different URL.
- **304 Not Modified**: The resource has not been modified since the last request (used for caching).

---

### **4xx Client Errors**
- **400 Bad Request**: The server could not understand the request due to invalid syntax.
- **401 Unauthorized**: Authentication is required to access the resource.
- **403 Forbidden**: The client does not have permission to access the resource.
- **404 Not Found**: The requested resource could not be found on the server.
- **405 Method Not Allowed**: The HTTP method used is not allowed for the resource.
- **409 Conflict**: The request could not be completed due to a conflict with the current state of the resource.
- **422 Unprocessable Entity**: The server understands the request but cannot process it (e.g., validation errors).

---

### **5xx Server Errors**
- **500 Internal Server Error**: The server encountered an unexpected condition that prevented it from fulfilling the request.
- **501 Not Implemented**: The server does not support the functionality required to fulfill the request.
- **502 Bad Gateway**: The server received an invalid response from an upstream server.
- **503 Service Unavailable**: The server is currently unable to handle the request (e.g., maintenance or overload).
- **504 Gateway Timeout**: The server did not receive a timely response from an upstream server.

---

### Notes
- **2xx** codes indicate success.
- **3xx** codes indicate redirection.
- **4xx** codes indicate client-side errors.
- **5xx** codes indicate server-side errors.

---

# Machine learning model with FastAPI

## library required to install

```bash
pip install pandas scikit-learn
```

---

# Frontend for FastAPI

## library required to install

```bash
pip install streamlit
```

--- 

# to run the API run the below command in one of the terminal
```bash
uvicorn app:app --reload
```

# to run the app, execute below command in one of the terminal
```bash
streamlit run frontend.py
```

---