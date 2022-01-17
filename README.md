# My Bank App

## Step 1: CustomerService

Create a microservice (CustomerService) which will be responsible for handling the customer data and will expose the following endpoints:

### Create Customer Endpoint

**Endpoint**: POST /api/customer

**Body**: 
```json
{
    "firstName": "John",
    "lastName": "Doe",
    "birthdate": "1992-07-20",
    "nationality": "Brazil",
    "document": {
        "type": "passport | id",
        "number": "FG123345BR"
    },	
    "addresses": [
        {
            "type": "delivery | billing",
            "postCode": "38401293",
            "address": "Rua das Oliveiras",
            "number": "123",
            "complement": "Optional"
        }
    ]
}
```

This endpoint should validate customer data, save the customer into the database and finally publishes an event into kafka (CustomerCreatedEvent) with the following data:

CustomerCreatedEvent
```json
{
    "customerId": "cfb45ec7-f6f8-408b-8115-68d8c7fadbea"
}
```

If everything works correctly, the endpoint should return the HTTP status  `201 (Created)`

### Get Customer By ID Endpoint

**Endpoint**: GET /api/customer/{customerId}

This endpoint should look for the customer with given id into the database and return the data following the format below. The endpoint should return the HTTP status `200 OK` if the customer is found or `404 NOT FOUND` otherwise.

```json
{
    "id": "cfb45ec7-f6f8-408b-8115-68d8c7fadbea"
    "firstName": "John",
    "lastName": "Doe",
    "birthdate": "1992-07-20",
    "nationality": "Brazil",
    "document": {
        "type": "passport",
        "number": "FG123345BR"
    },	
    "addresses": [
        {
            "id": "9a1673df-c929-416b-b6fc-ed44b2942c41"
            "type": "delivery | billing",
            "postCode": "38401293",
            "address": "Rua das Oliveiras",
	    "number": "123",
	    "complement": "Optional"
	}
    ]
}
```


