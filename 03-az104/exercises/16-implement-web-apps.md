# Exercise 16 Implement Web Apps
- Learning path 4. Deploy and manage Azure compute resources
- Module: 3. Configure Azure App Service

---

## Task 1 Web app aanmaken en configureren

Uitgevoerd via **Azure portal > App Services > + Create > Web App**

| Setting | Value |
|---|---|
| Resource group | groupex16 (nieuw) |
| Web app name | 16ename |
| Publish | Code |
| Runtime stack | PHP 8.2 |
| Operating system | Linux |
| Region | West Europe |
| Pricing plan | Premium V3 P1V3 |

---

## Task 2 Deployment slot aanmaken

Uitgevoerd via **Web App > Deployment > Deployment slots > Add slot**

| Setting | Value |
|---|---|
| Name | staging |
| Clone settings from | Do not clone settings |

---

## Task 3 Web app deployment settings configureren

Uitgevoerd via **Staging slot > Deployment Center > Settings**

| Setting | Value |
|---|---|
| Source | External Git |
| Repository | https://github.com/Azure-Samples/php-docs-hello-world |
| Branch | master |

Staging slot URL getest — Hello World zichtbaar.

---

## Task 4 Deployment slots swappen

Uitgevoerd via **Deployment slots > Swap**

Na de swap toont de productie slot de Hello World pagina.

---

## Task 5 Autoscaling configureren en testen

Uitgevoerd via **App Service plan > Scale out > Automatic**

| Setting | Value |
|---|---|
| Scaling mode | Automatic |
| Maximum burst | 2 |

Load test aangemaakt en uitgevoerd via **Diagnose and solve problems > Load Test**.

---

## Task 6 Clean up

Resource group `groupex16` verwijderd.

---
