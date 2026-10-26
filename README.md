# MyPrescription

**Digital prescriptions with security built in.** A doctor issues a prescription, the patient shows a single-use code (or QR code) at the pharmacy, and the pharmacist marks the drug as delivered. Everyone sees only what they need.

University project on secure digital healthcare, 2022–2023, built by two people: [Davide Albiero](https://github.com/Edivad99) and Matteo Tossuto.

## How it works

1. The **doctor** creates a prescription for one of their patients.
2. The **patient** gets a notification and sees it in their dashboard, together with a single-use code (and QR code). They can regenerate it at any time.
3. The **pharmacist** scans the QR code or types the code, sees only the drug name, the exemption and the creation date, and marks the prescription as delivered.
4. The **patient** is notified as soon as the drug has been delivered.

## Security

| Requirement | What we did |
|---|---|
| Data in transit | All traffic over HTTPS |
| Passwords | Stored hashed in the database, never in clear text |
| Authentication | Email and password, plus a **2FA code** (enabled by default) |
| Authorization | JWT tokens; each role (doctor, patient, pharmacist) can reach only its own pages and data |
| Least privilege | The pharmacist sees only what is needed to deliver the drug |

## Tech stack

- **Client:** Blazor WebAssembly (C#, Razor), QR code generation and scanning
- **Server:** ASP.NET Core Web API (C#), JWT authentication, notification service
- **Database:** MySQL (schema in [`database.sql`](database.sql))

```
MyPrescription.Client   Blazor UI, pages split by role (Doctor, Patient, Pharmacist)
MyPrescription.Server   REST API: auth, doctors, patients, prescriptions, notifications
MyPrescription.Data     Entities and repositories
MyPrescription.Common   DTOs and models shared by client and server
```

## Run it locally

1. Create the database by running `database.sql` on a MySQL instance.
2. Set the connection string and JWT settings in the server's `appsettings.json`.
3. Start `MyPrescription.Server`, then `MyPrescription.Client`, from Visual Studio or with `dotnet run`.

The full feature list is in [`Features.md`](Features.md).
