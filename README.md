# BambangShop Publisher App
Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

---

## About this Project
In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

This project consists of four modules:
1.  `controller`: this module contains handler functions used to receive request and send responses.
    In Model-View-Controller (MVC) pattern, this is the Controller part.
2.  `model`: this module contains structs that serve as data containers.
    In MVC pattern, this is the Model part.
3.  `service`: this module contains structs with business logic methods.
    In MVC pattern, this is also the Model part.
4.  `repository`: this module contains structs that serve as databases and methods to access the databases.
    You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.
This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.
This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.
The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

## API Documentations

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.
This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

Postman is an installable client that you can use to test web endpoints using HTTP request.
You can also make automated functional testing scripts for REST API projects using this client.
You can install Postman via this website: https://www.postman.com/downloads/

## How to Run in Development Environment
1.  Set up environment variables first by creating `.env` file.
    Here is the example of `.env` file:
    ```bash
    APP_INSTANCE_ROOT_URL="http://localhost:8000"
    ```
    Here are the details of each environment variable:
    | variable              | type   | description                                                |
    |-----------------------|--------|------------------------------------------------------------|
    | APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |
2.  Use `cargo run` to run this app.
    (You might want to use `cargo check` if you only need to verify your work without running the app.)

## Mandatory Checklists (Publisher)
-   [X] Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.
-   **STAGE 1: Implement models and repositories**
    -   [X] Commit: `Create Subscriber model struct.`
    -   [X] Commit: `Create Notification model struct.`
    -   [X] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`
    -   [X] Commit: `Implement add function in Subscriber repository.`
    -   [X] Commit: `Implement list_all function in Subscriber repository.`
    -   [X] Commit: `Implement delete function in Subscriber repository.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-1" questions in this README.
-   **STAGE 2: Implement services and controllers**
    -   [X] Commit: `Create Notification service struct skeleton.`
    -   [X] Commit: `Implement subscribe function in Notification service.`
    -   [X] Commit: `Implement subscribe function in Notification controller.`
    -   [X] Commit: `Implement unsubscribe function in Notification service.`
    -   [X] Commit: `Implement unsubscribe function in Notification controller.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-2" questions in this README.
-   **STAGE 3: Implement notification mechanism**
    -   [X] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`
    -   [X] Commit: `Implement notify function in Notification service to notify each Subscriber.`
    -   [X] Commit: `Implement publish function in Program service and Program controller.`
    -   [X] Commit: `Edit Product service methods to call notify after create/delete.`
    -   [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

## Your Reflections
This is the place for you to write reflections:

### Mandatory (Publisher) Reflections

#### Reflection Publisher-1

1. Sebenarnya, penggunaan single modle struct memang bisa jadi cukup untuk digunakan. Akan tetapi, penggunaan interface atau trait dalam desain observer memberikan keunggulan dibanding penggunaan single model struct. Di antara keunggulan tersebut adalah dekopling, menunjang fleksibilitas, dan mendukung polimorfisme. Dengan demikian, pengguna interface masih dibutuhkan untuk menghasilkan kode dengan kualitas yang lebih baik. Dengan menerapkan interface atau trait, diharapkan kode akan lebih bersih, terorganisir, dan mudah diadaptasi pada kebutuhan mendatang.
   
2. Penggunaan vec mungkin memiliki keunggulan berupa implementasinya yang sederhana. Akan tetapi, Dashmap lebih unggul untuk kasus ini karena dashmap memberikan akses yang lebih cepat, menjamin keunikan secara otomatis, dan memberikan kemudahan dalam mengelola seperti menghapus dan menambah data. Dengan demikian, dalam kasus ini vec mungkin saja digunakan, tetapi Dashmap akan memberikan keuntungan yang signifikan. Oleh karena itu, menurut saya, tetap diperlukan Dashmap dalam implementasi kasus ini.

3. Singleton pettern memiliki tujuan untuk memastikan bahwa sebuah kelas memiliki satu instansi saja dan menyediakan titik akses global ke instansi tersebut, sedangkan dashmap bekerja dengan keunggulan concurrent acces dan thread safety. Implementasi yang optimal adalah dengan menggunakan dashmap dalam konteks singleton. Dengan kata lain, menggabungkan keduanya alih-alih memilih salah satu. Dengan melakukan hal tersebut, Dashmap akan memberikan thread-safety yang efisien untuk operasi map, sedangkan singleton akan memastikan bahwa hanya ada instans Dashmap yang diakses secara global.

#### Reflection Publisher-2

1. Pemisahan antara `Service` dan `Repository` sejatinya diperlukan untuk menghasilkan program yang bersih, terstruktur, dan memiliki maintainability yang baik. Dengan memisahkan keduanya, kita mendapatkan keuntungan berupa penerapan SRP, memberikan kohesi yang lebih tinggi, menunjang testability, menghasilkan program yang lebih fleksibel, dan membuat program menjadi reusable. Dengan demikian, pemisahan tersebut penting untuk menghasilkan program dengan kualitas yang lebih baik

#### Reflection Publisher-3
