Please take referece from below code for the class diagram:
```mermaid
classDiagram
    %% Define Interfaces
    class AuthService {
        <<interface>>
        +login(username: String, password: String): Boolean
        +logout(): void
    }

    class PaymentGateway {
        <<interface>>
        +processPayment(amount: Float): Boolean
    }

    %% Define Classes
    class User {
        <<abstract>>
        +String username
        +String email
        +String password
        +login()
        +logout()
    }

    class Admin {
        +manageUsers()
        +viewReports()
    }

    class Customer {
        +String name
        +String address
        +placeOrder()
        +trackOrder()
    }

    class Order {
        +int orderId
        +Date orderDate
        +float totalAmount
        +calculateTotal()
        +updateStatus()
    }

    class Product {
        +String name
        +float price
        +int stock
        +updateStock()
    }

    class Payment {
        +String method
        +float amount
        +Date paymentDate
        +processPayment()
    }

    class DeliveryStatus {
        +String status
        +Date lastUpdate
        +updateStatus()
    }

    %% Define Relationships
    User <|-- Admin
    User <|-- Customer
    Admin ..|> AuthService : implements
    Customer ..|> AuthService : implements
    Customer "1" --> "*" Order : places
    Order "*" --> "1" Payment : includes
    Order "*" --> "*" Product : contains
    Order "*" --> "1" DeliveryStatus : has
    Admin ..> Customer : manages
    Customer --> Payment : makes
    Customer --> Order : places
    Customer --> Product : views

    %% Define Styles
    classDef User fill:#f9f,stroke:#333,stroke-width:2px;
    classDef Admin fill:#ccf,stroke:#333,stroke-width:2px;
    classDef Customer fill:#cfc,stroke:#333,stroke-width:2px;
    classDef Order fill:#fcf,stroke:#333,stroke-width:2px;
    classDef Product fill:#cff,stroke:#333,stroke-width:2px;
    classDef Payment fill:#ffc,stroke:#333,stroke-width:2px;
    classDef DeliveryStatus fill:#fcc,stroke:#333,stroke-width:2px;
    classDef AuthService fill:#cfc,stroke:#333,stroke-width:2px;
    classDef PaymentGateway fill:#cff,stroke:#333,stroke-width:2px;

    %% Add Notes
    note for User "Abstract class representing a system user."
    note for Admin "Class implementing AuthService interface for admin-specific authentication."
    note for Customer "Class implementing AuthService interface for customer-specific authentication."
    note for Order "Class representing an order placed by a customer."
    note for Product "Class representing a product available for purchase."
    note for Payment "Class handling payment transactions for orders."
    note for DeliveryStatus "Class tracking the delivery status of orders."
    note for AuthService "Interface defining authentication operations."
    note for PaymentGateway "Interface defining payment processing operations."

    %% Add Annotations
    class User {
        <<abstract>>
    }
    class Admin {
        <<interface>>
    }
    class Customer {
        <<service>>
    }
    class Order {
        <<entity>>
    }
    class Product {
        <<entity>>
    }
    class Payment {
        <<entity>>
    }
    class DeliveryStatus {
        <<entity>>
    }
    class AuthService {
        <<interface>>
    }
    class PaymentGateway {
        <<interface>>
    }

    %% Set Diagram Direction
    direction TB
	


Please take referece from below code for the sequence diagram:
```mermaid
sequenceDiagram
    participant User
    participant WebApp
    participant AuthService
    participant Database
    participant OrderService
    participant PaymentGateway

    %% User initiates login
    User->>WebApp: Enter credentials
    WebApp->>AuthService: Validate credentials
    activate AuthService
    AuthService->>Database: Query user data
    Database-->>AuthService: Return user data
    deactivate AuthService

    alt Valid credentials
        AuthService-->>WebApp: Authentication success
        WebApp-->>User: Redirect to dashboard
    else Invalid credentials
        AuthService-->>WebApp: Authentication failed
        WebApp-->>User: Show error message
    end

    %% User places an order
    User->>WebApp: Add items to cart
    WebApp->>OrderService: Create order
    activate OrderService
    OrderService->>Database: Save order details
    Database-->>OrderService: Order saved
    deactivate OrderService

    %% User proceeds to payment
    User->>WebApp: Checkout
    WebApp->>PaymentGateway: Process payment
    activate PaymentGateway
    PaymentGateway->>PaymentGateway: Validate payment details
    PaymentGateway-->>WebApp: Payment processed
    deactivate PaymentGateway

    %% Final confirmation
    WebApp-->>User: Order confirmed


C4: diagram reference

    C4Context
      title System Context diagram for Internet Banking System
      Enterprise_Boundary(b0, "BankBoundary0") {
        Person(customerA, "Banking Customer A", "A customer of the bank, with personal bank accounts.")
        Person(customerB, "Banking Customer B")
        Person_Ext(customerC, "Banking Customer C", "desc")

        Person(customerD, "Banking Customer D", "A customer of the bank, <br/> with personal bank accounts.")

        System(SystemAA, "Internet Banking System", "Allows customers to view information about their bank accounts, and make payments.")

        Enterprise_Boundary(b1, "BankBoundary") {

          SystemDb_Ext(SystemE, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc.")

          System_Boundary(b2, "BankBoundary2") {
            System(SystemA, "Banking System A")
            System(SystemB, "Banking System B", "A system of the bank, with personal bank accounts. next line.")
          }

          System_Ext(SystemC, "E-mail system", "The internal Microsoft Exchange e-mail system.")
          SystemDb(SystemD, "Banking System D Database", "A system of the bank, with personal bank accounts.")

          Boundary(b3, "BankBoundary3", "boundary") {
            SystemQueue(SystemF, "Banking System F Queue", "A system of the bank.")
            SystemQueue_Ext(SystemG, "Banking System G Queue", "A system of the bank, with personal bank accounts.")
          }
        }
      }

      BiRel(customerA, SystemAA, "Uses")
      BiRel(SystemAA, SystemE, "Uses")
      Rel(SystemAA, SystemC, "Sends e-mails", "SMTP")
      Rel(SystemC, customerA, "Sends e-mails to")

      UpdateElementStyle(customerA, $fontColor="red", $bgColor="grey", $borderColor="red")
      UpdateRelStyle(customerA, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
      UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
      UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
      UpdateRelStyle(SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")

      UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")





