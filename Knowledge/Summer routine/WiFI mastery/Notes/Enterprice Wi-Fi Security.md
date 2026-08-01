# Enterprise Wi-Fi Security

## **802.1X**

**802.1X** is a **network access control** standard. It makes sure that only **authorized users or devices** can connect to a network.

### **Flow**

1. A device tries to connect to the **Wi-Fi network**.
2. The **Access Point (AP)** blocks normal network access.
3. The AP asks the device to **authenticate**.
4. The device sends its identity using an **EAP** method.
5. The AP forwards the authentication request to the **RADIUS server**.
6. If the authentication is successful, the AP **allows network access**.
7. If authentication fails, access is **denied**.

> **802.1X controls who is allowed to enter the network.**

---

## **EAP (Extensible Authentication Protocol)**

**EAP** is an **authentication framework**. It does not authenticate users by itself. Instead, it provides **different authentication methods**, such as **EAP-TLS** and **PEAP**.

### **Flow**

1. The device starts the authentication process.
2. The server chooses an **EAP method**.
3. The device and server exchange authentication messages.
4. The selected EAP method verifies the user's identity.
5. The server returns **Success** or **Failure**.

> **EAP is the set of rules used during authentication.**

---

## **EAP-TLS**

**EAP-TLS** uses **digital certificates** to prove the identity of both the **client** and the **server**. It provides **mutual authentication**, making it one of the most secure methods.

### **Flow**

1. The client connects to the Wi-Fi network.
2. The server sends its **digital certificate**.
3. The client verifies that the server certificate is trusted.
4. The client sends its own **digital certificate**.
5. The server verifies the client's certificate.
6. If both certificates are valid, a **secure encrypted session** is created.
7. The RADIUS server approves the connection.
8. The AP allows access to the network.

> **Both the client and the server prove their identities using certificates.**

---

## **PEAP (Protected EAP)**

**PEAP** creates an **encrypted TLS tunnel** before sending the user's login information. Usually, only the **server** needs a certificate.

### **Flow**

1. The client connects to the Wi-Fi network.
2. The server sends its **certificate**.
3. The client verifies the server certificate.
4. A **secure TLS tunnel** is created.
5. Inside the encrypted tunnel, the client sends its **username and password**.
6. The server verifies the credentials.
7. If they are correct, the RADIUS server approves access.
8. The AP allows the client onto the network.

> **Only the server uses a certificate. The user's password is protected inside the encrypted tunnel.**

---

## **RADIUS (Remote Authentication Dial-In User Service)**

**RADIUS** is an **authentication server**. It stores or checks user credentials and decides whether a device can access the network.

### **Flow**

1. The client tries to connect.
2. The AP receives the authentication request.
3. The AP forwards the request to the **RADIUS server**.
4. The RADIUS server performs the selected **EAP authentication method**.
5. The server checks the user's credentials or certificates.
6. The RADIUS server sends **Access-Accept** or **Access-Reject** to the AP.
7. The AP either allows or blocks network access.

> **RADIUS makes the final decision about whether the user can join the network.**

---

# **Complete Enterprise Wi-Fi Authentication Flow**

1. The **client** connects to the **Access Point (AP)**.
2. The AP starts **802.1X authentication**.
3. The client and the **RADIUS server** communicate using **EAP**.
4. The chosen EAP method (**EAP-TLS** or **PEAP**) verifies the user's identity.
5. The **RADIUS server** sends **Access-Accept** or **Access-Reject**.
6. The AP either **grants** or **denies** access to the network.

### **Remember**

- **802.1X** = Controls access to the network.
- **EAP** = Authentication framework.
- **EAP-TLS** = Uses **client and server certificates**.
- **PEAP** = Uses a **server certificate** and protects the **username/password** inside a TLS tunnel.
- **RADIUS** = Authentication server that makes the final access decision.

---
