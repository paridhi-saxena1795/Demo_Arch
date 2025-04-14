```mermaid
classDiagram
    class SpringBootXmlJsonTransformApplication {
        +main(String[] args)
    }

    class RequestController {
        +processRequest(String xmlInput) ResponseEntity<Record>
    }

    class Record {
        -Long id
        -String name
        -Double amount
        +getId() Long
        +setId(Long id)
        +getName() String
        +setName(String name)
        +getAmount() Double
        +setAmount(Double amount)
    }

    class RecordRepository {
        <<interface>>
        +findById(Long id) Optional<Record>
        +save(Record record) Record
    }

    class RequestService {
        -RecordRepository repository
        -RestTemplate restTemplate
        +handleRequest(Long id) Record
    }

    class RestTemplateConfig {
        +restTemplate() RestTemplate
    }

    SpringBootXmlJsonTransformApplication --> RequestController
    RequestController --> RequestService
    RequestService --> RecordRepository
    RequestService --> Record
    RequestService --> RestTemplate
    RecordRepository --> Record
    RestTemplateConfig --> RestTemplate
