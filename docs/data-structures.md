# Data Structures for Health Tracker

This document defines the core data structures used in the Health Tracker system. These structures form the foundation for data storage, transfer, and manipulation across the backend and frontend layers.

## Core Entities

### User
Represents a registered user of the system.

- UserId (GUID): Unique identifier for the user.
- Username (string): User's login name.
- Email (string): User's email address.
- CreatedAt (DateTime): Account creation timestamp.
- UpdatedAt (DateTime): Last update timestamp.

### NutritionEntry
Represents a single nutrition log entry.

- EntryId (GUID): Unique identifier for the entry.
- UserId (GUID): Reference to the user who logged the entry.
- Date (DateTime): Date of the nutrition entry.
- MealType (enum): Breakfast, Lunch, Dinner, Snack.
- FoodItems (List of FoodItem): List of foods consumed.
- TotalCalories (int): Total calories consumed in the entry.
- CreatedAt (DateTime): Timestamp of entry creation.
- UpdatedAt (DateTime): Timestamp of last update.

### FoodItem
Represents a food item within a nutrition entry.

- FoodItemId (GUID): Unique identifier.
- Name (string): Name of the food.
- Quantity (float): Amount consumed.
- Unit (string): Unit of measurement (e.g., grams, pieces).
- Calories (int): Calories per quantity.
- Protein (float): Protein content in grams.
- Carbohydrates (float): Carbohydrate content in grams.
- Fats (float): Fat content in grams.

### ExerciseEntry
Represents a single exercise log entry.

- EntryId (GUID): Unique identifier.
- UserId (GUID): Reference to the user.
- Date (DateTime): Date of exercise.
- ExerciseType (enum): Type of exercise (e.g., Running, Cycling).
- DurationMinutes (int): Duration in minutes.
- CaloriesBurned (int): Estimated calories burned.
- CreatedAt (DateTime): Timestamp of entry creation.
- UpdatedAt (DateTime): Timestamp of last update.

### HealthMetricEntry
Represents a health metric measurement.

- EntryId (GUID): Unique identifier.
- UserId (GUID): Reference to the user.
- Date (DateTime): Date of measurement.
- MetricType (enum): Type of metric (e.g., Weight, BloodPressure).
- Value (float or string): Measured value.
- Unit (string): Unit of measurement.
- CreatedAt (DateTime): Timestamp of entry creation.
- UpdatedAt (DateTime): Timestamp of last update.

## Enumerations

- MealType: Breakfast, Lunch, Dinner, Snack.
- ExerciseType: Running, Cycling, Swimming, Weightlifting, Yoga, Other.
- MetricType: Weight, BloodPressure, HeartRate, SleepDuration, Other.

## Notes

- All entries are linked to a UserId to maintain user-specific data isolation.
- Timestamps support audit and synchronization features.
- Units are standardized where possible to ensure consistency.

This foundational data structure design supports extensibility for future health tracking features and integrations.

## Additional Features

### Food Suggestions
The system will provide personalized food suggestions based on user preferences, dietary restrictions, and health goals. This feature will leverage the NutritionEntry and FoodItem data structures to recommend foods that align with the user's nutritional needs.

### Blood Type Diet Assistance
The system will offer guidance and assistance for users interested in eating according to their blood type. This includes:

- Storing user's blood type information.
- Providing recommended and avoidable foods based on blood type.
- Integrating blood type dietary advice into food suggestions and nutrition tracking.

### Proposed Data Structure Additions

#### User (extended)
- BloodType (string, optional): User's blood type (e.g., A, B, AB, O).

#### FoodItem (extended)
- BloodTypeCompatibility (List of strings, optional): List of blood types for which the food is recommended or not recommended.

These additions support enhanced personalization and health guidance features.
