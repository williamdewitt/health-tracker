# Activity Diagrams for Health Tracker

This document provides UML activity diagrams representing workflows of key processes in the Health Tracker system. Activity diagrams model stepwise activities and actions with support for decisions, concurrency, and data flow.

## 1. User Registration and Authentication

```mermaid
stateDiagram-v2
    [*] --> EnterRegistrationDetails
    EnterRegistrationDetails --> ValidateInput
    ValidateInput --> RegistrationSuccess: Valid
    ValidateInput --> RegistrationFailure: Invalid
    RegistrationFailure --> EnterRegistrationDetails
    RegistrationSuccess --> SendConfirmationEmail
    SendConfirmationEmail --> [*]

    RegistrationSuccess --> Login
    Login --> ValidateCredentials
    ValidateCredentials --> LoginSuccess: Valid
    ValidateCredentials --> LoginFailure: Invalid
    LoginFailure --> Login
    LoginSuccess --> [*]
```

## 2. Nutrition Logging

```mermaid
stateDiagram-v2
    [*] --> SelectDateAndMealType
    SelectDateAndMealType --> AddFoodItems
    AddFoodItems --> CalculateTotals
    CalculateTotals --> SaveEntry
    SaveEntry --> EntrySaved
    EntrySaved --> [*]

    EntrySaved --> EditEntry
    EditEntry --> AddFoodItems
    EntrySaved --> DeleteEntry
    DeleteEntry --> [*]
```

## 3. Exercise Tracking

```mermaid
stateDiagram-v2
    [*] --> SelectExerciseType
    SelectExerciseType --> EnterDurationAndCalories
    EnterDurationAndCalories --> SaveExerciseEntry
    SaveExerciseEntry --> EntrySaved
    EntrySaved --> [*]

    EntrySaved --> EditEntry
    EditEntry --> EnterDurationAndCalories
    EntrySaved --> DeleteEntry
    DeleteEntry --> [*]
```

## 4. Health Metrics Monitoring

```mermaid
stateDiagram-v2
    [*] --> SelectMetricType
    SelectMetricType --> EnterMetricValue
    EnterMetricValue --> SaveMetricEntry
    SaveMetricEntry --> EntrySaved
    EntrySaved --> [*]

    EntrySaved --> EditEntry
    EditEntry --> EnterMetricValue
    EntrySaved --> DeleteEntry
    DeleteEntry --> [*]
```

## 5. Food Suggestions and Blood Type Diet Assistance

```mermaid
stateDiagram-v2
    [*] --> RetrieveUserPreferences
    RetrieveUserPreferences --> RetrieveBloodType
    RetrieveBloodType --> GenerateFoodSuggestions
    GenerateFoodSuggestions --> DisplaySuggestions
    DisplaySuggestions --> [*]
```

## Notes

- Each activity diagram models the flow of actions and decisions for the respective use case.
- Loops represent editing or retrying actions.
- The diagrams support clear visualization of workflows for developers and stakeholders.

This documentation complements the core use cases and supports detailed design and implementation planning.
