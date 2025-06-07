[<< Back](../README.md)

## Design
The software architecture diagram(s) and design(s).

### Introduction
We leverage the iDesign software architectural principals in the design of this solution.

The below describes the layers of the system and their high-level responsibilities.

### Architecture
The architecture of the solution should be a layered one. Specifically 3 layers deep. These layers are also only allowed to depend on components adjacent of itself or down (never up - e.g. Engines shouldn't depend on managers). All components should be color coded correctly based on the description below for ease of reading.
| Layer | Description |
| --- | --- |
| Managers (Green) | These components orchestrate other code paths and often fascilitate use cases and as such would be the entry point to the application. |
| Engines (Orange) | These components perform complex operations exclusively. |
| Data Access (Grey) | These components perform IO operations exclusively. |
| Models (Purple) | These are simple data structures (DTOs) / models and occasionally enums. |

### Design Documentation
| Content | Description
| -- | -- |
| [Use Cases](./designs/1_use_cases.md) | Use case diagram(s).
| [High-Level System Components](./designs/2_system_components.md) | High-level system components.
| [Class Diagrams](./designs/3_class.md) | Class diagram(s).
| [Sequence Diagrams](./designs/4_sequence.md) | Sequence diagram(s).
| [Frontend](./designs/5_frontend.md) | Frontend.
| [Error Handling Sequences](./designs/error_handling_sequences.md) | Error handling & resilience patterns.
| [Error Handling Guide](./error_handling.md) | Comprehensive error handling guidelines.
| [Error Monitoring](./error_monitoring.md) | Error monitoring & observability guide.

[<< Back](../README.md)