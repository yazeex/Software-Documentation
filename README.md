# Online Banking System User Manual

## Introduction
The TMT Banking System is a straightforward, user-friendly software designed to facilitate
basic banking operations. It aims to enhance customers’ experience by offering
essential financial services efficiently and securely. With intuitive navigation and a focus
on simplicity, the TMT system provides access to fundamental banking functionalities
while maintaining data security and convenience

## System Architecture
The TMT Banking System is designed as a client-server architecture, facilitating online banking operations. It is divided into multiple layers, ensuring scalability, security, and performance. Here’s a breakdown of the system architecture:

### Main Components

1. **Login and Registration**: Allows customers to create new accounts and access
existing ones securely.

3. **Transfers**: Supports intra-system fund transfers for seamless transactions.

5. **Deposit and Withdrawal**: Users can manage their finances by depositing or
withdrawing funds conveniently.
 
7. **View Balance**: Offers real-time updates on account balances.
 
9. **Change PIN**: change Personal Identification Numbers
(PIN) to ensure security.

11. **Profile edit**: Displays a customer list with essential details such as
name, account type, and contact information.



### System Flow Example: Login Process
1. **Client Layer**: The user inputs their account number and PIN on the login screen.

2. **Application Layer**: The credentials are sent to the application layer, where they are verified against the database.

3. **Data Access Layer**:A query is executed to match the credentials with the stored user data in the database.

4. **Application Layer**: If valid, a session is initiated for the user, and they are granted access. If invalid, an error message is returned.

5. **Client Layer**:The result (success or error) is displayed to the user.



---


## Core Components and Modules

### 1.**Login**
- **Description**:Authenticates a user by checking their account number and PIN.
- **Endpoint**: `/api/login`
- **Method**: `POST`
- **Request**:
    - **Headers**:
      - `Content-Type: application/json`
- **Body**:
  ```java
  {
  "accountNumber": "string",
  "pin": "string"
  ]

 
- **Response**:
  - **Success (200)**:
    
```java
{
  "message": "Login successful",
  "token": "JWT Token"
]
```


- **Error (401)**"
  ```java
  {
  "error": "Invalid credentials",
  "message": "Incorrect account number or pin"
  ]
  ```

   - **Error (500)**:

  ```java
  {
  "error": "Server error",
  "message": "An internal error occurred"
  }
  ```

### 2.**Registration**
- **Description**:Creates a new account by registering a user with the required details
- **Endpoint**: `/api/register`
- **Method**: `POST`
- **Request**:
  - **Headers**:
    - `Content-Type: application/json`
- **Body:**

```java
{
  "name": "string",
  "dob": "YYYY-MM-DD",
  "pin": "string",
  "accountType": "string",
  "ethnicity": "string",
  "gender": "string",
  "mobile": "string",
  "address": "string",
  "securityQuestion": "string",
  "securityAnswer": "string",
  "initialDeposit": "number"
}

```
- **Success (201):**
  ```java
  {
  "accountNumber": "string",
  "message": "Account created successfully"
  }
  ```
  - **Error (400):**
    
   ```java
   {
  "error": "Validation error",
  "message": "Missing or invalid parameters"
   }





### 3.**Transfers**
- **Description**:Transfers a specified amount between accounts.
- **Endpoint:** `/api/transfer`
- **Method:** `POST`
- **Request:**
  - **Headers:**
     - `Authorization: Bearer token`
     - `Content-Type: application/json`
- **Body:**<br>

```java
{
  "fromAccountNumber": "string",
  "toAccountNumber": "string",
  "amount": "number"
}

```
- **Response:**
- **Success (200):**
```java
{
  "message": "Transfer successful",
  "newBalance": "number"
}
```
- **Error (400):**
```java
{
  "error": "Insufficient balance",
  "message": "Transfer amount exceeds available balance"
}
```
### 4.**Deposit**
- **Description**:Deposits a specified amount into the user's account.
  - **Endpoint:** `/api/deposit`
- **Method:** `POST`
- **Request**:
  - **Headers:**
   - `Authorization: Bearer token`
   - `Content-Type: application/json`
 
- **Body:**
  
```java
{
  "accountNumber": "string",
  "amount": "number"
}
```
- **Response:**
- **Success (200):**
```java
{
  "message": "Deposit successful",
  "newBalance": "number"
}
```
- **Error (400):**
```java
{
  "error": "Invalid deposit amount",
  "message": "Amount cannot be negative"
}
```
  


### 5.**Withdrawal**
- **Description**:Withdraws a specified amount from the user's account.
- **Endpoint**: `/api/withdraw`
- **Method**: `POST`
- **Request:**
 - **Headers:**
    - ` Authorization: Bearer token`
   - ` Content-Type: application/json`
 -  **Body:**
```java
{
  "accountNumber": "string",
  "amount": "number"
}
```
- **Response:**
   - **Success (200):**
 ```java
{
  "message": "Withdrawal successful",
  "newBalance": "number"
}
```
- **Error (400):**
```java
{
  "error": "Insufficient balance",
  "message": "Withdrawal amount exceeds available balance"
}
``` 


### 6.**View Balance**
- **Description**: Retrieves the balance of a specified account.
- **Endpoint**: `/api/balance`
- **Method**: `GET`
- **Request:**
 - **Headers:**
    - `Authorization: Bearer token`
  - **Query Parameters:**
    - `accountNumber`: The account number of the user.
  - **Response:**
  - **Success (200):**
 
```java
{
  "balance": "number",
  "accountNumber": "string"
}
```
- **Error (404):**
```java
{
  "error": "Account not found",
  "message": "No account exists with this number"
}
```

### 7.**Change PIN**
- **Description**:Changes the account's PIN for security purposes.
- **Endpoint**: `/api/changePIN`
- **Method**: `PUT`
- **Request:**
  - **Headers:**
     - `Authorization: Bearer token`
     - `Content-Type: application/json`
- **Body:**
```java
{
  "accountNumber": "string",
  "oldPIN": "string",
  "newPIN": "string"
}
```
- **Response:**
- **Success (200):**
```java
{
  "message": "PIN changed successfully"
}
```
- **Error (400):**
```java
{
  "error": "Invalid PIN",
  "message": "Old PIN is incorrect"
}
```


### 8.**Profile Edit**
- **Description**:Edits and updates the profile details of the user.
- **Endpoint**: `/api/editProfile`
- **Method**: `PUT`
- **Request:**
  - **Headers:**
     - `Authorization: Bearer token`
     - `Content-Type: application/json`
- **Body:**

```java
{
  "accountNumber": "string",
  "name": "string",
  "address": "string",
  "mobile": "string",
  "ethnicity": "string",
  "gender": "string",
  "dob": "YYYY-MM-DD"
}
```
- **Response:**
- **Success (200):**
```java
{
  "message": "Profile updated successfully"
}
```
- **Error (404):**
```java
{
  "error": "Account not found",
  "message": "No account found with this number"
}
```


This repo is for the  UQU software documentation course.
