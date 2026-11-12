# Restful Booker API Tests

![API Tests](https://github.com/burakcilbir/restful-booker-api-tests/actions/workflows/api-tests.yml/badge.svg)

Functional API test suite for [Restful Booker](https://restful-booker.herokuapp.com/apidoc/index.html), a public practice API for hotel bookings. Built with **Postman** and run from the command line with **Newman**, with tests running automatically on **GitHub Actions**.

## What Is Tested

| Area | Scenario | Check |
|---|---|---|
| Health | API is up | `201` |
| Auth | Create token with valid credentials | Token returned and saved for later requests |
| Auth | Create token with wrong password | No token, `Bad credentials` |
| Booking | Create booking | `200`, **JSON schema validation**, saved data matches the request |
| Booking | Get booking by id | Returns the created booking |
| Booking | Search bookings by name | Results include the created booking |
| Booking | Full update (PUT) with token | All fields updated |
| Booking | Partial update (PATCH) with token | Only the sent field changes |
| Booking | Update without token | Rejected with `403` |
| Booking | Delete booking | `201` |
| Booking | Get deleted booking | `404` |

Every request also checks that the **response time is under 3 seconds**.

## Highlights

- **Request chaining:** the token and booking id from earlier responses are stored in collection variables and reused by later requests.
- **Random test data:** each run creates a booking with a new random name and price, so runs don't depend on each other.
- **Positive and negative tests:** happy path plus wrong credentials, missing token and deleted resources.
- **CI:** runs on every push and every Monday, and uploads an HTML report as a build artifact.

## Running the Tests

Requirements: Node.js 18+

```bash
npm install
npm test
```

An HTML report is generated at `reports/report.html`.

You can also import `restful-booker.postman_collection.json` into Postman and run it with the Collection Runner.
