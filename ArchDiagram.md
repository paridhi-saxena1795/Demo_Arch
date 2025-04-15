# Architecture Diagram

```mermaid
flowchart TD
    subgraph Client
        A[Postman] -->|Sends XML Input| B[RequestController]
    end

    subgraph Application
        B[RequestController] -->|Calls| C[RequestService]
        C[RequestService] -->|Fetches Record| D[RecordRepository]
        C[RequestService] -->|Calls External API| E[RestTemplate]
        E[RestTemplate] -->|Fetches Data| F[ThirdPartyService]
        C[RequestService] -->|Saves Record| D[RecordRepository]
    end

    subgraph Database
        D[RecordRepository] -->|Stores and Retrieves| G[Database]
    end

    subgraph External
        F[ThirdPartyService]
    end

    A -->|Receives JSON Response| B
    B -->|Returns JSON Response| A
