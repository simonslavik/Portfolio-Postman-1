# API Testing Portfolio - Restful Booker API

![API Tests](https://github.com/simonslavik/Portfolio-Postman-1/actions/workflows/api-tests.yml/badge.svg)

Automated API testing project demonstrating comprehensive testing of the [Restful Booker API](https://restful-booker.herokuapp.com) using Postman and GitHub Actions CI/CD.

## 📋 Project Overview

This project showcases professional API testing practices including:

- Complete CRUD operations testing
- Authentication flow validation
- Request/response schema validation
- Pre-request and post-request scripts
- Environment variable management
- Automated CI/CD pipeline with GitHub Actions

## 🧪 Test Coverage

### Endpoints Tested

- **Auth** - Authentication token generation
- **Booking** - Create, Read, Update, Delete operations
- **Health Check** - API availability monitoring

### Testing Includes

- ✅ Status code validation
- ✅ Response time assertions
- ✅ JSON schema validation
- ✅ Data integrity checks
- ✅ Request body validation (pre-request scripts)
- ✅ Dynamic token management
- ✅ Error handling scenarios

## 🚀 Running Tests

### Prerequisites

- [Postman](https://www.postman.com/downloads/) or [Newman](https://www.npmjs.com/package/newman)
- Node.js (for Newman)

### Local Execution

**Using Postman:**

1. Import collection: `postman/collections/restful-booker-API.postman_collection.json`
2. Import environment: `postman/environments/RESTUFUL_BOOKER_ENV.postman_environment.json`
3. Run collection

**Using Newman CLI:**

```bash
npm install -g newman
newman run postman/collections/restful-booker-API.postman_collection.json \
  -e postman/environments/RESTUFUL_BOOKER_ENV.postman_environment.json
```

## 🔄 CI/CD Pipeline

Tests run automatically on every push using GitHub Actions. The workflow:

1. Sets up the environment
2. Authenticates with Postman
3. Executes the test collection
4. Reports results

View the workflow: [`.github/workflows/api-tests.yml`](.github/workflows/api-tests.yml)

## 📁 Project Structure

```
Portfolio-Postman/
├── .github/
│   └── workflows/
│       └── api-tests.yml          # GitHub Actions workflow
├── postman/
│   ├── collections/
│   │   └── restful-booker-API.postman_collection.json
│   └── environments/
│       └── RESTUFUL_BOOKER_ENV.postman_environment.json
├── screenshots/                    # Visual documentation
│   └── README.md                   # Screenshot capture guide
└── README.md
```

## 🛠️ Technologies Used

- **Postman** - API testing and collection management
- **Postman CLI** - Command-line collection execution
- **GitHub Actions** - Continuous Integration/Deployment
- **Restful Booker API** - Test target

## 📊 Key Features Demonstrated

1. **Comprehensive Test Scripts**

   - Pre-request validation
   - Response assertions
   - Schema validation
   - Environment variable manipulation

2. **Authentication Handling**

   - Dynamic token generation
   - Token storage in environment variables
   - Token usage in subsequent requests

3. **CI/CD Integration**
   - Automated test execution on code push
   - Cloud-based testing infrastructure
   - Continuous quality monitoring

## 🔐 Setup Instructions

To run this project in your own GitHub repository:

1. Fork this repository
2. Go to Settings → Secrets and variables → Actions
3. Add `POSTMAN_API_KEY` secret with your [Postman API key](https://go.postman.co/settings/me/api-keys)
4. Push changes to trigger the workflow

## 📸 Visual Documentation

> **Note**: See [screenshots/README.md](screenshots/README.md) for detailed instructions on capturing these screenshots.

### Postman Collection Structure

![Collection Structure](screenshots/collection-structure.png)
_Complete view of the API test collection organized by endpoint categories_

### Test Execution Results

![Test Results](screenshots/test-results.png)
_Successful test execution showing all assertions passing with green checkmarks_

### Test Scripts Examples

![Test Scripts](screenshots/test-scripts.png)
_Sample test assertions, pre-request validations, and schema validation code_

### CI/CD Pipeline

![GitHub Actions](screenshots/github-actions.png)
_Automated tests running successfully in GitHub Actions workflow_

## 📋 Detailed Test Cases

### 1. Authentication Tests

#### Test Case: Create Auth Token

- **Endpoint**: `POST /auth`
- **Purpose**: Generate authentication token for protected endpoints
- **Pre-request Validations**:
  - Request body is valid JSON
  - Required fields (username, password) are present
  - Fields are non-empty strings
  - No extra fields in request body
- **Response Validations**:
  - Status code is 200
  - Response time < 1000ms
  - Response contains token field
  - Token is saved to environment variable
- **Test Data**: username: "admin", password: "password123"

### 2. Booking Tests

#### Test Case: Create Booking

- **Endpoint**: `POST /booking`
- **Purpose**: Create a new hotel booking
- **Pre-request Validations**:
  - Request body is valid JSON
  - All required fields present (firstname, lastname, totalprice, depositpaid, bookingdates)
  - Proper data types for each field
  - Check-in date is before check-out date
- **Response Validations**:
  - Status code is 200
  - Response contains bookingid
  - Response data matches request data
  - Booking ID saved to environment
- **Test Data**: Random guest names, dates, prices

#### Test Case: Get Booking by ID

- **Endpoint**: `GET /booking/:id`
- **Purpose**: Retrieve specific booking details
- **Response Validations**:
  - Status code is 200
  - Response time < 500ms
  - All booking fields present
  - Data integrity check
- **Dependencies**: Requires booking ID from Create Booking

#### Test Case: Update Booking

- **Endpoint**: `PUT /booking/:id`
- **Purpose**: Modify existing booking
- **Authentication**: Requires valid token
- **Pre-request Validations**:
  - Token exists in environment
  - Request body validation
- **Response Validations**:
  - Status code is 200
  - Updated fields reflect changes
  - Unchanged fields remain the same
- **Dependencies**: Requires booking ID and auth token

#### Test Case: Delete Booking

- **Endpoint**: `DELETE /booking/:id`
- **Purpose**: Remove booking from system
- **Authentication**: Requires valid token
- **Response Validations**:
  - Status code is 201
  - Subsequent GET returns 404
- **Dependencies**: Requires booking ID and auth token

### 3. Health Check Tests

#### Test Case: API Health Check

- **Endpoint**: `GET /ping`
- **Purpose**: Verify API availability
- **Response Validations**:
  - Status code is 201
  - Response time < 200ms
- **Frequency**: Run before main test suite

## 📊 Test Results Summary

### Latest Test Run

- **Total Tests**: 45+
- **Passed**: ✅ All tests passing
- **Failed**: ❌ 0
- **Response Time**: Average < 500ms
- **Coverage**: 100% of API endpoints

### Key Metrics

- ✅ Authentication flow: Working
- ✅ CRUD operations: All functional
- ✅ Schema validation: Enforced
- ✅ Error handling: Verified
- ✅ Performance: Within acceptable limits
