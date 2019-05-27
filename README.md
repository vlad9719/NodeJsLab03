# NodeJsLab03

This repo contains 2 packages: ```task1``` and ```task2```. 
Both of them implement similar task,
which is to provide an API for managing contracts between Renter and Stock entities. 
The folder ```task1```
contains implementation using Express and SQL.
The folder ```task2``` contains implementation using Express and ORM.

### Installing

Step 1. Clone the repo 
```
git clone https://github.com/vlad9719/NodeJsLab03

cd NodeJsLab03
```

Step 2. Go to   ```task1``` folder

```
cd task1
```

Step 3. Install dependencies
```
npm install
```

Step 4. Create database ```contracts```. You may wish to provide your database 
credentials in ```createDatabase.ts``` file
```
ts-node createDatabase.ts
```

Step 5. Add records to database. The following command can add 500 000
records, but you may stop its execution after a couple of minutes to have a couple
of thousand of records in your database.
```
ts-node seedDatabase.ts
```

Step 6. Add indices
```
ts-node addIndices
```

Step 7. Run the server

```
ts-node index.ts
```

## API in action

Use Postman for checking API's work

Step 1. Check whether server is working using ```healthcheck``` endpoint with ```GET``` request.

The endpoint's URL is as follows:

```
GET localhost:8080/api/healthcheck
```

The expected response example is as follows:
```
{
    "message": "Server is running",
    "serverStartedRunningAt": "27-4-2019",
    "serverAlreadyRuns (ms)": 2318
}
```

Step 2. Add a new contract using ```contract``` endpoint with ```POST``` request.

The endpoint's URL is as follows:

```
POST localhost:8080/api/contract/<renter_id>/<stock_id>
```

Put valid ```renter_id``` and ```stock_id``` in the URL of request, which you can find
 in database ```contracts``` you've created.
You should provide JSON body for this request with required numeric parameter ```rentalCost```.

API expects you to send it JSON body like this:

```
{
	"rentalCost": 8930
}
```

The expected response looks like this:
```
{
    "data": {
        "renter_id": 5,
        "stock_id": 3000,
        "rental_cost": 1234,
        "created_at": "2019-05-27T20:35:37.721Z"
    }
}
```


Step 3. Delete a contract you've just created with ```DELETE``` HTTP method.

The endpoint's URL is as follows:

```
DELETE localhost:8080/contract/<renter_id>/<stock_id>
```

Put valid ```renter_id``` and ```stock_id``` in the URL of request, which you can find
 in database ```contracts``` you've created.


The expected response looks like this:
```
{
    "data": {
        "deletedContract": {
            "renter_id": 5,
            "stock_id": 3000,
            "rental_cost": 1234,
            "created_at": "2019-05-27"
        }
    }
}
```

Step 4. View all stocks rented by a particular renter with ```GET``` method.

The endpoint's URL is as follows:

```
GET localhost:8080/api/stocks/<renter_id>
```
Put a valid ```renter_id``` in the URL of request, which you can find
 in database ```contracts``` you've created.


The expected response looks like this:
```
{
    "data": [
        {
            "contracts": [
                {
                    "createdAt": "2019-05-25",
                    "stockName": "Stock 5",
                    "rentalCost": 6798.3
                }
            ]
        },
        {
            "total": 6798.3
        }
    ]
}
```

Step 5. View all renters that rented a particular stock using ```renters``` endpoint
and ```GET``` method

The endpoint's URL is as follows:

```
GET localhost:8080/api/renters/<stock_id>
```
Put a valid ```stock_id``` in the URL of request, which you can find
 in database ```contracts``` you've created.


The expected response looks like this:
```
{
    "data": [
        {
            "contracts": [
                {
                    "createdAt": "2019-05-25",
                    "stockName": "Stock 5",
                    "rentalCost": 6798.3
                },
                {
                    "createdAt": "2019-05-27",
                    "stockName": "Stock 6000",
                    "rentalCost": 1234
                }
            ]
        },
        {
            "total": 8032.3
        }
    ]
}
```

Step 6. Check average response time for ```GET```ting 10000 records
using ```time-report``` endpoint.

The endpoint's URL is as follows:

```
GET localhost:8080/api/time-report
```

The expected response looks like this:
```
{
    "data": {
        "averageRequestTime (ms)": 71.719
    }
}
```

###Checking task2

You may now stop the server, go to directory task2 and start the server, that
uses Sequelize for the API:
```
cd ..
cd task2
ts-node index.ts
```

You can check this API work in the similar way that you checked API
built in ```task1```.