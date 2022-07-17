1. Microservice architecture: Each functionality is deployed separately with an API. Being database-centric and having the need for distributed systems (multiple hotels) are the main reasons for choosing this architecture.
2. Each API call represents a business case (making a reservation for example).
3. Each API call is composed as follows:
	1. Data fetching: Data objects are read from the database or other sources.
	2. Precondition: Conditions that may prevent the action are checked (no license for example).
	3. Actions: Data modifications and additional inquiries are collected in a queue and used to modify data objects.
	4. Postcondition: Data objects are checked for correctness and consistency (no free room for example).
	5. Commit: Data objects are written to databases and external systems.
4. Data objects are passed through each step until the end of the API call.
5. Concurrency issues must be dealt with before committing.
6. During API calls, further input may be required. In this case, the API call result would be “additional info required” and a new API call with the required information should be sent to continue. For example: when creating a reservation, the user may be asked whether they wish to upgrade or not.